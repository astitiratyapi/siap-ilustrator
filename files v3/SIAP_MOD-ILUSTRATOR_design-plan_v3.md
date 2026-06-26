# Design Plan — Penugasan Ilustrator (Admin)
## SIAP Pusmendik · MOD-ILUSTRATOR · v3

---

## Changelog v3

| Item | v2 | v3 |
|---|---|---|
| Entry point assign | Dropdown "+ Tambah Penugasan" → opsi "Tambah Ilustrasi" | Ikon [image-plus] per baris soal di tabel, klik langsung buka modal |
| Tombol terpisah | Ada tombol "Tambah Ilustrasi" | Tidak ada — hanya ikon baris |
| Jumlah status | 4 (Belum / Siap / Sedang / Selesai) | 3 (Belum Ditugaskan / Sedang Dikerjakan / Selesai) |
| Edit setelah assign | Bisa ubah Ilustrator + Catatan | Status Sedang + Selesai: HANYA Catatan yang bisa diubah, Ilustrator terkunci |
| Tampilan list | Tab "Penugasan Ilustrasi" terpisah | Kolom "Ilustrasi" langsung di tabel Penugasan existing |
| Modul baru | Tidak ada | Halaman "Rekapitulasi Ilustrator" di sidebar → Rekapitulasi |

---

## 1. Ringkasan Fitur

**Penugasan Ilustrator** menambahkan kemampuan assign Ilustrator langsung dari tabel penugasan soal existing, tanpa halaman atau modal wizard terpisah. Kolom "Ilustrasi" baru ditambahkan ke tabel existing untuk menampilkan status + trigger aksi.

**Rekapitulasi Ilustrator** adalah halaman baru di bawah menu Rekapitulasi sidebar, menampilkan ringkasan pekerjaan per Ilustrator untuk kebutuhan pembayaran berdasarkan jumlah gambar yang diselesaikan.

---

## 2. Entry Point & Trigger

### Assign Ilustrator
- **Dari mana:** Tabel Penugasan Penulisan existing → kolom Aksi → ikon [lucide: image-plus] (hanya muncul di baris yang status Ilustrasinya "Belum Ditugaskan")
- **Mekanisme:** Klik ikon → modal tunggal (bukan wizard) → form → Simpan
- **Tidak ada:** Tombol terpisah, opsi dropdown, tab baru, atau halaman baru

### Melihat/Edit Ilustrasi yang Sudah Ditugaskan
- **[lucide: eye] #0db8e8** — buka modal detail read-only (tersedia di semua status)
- **[lucide: message-square] #f59e0b** — buka modal edit catatan (hanya muncul di status Sedang + Selesai)
- **[lucide: image-plus]** — hilang setelah assign, digantikan dua ikon di atas

### Rekapitulasi Ilustrator
- **Dari mana:** Sidebar → Rekapitulasi (expanded) → Ilustrator
- **Style:** Identik dengan halaman "Rekapitulasi Penulis" existing

---

## 3. Status & Transisi

```
[BELUM DITUGASKAN]
  Icon di baris: [image-plus] #0db8e8 — klik = buka modal assign
      ↓ Admin assign (Ilustrator + Jumlah Gambar + Deadline)
[SEDANG DIKERJAKAN]
  Icon di baris: [eye] + [message-square]
  Modal: Ilustrator LOCKED, hanya Catatan yang editable
      ↓ Admin klik "Tandai Selesai" (dari modal detail atau aksi baris)
[SELESAI] ← terminal
  Icon di baris: [eye] + [message-square]
  Modal: Ilustrator LOCKED, hanya Catatan yang editable
```

> **Pertanyaan terbuka (OI-11):** Apakah status berubah otomatis ke "Sedang Dikerjakan" saat Admin menyimpan assign? Atau perlu aksi terpisah "Mulai Kerjakan"? Design ini mengasumsikan **otomatis Sedang Dikerjakan** saat assign berhasil.

---

## 4. Edit Permissions per Status

| Field | Belum Ditugaskan | Sedang Dikerjakan | Selesai |
|---|---|---|---|
| Pilih Ilustrator | Ya (modal assign) | ❌ Terkunci | ❌ Terkunci |
| Jumlah Gambar | Ya (modal assign) | ❌ Terkunci | ❌ Terkunci |
| Deadline | Ya (modal assign) | ❌ Terkunci | ❌ Terkunci |
| Catatan untuk Ilustrator | Saat assign (opsional) | ✅ Editable | ✅ Editable |

---

## 5. Kolom "Ilustrasi" di Tabel Existing

Kolom baru ditambahkan di antara kolom "Disetujui/Ditugaskan" dan "Action":

| Status | Tampilan di Kolom | Ikon di Kolom Aksi |
|---|---|---|
| Belum Ditugaskan | Badge abu "Belum" | [image-plus] #0db8e8 + [eye] + [edit] + [trash] |
| Sedang Dikerjakan | Badge kuning "Sedang" | [eye] + [message-square] + [edit] + [trash] |
| Selesai | Badge hijau "Selesai" | [eye] + [message-square] + [edit] + [trash] |

> Catatan: Ikon [edit] dan [trash] merujuk ke edit/hapus penugasan soal itu sendiri (existing). Ikon [image-plus] dan [message-square] adalah ikon baru khusus untuk fungsi ilustrasi.

---

## 6. Aturan Bisnis

| ID | Aturan |
|---|---|
| BR-01 | 1 Ilustrator per kode soal |
| BR-02 | 1 kode soal bisa punya >1 gambar — wajib diisi jumlahnya |
| BR-03 | Hanya Admin yang bisa assign, update status, edit catatan |
| BR-04 | Trigger assign: ikon per baris — bukan tombol terpisah |
| BR-05 | Tidak ada tombol "Tambah Penugasan Ilustrasi" di mana pun |
| BR-06 | 3 status saja: Belum / Sedang / Selesai |
| BR-07 | Status Sedang + Selesai: Ilustrator tidak bisa diubah, hanya Catatan |
| BR-08 | Rekap Ilustrator: jumlah gambar ditugaskan + selesai, untuk pembayaran |

---

## 7. Struktur Data

### Tabel: `illustration_assignments`

| Field | Tipe | Keterangan |
|---|---|---|
| `id` | UUID | Primary key |
| `penugasan_id` | FK → penugasan | Link ke penugasan soal existing |
| `question_code` | VARCHAR | Kode soal / stimulus |
| `illustrator_id` | FK → users | Ilustrator yang ditugaskan |
| `illustrator_name` | VARCHAR | Cache nama Ilustrator |
| `image_count` | INT | Jumlah gambar (min 1) |
| `status` | ENUM | `BELUM` / `SEDANG` / `SELESAI` |
| `deadline` | DATE | Deadline ilustrasi |
| `catatan` | TEXT nullable | Catatan Admin untuk Ilustrator |
| `images_completed` | INT default 0 | Jumlah gambar yang sudah selesai (untuk rekap) |
| `assigned_at` | DATETIME | Waktu assign |
| `completed_at` | DATETIME nullable | Waktu selesai |
| `created_by` | FK → users | Admin yang assign |
| `updated_by` | FK → users | Admin yang terakhir update |
| `created_at` | DATETIME | |
| `updated_at` | DATETIME | |

---

## 8. Rekapitulasi Ilustrator — Kolom Tabel

| Kolom | Sumber Data | Keterangan |
|---|---|---|
| Nama | users.name | Nama Ilustrator |
| Email | users.email | Email Ilustrator |
| Jumlah Soal Ditugaskan | COUNT(illustration_assignments) | Total soal yang pernah ditugaskan |
| Jumlah Gambar Ditugaskan | SUM(image_count) | Total gambar (termasuk yang belum selesai) |
| Gambar Selesai | SUM(images_completed) WHERE status=SELESAI | Untuk dasar perhitungan pembayaran |
| Gambar Belum Selesai | Gambar Ditugaskan - Gambar Selesai | |
| % Selesai | (Selesai / Ditugaskan) × 100 | Badge warna: hijau ≥80%, kuning 50-79%, merah <50% |

> **Catatan pembayaran:** Ilustrator dibayar berdasarkan jumlah gambar yang **selesai** (Gambar Selesai), bukan jumlah soal. Kolom ini yang menjadi acuan keuangan.

---

## 9. User Stories (Revised v3)

### US-01 — Assign Ilustrator dari Baris Soal
**Sebagai Admin**, saya ingin mengklik ikon assign langsung di baris soal yang belum ada ilustrasinya, **sehingga** saya tidak perlu berpindah halaman untuk menugaskan Ilustrator.

AC-01.1: Kolom "Ilustrasi" baru ada di tabel Penugasan, menampilkan status + ikon aksi
AC-01.2: Ikon [image-plus] hanya muncul di baris dengan status "Belum Ditugaskan"
AC-01.3: Klik ikon → modal assign langsung terbuka (single step, bukan wizard)
AC-01.4: Modal menampilkan info soal read-only + form: Ilustrator (wajib), Jumlah Gambar (wajib), Deadline (wajib), Catatan (opsional)
AC-01.5: Setelah simpan: modal tutup, badge di kolom Ilustrasi berubah "Sedang", ikon berubah ke [eye]+[message-square], toast sukses

### US-02 — Edit Catatan (Status Sedang/Selesai)
**Sebagai Admin**, saya ingin mengubah catatan untuk Ilustrator tanpa bisa mengubah siapa Ilustratornya, **sehingga** saya tetap bisa memberikan klarifikasi tanpa risiko mengubah penugasan yang sedang berjalan.

AC-02.1: Ikon [message-square] hanya muncul di baris status Sedang/Selesai
AC-02.2: Modal edit catatan menampilkan field Ilustrator dengan lock indicator — tidak bisa diklik/diubah
AC-02.3: Field Catatan editable, max 500 karakter
AC-02.4: Setelah simpan: toast "Catatan berhasil diperbarui", modal tutup

### US-03 — Lihat Detail Ilustrasi
**Sebagai Admin**, saya ingin melihat detail lengkap penugasan ilustrasi termasuk deskripsi gambar dan riwayat aktivitas, **sehingga** saya bisa memverifikasi progress tanpa mengubah data.

AC-03.1: Ikon [eye] tersedia di semua status
AC-03.2: Modal detail menampilkan: info soal, deskripsi per gambar, Ilustrator, status, catatan, riwayat
AC-03.3: Dari modal detail, tombol "Edit Catatan" tersedia (jika status Sedang/Selesai)
AC-03.4: Dari modal detail, tombol "Tandai Selesai" tersedia (jika status Sedang)

### US-04 — Update Status ke Selesai
**Sebagai Admin**, saya ingin menandai ilustrasi sebagai selesai setelah Ilustrator melaporkan pekerjaan mereka, **sehingga** rekap akurat untuk keperluan pembayaran.

AC-04.1: Update status tersedia dari kolom aksi tabel (mini dropdown) atau dari modal detail
AC-04.2: Perubahan ke "Selesai" memerlukan konfirmasi kecil: "Tandai sebagai Selesai? Tidak dapat diubah."
AC-04.3: Setelah Selesai: badge berubah hijau, images_completed diperbarui, completed_at tersimpan

### US-05 — Lihat Rekapitulasi per Ilustrator
**Sebagai Admin**, saya ingin melihat ringkasan pekerjaan setiap Ilustrator (jumlah gambar ditugaskan vs selesai), **sehingga** saya dapat menyiapkan data pembayaran dengan akurat.

AC-05.1: Halaman Rekapitulasi Ilustrator dapat diakses dari sidebar → Rekapitulasi → Ilustrator
AC-05.2: Style halaman identik dengan Rekapitulasi Penulis existing
AC-05.3: Tabel menampilkan: Nama, Email, Jumlah Soal, Jumlah Gambar Ditugaskan, Gambar Selesai, Gambar Belum Selesai, % Selesai
AC-05.4: Kolom % Selesai menggunakan badge warna (hijau/kuning/merah) untuk visual scanning cepat
AC-05.5: Tersedia tombol "Rekap Ilustrator.Xls" untuk export

---

## Accessibility Token Report
Generated: 2026-06-26 | Standard: WCAG 2.1 AA | Brand: SIAP actual

| Pair | Ratio | Normal text | Large text | UI |
|---|---|---|---|---|
| white on #0db8e8 | ~3.0:1 | FAIL | PASS | PASS |
| white on #1a2332 | ~12.5:1 | PASS | PASS | PASS |
| #111827 on white | 16.0:1 | PASS | PASS | PASS |
| #4b5563 on white | 7.0:1 | PASS | PASS | PASS |
| #9ca3af on white | 2.8:1 | FAIL | FAIL | FAIL |

**Overall:** WARNING — #0db8e8 tidak lolos untuk teks kecil. Gunakan hanya pada ikon, tombol, badge border. Semua teks body dan label: #111827 atau #4b5563.
