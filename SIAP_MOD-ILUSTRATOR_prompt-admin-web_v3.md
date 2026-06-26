# AI Design Prompt — Penugasan Ilustrator (Admin)
## SIAP Pusmendik · MOD-ILUSTRATOR · v3 (inline row trigger + 3-status + rekap ilustrator)
### Platform: Admin Web · 1366px · greenfield

---

# BRAND GUIDELINE

## Project
**Name:** SIAP (Sistem Informasi Asesmen dan Pembelajaran) — Pusmendik
**Client:** Pusat Penilaian Pendidikan (Pusmendik), Kemendikbud
**Design System:** A'raf DS — PT Badr Interactive (SIAP brand override)
**Icon Library:** Lucide — lucide.dev/icons
**Logo Source:** Untitled UI Logos — untitledui.com/resources/logos

---

## Brand Colors (SIAP Actual)

| Role | Hex | Usage |
|---|---|---|
| Sidebar bg | #1a2332 | Background sidebar seluruh app |
| Primary / CTA | #0db8e8 | Tombol CTA utama, active tab underline, ikon view, pagination active |
| Secondary btn | #ffffff fill + #e5e7eb border | Tombol Template .xls, Export, Rekap |
| Icon assign | #0db8e8 | Ikon trigger assign ilustrator (image-plus) — hanya muncul di baris Belum Ditugaskan |
| Icon view/detail | #0db8e8 | Eye icon di status Sedang/Selesai — membuka modal detail (catatan termasuk di dalam) |
| Success | #16a34a | Status Selesai |
| Warning | #ba7517 | Status Sedang Dikerjakan |
| Neutral | #6b7280 | Status Belum Ditugaskan |

> text_tertiary (#9ca3af) TIDAK lolos WCAG AA — gunakan hanya sebagai placeholder/decorative. Semua teks readable: text_primary #111827 atau text_secondary #4b5563.

---

## Status Badges — Penugasan Ilustrasi (3 status per feedback v3)

| Status | Background | Text | Border |
|---|---|---|---|
| Belum Ditugaskan | #f9fafb | #6b7280 | #e5e7eb |
| Sedang Dikerjakan | #fefce8 | #ba7517 | #ba7517 |
| Selesai | #f0fdf4 | #16a34a | #16a34a |

> v3 change: Status "Siap Dikerjakan" dihapus. 3 status saja: Belum Ditugaskan → Sedang Dikerjakan → Selesai.

---

## Edit Permissions per Status (v3 business rule)

| Status | Boleh ubah Ilustrator | Boleh ubah Catatan | Trigger di kolom Ilustrasi |
|---|---|---|---|
| Belum Ditugaskan | Ya (via modal assign) | — (belum ada data) | [image-plus] #0db8e8 |
| Sedang Dikerjakan | TIDAK (locked) | Ya — dari dalam modal detail | [eye] #0db8e8 |
| Selesai | TIDAK (locked) | Ya — dari dalam modal detail | [eye] #0db8e8 |

> Tidak ada ikon catatan terpisah. Catatan diakses dan diedit dari dalam modal detail — ikon [eye] adalah satu-satunya entry point untuk status Sedang dan Selesai.

---

# CONTEXT BLOCK

```json
{
  "project_name": "SIAP Pusmendik",
  "client": "Pusmendik — Kemendikbud",
  "module_id": "MOD-ILUSTRATOR",
  "module_name": "Penugasan Ilustrator + Rekapitulasi Ilustrator",
  "platform": "Admin Web",
  "mode": "greenfield",
  "frame_width": 1366,
  "frame_height": 900,
  "design_system": "A'raf DS — PT Badr Interactive (SIAP brand override)",
  "font": "Plus Jakarta Sans",
  "language": "Indonesian",
  "stage": "POC — happy flow first draft untuk konfirmasi stakeholder",
  "flow_inspiration": "Inline row-level trigger → modal assign (bukan wizard multi-step)",
  "visual_inspiration": "SIAP existing style — dark sidebar, cyan primary, table-dense, sama dengan Rekapitulasi Penulis",
  "icon_library": "Lucide — lucide.dev/icons",
  "entry_point": "Kolom 'Ilustrasi' terpisah dari kolom Action: [image-plus] untuk Belum Ditugaskan, [eye] untuk Sedang/Selesai",
  "tokens": {
    "brand_primary": "#0db8e8",
    "sidebar_bg": "#1a2332",
    "page_bg": "#f9fafb",
    "card_surface": "#ffffff",
    "border_default": "#e5e7eb",
    "text_primary": "#111827",
    "text_secondary": "#4b5563",
    "text_tertiary": "#9ca3af",
    "success": "#16a34a", "success_bg": "#f0fdf4",
    "warning": "#ba7517", "warning_bg": "#fefce8",
    "error": "#dc2626",   "error_bg":   "#fef2f2",
    "neutral_text": "#6b7280", "neutral_bg": "#f9fafb"
  },
  "business_rules": {
    "BR-01_one_illustrator_per_soal": "1 Ilustrator per kode soal — tidak bisa split",
    "BR-02_multiple_images_per_soal": "1 kode soal bisa punya lebih dari 1 gambar — jumlah wajib diisi",
    "BR-03_admin_only": "Hanya Admin yang bisa assign, update status, dan edit catatan",
    "BR-04_trigger_from_row": "Trigger assign ilustrator berasal dari ikon di baris soal (status Belum Ditugaskan) — bukan dari button terpisah",
    "BR-05_no_button_trigger": "Tidak ada tombol 'Tambah Penugasan Ilustrasi' terpisah — entry hanya dari ikon baris",
    "BR-06_3_statuses": "Hanya 3 status: Belum Ditugaskan → Sedang Dikerjakan → Selesai",
    "BR-07_lock_ilustrator_after_assign": "Setelah status Sedang Dikerjakan atau Selesai — Ilustrator TIDAK bisa diubah, hanya Catatan yang bisa diubah",
    "BR-08_rekap_ilustrator": "Halaman Rekapitulasi Ilustrator menampilkan: jumlah gambar ditugaskan, jumlah gambar selesai, per Ilustrator — untuk keperluan pembayaran"
  }
}
```

---

# SECTION 1 — VISUAL REFERENCES

## Flow Reference — Inline Row Trigger → Single Modal (adapted FLOW-06)

### What to adopt
Kolom "Ilustrasi" baru ditambahkan sebelum kolom Action existing. Kolom ini berisi badge status + satu ikon trigger:
- Status **Belum Ditugaskan**: badge abu + [lucide: image-plus] #0db8e8 → klik buka modal assign
- Status **Sedang/Selesai**: badge warna + [lucide: eye] #0db8e8 → klik buka modal detail

Modal detail adalah satu-satunya modal untuk status Sedang dan Selesai. Di dalamnya, Admin bisa melihat semua info (Ilustrator, deskripsi gambar, catatan) dan mengedit catatan jika diperlukan.

Kolom Action existing (eye/pencil/trash) untuk penugasan soal — tidak disentuh, tidak diubah.

### What NOT to adopt
- Ikon [message-square] atau ikon catatan terpisah — catatan ada di dalam modal detail, tidak perlu ikon sendiri
- Tombol atau opsi terpisah untuk trigger ilustrasi (dihapus dari v2)
- Wizard multi-step (modal assign adalah single step langsung)

### Kolom "Ilustrasi" — Icon Rules per Status
Kolom terpisah dari kolom Action, posisi: setelah "Disetujui/Ditugaskan", sebelum "Action".
Lebar kolom: max 120px. Isi: badge status + 1 ikon saja.

| Status | Badge | Ikon di kolom Ilustrasi | Tooltip |
|---|---|---|---|
| Belum Ditugaskan | abu #f9fafb/#6b7280 | [lucide: image-plus] 16px #0db8e8 | "Tugaskan Ilustrator" |
| Sedang Dikerjakan | kuning #fefce8/#ba7517 | [lucide: eye] 16px #0db8e8 | "Lihat Detail Ilustrasi" |
| Selesai | hijau #f0fdf4/#16a34a | [lucide: eye] 16px #0db8e8 | "Lihat Detail Ilustrasi" |

Kolom Action existing (tetap 3 ikon, tidak diubah):
[lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

---

## Visual Style Reference — SIAP Existing (replikasi exact)

Tone: Profesional, government-adjacent, dense table. Replikasi exact dari screenshot existing.

Karakteristik WAJIB:
- Sidebar #1a2332, active item highlight #0db8e8 rounded, inactive rgba(255,255,255,0.6)
- Content area #f9fafb, tabel clean border-bottom only
- Tab bar di bawah page title: underline active #0db8e8 2px, 14px Medium
- Action icons tabel: eye #0db8e8, edit-note #f59e0b, delete #ef4444
- Pagination: angka, active page #0db8e8 bg white text rounded
- Filter button: border #0db8e8, text #0db8e8, white bg

Halaman Rekapitulasi Ilustrator:
  Replikasi exact halaman "Rekapitulasi Penulis" dari screenshot — struktur tab, tabel, pagination, tombol export identik.
  Ganti kolom sesuai data ilustrator (bukan data penulis).

---

# SECTION 2 — LAYOUT RULES

## Master Layout Rules — Admin Web (SIAP style)

### Screen Structure
```
[Sidebar — 220px, #1a2332 bg, fixed]
  Header: "SIAP | Pusmendik" white text, 20px pad
  User: avatar "h" circle + "hawarie / admin" white small
  Nav items (44px, 16px H, 8px radius):
    Active: #0db8e8 bg, white 13px Medium
    Inactive: transparent, rgba(255,255,255,0.6)
  Menu items: User Management, Penugasan, Event Management, Framework Management,
    Repositori, Pengumuman, Master Data, Perakitan,
    Rekapitulasi [expanded, caret-up]: PJM | Penulis | Ilustrator (NEW, active),
    Riwayat Pengguna, Analisis Soal
  Topright: [lucide: bell] 20px abu + avatar "h" 32px

[Content Area — #f9fafb bg, 24px padding]
  Page title row: judul + tombol aksi kanan
  Tab bar (jika ada tabs): underline style
  Action row: Show dropdown + Delete + Filter + Search
  Tabel
  Pagination
```

### Spacing
```
Content: 24px | Row: 56px height | Cell H: 16px | Button gap: 8px
Modal padding: 24px | Modal width: 520px (assign) / 560px (detail)
```

### Modal Rules — Assign Ilustrator (single-step)
```
Overlay: rgba(0,0,0,0.5)
Modal: white, 520px wide, 12px radius, 0 8px 32px rgba(0,0,0,0.2), centered
Header: "Tugaskan Ilustrator" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan | 20px pad | border-bottom #e5e7eb
Body: 24px pad
  Info section: #f9fafb bg, 8px radius, 16px pad — read-only data kode soal
  Form: Pilih Ilustrator (dropdown, required) | Jumlah Gambar (number, required) | Deadline (date, required) | Catatan (textarea, optional)
Footer: border-top #e5e7eb | 20px pad | "Batal" secondary kiri | "Simpan Penugasan" primary #0db8e8 kanan
```

### Modal Rules — Detail Ilustrasi (satu modal untuk view + edit catatan + update status)
```
Modal: white, 560px wide, 12px radius
Header: "Detail Penugasan Ilustrasi" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan | border-bottom #e5e7eb
Body: 24px pad
  Row atas: nama penugasan Bold + status badge kanan
  Info grid #f9fafb bg, 8px radius, 16px pad:
    Ilustrator (Bold) | Jumlah Gambar | Deadline | Selesai (jika ada) | Event
    Lock indicator di bawah nama Ilustrator: [lucide: lock] 12px #9ca3af + "Tidak dapat diubah" 11px #9ca3af
  Deskripsi Ilustrasi: per gambar dalam card #f9fafb, header "Gambar N" + deskripsi + link referensi
  Catatan: label "Catatan" SemiBold + textarea EDITABLE (bukan read-only) — user bisa langsung edit
    Tombol "Simpan Catatan" — muncul hanya saat isi textarea berubah (dirty state), posisi kanan bawah textarea
  Riwayat: timeline vertikal (assigned, status changed, dll)
Footer: border-top #e5e7eb | 20px pad
  Kiri: "Tutup" secondary
  Kanan: "Tandai Selesai" primary #0db8e8 (hanya jika status = Sedang, dengan mini konfirmasi inline)
```

---

## Module-Specific Layout Rules

### Tabel Penugasan Penulisan (existing) — Tambah Kolom "Ilustrasi"
Kolom baru ditambahkan setelah "Disetujui/Ditugaskan", sebelum "Action". Lebar: 120px max.
Kolom Action existing (eye/pencil/trash) TIDAK DIUBAH — tetap 3 ikon untuk fungsi penugasan soal.

Isi kolom "Ilustrasi":
  Belum Ditugaskan: badge "Belum" abu + [lucide: image-plus] 16px #0db8e8, gap 6px
  Sedang Dikerjakan: badge "Sedang" kuning + [lucide: eye] 16px #0db8e8, gap 6px
  Selesai: badge "Selesai" hijau + [lucide: eye] 16px #0db8e8, gap 6px

Badge compact (agar muat dalam 120px):
  Teks singkat: "Belum" / "Sedang" / "Selesai" (bukan teks panjang)
  9999px radius, 6px H pad, 4px V pad, 11px Medium

### Rekapitulasi Ilustrator — Struktur Halaman (sama dengan Rekapitulasi Penulis)
Halaman: /rekapitulasi/ilustrator
Sidebar menu: Rekapitulasi → sub-item "Ilustrator" (sejajar dengan PJM dan Penulis)
Page title: "Rekapitulasi Ilustrator"
Tombol kanan: "Rekap Ilustrator.Xls" secondary [lucide: download] (sama pola "Rekap Penulisan Soal Terbatas.Xls")
Tab bar: (satu tab saja atau multiple jika ada kategori) — "Semua Ilustrator"
Action row: Show dropdown (10) | Filter button | Search "Cari..."
Tabel:
  Header: Nama | Email | Jumlah Soal Ditugaskan | Jumlah Gambar Ditugaskan | Gambar Selesai | Gambar Belum Selesai | % Selesai | Aksi
  Row: 56px height, border-bottom 1px #e5e7eb
  Kolom numerik: right-aligned, 13px Regular #111827
  % Selesai: teks + mini progress bar (optional), atau badge warna (hijau ≥80%, kuning 50-79%, merah <50%)
  Aksi: [lucide: eye] 16px #0db8e8 (lihat detail soal yang dikerjakan)
Pagination: "Showing X to Y of Z records" | Prev / angka / Next

---

# SECTION 3 — FLOW MAP

## Entry Points
1. Halaman Penugasan → tabel penugasan → klik [lucide: image-plus] di kolom Aksi baris soal status "Belum Ditugaskan"
2. Sidebar → Rekapitulasi → Ilustrator (halaman rekap, akses mandiri)

## Happy Flow A — Assign Ilustrator (dari tabel Penugasan)

[A-01: Halaman Penugasan Penulisan (existing, dengan kolom Ilustrasi baru)]
Tabel menampilkan kolom "Ilustrasi" baru di antara "Disetujui/Ditugaskan" dan "Action".
Baris soal dengan status Ilustrasi "Belum Ditugaskan": kolom Aksi menampilkan [lucide: image-plus] #0db8e8 sebagai ikon pertama.
    ↓ Admin klik [lucide: image-plus] pada baris soal yang diinginkan
[A-02: Modal Assign Ilustrator — single step]
Modal muncul dengan info soal read-only di atas, form di bawah.
Admin isi: Ilustrator (dropdown wajib) + Jumlah Gambar (number wajib, min 1) + Deadline (date wajib) + Catatan (textarea opsional).
    ↓ klik "Simpan Penugasan"
    ├─ SUKSES → Modal tertutup, kolom Ilustrasi baris tersebut berubah → badge "Sedang" + [eye], toast sukses
    └─ VALIDASI ERROR → inline error per field, modal tetap terbuka untuk retry

    ↓ Admin klik [lucide: eye] di kolom Ilustrasi baris status "Sedang" atau "Selesai"
[A-03: Modal Detail Ilustrasi — satu modal untuk view + edit catatan + tandai selesai]
Menampilkan semua info ilustrasi sekaligus. Catatan langsung editable di dalam modal ini.
  - Info soal + Ilustrator (locked) + badge status + deadline
  - Deskripsi per gambar dalam card (Gambar 1, Gambar 2, dst)
  - Field "Catatan": textarea yang bisa langsung diedit — tidak perlu tombol "Edit" dulu
    Tombol "Simpan Catatan" muncul hanya saat textarea berubah (dirty state)
  - Riwayat aktivitas (timeline)
    ↓ Admin edit catatan → klik "Simpan Catatan" (muncul saat ada perubahan)
    ├─ SUKSES → toast "Catatan diperbarui", modal tetap terbuka
    └─ ERROR → toast error
    ↓ Admin klik "Tandai Selesai" di footer (hanya muncul jika status = Sedang)
    → Mini konfirmasi inline: "Tandai selesai? Tidak dapat diubah." + tombol "Ya" / "Batal"
    ├─ Ya → badge di modal + di tabel berubah hijau "Selesai", footer "Tandai Selesai" hilang
    └─ Batal → tidak ada perubahan

## Happy Flow B — Rekapitulasi Ilustrator

[R-01: Halaman Rekapitulasi Ilustrator]
Entry: sidebar → Rekapitulasi → Ilustrator
Tabel merangkum per Ilustrator: jumlah soal, jumlah gambar total, gambar selesai, gambar belum selesai, persentase.
    ↓ klik [lucide: eye] pada baris Ilustrator
[R-02: Out of scope v3 — tersedia di Delta 4]

## Dead-End Screens
- Status "Selesai": hanya [eye] di kolom Ilustrasi — tidak ada image-plus, tidak ada "Tandai Selesai" di modal

## Always-Reachable
- A-01: via sidebar "Penugasan"
- R-01: via sidebar "Rekapitulasi → Ilustrator"

---

# SECTION 4 — MAIN PROMPT

Design dua area baru untuk SIAP Pusmendik Admin Web:
(1) Kolom Ilustrasi + ikon trigger pada tabel Penugasan existing.
(2) Halaman Rekapitulasi Ilustrator (baru, di sidebar Rekapitulasi).
Plus Jakarta Sans, SIAP tokens (sidebar #1a2332, primary #0db8e8), 8px grid.
Semua copy Bahasa Indonesia. 1366×900px frames. Light mode content + dark sidebar.

Replikasi exact SIAP existing: sidebar #1a2332, tabel clean border-bottom, pagination #0db8e8 active, tabs underline.

Produce 7 screens:

---

### SCREEN A-01 | Halaman Penugasan Penulisan — Kolom Ilustrasi Baru

Context: Halaman Penugasan existing (seperti screenshot referensi), dengan penambahan kolom "Ilustrasi" dan penambahan ikon assign pada kolom Action. Tab aktif adalah tab Penugasan Soal Terbatas (atau tab Penulisan — ikuti tab yang sedang aktif di existing).

Sidebar (220px, #1a2332):
- "SIAP | Pusmendik" 14px Bold white, 20px pad
- Avatar "h" circle + "hawarie / admin" white
- Active: "Penugasan" #0db8e8 bg, white 13px Medium, [lucide: grid] 16px white
- Inactive items: rgba(255,255,255,0.6), ikon abu
- "Rekapitulasi" inactive + [lucide: chevron-down] (collapsed di screen ini)
- [lucide: bell] + avatar "h" pojok kanan bawah sidebar

Content area (#f9fafb, 24px pad):

Page header:
- "Penugasan" 18px Bold #111827 kiri
- Kanan: "Template .xls" secondary [lucide: download] 14px | "Bulk Edit" secondary [lucide: edit] | "Import Data" secondary [lucide: upload] | "+ Tambah Penugasan" primary #0db8e8 fill white 14px Bold, 44px, 8px radius

Action row:
- Show "10" dropdown | "Delete Selected Row" secondary disabled | [spacer] | "Filter" border-#0db8e8 text-#0db8e8 white-bg 36px 8px-radius | Search input "Cari" 240px [lucide: search] 14px #9ca3af

Table (white bg, border-bottom per row):

Header row (13px SemiBold #4b5563, 44px, border-bottom #e5e7eb):
[ ] | Nama Penugasan | Nama PJM | Jenis Penugasan | Event | Deadline Penugasan ↕ | Deadline Validasi | Disubmit | Diperbaiki | Disetujui/Ditugaskan | **Ilustrasi** | Action

Data row 1 (56px, border-bottom #e5e7eb) — soal BELUM ditugaskan ilustrasi:
[ ] | "2026-SMK-Kode Program Keahlian-Nama Penulis" 13px #111827 | "Teknik Jaringan Komputer..." 13px #4b5563 | "Penulisan Terbatas Soal Single" 13px #4b5563 | "Penulisan Soal Program Keahlian SMK 2026" 13px #4b5563 | "26 Jun 2026" | "29 Jun 2026" | "4" | "2" | "3/25" |
Kolom Ilustrasi: badge "Belum" #f9fafb bg #6b7280 text #e5e7eb border 11px Medium + [lucide: image-plus] 16px #0db8e8 tooltip "Tugaskan Ilustrator", gap 6px, flex align-center |
Action (tidak diubah): [lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

Data row 2 (56px) — soal SEDANG dikerjakan ilustrasi:
[ ] | "(P01) 2026-SMK-TPG-Ir. Dian Eksana..." | "Farah Perwitasari" | "Penulisan Terbatas Soal Single" | ... | "26 Jun 2026" | "29 Jun 2026" | "25" | "0" | "0/25" |
Kolom Ilustrasi: badge "Sedang" #fefce8 bg #ba7517 text 11px Medium + [lucide: eye] 16px #0db8e8 tooltip "Lihat Detail Ilustrasi", gap 6px |
Action (tidak diubah): [lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

Data row 3 (56px) — soal SELESAI ilustrasi:
[ ] | "(P01) 2026-SMK-KPB-Ir. Maris Setyo..." | "Farah Perwitasari" | "Penulisan Terbatas Soal Single" | ... | "26 Jun 2026" | "29 Jun 2026" | "12" | "0" | "0/25" |
Kolom Ilustrasi: badge "Selesai" #f0fdf4 bg #16a34a text 11px Medium + [lucide: eye] 16px #0db8e8 tooltip "Lihat Detail Ilustrasi", gap 6px |
Action (tidak diubah): [lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

Data rows 4-10: repeat pattern Belum/Sedang/Selesai bervariasi sesuai data existing

Table footer:
"Showing 1 to 10 of 237 records" 13px #4b5563 kiri
Pagination: "Prev" | "1" active #0db8e8 bg white 13px 8px-radius | "2" "3" "4" "5" "..." "10" | "Next"

---

### SCREEN A-02 | Modal — Assign Ilustrator (dari ikon image-plus baris Belum Ditugaskan)

Context: Admin klik [lucide: image-plus] di baris pertama (soal "2026-SMK-Kode Program Keahlian"). Modal overlay muncul. Background tabel dimmed rgba(0,0,0,0.5).

Modal (520px wide, white, 12px radius, 0 8px 32px rgba(0,0,0,0.2), centered):

Header (20px pad, border-bottom #e5e7eb):
"Tugaskan Ilustrator" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan

Body (24px pad):

Info Soal section (#f9fafb bg, 8px radius, 16px pad, margin-bottom 20px):
Row: "Nama Penugasan" 12px Medium #9ca3af → "2026-SMK-Kode Program Keahlian-Nama Penulis" 13px #111827
Row: "Event" 12px Medium #9ca3af → "Penulisan Soal Program Keahlian SMK 2026" 13px #4b5563
Row: "PJM" 12px Medium #9ca3af → "Teknik Jaringan Komputer dan Telekomunikasi" 13px #4b5563
Divider 1px #e5e7eb 8px V margin
Row: "Deskripsi Ilustrasi" 12px Medium #9ca3af
Text: "Buatkan gambar yang menunjukkan topologi jaringan komputer dalam lingkungan sekolah..." 13px Regular #4b5563 (full text, scrollable jika panjang)

Form section:

Field 1: "Pilih Ilustrator *" 13px Medium #4b5563
Dropdown 100%, 44px height, 8px radius, 1px #e5e7eb border
Placeholder "Cari atau pilih ilustrator..." 13px #9ca3af
[lucide: chevron-down] 16px #9ca3af kanan

Field 2 (2 col, gap 12px):
Kol kiri: "Jumlah Gambar *" 13px Medium #4b5563
  Input number 100%, 44px, 1px #e5e7eb, value "1"
  [lucide: minus] 20px kiri | value centered | [lucide: plus] 20px kanan (stepper buttons, 32px each, border-right/left #e5e7eb)
Kol kanan: "Deadline Ilustrasi *" 13px Medium #4b5563
  Date input 100%, 44px, 1px #e5e7eb
  [lucide: calendar] 16px #9ca3af kanan

Field 3: "Catatan untuk Ilustrator" 13px Medium #4b5563 + "(opsional)" 12px #9ca3af inline
Textarea 100%, 88px (3 baris), 8px radius, 1px #e5e7eb
Placeholder "Tambahkan catatan jika deskripsi gambar perlu klarifikasi..."
Counter "0/500" 12px #9ca3af kanan bawah

Footer (border-top #e5e7eb, 20px pad):
"Batal" secondary white 1px #e5e7eb #111827, 44px, 8px radius |
"Simpan Penugasan" primary #0db8e8 fill white 14px Bold, 44px, 8px radius
(Simpan disabled — #e5e7eb bg, #9ca3af text — karena Ilustrator belum dipilih dalam state ini)

---

### SCREEN A-03 | Modal — Detail Ilustrasi (dari ikon eye di kolom Ilustrasi, status Sedang/Selesai)

Context: Admin klik [lucide: eye] di kolom Ilustrasi baris status "Selesai". Modal detail muncul. Ini adalah satu modal yang menggabungkan view, edit catatan, dan update status — tidak ada modal terpisah untuk catatan.

Modal (560px wide, white, 12px radius, 0 8px 32px rgba(0,0,0,0.2), centered):

Header (20px pad, border-bottom #e5e7eb):
"Detail Penugasan Ilustrasi" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan

Body (24px pad, scrollable):

Row atas (flex, space-between, margin-bottom 16px):
Left: "(P01) 2026-SMK-KPB-Ir. Maris Setyo Nugroho, S.Pd., M.Eng." 14px Bold #111827
Right: badge "Selesai" #f0fdf4 bg #16a34a text #16a34a border, 9999px, 8px H pad

Info grid (#f9fafb bg, 8px radius, 16px pad, margin-bottom 20px):
Row: "Ilustrator" 12px #9ca3af → "Margaret" 13px Bold #111827 + [lucide: lock] 12px #9ca3af 4px-gap + "tidak dapat diubah" 11px #9ca3af italic
Row: "Jumlah Gambar" 12px #9ca3af → "2 gambar" 13px #111827
Row: "Deadline" 12px #9ca3af → "28 Jun 2026" 13px #111827
Row: "Selesai" 12px #9ca3af → "27 Jun 2026, 14:30" 13px #16a34a Bold
Row: "Event" 12px #9ca3af → "Penulisan Soal Program Keahlian SMK 2026" 13px #4b5563

Section "Deskripsi Ilustrasi" (margin-top 4px):
"Deskripsi Ilustrasi" 13px SemiBold #111827 margin-bottom 8px

Card Gambar 1 (#f9fafb bg, 8px radius, 12px pad, margin-bottom 8px):
Row: "Gambar 1" 12px SemiBold #111827 (kiri) + [lucide: external-link] 12px #0db8e8 + "Lihat referensi ↗" 12px Medium #0db8e8 (kanan, link)
"Pekerja las memakai APD lengkap sedang mengelas rangka besi." 13px Regular #4b5563

Card Gambar 2 (#f9fafb bg, 8px radius, 12px pad):
"Gambar 2" 12px SemiBold #111827
"Detail sambungan las sebelum dan sesudah finishing." 13px Regular #4b5563

Section "Catatan" (divider atas 1px #e5e7eb, margin-top 16px, padding-top 16px):
"Catatan" 13px SemiBold #111827 margin-bottom 8px
Textarea editable 100%, 88px, 8px radius, 1px #e5e7eb border — prefilled: "Tolong pastikan proporsi gambar sesuai referensi yang diberikan."
Counter "52/500" 12px #9ca3af kanan bawah textarea
Tombol "Simpan Catatan" ghost #0db8e8 13px Medium — muncul di kanan bawah textarea HANYA saat konten textarea berubah (dirty state); tersembunyi saat tidak ada perubahan

Section "Riwayat" (divider atas 1px #e5e7eb, margin-top 16px, padding-top 16px):
"Riwayat Aktivitas" 13px SemiBold #111827
Timeline vertikal (connector 1px #e5e7eb):
  [lucide: check-circle] 14px #16a34a | "Ditandai Selesai" 13px #111827 | "27 Jun 2026, 14:30 · hawarie" 12px #9ca3af
  [lucide: refresh-cw] 14px #ba7517 | "Status Sedang Dikerjakan" 13px #111827 | "26 Jun 2026, 10:45 · hawarie" 12px #9ca3af
  [lucide: user-plus] 14px #0db8e8 | "Ditugaskan ke Margaret" 13px #111827 | "26 Jun 2026, 10:30 · hawarie" 12px #9ca3af

Footer (border-top #e5e7eb, 20px pad):
"Tutup" secondary white 44px 8px-radius kiri
(Jika status = Sedang: tambahkan "Tandai Selesai" primary #0db8e8 44px kanan)
(Jika status = Selesai: tidak ada tombol aksi di kanan — hanya "Tutup")

---

---

### SCREEN A-04 | Toast Notifications + Confirmation "Tandai Selesai"

Context: Satu frame menampilkan A-01 sebagai background + toast sukses kanan bawah + mini confirmation dialog inline di dalam modal detail A-03.

TOAST (fixed bottom-right, 320px, white, 12px radius, 0 4px 12px rgba(0,0,0,0.15), 16px pad):
Left accent 4px #16a34a | [lucide: check-circle] 18px #16a34a | "Penugasan berhasil disimpan" 14px Medium #111827 | "Gabbie ditugaskan ke 2026-SMK-KPB-Ir. Maris..." 12px #4b5563 | [lucide: x] 14px #9ca3af pojok kanan atas

MINI CONFIRMATION (muncul inline di atas footer modal A-03 saat "Tandai Selesai" diklik):
Banner full-width di dalam modal body, di atas footer, background #fefce8 border-top 1px #ba7517:
[lucide: alert-triangle] 14px #ba7517 + "Tandai sebagai Selesai? Status tidak dapat dikembalikan." 13px #ba7517 Medium
Button row kanan: "Batal" 13px ghost #4b5563 | "Ya, Selesai" 13px Medium #0db8e8 text button

---

### SCREEN R-01 | Halaman Rekapitulasi Ilustrator

Context: Admin klik sidebar → Rekapitulasi → Ilustrator. Halaman ini mirip EXACT dengan halaman "Rekapitulasi Penulis" dari screenshot, namun dengan kolom tabel yang disesuaikan untuk data ilustrator.

Sidebar (220px, #1a2332):
- "SIAP | Pusmendik" + user info (sama)
- "Rekapitulasi" active expanded [lucide: chevron-up]:
  Sub-item "PJM" inactive 13px rgba(255,255,255,0.6) 40px 24px-H-pad
  Sub-item "Penulis" inactive
  Sub-item "Ilustrator" ACTIVE: #0db8e8 bg, white 13px Medium, 40px, 24px H pad
- Semua menu lain inactive

Content area (#f9fafb, 24px pad):

Page header:
"Rekapitulasi Ilustrator" 18px Bold #111827 kiri
Kanan: "Rekap Ilustrator.Xls" secondary [lucide: download] 14px #4b5563 + border #e5e7eb, 44px, 8px radius

(No tabs — satu view saja, atau jika ada kategori bisa ditambahkan nanti via delta)

Action row:
"Show" label 13px #4b5563 | "10" dropdown | [spacer flex-grow] | "Filter" border-#0db8e8 text-#0db8e8, 36px | Search input "Cari..." 240px [lucide: search] 14px #9ca3af, 36px, 1px #e5e7eb, 8px radius

Table (white bg, clean border-bottom):

Header row (13px SemiBold #4b5563, 44px, border-bottom #e5e7eb, border-top #e5e7eb):
Nama | Email | Jumlah Soal Ditugaskan | Jumlah Gambar Ditugaskan | Gambar Selesai | Gambar Belum Selesai | % Selesai | Aksi

Data row 1 (56px, border-bottom #e5e7eb):
"Gabbie" 13px Bold #111827 | "gabbie@ilustrasi.id" 13px #4b5563 | "12" center | "18" center | "15" center #16a34a | "3" center #ba7517 | "83%" center (badge: #f0fdf4 bg #16a34a text pill) | [lucide: eye] 16px #0db8e8

Data row 2 (56px):
"Margaret" 13px Bold #111827 | "margaret@gmail.com" 13px #4b5563 | "8" | "14" | "14" #16a34a | "0" #9ca3af | "100%" (#f0fdf4 #16a34a) | [lucide: eye] #0db8e8

Data row 3 (56px):
"Monifa" 13px Bold #111827 | "monifa@mail.com" 13px #4b5563 | "5" | "7" | "3" | "4" #ba7517 | "43%" (#fefce8 #ba7517 badge) | [lucide: eye] #0db8e8

Data row 4 (56px):
"Intan Indreswari" 13px Bold #111827 | "intan@pusmendik.go.id" 13px #4b5563 | "3" | "9" | "0" | "9" #ef4444 | "0%" (#fef2f2 #dc2626 badge) | [lucide: eye] #0db8e8

Data rows 5-10: continue pattern

Table footer:
"Showing 1 to 10 of 23 records" 13px #4b5563 kiri
Pagination: "Prev" secondary | "1" active #0db8e8 bg white, 8px radius | "2" "3" | "Next" secondary

---

### SCREEN R-02 | Rekapitulasi Ilustrator — Kolom % Selesai Badge Variants

Context: Close-up / component guide frame untuk menunjukkan badge % selesai dalam 3 kondisi. Tampilkan sebagai annotation frame di samping atau bagian dari R-01.

% Selesai badge variants:
- ≥80%: "83%" — #f0fdf4 bg, #16a34a text, #16a34a border, 9999px radius, 8px H pad, 5px V pad, 11px Medium
- 50–79%: "67%" — #fefce8 bg, #ba7517 text, #ba7517 border
- <50%: "43%" — #fef2f2 bg, #dc2626 text, #dc2626 border
- 0%: "0%" — #fef2f2 bg, #dc2626 text (paling kritis, perlu perhatian)
- 100%: "100%" — #f0fdf4 bg, #16a34a text (sempurna)

Catatan desain: Badge % selesai lebih informatif dari teks numerik saja karena memberikan sinyal visual instan untuk Admin mengetahui ilustrator mana yang tertinggal.

---

# SECTION 5 — OUTPUT CHECKLIST

- [ ] A-01: Halaman Penugasan existing + kolom "Ilustrasi" baru — badge per status + 1 ikon (image-plus atau eye), kolom Action 3 ikon TIDAK BERUBAH
- [ ] A-02: Modal Assign Ilustrator — info soal read-only, form 3 field wajib + catatan opsional, Simpan disabled saat wajib kosong
- [ ] A-03: Modal Detail Ilustrasi — info + deskripsi per gambar + catatan EDITABLE inline + "Simpan Catatan" ghost muncul saat dirty + riwayat + footer "Tandai Selesai" (jika Sedang) atau hanya "Tutup" (jika Selesai)
- [ ] A-04: Toast sukses + mini confirmation "Tandai Selesai" banner inline di dalam modal
- [ ] R-01: Halaman Rekapitulasi Ilustrator — sidebar sub-menu "Ilustrator" active, tabel kolom pembayaran, pagination
- [ ] R-02: Badge % Selesai variants — 5 state (0%, <50%, 50-79%, ≥80%, 100%)

Global checks:
- [ ] brand_primary = #0db8e8, sidebar_bg = #1a2332 konsisten semua screen
- [ ] 3 status: Belum / Sedang / Selesai — tidak ada "Siap Dikerjakan"
- [ ] Kolom "Ilustrasi" terpisah dari kolom "Action"
- [ ] Kolom Action: tetap 3 ikon existing (eye/edit/trash) di semua status — TIDAK BERUBAH
- [ ] Kolom Ilustrasi: [image-plus] untuk Belum, [eye] untuk Sedang dan Selesai — 1 ikon saja
- [ ] Modal detail A-03: TIDAK ada tombol "Edit Catatan" terpisah — catatan langsung editable di dalam modal
- [ ] Tidak ada modal terpisah untuk edit catatan — dihapus, digabung ke A-03
- [ ] "Simpan Catatan" ghost button hanya muncul saat textarea berubah (dirty state)
- [ ] Ikon [message-square] tidak ada di mana pun — dihapus total
- [ ] R-01 style identik dengan Rekapitulasi Penulis dari screenshot
- [ ] R-02: Badge % Selesai variants — 5 state (0%, <50%, 50-79%, ≥80%, 100%)

Global checks:
- [ ] brand_primary = #0db8e8, sidebar_bg = #1a2332 konsisten semua screen
- [ ] 3 status saja: Belum / Sedang / Selesai — tidak ada "Siap Dikerjakan"
- [ ] Trigger assign HANYA dari ikon image-plus di baris tabel — tidak ada tombol terpisah
- [ ] Status Sedang + Selesai: ikon image-plus TIDAK ADA di kolom aksi
- [ ] Status Sedang + Selesai: field Ilustrator di modal LOCKED, hanya Catatan editable
- [ ] R-01 style identik dengan Rekapitulasi Penulis dari screenshot
- [ ] Ikon: image-plus #0db8e8 (kolom Ilustrasi, Belum) | eye #0db8e8 (kolom Ilustrasi, Sedang/Selesai) | eye #0db8e8 + edit #f59e0b + trash #ef4444 (kolom Action, tidak berubah)
- [ ] Semua copy Bahasa Indonesia
- [ ] Spec labels Bahasa Inggris, copy values Bahasa Indonesia

---

# SECTION 6 — DELTA PROMPTS

### Delta 1 — Add: Validasi Error di Modal Assign (A-02)

ADMIN WEB — Add error states di A-02 saat "Simpan Penugasan" diklik dengan field kosong.
Dropdown Ilustrator kosong: border 1.5px #dc2626, bg #fef2f2 + "[lucide: alert-circle] 12px #dc2626 Pilih ilustrator terlebih dahulu" di bawah field.
Date picker kosong: border 1.5px #dc2626 + "[lucide: alert-circle] 12px #dc2626 Deadline wajib diisi".
Tombol "Simpan" tetap enabled setelah error (user bisa retry).
Modal tidak menutup saat ada error — scroll ke field error pertama otomatis.

### Delta 2 — Add: Status Update dari Modal A-04 (Sedang → Selesai)

ADMIN WEB — Add tombol update status di footer modal A-04.
Jika status saat ini = Sedang Dikerjakan: tambahkan tombol "Tandai Selesai" secondary kanan dari "Edit Catatan".
Klik "Tandai Selesai" → mini confirmation dialog overlay di dalam modal:
  "Tandai ilustrasi ini sebagai Selesai?" 14px #111827
  "Status tidak dapat dikembalikan ke Sedang Dikerjakan." 12px #9ca3af
  "Batal" ghost | "Ya, Tandai Selesai" primary #0db8e8
  Jika Ya → status badge di header modal berubah hijau, modal refresh data, timeline dapat entry baru.

### Delta 3 — Add: Filter Expanded di Halaman Penugasan (A-01)

ADMIN WEB — Add filter panel yang expand dari tombol "Filter" di A-01 untuk memfilter berdasarkan status Ilustrasi.
Filter panel (accordion, muncul di bawah action row, white card, 1px #e5e7eb border, 12px radius, 16px pad):
  Row 1: "Status Ilustrasi" label + chip group: [Semua] [Belum Ditugaskan] [Sedang Dikerjakan] [Selesai]
    Active chip: #e0f7fd bg, #0db8e8 text, #0db8e8 border | Inactive: white + #e5e7eb + #4b5563
  Row 2: "Ilustrator" label + dropdown searchable 200px
  Footer: "Reset" ghost #0db8e8 kiri | "Terapkan" primary #0db8e8 kanan

### Delta 4 — Add: Halaman Detail Ilustrator (dari R-01)

ADMIN WEB — Add Screen R-02b: halaman detail per ilustrator dari klik [lucide: eye] di R-01.
Layout: halaman full (bukan modal) karena data bisa banyak.
Page title: "Detail Rekapitulasi — [Nama Ilustrator]" + breadcrumb "Rekapitulasi Ilustrator > Gabbie"
Header card: Nama + Email + Total Soal + Total Gambar + Gambar Selesai + % Selesai badge besar
Tabel soal yang ditangani:
  Kolom: Nama Penugasan | Kode Soal | Jumlah Gambar | Status | Deadline | Selesai
  Filter: Status (Semua / Sedang / Selesai)
Tombol "Ekspor Detail" secondary kanan atas

### Delta 5 — Fix: Kolom "Ilustrasi" di Tabel Sempit — Tampilan Compact

ADMIN WEB — Fix kolom "Ilustrasi" di A-01 jika tabel terlalu lebar karena kolom baru.
Opsi A (recommended): Gabungkan badge status ilustrasi dengan ikon assign ke dalam satu cell:
  Cell: 100px width max | badge status (11px, pill) | spasi | ikon aksi ilustrasi
  Belum: badge abu + [lucide: image-plus] 14px #0db8e8 kanan
  Sedang: badge kuning
  Selesai: badge hijau
Opsi B: Hilangkan kolom "Ilustrasi" terpisah, pindahkan semua ke kolom "Action" saja — badge + ikon jadi satu.

### Delta 6 — Add: Empty State Rekap Ilustrator (R-01 tanpa data)

ADMIN WEB — Add empty state di R-01 ketika belum ada penugasan ilustrasi sama sekali.
Replace area tabel:
  [lucide: users] 48px #e5e7eb centered
  "Belum ada data ilustrator" 16px Bold #111827 center
  "Mulai tugaskan ilustrator dari halaman Penugasan" 14px #4b5563 center (240px max-width)
  "Buka Halaman Penugasan →" text button #0db8e8 13px Medium centered

---

# OPEN ITEMS & ASUMSI (v3)

## Changelog v3
- ✅ Entry point: dihapus dari dropdown button, sekarang HANYA ikon per baris soal
- ✅ Status disederhanakan: 3 status (Belum / Sedang / Selesai) — hapus "Siap Dikerjakan"
- ✅ Edit permission: Sedang + Selesai hanya bisa edit Catatan, Ilustrator terkunci
- ✅ Modul baru: Rekapitulasi Ilustrator (sub-item sidebar di bawah Rekapitulasi)
- ✅ Kolom Ilustrasi di tabel Penugasan existing (bukan tab terpisah)
- ✅ Halaman Rekap style identik dengan Rekapitulasi Penulis

## Asumsi yang masih terbuka:

| ID | Asumsi | Dampak jika Salah |
|---|---|---|
| OI-01 | Admin yang update status Sedang → Selesai, bukan Ilustrator | Jika Ilustrator bisa self-update, perlu role terpisah |
| OI-02 | Ilustrator tidak punya akses login ke SIAP | Jika punya, perlu notifikasi dan tampilan Ilustrator |
| OI-03 | "Status Sedang Dikerjakan" langsung di-assign oleh Admin saat assign, atau perlu trigger manual "Mulai Dikerjakan"? | Jika auto-Sedang saat assign, UI berbeda |
| OI-04 | Rekap Ilustrator: kolom "Gambar Selesai" dihitung otomatis dari status soal = Selesai | Jika dihitung manual, perlu mekanisme input terpisah |
| OI-05 | 1 kode soal = 1 ilustrator (tidak split per gambar ke orang berbeda) | Jika split, model data dan UI berubah signifikan |
| OI-06 | Hex exact brand #0db8e8 — dikonfirmasi dari estimasi screenshot | Minta dev untuk hex resmi |
| OI-11 (baru) | "Status Sedang Dikerjakan" otomatis setelah assign — tidak perlu tombol "Mulai" terpisah | Jika perlu tombol "Mulai", tambah transisi Belum → Sedang via konfirmasi |
| OI-12 (baru) | Kolom Ilustrasi di tabel tidak membuat tabel terlalu lebar (sudah 11 kolom di existing) | Jika terlalu lebar, gunakan Delta 5 untuk compact layout |

## Pertanyaan untuk Developer:
- Hex exact brand SIAP primary? (#0db8e8 atau berbeda?)
- Apakah soal yang butuh ilustrasi memiliki flag khusus di database? Atau semua soal diasumsikan butuh ilustrasi?
- Status "Sedang Dikerjakan" — apakah otomatis saat assign atau perlu diubah manual oleh Admin?
- Apakah ada batas maksimum jumlah gambar per soal?

---

# ADJUSTMENT PROMPT — Kolom Ilustrasi: Badge Klikable

> Bagian ini adalah adjustment terhadap Screen A-01 dan spesifikasi kolom "Ilustrasi" yang sudah ada di prompt v3 di atas. Terapkan perubahan ini, abaikan spesifikasi kolom Ilustrasi yang sebelumnya.

---

## Perubahan: Kolom "Ilustrasi" — Badge Klikable sebagai Action Zone

### Konsep
Badge di kolom Ilustrasi berfungsi ganda: status indicator sekaligus trigger aksi. Tidak ada ikon lepas atau teks link terpisah di luar badge. Klik badge = buka modal yang relevan sesuai status.

Kolom Action (eye/edit/trash) untuk penugasan soal **tidak berubah sama sekali**.

---

### Spesifikasi Badge per Status

**Status: Belum Ditugaskan**
```
Badge style: #e0f7fd bg · #0db8e8 text · 0.5px #0db8e8 border · 9999px radius · 6px H pad · 4px V pad
Ikon kiri dalam badge: [lucide: image-plus] 12px, warna #0db8e8
Label: "Belum"
Cursor: pointer
Hover: background sedikit lebih gelap (#c5f0fa), border tetap
Tooltip: "Tugaskan ilustrator" — WAJIB, karena aksi tidak obvious dan badge klikable tidak self-evident
Klik → buka Modal Assign Ilustrator (A-02)
```

**Status: Diproses (Sedang Dikerjakan)**
```
Badge style: #fefce8 bg · #854f0b text · 0.5px #ef9f27 border · 9999px radius · 6px H pad · 4px V pad
Ikon kiri dalam badge: [lucide: pencil] 12px, warna #854f0b
Label: "Diproses"
Cursor: pointer
Hover: background sedikit lebih gelap (#fef08a)
Tooltip: tidak perlu — [pencil] sudah self-explanatory sebagai "edit"
Klik → buka Modal Detail Ilustrasi (A-03) dengan catatan editable
```

**Status: Selesai**
```
Badge style: #eaf3de bg · #3b6d11 text · 0.5px #97c459 border · 9999px radius · 6px H pad · 4px V pad
Ikon kiri dalam badge: [lucide: eye] 12px, warna #3b6d11
Label: "Selesai"
Cursor: pointer
Hover: background sedikit lebih gelap (#d1e9b8)
Tooltip: tidak perlu — [eye] + label "Selesai" sudah cukup jelas sebagai "lihat"
Klik → buka Modal Detail Ilustrasi (A-03) dalam mode read-only (tidak ada "Tandai Selesai" di footer)
```

> Tooltip di kolom Action (eye/edit/trash) tetap WAJIB karena icon-only tanpa label teks:
> [lucide: eye] → "Lihat detail penugasan" · [lucide: edit-2] → "Edit penugasan" · [lucide: trash-2] → "Hapus penugasan"

---

### Perbedaan Modal A-03 berdasarkan status yang membuka

**Dibuka dari badge "Diproses":**
- Field Catatan: `editable` (textarea aktif, bisa langsung diketik)
- Tombol "Simpan Catatan": tersembunyi, muncul saat textarea berubah (dirty state)
- Footer: "Tutup" (kiri) + "Tandai Selesai" primary #0db8e8 (kanan)

**Dibuka dari badge "Selesai":**
- Field Catatan: `read-only` (tampilkan teks catatan tanpa border input, style seperti label biasa)
- Tidak ada "Simpan Catatan"
- Footer: "Tutup" saja — tidak ada tombol aksi lain

---

### Implikasi pada Screen A-01 — Update baris tabel

Ganti spesifikasi kolom Ilustrasi di setiap baris menjadi:

```
Baris Belum:
  Kolom Ilustrasi: badge klikable — [lucide: image-plus] 12px + "Belum"
                   warna #e0f7fd / #0db8e8 / border #0db8e8

Baris Diproses:
  Kolom Ilustrasi: badge klikable — [lucide: pencil] 12px + "Diproses"
                   warna #fefce8 / #854f0b / border #ef9f27

Baris Selesai:
  Kolom Ilustrasi: badge klikable — [lucide: eye] 12px + "Selesai"
                   warna #eaf3de / #3b6d11 / border #97c459

Kolom Action (semua baris, tidak berubah):
  [lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444
```

> CATATAN: Ikon [eye] di badge "Selesai" berwarna #3b6d11 (hijau tua, mengikuti warna badge). Ikon [eye] di kolom Action berwarna #0db8e8 (cyan). Warna berbeda + posisi kolom berbeda = tidak ada ambiguitas meski ikon sama.

---

### Checklist tambahan untuk adjustment ini

- [ ] Badge di kolom Ilustrasi memiliki `cursor: pointer` dan hover state
- [ ] Ikon di dalam badge mengikuti warna text badge (bukan selalu cyan)
- [ ] Badge "Belum": tooltip "Tugaskan ilustrator" — wajib
- [ ] Badge "Diproses": tidak ada tooltip — [pencil] self-explanatory
- [ ] Badge "Selesai": tidak ada tooltip — [eye] + label sudah jelas
- [ ] Kolom Action (eye/edit/trash): tooltip wajib di semua ikon karena icon-only
- [ ] Modal A-03 mendeteksi status pembuka: Diproses = editable + footer "Tandai Selesai", Selesai = read-only + footer "Tutup" saja
- [ ] Kolom Action (eye/edit/trash) tidak berubah di semua baris

---

# ADJUSTMENT PROMPT — Section "File Gambar" di Modal Detail A-03

> Tambahkan section ini ke Modal Detail Ilustrasi (A-03) yang sudah ada. Sisipkan setelah section "Deskripsi Ilustrasi" dan sebelum section "Catatan".

---

## Section "File Gambar" — Admin view only, upload dilakukan oleh Ilustrator

### Konteks
Ilustrator memiliki role dan akses login sendiri di SIAP. Mereka yang mengupload file gambar dari sisi mereka. Admin hanya melihat, memverifikasi, dan mendownload hasil upload — tidak ada tombol upload di sisi Admin.

---

### Spesifikasi Section

**Jika Ilustrator belum upload file sama sekali (status Diproses, belum ada file):**
```
Section header: "File Gambar" 13px SemiBold #111827
State empty: #f9fafb bg, 8px radius, 16px pad, border 0.5px dashed #e5e7eb
  [lucide: image] 24px #9ca3af centered
  "Ilustrator belum mengupload file gambar" 13px Regular #9ca3af center
  "File akan muncul di sini setelah Ilustrator mengupload" 12px #9ca3af center
```

**Jika ada file terupload (satu card per gambar, sesuai jumlah gambar di penugasan):**

Card Gambar 1 (#f9fafb bg, 8px radius, 12px pad, margin-bottom 8px):
```
Row atas (flex, space-between):
  Kiri: "Gambar 1" 12px SemiBold #111827
  Kanan: "Diupload 27 Jun 2026, 09.14" 11px #9ca3af

Preview area (margin-top 8px):
  Thumbnail image 100% width, max-height 160px, object-fit contain
  bg #ffffff, border 0.5px #e5e7eb, 6px radius
  Klik thumbnail → buka lightbox/preview full-size di tab baru atau overlay

Row bawah (margin-top 8px, flex, space-between, align-center):
  Kiri: nama file "gambar-1-pengelasan.jpg" 12px #4b5563 + ukuran "2.4 MB" 11px #9ca3af, gap 6px
  Kanan: [lucide: download] 16px #0db8e8, tombol ghost, tooltip "Unduh file"
            [lucide: external-link] 16px #0db8e8, tombol ghost, tooltip "Buka di tab baru"
```

Card Gambar 2 (sama strukturnya, jika ada):
```
Jika Ilustrator belum upload gambar ke-2 tapi sudah upload gambar ke-1:
  Card tetap ditampilkan dengan state empty:
  "Gambar 2 belum diupload" 12px #9ca3af italic, #f9fafb bg dashed border
```

---

### Aturan tampilan

```
Jumlah card = jumlah gambar yang di-set saat assign (field "Jumlah Gambar")
Setiap card selalu ditampilkan — jika file belum ada, tampilkan empty state per card
Urutan: Gambar 1, Gambar 2, dst — sesuai urutan yang ditetapkan saat assign
File yang diterima: JPG, PNG, PDF — Admin tidak perlu tahu teknisnya, cukup preview + download
Thumbnail PDF: tampilkan ikon [lucide: file-text] 32px #0db8e8 centered (tidak bisa preview inline)
```

---

### Implikasi pada tombol "Tandai Selesai"

```
"Tandai Selesai" di footer modal A-03 (hanya muncul jika status Diproses):
  Enabled normal: jika semua gambar sudah terupload
  Enabled dengan warning: jika ada gambar yang belum terupload
    → tampilkan info banner kuning di atas footer sebelum konfirmasi:
      [lucide: alert-triangle] 14px #ba7517
      "Gambar 2 belum diupload. Yakin ingin menandai selesai?"
  Admin tetap bisa tandai selesai meski ada gambar yang belum upload
  — keputusan ada di Admin, sistem tidak memblokir
```

---

### Posisi section dalam modal A-03 (urutan lengkap)

```
1. Header modal
2. Info grid (Ilustrator locked, Jumlah Gambar, Deadline, Event)
3. Deskripsi Ilustrasi (per gambar — deskripsi teks dari penulis soal)
4. ── File Gambar (NEW) ── ← sisipkan di sini
5. Catatan (editable jika Diproses, read-only jika Selesai)
6. Riwayat Aktivitas
7. Footer
```

---

### Checklist untuk section ini

- [ ] Section "File Gambar" muncul setelah "Deskripsi Ilustrasi", sebelum "Catatan"
- [ ] Jumlah card = jumlah gambar yang di-set saat assign
- [ ] Card yang belum ada file-nya tampilkan empty state (dashed border, bukan hilang)
- [ ] Thumbnail klikable — buka preview full-size
- [ ] Tombol download dan buka tab baru tersedia per file
- [ ] Tidak ada tombol upload di sisi Admin — read-only
- [ ] "Tandai Selesai" bisa diklik meski ada gambar belum upload, tapi muncul warning banner dulu
- [ ] Thumbnail PDF: tampilkan ikon file-text, bukan preview gambar

---

# ADJUSTMENT PROMPT — Koreksi Tabel: Halaman Detail Penugasan (Tabel Soal)

> Koreksi dari asumsi sebelumnya. Tabel yang menjadi host kolom Ilustrasi bukan tabel daftar penugasan, melainkan tabel daftar soal di dalam halaman detail penugasan. Abaikan spesifikasi tabel A-01 sebelumnya yang merujuk ke tabel penugasan.

---

## Konteks tabel yang benar

Tabel ini muncul di dalam halaman detail sebuah penugasan — menampilkan daftar soal yang termasuk dalam penugasan tersebut.

Kolom existing (tidak diubah):
```
[ ] | Nomor Soal | Kode Soal | Judul Stimulus | Penulis | Level | Jenis Soal | Tipe Soal | Justifikasi | Status | Action
```

Kolom Action existing berisi:
- [eye] #0db8e8 — lihat detail soal
- [pencil] #9ca3af — edit soal (disabled di status tertentu)
- [trash] #ef4444 — hapus soal
- [lock] #0db8e8 — lock/unlock soal
- [more-vertical] — opsi tambahan (three-dot menu)

---

## Dua kolom baru yang ditambahkan

Posisi: **setelah kolom Status, sebelum kolom Action**

### Kolom 1 — "Ilustrasi"
Lebar: 110px max. Isi: badge klikable saja, tidak ada elemen lain.

```
Status Belum Ditugaskan:
  Badge: [lucide: image-plus] 12px + "Belum"
  Style: #e0f7fd bg · #0db8e8 text · 0.5px #0db8e8 border · 9999px radius
  Cursor: pointer · Tooltip: "Tugaskan ilustrator"
  Klik → Modal Assign Ilustrator

Status Diproses:
  Badge: [lucide: pencil] 12px + "Diproses"
  Style: #fefce8 bg · #854f0b text · 0.5px #ef9f27 border · 9999px radius
  Cursor: pointer · Tooltip: tidak perlu
  Klik → Modal Detail Ilustrasi (catatan editable)

Status Selesai:
  Badge: [lucide: eye] 12px + "Selesai"
  Style: #eaf3de bg · #3b6d11 text · 0.5px #97c459 border · 9999px radius
  Cursor: pointer · Tooltip: tidak perlu
  Klik → Modal Detail Ilustrasi (read-only)
```

> Tidak semua soal butuh ilustrasi. Jika soal tidak memerlukan ilustrasi, kolom ini kosong (tidak ada badge).

---

## Spesifikasi baris tabel lengkap (setelah perubahan)

```
Header row:
[ ] | Nomor Soal | Kode Soal | Judul Stimulus | Penulis | Level | Jenis Soal
    | Tipe Soal | Justifikasi | Status | Ilustrasi (NEW) | Action

Data row contoh 1 — soal Disetujui, belum ada ilustrasi:
[ ] | 1 | 26TJKWDKPJB249MK-000000-0002 | - | Penulis Akademik | SMK | Single
    | Pilihan Ganda | MUDAH
    | badge "Disetujui" hijau + "diperbaiki 0 kali" 11px #9ca3af
    | badge Ilustrasi: [image-plus] + "Belum" #e0f7fd/#0db8e8
    | [eye] [pencil-disabled] [trash] [lock] [more-vertical]

Data row contoh 2 — soal Diperbaiki, ilustrasi Diproses:
[ ] | 2 | 26TJKWDKPBI250MK-000000-0001 | - | Penulis Akademik | SMK | Single
    | MCMA | -
    | badge "Diperbaiki" amber + "diperbaiki 1 kali" 11px #9ca3af
    | badge Ilustrasi: [pencil] + "Diproses" #fefce8/#854f0b
    | [eye] [pencil] [trash] [lock] [more-vertical]

Data row contoh 3 — soal Disetujui, ilustrasi Selesai:
[ ] | 3 | 26TJKWDKPBI250MK-000000-0003 | - | Penulis Akademik | SMK | Single
    | Kategori (Radio) | SEDANG
    | badge "Disetujui" hijau + "diperbaiki 1 kali" 11px #9ca3af
    | badge Ilustrasi: [eye] + "Selesai" #eaf3de/#3b6d11
    | [eye] [pencil-disabled] [trash] [lock] [more-vertical]

Data row contoh 4 — soal tidak butuh ilustrasi (kolom kosong):
[ ] | 4 | 26TJKWDKPBI250MK-000000-0006 | - | Penulis Akademik | SMK | Single
    | Pilihan Ganda | MUDAH
    | badge "Disetujui" hijau + "diperbaiki 1 kali" 11px #9ca3af
    | kolom Ilustrasi: kosong (—)
    | [eye] [pencil-disabled] [trash] [lock] [more-vertical]
```

---

## Style kolom Status (dari screenshot — replikasi exact)

```
Badge status soal (bukan ilustrasi):
  "Disetujui": #16a34a fill, white text, 9999px radius, 8px H pad — solid fill (bukan outline)
  "Diperbaiki": #f59e0b fill, white text — solid fill
  Sub-label di bawah badge: "diperbaiki X kali" 11px #0db8e8 (link style, klikable)

Action icons (existing, tidak diubah):
  [eye] #0db8e8 — dengan border kotak tipis di baris pertama (selected state)
  [pencil] #9ca3af disabled / #f59e0b active
  [trash] #ef4444
  [lock] #0db8e8
  [more-vertical] #9ca3af
```

---

## Checklist

- [ ] Tabel yang dimaksud adalah tabel soal di dalam halaman detail penugasan — bukan tabel daftar penugasan
- [ ] Kolom "Ilustrasi" disisipkan setelah "Status", sebelum "Action"
- [ ] Kolom Action existing (eye/pencil/trash/lock/more) tidak berubah
- [ ] Badge Ilustrasi kosong (—) untuk soal yang tidak butuh ilustrasi
- [ ] Badge status soal existing: solid fill (hijau/amber), bukan outline
- [ ] Sub-label "diperbaiki X kali" di bawah badge status soal: 11px #0db8e8

---

# ADJUSTMENT PROMPT — Tambah Section Ilustrasi di Halaman Detail Penugasan

> Halaman Detail Penugasan sudah memiliki header stats (stat cards soal + waktu tersisa) dan info penugasan di atas tabel soal. Tambahkan satu stat card baru untuk ilustrasi di dalam stats bar yang sudah ada, dan satu info row di section info penugasan.

---

## Konteks halaman existing (dari screenshot)

Halaman Detail Penugasan terdiri dari:
1. Page title "Detail Penugasan" + tombol "Edit Penugasan" kanan
2. Stats bar — deretan stat cards horizontal: Soal Ditugaskan, Soal Wajib, Soal Rekomendasi, Soal Disubmit, Soal Diperbaiki, Soal Disetujui + card "Waktu Tersisa" (amber)
3. Info penugasan — grid 2 kolom: Nama Penugasan, Jenis Penugasan, Deadline Validasi, Event, Deadline Penugasan, Penanggung Jawab Materi
4. Tabel soal (dengan kolom Ilustrasi baru — lihat adjustment sebelumnya)

---

## Perubahan 1 — Tambah stat card Ilustrasi di stats bar

### Style stats bar existing (replikasi exact)
```
Container: background #2d7d9a (teal-navy), border-radius 8px, padding 0
Setiap card: flex-1, padding 16px 20px, border-right 1px rgba(255,255,255,0.2)
Label: 11px SemiBold white uppercase letter-spacing 0.05em, margin-bottom 6px
Nilai: 28px Bold white
Card "Waktu Tersisa": background #e8b84b (amber), border-radius 0 8px 8px 0
  Label: 11px SemiBold #7a4f00 uppercase
  Nilai: 18px Bold #7a4f00 ("0 hari 9 jam 51 menit")
```

### Card baru yang ditambahkan
Sisipkan **sebelum card "Waktu Tersisa"**, setelah "Soal Disetujui":

```
Card "ILUSTRASI SELESAI":
  Background: sama dengan card soal lainnya (#2d7d9a)
  Border-right: 1px rgba(255,255,255,0.2)
  Label: "ILUSTRASI SELESAI" 11px SemiBold white uppercase
  Nilai: "3/25" 28px Bold white
    Format: [jumlah selesai] / [jumlah total soal butuh ilustrasi]
    Jika belum ada yang selesai: "0/25"
    Jika semua soal tidak butuh ilustrasi: tidak tampilkan card ini
```

### Stats bar setelah perubahan (urutan lengkap)
```
[Soal Ditugaskan] [Soal Wajib] [Soal Rekomendasi] [Soal Disubmit]
[Soal Diperbaiki] [Soal Disetujui] [Ilustrasi Selesai ✦] [Waktu Tersisa]
```

---

## Perubahan 2 — Tidak ada perubahan di section info penugasan

Section info (Nama Penugasan, Jenis, Deadline, Event, dst) tidak perlu ditambah apapun — data ilustrasi sudah cukup terwakili di stats bar dan tabel soal.

---

## Spesifikasi lengkap stats bar (untuk generate ulang)

```
Container stats bar:
  Background: #2d7d9a
  Border-radius: 8px
  Display: flex
  Width: 100%
  Margin-bottom: 16px

Setiap card soal (flex-1):
  Padding: 16px 20px
  Border-right: 1px solid rgba(255,255,255,0.2)
  Label: "SOAL DITUGASKAN" / "SOAL WAJIB" / dst — 11px SemiBold #ffffff uppercase
  Nilai: 28px Bold #ffffff

Card "ILUSTRASI SELESAI" (flex-1, NEW):
  Style identik dengan card soal
  Label: "ILUSTRASI SELESAI"
  Nilai: "X/Y" — X = gambar selesai, Y = total gambar ditugaskan

Card "WAKTU TERSISA" (flex: 0 0 200px):
  Background: #e8b84b
  Border-radius: 0 8px 8px 0 (hanya kanan yang rounded)
  Padding: 16px 24px
  Label: "WAKTU TERSISA" 11px SemiBold #7a4f00 uppercase center
  Nilai: "0 hari 9 jam 51 menit" 18px Bold #7a4f00 center
```

---

## Checklist

- [ ] Card "Ilustrasi Selesai" disisipkan sebelum "Waktu Tersisa" di stats bar
- [ ] Style card Ilustrasi identik dengan card soal lainnya (background, font, warna)
- [ ] Format nilai: "X/Y" bukan hanya angka tunggal
- [ ] Card tidak muncul jika tidak ada soal yang butuh ilustrasi dalam penugasan ini
- [ ] Card "Waktu Tersisa" tetap paling kanan dengan background amber — tidak berubah posisi
- [ ] Section info penugasan tidak ada perubahan
