# Design Plan — Penugasan Ilustrator (Admin)
## SIAP Pusmendik · MOD-ILUSTRATOR · v2 (revised entry point + brand colors)

---

## Changelog v2

| Item | v1 | v2 |
|---|---|---|
| Entry point | Sub-menu sidebar "Penugasan Ilustrator" | Dropdown "+ Tambah Penugasan" → opsi "Tambah Ilustrasi" |
| Tab di halaman existing | Halaman baru terpisah | Tab baru "Penugasan Ilustrasi" di halaman Penugasan existing |
| Brand primary | #004990 (A'raf DS default — asumsi) | #0db8e8 (cyan — dari screenshot existing) |
| Sidebar color | A'raf DS sidebar (tidak dispesifikkan) | #1a2332 dark navy (dari screenshot existing) |
| Action icons | #004990 semua | Eye #0db8e8, Edit #f59e0b, Delete #ef4444 (sesuai existing) |
| Status badge "Siap" | #eff6ff / #0069d2 | #e0f7fd / #0db8e8 (sesuai brand cyan SIAP) |
| OI-08 | Open item: struktur navigasi belum jelas | Diselesaikan: tidak ada menu baru di sidebar |

---

## 1. Ringkasan Fitur

Fitur **Penugasan Ilustrator** memungkinkan Admin SIAP untuk menugaskan satu Ilustrator ke satu kode soal yang memiliki kebutuhan ilustrasi/gambar. Fitur ini menggantikan proses manual menggunakan spreadsheet tracking.

**Entry point utama:** Dropdown tombol "+ Tambah Penugasan" (pojok kanan atas halaman Penugasan) → opsi ke-4 "Tambah Ilustrasi" → modal wizard 2-step.

**Tampilan list:** Tab baru "Penugasan Ilustrasi" di halaman Penugasan existing, sejajar dengan "Penugasan Penulisan".

---

## 2. Konteks Sistem Existing

### Halaman Penugasan (Dashboard)
- Menampilkan daftar penugasan dengan kolom: Nama Penugasan, Nama PJM, Jenis Penugasan, Event, Deadline Penugasan, Deadline Validasi, Disubmit, Diperbaiki, Disetujui/Ditugaskan, Action
- 237 records per Juni 2026
- Action: View (cyan eye), Edit (amber pencil), Hapus (red trash)
- Tombol "+ Tambah Penugasan" sudah memiliki dropdown dengan 3 opsi: Tambah Penulisan, Tambah Perevisian, Tambah Penulisan Soal Terbatas

### Brand SIAP (dari screenshot)
- Sidebar: #1a2332 (dark navy)
- Primary / CTA: #0db8e8 (cyan bright) — tombol "+ Tambah Penugasan", tombol Filter, active tab
- Secondary buttons: white fill, 1px #e5e7eb border
- Icon view: #0db8e8 | Icon edit: #f59e0b | Icon delete: #ef4444
- Page background: #f9fafb | Card: #ffffff | Border: #e5e7eb

### Spreadsheet Manual yang Digantikan
- Nama Penulis, Mata Pelajaran, Kode Soal/Stimulus
- Deskripsi gambar/ilustrasi (dari penulis soal)
- Referensi gambar (URL)
- Catatan Ilustrator (jika deskripsi kurang jelas)
- Status: Sedang (PROSES ILUSTRASI) / Selesai (OK)
- Nama Ilustrator

---

## 3. Aturan Bisnis Utama

| ID | Aturan |
|---|---|
| BR-01 | 1 Ilustrator menangani ilustrasi pada 1 kode soal |
| BR-02 | Dalam 1 kode soal, ilustrasi dapat terdiri dari lebih dari 1 gambar |
| BR-03 | Penugasan ilustrator hanya dapat dilakukan oleh Admin |
| BR-04 (asumsi) | 1 kode soal hanya dapat ditugaskan ke 1 Ilustrator pada satu waktu |
| BR-05 (asumsi) | Admin dapat mengubah penugasan (re-assign) jika belum Selesai |
| BR-06 (asumsi) | Status progres ditandai oleh Admin berdasarkan laporan Ilustrator |
| BR-07 | Penugasan Ilustrator tidak memiliki menu sidebar — diakses via dropdown existing |

---

## 4. Identifikasi Entitas & Field Database

### Tabel: `illustration_assignments`

| Field | Tipe | Keterangan |
|---|---|---|
| `id` | UUID / INT | Primary key |
| `question_code_id` | FK → soal/stimulus | Kode soal yang membutuhkan ilustrasi |
| `question_code` | VARCHAR | Nomor kode soal (e.g., `26FISKALKLPF10SA-000000-0035`) |
| `author_name` | VARCHAR | Nama penulis soal (dari sistem existing) |
| `subject` | VARCHAR | Mata pelajaran |
| `illustration_description` | TEXT | Deskripsi gambar/ilustrasi dari penulis soal |
| `reference_url` | TEXT (nullable) | URL referensi gambar |
| `illustrator_id` | FK → users | ID Ilustrator yang ditugaskan |
| `illustrator_name` | VARCHAR | Nama Ilustrator |
| `illustrator_note` | TEXT (nullable) | Catatan Admin/Ilustrator |
| `status` | ENUM | `BELUM_DITUGASKAN` / `SIAP_DIKERJAKAN` / `SEDANG_DIKERJAKAN` / `SELESAI` |
| `image_count` | INT | Jumlah gambar dalam 1 kode soal ini |
| `assigned_at` | DATETIME | Tanggal ditugaskan |
| `completed_at` | DATETIME (nullable) | Tanggal selesai |
| `deadline` | DATE | Deadline pengerjaan ilustrasi |
| `created_by` | FK → users | Admin yang membuat penugasan |
| `updated_by` | FK → users | Admin yang terakhir mengupdate |
| `created_at` | DATETIME | Timestamp buat |
| `updated_at` | DATETIME | Timestamp update |

### Tabel: `illustration_images` (opsional)

| Field | Tipe | Keterangan |
|---|---|---|
| `id` | UUID / INT | Primary key |
| `assignment_id` | FK → illustration_assignments | Parent |
| `image_sequence` | INT | Urutan gambar (1, 2, 3…) |
| `image_description` | TEXT | Deskripsi gambar individual |
| `image_reference_url` | TEXT (nullable) | URL referensi per gambar |
| `image_status` | ENUM | `BELUM` / `SEDANG` / `SELESAI` |
| `completed_at` | DATETIME (nullable) | Selesai |

---

## 5. User Stories & Acceptance Criteria

### US-01 — Lihat Daftar Penugasan Ilustrator

**Sebagai Admin**, saya ingin melihat daftar semua kode soal yang membutuhkan ilustrasi di tab khusus, **sehingga** saya dapat memantau progress tanpa meninggalkan halaman Penugasan.

**Acceptance Criteria:**
- AC-01.1: Tab "Penugasan Ilustrasi" tampil di sebelah "Penugasan Penulisan" pada halaman Penugasan
- AC-01.2: Tabel menampilkan: Kode Soal, Nama Penulis, Mata Pelajaran, Deskripsi Ilustrasi (preview 2 baris), Ilustrator, Status badge, Deadline, Aksi
- AC-01.3: Status badge: abu (Belum Ditugaskan), cyan (Siap Dikerjakan), kuning (Sedang), hijau (Selesai)
- AC-01.4: Admin dapat filter berdasarkan Status, Mata Pelajaran, Ilustrator (via tombol Filter existing)
- AC-01.5: Admin dapat mencari berdasarkan Kode Soal atau Nama Penulis
- AC-01.6: Pagination sesuai pola existing (Showing X to Y of Z records)

### US-02 — Tambah Penugasan Ilustrasi (via dropdown)

**Sebagai Admin**, saya ingin mengakses fitur "Tambah Ilustrasi" dari dropdown tombol "+ Tambah Penugasan" yang sudah ada, **sehingga** saya tidak perlu mencari menu baru atau berpindah halaman.

**Acceptance Criteria:**
- AC-02.1: Dropdown "+ Tambah Penugasan" menampilkan opsi ke-4 "Tambah Ilustrasi" (dengan separator dari 3 opsi existing)
- AC-02.2: Klik "Tambah Ilustrasi" membuka modal wizard 2-step (bukan halaman baru)
- AC-02.3: Step 1 menampilkan daftar kode soal yang belum ditugaskan ilustrasinya
- AC-02.4: Admin dapat memilih satu atau lebih kode soal di Step 1
- AC-02.5: Tombol "Lanjut" di Step 1 hanya aktif jika minimal 1 kode soal dipilih

### US-03 — Assign Ilustrator (Step 2 Modal)

**Sebagai Admin**, saya ingin mengisi Ilustrator, Jumlah Gambar, dan Deadline dalam satu form di Step 2, **sehingga** penugasan dapat langsung tersimpan tanpa langkah tambahan.

**Acceptance Criteria:**
- AC-03.1: Form Step 2 menampilkan summary kode soal terpilih (read-only)
- AC-03.2: Field Ilustrator (dropdown, wajib) + Jumlah Gambar (number, wajib, min 1) + Deadline (date picker, wajib) + Catatan (textarea, opsional)
- AC-03.3: Tombol "Simpan Penugasan" disabled jika Ilustrator atau Deadline kosong
- AC-03.4: Setelah simpan berhasil: modal tertutup, tab "Penugasan Ilustrasi" refresh, baris baru muncul dengan status "Siap Dikerjakan", toast sukses muncul
- AC-03.5: Jika multi-select di Step 1: Ilustrator + Deadline yang sama diterapkan ke semua kode soal terpilih, dengan info banner peringatan

### US-04 — Lihat Detail & Edit Penugasan

**Sebagai Admin**, saya ingin melihat detail lengkap satu kode soal dan mengedit penugasan yang belum selesai, **sehingga** saya dapat mengakomodasi perubahan ketersediaan Ilustrator.

**Acceptance Criteria:**
- AC-04.1: Klik ikon view → modal detail menampilkan: info kode soal, deskripsi lengkap, referensi URL, Ilustrator, status, riwayat aktivitas
- AC-04.2: Tombol "Edit Penugasan" di modal detail hanya aktif jika status bukan Selesai
- AC-04.3: Edit membuka form yang sama dengan Step 2, ter-prefill dengan data existing
- AC-04.4: Setelah simpan perubahan: konfirmasi dialog → status kembali ke "Siap Dikerjakan"

### US-05 — Update Status Progress

**Sebagai Admin**, saya ingin memperbarui status progress langsung dari tabel, **sehingga** tidak perlu membuka halaman detail hanya untuk update status.

**Acceptance Criteria:**
- AC-05.1: Kolom Aksi memiliki akses ke dropdown status (atau tombol quick-action)
- AC-05.2: Transisi valid: Siap → Sedang (langsung), Sedang → Selesai (dengan konfirmasi)
- AC-05.3: Status "Selesai" bersifat final — ikon edit dan delete tidak lagi tampil di baris tersebut
- AC-05.4: Setiap perubahan status dicatat di riwayat aktivitas

---

## 6. State Machine — Status Penugasan Ilustrasi

```
[BELUM_DITUGASKAN]
      ↓ Admin klik "Tambah Ilustrasi" → isi Step 2 → Simpan
[SIAP_DIKERJAKAN] — badge #e0f7fd / #0db8e8
      ↓ Admin update status "Sedang Dikerjakan"
[SEDANG_DIKERJAKAN] — badge #fefce8 / #ba7517
      ↓ Admin update status "Selesai" + konfirmasi
[SELESAI] ← terminal — badge #f0fdf4 / #16a34a
      ↑ Re-assign dari SIAP atau SEDANG → kembali ke SIAP_DIKERJAKAN
```

---

## 7. Struktur Navigasi (Revisi v2)

```
Sidebar → menu "Penugasan"
  └─ Halaman /penugasan
       ├─ Tab 1: "Penugasan Penulisan" (existing)
       └─ Tab 2: "Penugasan Ilustrasi" (new)

Tombol "+ Tambah Penugasan" (tersedia di semua tab):
  Dropdown:
    ├─ Tambah Penulisan (existing)
    ├─ Tambah Perevisian (existing)
    ├─ Tambah Penulisan Soal Terbatas (existing)
    ├─ ─────────────────── (separator)
    └─ Tambah Ilustrasi (NEW) → Modal Wizard 2-step
```

---

## 8. Rekomendasi Pendekatan Implementasi

Karena fitur ini diintegrasikan ke halaman existing tanpa route baru, pendekatan yang direkomendasikan:

**Frontend:** Tab component di halaman /penugasan. Tab "Penugasan Ilustrasi" lazy-load data saat pertama kali diklik. Modal wizard menggunakan overlay component yang sudah ada di codebase (jika ada pola modal existing).

**Dropdown:** Tambahkan 1 item ke dropdown button yang sudah ada. Separator visual memisahkan antara "penugasan penulis" dan "penugasan ilustrator" agar tidak menimbulkan kebingungan.

**API:** Endpoint terpisah untuk illustration_assignments, tidak mencampur dengan penugasan penulisan soal yang sudah ada.

---

## Accessibility Token Report — WCAG 2.1 AA
Generated: 2026-06-26
Standard: WCAG 2.1 Level AA
Brand: SIAP actual (#0db8e8 primary, #1a2332 sidebar)

### Contrast Ratio Results

| Color Pair | Ratio | Normal text | Large text | UI elements |
|---|---|---|---|---|
| white on #0db8e8 | ~3.0:1 | FAIL | PASS | PASS |
| #0db8e8 on white | ~3.0:1 | FAIL | PASS | PASS |
| white on #1a2332 | ~12.5:1 | PASS | PASS | PASS |
| text_primary on white | 16.0:1 | PASS | PASS | PASS |
| text_secondary on white | 7.0:1 | PASS | PASS | PASS |
| text_tertiary on white | 2.8:1 | FAIL | FAIL | FAIL |

### Issues Found

- WARNING: #0db8e8 on white = ~3.0:1 — hanya lolos untuk large text (≥18px) dan UI components (tombol, badge, ikon). JANGAN gunakan sebagai teks body kecil.
  Fix: Semua teks kecil (body, label, caption) tetap menggunakan #111827 atau #4b5563.
  Safe: tombol (besar), badge pill, ikon, tab active indicator, border.

- FAIL: text_tertiary (#9ca3af) on white = 2.8:1 — decorative only.

### Overall Result
WARNING — Brand primary #0db8e8 tidak lolos WCAG AA untuk normal text. Aman untuk tombol, badge, dan ikon.
Semua teks yang perlu dibaca harus menggunakan text_primary (#111827) atau text_secondary (#4b5563).
