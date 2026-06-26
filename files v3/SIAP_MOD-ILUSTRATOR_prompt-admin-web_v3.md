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
| Icon assign | #0db8e8 | Ikon trigger assign ilustrator (image-plus) di baris soal belum ditugaskan |
| Icon edit (catatan) | #f59e0b | Ikon edit catatan di status Sedang/Selesai |
| Icon view | #0db8e8 | Eye icon di semua status |
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

| Status | Boleh ubah Ilustrator | Boleh ubah Catatan |
|---|---|---|
| Belum Ditugaskan | Ya (via modal assign) | Tidak ada data |
| Sedang Dikerjakan | TIDAK | Ya |
| Selesai | TIDAK | Ya |

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
  "entry_point": "Ikon [lucide: image-plus] di kolom Aksi setiap baris soal yang statusnya Belum Ditugaskan",
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
Setiap baris soal di tabel memiliki kolom "Ilustrasi" yang menampilkan status ilustrasi soal tersebut. Jika status "Belum Ditugaskan", kolom ini menampilkan ikon [lucide: image-plus] yang bisa diklik untuk memicu modal assign langsung — tidak ada halaman atau wizard terpisah.

Modal assign: satu halaman (non-wizard), form singkat. Setelah submit: status berubah inline di baris, modal tertutup.

Jika status sudah "Sedang Dikerjakan" atau "Selesai": ikon berubah menjadi [lucide: message-square] (edit catatan) + [lucide: eye] (lihat detail) — tidak ada ikon assign lagi.

### What NOT to adopt
- Tombol "Tambah Penugasan Ilustrasi" di action bar (dihapus dari v2)
- Opsi di dropdown "+ Tambah Penugasan" (dihapus dari v2)
- Modal wizard 2-step (diganti single modal langsung)
- Tab "Penugasan Ilustrasi" terpisah — kolom Ilustrasi langsung ada di tabel Penugasan Penulisan existing

### Table Row Specs
Row: white bg, 1px #e5e7eb border-bottom, 56px min-height
Status badge ilustrasi: pill, 9999px radius, 8px H pad, 5px V pad, 11px Medium
Ikon trigger di kolom Aksi:
  Belum Ditugaskan: [lucide: image-plus] 16px #0db8e8 — tooltip "Tugaskan Ilustrator"
  Sedang/Selesai: [lucide: eye] 16px #0db8e8 + [lucide: message-square] 16px #f59e0b — tooltip "Lihat Detail" + "Edit Catatan"

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
Modal padding: 24px | Modal width: 520px (assign) / 560px (detail/edit catatan)
```

### Modal Rules — Assign Ilustrator (single-step, bukan wizard)
```
Overlay: rgba(0,0,0,0.5)
Modal: white, 520px wide, 12px radius, 0 8px 32px rgba(0,0,0,0.2), centered
Header: "Tugaskan Ilustrator" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan | 20px pad | border-bottom #e5e7eb
Body: 24px pad
  Info section: #f9fafb bg, 8px radius, 16px pad — read-only data kode soal
  Form: Pilih Ilustrator (dropdown, required) | Jumlah Gambar (number, required) | Deadline (date, required) | Catatan (textarea, optional)
Footer: border-top #e5e7eb | 20px pad | "Batal" secondary kiri | "Simpan" primary #0db8e8 kanan
```

### Modal Rules — Edit Catatan (status Sedang/Selesai)
```
Modal: white, 480px wide, 12px radius
Header: "Edit Catatan Ilustrator" 16px Bold #111827 | close
Body:
  Info card read-only: Kode Soal, Ilustrator (LOCKED — tidak bisa diubah), Status badge
  Lock indicator: [lucide: lock] 14px #9ca3af + "Ilustrator tidak dapat diubah setelah penugasan dimulai" 12px #9ca3af
  Textarea "Catatan untuk Ilustrator": editable, 120px, 500 char max
Footer: "Batal" secondary | "Simpan Catatan" primary #0db8e8
```

### Modal Rules — Lihat Detail (view only)
```
Modal: white, 560px wide, 12px radius
Header: "Detail Penugasan Ilustrasi" 16px Bold | close
Body:
  Info kode soal read-only
  Deskripsi ilustrasi lengkap + URL referensi (link)
  Ilustrator + status + deadline
  Catatan (read-only)
  Riwayat aktivitas (timeline)
Footer: "Tutup" secondary | (jika Sedang/Selesai) "Edit Catatan" primary #0db8e8
```

---

## Module-Specific Layout Rules

### Tabel Penugasan Penulisan (existing) — Tambah Kolom Ilustrasi
Kolom baru ditambahkan setelah kolom "Disetujui/Ditugaskan", sebelum "Action":
Kolom "Ilustrasi": 120px width
  Isi: status badge ilustrasi ("Belum" / "Sedang" / "Selesai")
  Jika Belum: badge abu + ikon [lucide: image-plus] 14px #0db8e8 kanan badge (clickable, trigger modal assign)
  Jika Sedang: badge kuning (text terpotong jadi "Sedang" saja agar muat)
  Jika Selesai: badge hijau

Kolom Action: tambahkan ikon:
  Jika Belum Ditugaskan: ikon [lucide: image-plus] 16px #0db8e8 sebagai salah satu aksi (paling kiri dari grup ikon aksi)
  Jika Sedang/Selesai: ikon [lucide: eye] 16px #0db8e8 + [lucide: message-square] 16px #f59e0b

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
    ├─ SUKSES → Modal tertutup, kolom Ilustrasi baris tersebut berubah → badge "Sedang Dikerjakan", ikon aksi berubah ke [eye] + [message-square], toast sukses kanan bawah
    └─ VALIDASI ERROR → inline error per field, modal tetap terbuka untuk retry

[A-03: Modal Edit Catatan — dari [lucide: message-square] di baris Sedang/Selesai]
Modal kecil muncul. Info kode soal + Ilustrator read-only + lock indicator.
Field "Catatan untuk Ilustrator" editable (prefill jika sudah ada catatan sebelumnya).
    ↓ klik "Simpan Catatan"
    ├─ SUKSES → Modal tertutup, catatan tersimpan, toast "Catatan berhasil diperbarui"
    └─ ERROR → toast error

[A-04: Modal Lihat Detail — dari [lucide: eye] di baris Sedang/Selesai]
Modal detail read-only. Tampilkan semua info + deskripsi lengkap + riwayat aktivitas.
Footer: tombol "Edit Catatan" (jika bukan Sedang/Selesai tidak ada batasan — tapi Ilustrator tetap locked).
    ↓ klik "Edit Catatan" → modal A-03 menggantikan A-04

[A-05: Update Status Sedang → Selesai — dari kolom Aksi atau dari modal detail A-04]
Admin klik ikon status atau tombol di modal detail → mini confirmation: "Tandai sebagai Selesai?"
    ├─ "Ya, Selesai" → status badge di baris berubah hijau "Selesai", completed_at tersimpan
    └─ "Batal" → tidak ada perubahan

## Happy Flow B — Rekapitulasi Ilustrator

[R-01: Halaman Rekapitulasi Ilustrator]
Entry: sidebar → Rekapitulasi → Ilustrator
Tabel merangkum per Ilustrator: jumlah soal, jumlah gambar total, gambar selesai, gambar belum selesai, persentase.
    ↓ klik [lucide: eye] pada baris Ilustrator
[R-02: Modal/Halaman Detail Ilustrator]
Daftar kode soal yang ditugaskan ke Ilustrator ini + status per soal.
(Out of scope untuk v3 prompt — delta prompt tersedia)

## Dead-End Screens
- Status "Selesai" di tabel: ikon image-plus tidak ada, hanya eye + message-square

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
**Kolom Ilustrasi: badge "Belum" #f9fafb bg #6b7280 text #e5e7eb border, 11px Medium** |
Action: [lucide: image-plus] 16px #0db8e8 (tooltip "Tugaskan Ilustrator") | [lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

Data row 2 (56px) — soal SEDANG dikerjakan ilustrasi:
[ ] | "(P01) 2026-SMK-TPG-Ir. Dian Eksana..." | "Farah Perwitasari" | "Penulisan Terbatas Soal Single" | ... | "26 Jun 2026" | "29 Jun 2026" | "25" | "0" | "0/25" |
**Kolom Ilustrasi: badge "Sedang" #fefce8 bg #ba7517 text, 11px Medium** |
Action: [lucide: eye] 16px #0db8e8 (tooltip "Lihat Detail Ilustrasi") | [lucide: message-square] 16px #f59e0b (tooltip "Edit Catatan Ilustrator") | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

Data row 3 (56px) — soal SELESAI ilustrasi:
[ ] | "(P01) 2026-SMK-KPB-Ir. Maris Setyo..." | "Farah Perwitasari" | "Penulisan Terbatas Soal Single" | ... | "26 Jun 2026" | "29 Jun 2026" | "12" | "0" | "0/25" |
**Kolom Ilustrasi: badge "Selesai" #f0fdf4 bg #16a34a text, 11px Medium** |
Action: [lucide: eye] 16px #0db8e8 | [lucide: message-square] 16px #f59e0b | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444

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

### SCREEN A-03 | Modal — Edit Catatan Ilustrator (status Sedang/Selesai, Ilustrator locked)

Context: Admin klik [lucide: message-square] pada baris soal status "Sedang Dikerjakan". Modal muncul. Ilustrator TIDAK bisa diubah.

Modal (480px wide, white, 12px radius):

Header (20px pad, border-bottom #e5e7eb):
"Edit Catatan Ilustrator" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan

Body (24px pad):

Info Locked section (#f9fafb bg, 8px radius, 16px pad, margin-bottom 20px):
Row: "Kode Soal" 12px #9ca3af → "(P01) 2026-SMK-TPG-Ir. Dian Eksana Wibowo S.T., M.Eng." 13px Bold #111827
Row: "Ilustrator" 12px #9ca3af → "Gabbie" 13px #111827 + [lucide: lock] 14px #9ca3af 4px-gap kanan nama
Row: "Status" 12px #9ca3af → badge "Sedang Dikerjakan" #fefce8 #ba7517
Row: "Deadline" 12px #9ca3af → "30 Jun 2026" 13px #111827

Lock warning (margin-top 12px, border-top #e5e7eb, padding-top 12px):
[lucide: info] 14px #9ca3af + "Ilustrator tidak dapat diubah setelah penugasan dimulai. Hubungi administrator jika ada perubahan mendesak." 12px Regular #9ca3af

Field "Catatan untuk Ilustrator" (margin-top 20px):
Label 13px Medium #4b5563
Textarea 100%, 120px, 8px radius, 1px #e5e7eb border (EDITABLE — ini yang bisa diubah)
Prefill contoh: "Tolong pastikan proporsi gambar panci sesuai referensi yang diberikan."
Counter "52/500" 12px #9ca3af kanan bawah

Footer (border-top #e5e7eb, 20px pad):
"Batal" secondary | "Simpan Catatan" primary #0db8e8

---

### SCREEN A-04 | Modal — Lihat Detail Penugasan Ilustrasi

Context: Admin klik [lucide: eye] pada baris soal status "Selesai". Modal full-detail read-only.

Modal (560px wide, white, 12px radius):

Header (20px pad, border-bottom #e5e7eb):
"Detail Penugasan Ilustrasi" 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan

Body (24px pad):

Row atas header info (flex, space-between):
Left: "(P01) 2026-SMK-KPB-Ir. Maris Setyo Nugroho, S.Pd., M.Eng." 14px Bold #111827
Right: badge "Selesai" #f0fdf4 #16a34a pill

Info grid (#f9fafb bg, 8px radius, 16px pad, margin-bottom 16px):
Row: "Ilustrator" → "Margaret" 13px Bold #111827 | "Jumlah Gambar" → "2 gambar" 13px #111827
Row: "Deadline" → "28 Jun 2026" 13px #111827 | "Selesai" → "27 Jun 2026, 14:30" 13px #16a34a
Row: "Event" → "Penulisan Soal Program Keahlian SMK 2026" 13px #4b5563

Divider 1px #e5e7eb

Section "Deskripsi Ilustrasi" (margin-top 16px):
"Deskripsi Ilustrasi" 13px SemiBold #111827 margin-bottom 8px
Gambar 1 (#f9fafb bg, 8px radius, 12px pad, margin-bottom 8px):
  "Gambar 1" 12px SemiBold #111827 | deskripsi 13px #4b5563 full text
  [lucide: external-link] 12px #0db8e8 + "Lihat referensi ↗" 12px Medium #0db8e8 kanan
Gambar 2 (#f9fafb bg, 8px radius, 12px pad):
  "Gambar 2" 12px SemiBold #111827 | deskripsi 13px #4b5563

Section "Catatan" (divider atas, margin-top 16px):
"Catatan" 13px SemiBold #111827
"Tolong pastikan proporsi gambar panci sesuai referensi yang diberikan." 13px #4b5563

Section "Riwayat" (divider atas, margin-top 16px):
"Riwayat Aktivitas" 13px SemiBold #111827
Timeline (vertikal, connector 1px #e5e7eb):
  [lucide: check-circle] 14px #16a34a | "Ditandai Selesai" 13px #111827 | "27 Jun 2026, 14:30 · hawarie" 12px #9ca3af
  [lucide: refresh-cw] 14px #ba7517 | "Status diubah ke Sedang Dikerjakan" 13px #111827 | "26 Jun 2026, 10:45 · hawarie" 12px #9ca3af
  [lucide: user-plus] 14px #0db8e8 | "Ditugaskan ke Margaret" 13px #111827 | "26 Jun 2026, 10:30 · hawarie" 12px #9ca3af

Footer (border-top #e5e7eb, 20px pad):
"Tutup" secondary kiri | "Edit Catatan" primary #0db8e8 kanan (bisa klik walau status Selesai — hanya catatan)

---

### SCREEN A-05 | Toast Notifications + Confirmation Mini Dialog

Context: Satu frame menampilkan A-01 sebagai background + toast sukses kanan bawah + mini confirmation dialog inline.

TOAST (fixed bottom-right, 320px, white, 12px radius, 0 4px 12px rgba(0,0,0,0.15), 16px pad):
Left accent 4px #16a34a | [lucide: check-circle] 18px #16a34a | "Penugasan berhasil disimpan" 14px Medium #111827 | "Gabbie ditugaskan ke 2026-SMK-KPB-Ir. Maris..." 12px #4b5563 | [lucide: x] 14px #9ca3af pojok kanan atas

MINI CONFIRMATION DIALOG (floating card dari action di tabel):
Posisi: muncul dekat baris yang di-trigger (bubbles dari ikon)
Card: white, 8px radius, 1px #e5e7eb border, 0 4px 12px rgba(0,0,0,0.15), 240px, 16px pad
"Tandai sebagai Selesai?" 13px Medium #111827
"Status tidak dapat dikembalikan." 12px #9ca3af
Button row: "Batal" 13px #4b5563 ghost | "Ya, Selesai" 13px Medium #0db8e8 text button

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

- [ ] A-01: Halaman Penugasan existing + kolom "Ilustrasi" baru — 3 row example (Belum/Sedang/Selesai), ikon aksi per status berbeda
- [ ] A-02: Modal Assign Ilustrator — info soal read-only, form 3 field wajib, Simpan disabled state
- [ ] A-03: Modal Edit Catatan — Ilustrator LOCKED, lock indicator, textarea editable
- [ ] A-04: Modal Lihat Detail — info lengkap, deskripsi per gambar, riwayat aktivitas, footer Edit Catatan
- [ ] A-05: Toast + Confirmation mini dialog — inline dari tabel
- [ ] R-01: Halaman Rekapitulasi Ilustrator — sidebar "Ilustrator" active di sub-menu Rekapitulasi, tabel dengan kolom pembayaran
- [ ] R-02: Badge % Selesai variants — 5 state (0%, <50%, 50-79%, ≥80%, 100%)

Global checks:
- [ ] brand_primary = #0db8e8, sidebar_bg = #1a2332 konsisten semua screen
- [ ] 3 status saja: Belum / Sedang / Selesai — tidak ada "Siap Dikerjakan"
- [ ] Trigger assign HANYA dari ikon image-plus di baris tabel — tidak ada tombol terpisah
- [ ] Status Sedang + Selesai: ikon image-plus TIDAK ADA di kolom aksi
- [ ] Status Sedang + Selesai: field Ilustrator di modal LOCKED, hanya Catatan editable
- [ ] R-01 style identik dengan Rekapitulasi Penulis dari screenshot
- [ ] Ikon image-plus #0db8e8 | eye #0db8e8 | message-square #f59e0b | edit #f59e0b | trash #ef4444
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
