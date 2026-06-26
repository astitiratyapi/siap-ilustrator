# AI Design Prompt — Penugasan Ilustrator (Admin)
## SIAP Pusmendik · MOD-ILUSTRATOR · Penugasan ilustrator ke kode soal oleh Admin
### Platform: Admin Web · 1366px · greenfield · v2 (revised entry point + brand colors)

---

# BRAND GUIDELINE

## Project
**Name:** SIAP (Sistem Informasi Asesmen dan Pembelajaran) — Pusmendik
**Client:** Pusat Penilaian Pendidikan (Pusmendik), Kemendikbud
**Design System:** A'raf DS — PT Badr Interactive (dengan override warna SIAP)
**Icon Library:** Lucide — lucide.dev/icons
**Logo Source:** Untitled UI Logos — untitledui.com/resources/logos

---

## Brand Colors (SIAP Actual — dari screenshot existing)

### Sidebar / Shell Color
**Hex:** #1a2332
**Used for:** Background sidebar, top bar (dark shell seluruh aplikasi)
**White text on this color:** PASS — sidebar selalu dark, teks dan ikon putih/abu muda

### Primary / Accent Color
**Hex:** #0db8e8
**Used for:** Tombol CTA utama (+ Tambah Penugasan, Tambah Ilustrasi), active menu item di sidebar, link aksi primer, tombol Filter, step indicator aktif
**On white background:** Perlu dikonfirmasi — gunakan white text (#ffffff) di atas warna ini untuk tombol
**White text on this color:** Gunakan pada tombol solid; hindari sebagai teks body kecil

### Action Icon Colors (dari existing table)
**View / Lihat:** #0db8e8 (eye icon — sama dengan brand primary)
**Edit:** #f59e0b (amber — pencil icon)
**Delete:** #ef4444 (red — trash icon)

> Catatan: Warna brand SIAP menggunakan cyan cerah (#0db8e8) sebagai primary, bukan navy A'raf DS default (#004990). Sidebar menggunakan dark shell (#1a2332). Override ini diambil langsung dari screenshot aplikasi existing.

---

## System Colors (A'raf DS standard — tidak diubah)

| Role | Hex | Usage |
|---|---|---|
| Success | #16a34a | Status Selesai, konfirmasi berhasil |
| Warning | #ba7517 | Status Sedang Dikerjakan, deadline hampir lewat |
| Error | #dc2626 | Validasi gagal, deadline terlewat, aksi destruktif |
| Info | #0db8e8 | Status Siap Dikerjakan — samakan dengan brand primary SIAP |

---

## Text Colors

| Role | Hex | Usage | WCAG on white |
|---|---|---|---|
| Primary text | #111827 | Heading, kode soal, nama, label utama | 16.0:1 — PASS |
| Secondary text | #4b5563 | Deskripsi, body, konten card | 7.0:1 — PASS |
| Tertiary text | #9ca3af | Caption, placeholder, meta (decorative only) | 2.8:1 — FAIL untuk teks |

> text_tertiary (#9ca3af) TIDAK lolos WCAG AA. Gunakan text_secondary (#4b5563) untuk semua teks readable.

---

## Surface Colors

| Role | Hex | Usage |
|---|---|---|
| Page background | #f9fafb | Latar halaman konten (area putih abu muda) |
| Card surface | #ffffff | Semua card, modal, tabel |
| Border default | #e5e7eb | Border card, divider, border tabel, border input |
| Sidebar bg | #1a2332 | Background sidebar + topbar |
| Sidebar text inactive | rgba(255,255,255,0.55) | Menu item tidak aktif di sidebar |
| Sidebar text active | #ffffff | Menu item aktif + ikon aktif di sidebar |
| Sidebar active indicator | #0db8e8 | Background highlight item aktif (rounded) |
| Input focus border | #0db8e8 | Input saat dalam fokus |

---

## Typography

**Font family:** Plus Jakarta Sans
**Weights used:** Regular (400), Medium (500), SemiBold (600), Bold (700)

| Element | Size | Weight | Color |
|---|---|---|---|
| Page title | 18px | Bold | text_primary |
| Section heading | 15px | SemiBold | text_primary |
| Table header | 13px | SemiBold | text_secondary |
| Table cell body | 13px | Regular | text_primary |
| Label input | 13px | Medium | text_secondary |
| Caption / meta | 12px | Regular | text_tertiary |
| Badge / status pill | 11px | Medium | varies by status |
| Kode soal | 13px | Medium | text_primary |

---

## Component Color Guide

### Buttons (mengikuti style existing SIAP)
- **Primary button:** #0db8e8 fill, #ffffff 14px Bold — contoh: "+ Tambah Penugasan", "Tambah Ilustrasi"
- **Secondary button:** #ffffff fill, 1px #e5e7eb border, #111827 14px Medium — contoh: "Template .xls", "Bulk Edit", "Import Data"
- **Filter button:** #0db8e8 text + border 1px #0db8e8, white bg — sesuai pola existing (tombol Filter di halaman Penugasan)
- **Destructive / icon delete:** #ef4444 icon, no bg, hover: #fef2f2 bg
- **Disabled:** #e5e7eb fill, #9ca3af text

### Dropdown "Tambah Penugasan" (pola existing)
Menu item dalam dropdown: 14px Regular #111827, hover: #f9fafb bg
Separator antar group jika ada: 1px #e5e7eb

### Status Badges (Penugasan Ilustrasi)
- **Belum Ditugaskan:** #f9fafb bg · #6b7280 text · #e5e7eb border
- **Siap Dikerjakan:** #e0f7fd bg · #0db8e8 text · #0db8e8 border (sesuai brand cyan SIAP)
- **Sedang Dikerjakan:** #fefce8 bg · #ba7517 text · #ba7517 border
- **Selesai:** #f0fdf4 bg · #16a34a text · #16a34a border

### Action Icons (sesuai existing)
- [lucide: eye] 16px #0db8e8 (view)
- [lucide: edit-2] 16px #f59e0b (edit)
- [lucide: trash-2] 16px #ef4444 (delete)

---

## Accessibility Summary

**WCAG Standard:** 2.1 Level AA

| Pair | Ratio | Normal text | Large text | UI |
|---|---|---|---|---|
| white on #0db8e8 (brand primary) | ~3.0:1 | FAIL | PASS | PASS |
| #0db8e8 on white | ~3.0:1 | FAIL | PASS | PASS |
| text_primary on white | 16.0:1 | PASS | PASS | PASS |
| text_secondary on white | 7.0:1 | PASS | PASS | PASS |
| text_tertiary on white | 2.8:1 | FAIL | FAIL | FAIL |

**Overall:** WARNING — #0db8e8 sebagai warna brand tidak lolos untuk teks kecil. Gunakan hanya pada tombol (large UI), ikon, dan border. Semua label, body, dan teks tabel gunakan text_primary (#111827) atau text_secondary (#4b5563).

---

# CONTEXT BLOCK

```json
{
  "project_name": "SIAP Pusmendik",
  "client": "Pusmendik — Kemendikbud",
  "module_id": "MOD-ILUSTRATOR",
  "module_name": "Penugasan Ilustrator",
  "platform": "Admin Web",
  "mode": "greenfield",
  "frame_width": 1366,
  "frame_height": 900,
  "design_system": "A'raf DS — PT Badr Interactive (dengan SIAP brand override)",
  "font": "Plus Jakarta Sans",
  "language": "Indonesian",
  "stage": "POC — happy flow first draft untuk konfirmasi stakeholder",
  "flow_inspiration": "List + Detail dengan modal wizard 2-step (FLOW-06 + FLOW-07 hybrid)",
  "visual_inspiration": "SIAP existing style — dark sidebar shell, cyan primary, information-dense table",
  "icon_library": "Lucide — lucide.dev/icons",
  "entry_point": "Dropdown '+ Tambah Penugasan' → opsi ke-4 'Tambah Ilustrasi' → modal wizard 2-step",
  "tokens": {
    "brand_primary": "#0db8e8",
    "brand_secondary": "#0db8e8",
    "sidebar_bg": "#1a2332",
    "page_bg": "#f9fafb",
    "card_surface": "#ffffff",
    "border_default": "#e5e7eb",
    "text_primary": "#111827",
    "text_secondary": "#4b5563",
    "text_tertiary": "#9ca3af",
    "icon_view": "#0db8e8",
    "icon_edit": "#f59e0b",
    "icon_delete": "#ef4444",
    "success": "#16a34a",  "success_bg": "#f0fdf4",
    "warning": "#ba7517",  "warning_bg": "#fefce8",
    "error": "#dc2626",    "error_bg":   "#fef2f2",
    "info": "#0db8e8",     "info_bg":    "#e0f7fd"
  },
  "business_rules": {
    "BR-01_one_illustrator_per_soal": "1 Ilustrator menangani ilustrasi pada 1 kode soal — tidak bisa split ke beberapa Ilustrator",
    "BR-02_multiple_images_per_soal": "Dalam 1 kode soal, ilustrasi dapat terdiri dari lebih dari 1 gambar — jumlah gambar wajib diisi saat penugasan",
    "BR-03_admin_only": "Hanya Admin yang dapat membuat, mengubah, dan memperbarui status penugasan ilustrator",
    "BR-04_one_active_assignment": "1 kode soal hanya dapat ditugaskan ke 1 Ilustrator pada satu waktu — re-assign hanya jika status belum Selesai",
    "BR-05_status_forward_only": "Status hanya bisa maju: Belum Ditugaskan → Siap Dikerjakan → Sedang Dikerjakan → Selesai",
    "BR-06_tugaskan_requires_ilustrator_and_deadline": "Form penugasan tidak dapat disubmit jika Ilustrator atau Deadline belum dipilih — kedua field wajib diisi",
    "BR-07_entry_via_dropdown": "Penugasan Ilustrator tidak memiliki menu sidebar sendiri — diakses via dropdown '+ Tambah Penugasan' → opsi 'Tambah Ilustrasi'"
  }
}
```

---

# SECTION 1 — VISUAL REFERENCES

## Flow Reference — List + Modal Wizard Hybrid (FLOW-06 + FLOW-07 adapted)

### What to adopt
**Halaman list (panel bawah):** tabel penugasan ilustrasi yang muncul sebagai tab atau section baru di halaman Penugasan existing, bukan halaman terpisah. Filter chips horizontal di atas tabel.
**Entry point via dropdown:** tombol "+ Tambah Penugasan" existing memiliki dropdown dengan 3 opsi existing + 1 opsi baru "Tambah Ilustrasi". Klik "Tambah Ilustrasi" membuka modal wizard.
**Modal wizard 2-step:** Step 1 pilih kode soal (dari penugasan soal yang sudah ada), Step 2 assign ilustrator + deadline. Progress indicator di header modal.
**Tabel list:** kode soal + status badge + ilustrator + deadline + aksi inline (view, edit, update status).
**Detail via drawer/panel kanan** atau modal penuh — bukan halaman baru — agar konsisten dengan pola modal existing.

### What NOT to adopt
- Halaman terpisah dengan route baru (tidak ada di struktur navigasi existing)
- Sub-menu di sidebar (tidak ada — diakses dari dropdown saja)
- Infinite scroll (gunakan pagination sesuai pola existing)
- Left accent stripe pada tabel — existing tidak menggunakan pola ini

### Table Row Specs (matching existing SIAP style)
Row: white bg, 1px #e5e7eb border-bottom, 56px height (sesuai existing)
Header row: white bg, 13px SemiBold #4b5563, border-bottom 1px #e5e7eb
Status badge: pill 9999px radius, 8px H pad, 5px V pad, 11px Medium
Action icons: [lucide: eye] 16px #0db8e8 | [lucide: edit-2] 16px #f59e0b | [lucide: trash-2] 16px #ef4444
Row hover: very subtle #f9fafb (sesuai existing, tidak ada hover state yang kuat)
Checkbox: kiri setiap row + header row (sesuai existing)

---

## Visual Style Reference — SIAP Existing (dari screenshot)

Tone: Profesional, government-adjacent, fungsional. Dense information, consistent dengan aplikasi existing.

Key characteristics yang WAJIB direplikasi dari existing:
- **Dark sidebar (#1a2332):** seluruh sidebar dark navy, teks menu putih, active item highlight cyan rounded
- **Light content area:** background #f9fafb, card putih
- **Primary CTA:** fill solid #0db8e8, teks putih, 8px radius — contoh tombol "+ Tambah Penugasan"
- **Secondary CTAs:** white fill, 1px #e5e7eb border, teks #111827 — contoh "Template .xls", "Bulk Edit", "Import Data"
- **Filter button:** special style — bukan primary bukan secondary, gunakan style existing ("Filter" dengan border biru atau bold)
- **Table:** clean, minimal, border-bottom only per row, header abu, ikon aksi 3 warna (cyan/amber/red)
- **Dropdown dari button:** floating white card, 12px radius, shadow, list items 44px height, hover #f9fafb
- **Pagination:** "Prev" dan angka halaman, active page #0db8e8 bg white text (sesuai existing)

Apply token overrides:
Shell/sidebar: #1a2332 | Primary: #0db8e8 | Secondary button: white + #e5e7eb border
Text: #111827 primary, #4b5563 secondary | Background: #f9fafb | Card: #ffffff

---

# SECTION 2 — LAYOUT RULES

## Master Layout Rules — Admin Web (SIAP style)

### Screen Structure
```
[Sidebar — 220px, #1a2332 bg, fixed]
  "SIAP | Pusmendik" header: logo/wordmark white, 20px padding top
  User info: avatar circle "h" + "hawarie / admin" putih kecil, 20px padding
  Nav items: 44px height, 16px H pad, 8px radius
    Active: #0db8e8 bg (subtle tint atau fill), white text 13px Medium, ikon putih
    Inactive: transparent, rgba(255,255,255,0.6) text, ikon abu muda
  Menu items: User Management, Penugasan (active), Event Management, Framework Management,
    Repositori, Pengumuman, Master Data, Perakitan, Rekapitulasi (dengan caret expand),
    Riwayat Pengguna, Analisis Soal
  Bottom: notif bell + user avatar "h" rounded, #ffffff 24px

[Top Bar — integrated dengan content, bukan fixed bar terpisah]
  Kiri: page title "Penugasan" 18px Bold #111827
  Kanan: tombol-tombol aksi (Template .xls, Bulk Edit, Import Data, + Tambah Penugasan)

[Content Area — #f9fafb bg, 24px padding]
  Show dropdown + Delete Selected Row + Filter + Search bar
  Tabel utama dalam white card implicit (tabel langsung, border per row)
  Pagination di bawah tabel
```

### Spacing (Admin Web — SIAP)
```
Content padding: 24px | Row height: 56px | Table cell H pad: 16px
Filter/action area: 16px V margin bawah | Button gap: 8px
Modal padding: 24px | Modal max-width: 600px
```

### Dropdown Button Pattern (Tambah Penugasan)
```
Trigger button: "+ Tambah Penugasan" #0db8e8 fill, white 14px Medium, 44px height, 8px radius
Dropdown card: white, 8px radius, 1px #e5e7eb border, shadow 0 4px 12px rgba(0,0,0,0.12)
  Lebar: sama dengan tombol trigger atau lebih lebar (min 220px)
  Item: 44px height, 16px H pad, 14px Regular #111827, hover #f9fafb bg
  Separator: 1px #e5e7eb jika ada group
  Items existing: "Tambah Penulisan" | "Tambah Perevisian" | "Tambah Penulisan Soal Terbatas"
  Item baru:  separator 1px #e5e7eb + "Tambah Ilustrasi" [lucide: image] 16px #0db8e8 kiri
```

### Modal Wizard Rules
```
Overlay: rgba(0,0,0,0.5) full-screen
Modal: white, 600px wide, 12px radius, shadow 0 8px 32px rgba(0,0,0,0.18), centered
Header modal: 20px padding, border-bottom 1px #e5e7eb
  Title: 16px Bold #111827 | [lucide: x] 20px #9ca3af kanan (hover: #111827)
Step indicator (di bawah title, dalam header):
  2 steps horizontal, circles 28px
  Step selesai: #16a34a fill + [lucide: check] white 14px
  Step aktif: #0db8e8 fill + angka 13px Bold white
  Step belum: white fill + 1.5px #e5e7eb border + angka 13px #9ca3af
  Connector: 2px horizontal, #16a34a (selesai) / #e5e7eb (belum)
  Label 11px Medium di bawah circle: aktif #0db8e8 | selesai #16a34a | belum #9ca3af
Body: 24px padding, max-height 70vh, scrollable
Footer: 20px padding, border-top 1px #e5e7eb
  Kiri: "Kembali" secondary (disabled di step 1) | Kanan: "Lanjut" / "Simpan Penugasan" primary
```

---

## Module-Specific Layout Rules

### List + Table Rules (sesuai pola existing SIAP)
Tabel muncul di halaman Penugasan existing — BUKAN halaman baru.
Implementasi sebagai TAB BARU: di bawah action bar existing, tambahkan tab bar:
  Tab 1: "Penugasan Penulisan" (existing, default active)
  Tab 2: "Penugasan Ilustrasi" (new)
  Tab style: underline active (#0db8e8 bottom border 2px), 14px Medium, 44px height

Dalam tab "Penugasan Ilustrasi":
  Action bar (sama pola existing): [Template .xls secondary] [Import Data secondary] [+ Tambah Ilustrasi primary #0db8e8]
    Note: di tab ini, tombol "+ Tambah Penugasan" dropdown tidak ada — diganti dengan "+ Tambah Ilustrasi" langsung
  Show dropdown (10, 25, 50) + Delete Selected Row (disabled jika tidak ada pilihan) + Filter button + Search
  Tabel dengan kolom: checkbox | Kode Soal | Nama Penulis | Mata Pelajaran | Deskripsi Ilustrasi | Ilustrator | Status | Deadline | Aksi

Pagination: "Showing X to Y of Z records" kiri | Prev/angka/Next kanan (sesuai existing)
Active page: #0db8e8 bg, white text, 8px radius

### Tabel Filter Tambahan (di atas tabel, baris terpisah dari action bar)
Pola: sama dengan "Filter" button di existing (klik expand atau inline chips)
Filter: Status (All/Belum/Siap/Sedang/Selesai) | Mata Pelajaran | Ilustrator

---

# SECTION 3 — FLOW MAP

## Entry Points
Halaman Penugasan (existing) → TAB "Penugasan Ilustrasi"
ATAU: tombol "+ Tambah Penugasan" (existing, pojok kanan atas) → dropdown → "Tambah Ilustrasi" → modal wizard

## Happy Flow — Tambah Penugasan Ilustrasi (via dropdown)

[A-01: Halaman Penugasan — Tab "Penugasan Ilustrasi"] ← always-reachable via sidebar "Penugasan" → tab kedua
Admin melihat tabel kode soal dengan kolom: Kode Soal, Nama Penulis, Mata Pelajaran, Deskripsi Ilustrasi, Ilustrator, Status, Deadline, Aksi.
    ↓ klik "+ Tambah Penugasan" (pojok kanan atas, existing button)
    ↓ dropdown muncul → klik "Tambah Ilustrasi"
[A-02: Modal Wizard Step 1 — Pilih Kode Soal]
Modal muncul. Step indicator: Step 1 aktif (Pilih Kode Soal) | Step 2 inactive (Tugaskan Ilustrator).
Admin melihat tabel kode soal yang BELUM ditugaskan ilustrasinya (difilter otomatis: status = Belum Ditugaskan).
Tabel: Kode Soal | Nama Penulis | Mata Pelajaran | Preview Deskripsi | Checkbox pilih.
Search "Cari kode soal..." di atas tabel modal.
Admin centang satu atau lebih kode soal.
    ↓ klik "Lanjut" (enabled hanya jika minimal 1 kode soal dipilih)
[A-03: Modal Wizard Step 2 — Tugaskan Ilustrator]
Step indicator: Step 1 selesai (✓) | Step 2 aktif (Tugaskan Ilustrator).
Summary kode soal terpilih: "X kode soal dipilih" + daftar (scrollable, 2 baris jika banyak).
Form input:
  - Dropdown "Pilih Ilustrator *" (searchable)
  - Number input "Jumlah Gambar *" (default 1, per kode soal)
  - Date picker "Deadline Ilustrasi *"
  - Textarea "Catatan untuk Ilustrator" (opsional, 500 chars max)
Note jika multi-select: "Ilustrator dan deadline yang sama akan diterapkan ke semua kode soal terpilih" 12px #ba7517 dengan [lucide: info]
    ↓ klik "Simpan Penugasan" (primary, enabled hanya jika Ilustrator + Deadline terisi)
    ├─ SUKSES → Modal tertutup, tabel di A-01 refresh, baris baru muncul status "Siap Dikerjakan",
               toast sukses kanan bawah: "X penugasan berhasil disimpan"
    └─ VALIDASI ERROR → border merah + pesan inline, tombol Simpan tetap aktif untuk retry

[A-04: Modal Detail & Edit — dari klik ikon view/edit di tabel]
Modal full-detail: info kode soal (read-only) + deskripsi lengkap + ilustrator + status + riwayat.
Tombol "Edit Penugasan" secondary di footer modal (hanya jika status bukan Selesai).
    ↓ klik "Edit Penugasan" → form fields menjadi editable dalam modal yang sama (atau modal baru)
    ↓ klik "Simpan Perubahan"
    ↓ konfirmasi dialog inline: "Yakin mengubah penugasan ini?"
    ├─ Ya → data diperbarui, status kembali ke "Siap Dikerjakan"
    └─ Tidak → kembali ke modal detail

[A-05: Update Status] ← dari dropdown aksi inline di tabel (kolom Aksi atau klik ikon)
Dropdown kecil per baris: "Tandai Sedang Dikerjakan" | "Tandai Selesai"
    ├─ Sedang Dikerjakan → langsung update, badge berubah
    └─ Selesai → confirmation mini-dialog: "Tandai selesai? Aksi ini tidak dapat diubah."
               → Ya: status Selesai, icon aksi hanya View (tanpa edit/delete)

## Dead-End Screens
- Status "Selesai" → hanya View, tidak ada edit atau update lebih lanjut di baris tersebut

## Always-Reachable
- A-01: via sidebar "Penugasan" → pilih tab "Penugasan Ilustrasi"

## Handoff ke Modul Lain
→ Tab "Penugasan Penulisan": klik tab pertama di halaman yang sama
→ Entry langsung dari dropdown "+ Tambah Penugasan" di tab manapun

---

# SECTION 4 — MAIN PROMPT

Design Penugasan Ilustrator untuk SIAP Pusmendik Admin Web.
SIAP adalah platform manajemen soal pendidikan nasional. Fitur ini ditambahkan ke halaman Penugasan existing sebagai tab baru "Penugasan Ilustrasi", dan dapat diakses melalui dropdown button "+ Tambah Penugasan" → "Tambah Ilustrasi".
Plus Jakarta Sans, SIAP brand tokens (sidebar #1a2332, primary #0db8e8), 8px grid.
Semua copy dalam Bahasa Indonesia. 1366×900px frames. Light mode content area, dark sidebar shell.

Replikasi exact style dari UI existing SIAP:
- Sidebar: #1a2332 bg, white text, active item #0db8e8 highlight
- Content: #f9fafb bg, white tabel, minimal shadow
- Buttons: #0db8e8 fill primary, white fill + border secondary
- Table icons: eye #0db8e8, edit #f59e0b, trash #ef4444

Apply all Layout Rules from Section 2 strictly.
Follow the Flow Map from Section 3 exactly.

Produce 6 screens as frames (1366×900px):

---

### SCREEN A-01 | Halaman Penugasan — Tab "Penugasan Ilustrasi"

Context: Halaman Penugasan existing yang sudah ada, dengan penambahan tab bar. Tab "Penugasan Ilustrasi" sedang aktif. Ini adalah landing state setelah Admin memilih tab tersebut.

Sidebar (220px, #1a2332 bg):
- Header: "SIAP | Pusmendik" 14px Bold #ffffff, 20px H pad, 16px V pad
- User: avatar circle "h" #0db8e8 bg white "h" + "hawarie" 12px white + "admin" 11px rgba(255,255,255,0.6)
- Nav items (44px, 16px H, 8px radius):
  "Penugasan" — active: #0db8e8 fill rounded, white 13px Medium + [lucide: grid] 16px white kiri
  "User Management" — inactive: transparent, rgba(255,255,255,0.6), [lucide: user] abu
  "Event Management" — inactive
  "Framework Management" — inactive
  "Repositori" — inactive
  "Pengumuman" — inactive
  "Master Data" — inactive
  "Perakitan" — inactive
  "Rekapitulasi" — inactive, [lucide: chevron-down] kanan (expandable)
  "Riwayat Pengguna" — inactive
  "Analisis Soal" — inactive
- Bottom right: [lucide: bell] 20px rgba(255,255,255,0.6) + avatar circle "h" 32px

Content area (#f9fafb bg, 24px padding):

Page header row:
- Left: "Penugasan" 18px Bold #111827
- Right: tombol secondary "Template .xls" [lucide: download] 16px #4b5563 kiri | "Import Data" [lucide: upload] 16px #4b5563 kiri | "+ Tambah Penugasan" primary #0db8e8 fill white 14px Medium, 44px, 8px radius [lucide: plus] 16px white kiri
- Gap 8px antar tombol

Tab bar (margin-top 16px, border-bottom 1px #e5e7eb):
- Tab 1: "Penugasan Penulisan" 14px Regular #9ca3af, padding 0 16px 12px, tidak ada underline
- Tab 2: "Penugasan Ilustrasi" 14px Medium #0db8e8, padding 0 16px 12px, border-bottom 2px #0db8e8 (active indicator)

Action bar (margin-top 16px, sama pola existing):
- Left: "Show" label 13px #4b5563 + dropdown "10" + "Delete Selected Row" button (disabled state, border #e5e7eb, text #9ca3af)
- Right: "Filter" button (1px #0db8e8 border, #0db8e8 text 13px Medium, 36px height, 8px radius) + Search input "Cari kode soal atau penulis..." 240px, [lucide: search] 14px #9ca3af kiri, 36px height, 8px radius, 1px #e5e7eb border

Table (white bg, border-top 1px #e5e7eb):
Header row (white bg, border-bottom 1px #e5e7eb, 44px):
[ ] | Kode Soal/Stimulus | Nama Penulis | Mata Pelajaran | Deskripsi Ilustrasi | Ilustrator | Status | Deadline | Aksi
(13px SemiBold #4b5563, 16px H padding per cell)

Data row 1 — Siap Dikerjakan (56px):
[ ] | "26FISKALKLPF10SA-000000-0035" 13px Regular #111827 | "Wahyu Adam" 13px #111827 | "Fisika" 13px #4b5563 | "Buat gambar panci seperti pada referensi..." 12px #4b5563 2 baris terpotong | "Gabbie" 13px #111827 | badge "Siap Dikerjakan" #e0f7fd bg #0db8e8 text 11px Medium, 9999px radius | "30 Jun 2026" 13px #111827 | [lucide: eye] 16px #0db8e8 gap8 [lucide: edit-2] 16px #f59e0b gap8 [lucide: trash-2] 16px #ef4444

Data row 2 — Belum Ditugaskan (56px):
[ ] | "26ANTPANPDAA22SA-000000-0078" 13px #111827 | "Agusta Rudyana" 13px #111827 | "Antropologi" 13px #4b5563 | "Buatkan Seorang antropolog laki-laki usia muda..." 12px #4b5563 2 baris | "—" 13px #9ca3af | badge "Belum Ditugaskan" #f9fafb bg #6b7280 text #e5e7eb border | "—" 13px #9ca3af | [lucide: eye] 16px #0db8e8 gap8 [lucide: edit-2] 16px #f59e0b gap8 [lucide: trash-2] 16px #ef4444

Data row 3 — Selesai (56px):
[ ] | "26KORSMALITK01SA-000000-0088" 13px #111827 | "Ranti Eka Pratiwi" 13px #111827 | "Bahasa Korea" 13px #4b5563 | "Gambar siswa laki-laki bertuliskan 유다 di dada..." 12px #4b5563 2 baris | "Margaret" 13px #111827 | badge "Selesai" #f0fdf4 bg #16a34a text | "28 Jun 2026" 13px #111827 | [lucide: eye] 16px #0db8e8 (hanya view, tidak ada edit/delete karena Selesai)

Data row 4 — Sedang Dikerjakan (56px):
[ ] | "ARABILAAWB14SA-000000-0021" 13px #111827 | "Muhammad Ainul Mukmin" 13px #111827 | "Bahasa Arab" 13px #4b5563 | "Buatkan gambar kakak (lk) dan adik kecil (lk)..." 12px #4b5563 2 baris | "Monifa" 13px #111827 | badge "Sedang Dikerjakan" #fefce8 bg #ba7517 text | "27 Jun 2026" 13px #dc2626 (merah karena hampir lewat) | [lucide: eye] 16px #0db8e8 [lucide: edit-2] 16px #f59e0b

Table footer:
"Showing 1 to 10 of 47 records" 13px #4b5563 kiri
Pagination kanan: "Prev" secondary 36px | "1" active #0db8e8 bg white 13px | "2" | "3" | "4" | "5" | "..." | "10" | "Next" secondary 36px

---

### SCREEN A-02 | Dropdown "+ Tambah Penugasan" (dropdown expanded state)

Context: Admin klik tombol "+ Tambah Penugasan" di pojok kanan atas. Dropdown menu muncul di bawah tombol. Ini bisa terjadi dari tab "Penugasan Penulisan" atau "Penugasan Ilustrasi".

Tampilkan halaman A-01 sebagai background, dengan:

Dropdown card (floating, white, 8px radius, 1px #e5e7eb border, shadow 0 4px 16px rgba(0,0,0,0.12), 220px wide, positioned right-aligned di bawah tombol trigger, 4px gap):
- Item 1: "Tambah Penulisan" 14px Regular #111827, 44px height, 16px H pad, hover #f9fafb bg
- Item 2: "Tambah Perevisian" 14px Regular #111827, 44px height, 16px H pad, hover #f9fafb bg
- Item 3: "Tambah Penulisan Soal Terbatas" 14px Regular #111827, 44px height, 16px H pad, hover #f9fafb bg
- Separator: 1px #e5e7eb, 0 4px margin
- Item 4 (NEW): [lucide: image] 16px #0db8e8 kiri 8px gap | "Tambah Ilustrasi" 14px Medium #0db8e8 (warna berbeda untuk membedakan dari 3 opsi di atas), 44px height, 16px H pad, hover #e0f7fd bg

---

### SCREEN A-03 | Modal Wizard Step 1 — Pilih Kode Soal

Context: Modal muncul setelah Admin klik "Tambah Ilustrasi" dari dropdown. Background dimmed (rgba 0,0,0,0.5).

Modal (600px wide, white, 12px radius, centered, shadow 0 8px 32px rgba(0,0,0,0.2)):

Modal header (20px padding, border-bottom 1px #e5e7eb):
- "Tambah Penugasan Ilustrasi" 16px Bold #111827
- [lucide: x] 20px #9ca3af kanan (hover #111827)

Step indicator (16px padding, 8px margin-bottom, dalam header area):
- Step 1 aktif: circle 28px #0db8e8 fill, "1" 13px Bold white | connector 40px #e5e7eb | Step 2 belum: circle 28px white 1.5px #e5e7eb border "2" 13px #9ca3af
- Label bawah step 1: "Pilih Kode Soal" 11px Medium #0db8e8
- Label bawah step 2: "Tugaskan Ilustrator" 11px Regular #9ca3af

Modal body (24px padding):

Info banner #e0f7fd bg, 1px #0db8e8 border, 8px radius, 12px padding, margin-bottom 16px:
[lucide: info] 14px #0db8e8 kiri | "Pilih satu atau lebih kode soal yang memerlukan ilustrasi." 12px #0db8e8

Search (margin-bottom 12px):
Input "Cari kode soal atau nama penulis..." 100%, 36px height, [lucide: search] 14px #9ca3af kiri, 1px #e5e7eb border, 8px radius

Tabel kode soal belum ditugaskan (max-height 320px, scrollable):
Header: [ ] checkbox | Kode Soal/Stimulus | Nama Penulis | Mata Pelajaran (13px SemiBold #4b5563)
Row: 44px height | checkbox | kode soal 13px Regular #111827 | nama penulis 13px #4b5563 | mapel 13px #9ca3af

Row 1 selected (checkbox checked, row bg #e0f7fd):
[✓] | "26ANTPANPDAA22SA-000000-0078" | "Agusta Rudyana" | "Antropologi"

Row 2 unchecked:
[ ] | "ARABILAAWB14SA-000000-0021" | "Muhammad Ainul Mukmin" | "Bahasa Arab"

Row 3 unchecked:
[ ] | "KORELITSA015SA-000000-0044" | "Ranti Eka Pratiwi" | "Bahasa Korea"

Footer mini di bawah tabel (border-top 1px #e5e7eb, 12px padding):
"Showing 1 to 10 of 23 records" 12px #4b5563 | pagination kanan (compact)

Selection counter (kiri bawah sebelum footer modal):
"1 kode soal dipilih" 13px Medium #0db8e8

Modal footer (20px padding, border-top 1px #e5e7eb):
- "Batal" secondary white 44px | "Lanjut →" primary #0db8e8 44px (enabled karena 1 row dipilih)

---

### SCREEN A-04 | Modal Wizard Step 2 — Tugaskan Ilustrator

Context: Admin sudah memilih 1 kode soal di Step 1 dan klik "Lanjut". Modal tetap sama, konten berganti ke Step 2.

Modal header: sama (judul + close)

Step indicator (updated):
- Step 1 selesai: circle 28px #16a34a fill + [lucide: check] 12px white | connector 40px #16a34a
- Step 2 aktif: circle 28px #0db8e8 fill "2" 13px Bold white
- Label step 1: "Pilih Kode Soal" 11px #16a34a | Label step 2: "Tugaskan Ilustrator" 11px #0db8e8

Modal body (24px padding):

Summary kode soal terpilih (#f9fafb bg, 8px radius, 12px padding, margin-bottom 20px):
"Kode soal terpilih:" 12px Medium #4b5563
Card ringkas: "26ANTPANPDAA22SA-000000-0078" 13px Bold #111827 | "Agusta Rudyana · Antropologi" 12px #4b5563
[lucide: edit-2] 12px #0db8e8 kanan, tooltip "Kembali ubah pilihan"

Form fields:

Row 1:
Label "Pilih Ilustrator *" 13px Medium #4b5563 + "*" #dc2626
Dropdown 100%, 44px, 8px radius, 1px #e5e7eb border, [lucide: chevron-down] kanan
Placeholder "Cari atau pilih ilustrator..." 13px #9ca3af
Options tersedia: "Gabbie", "Margaret", "Monifa", "Intan Indreswari", "+ Tambah ilustrator baru"

Row 2 (2 kolom, 12px gap):
Kol kiri: "Jumlah Gambar *" 13px Medium #4b5563
  Input number 100%, 44px, 1px #e5e7eb, nilai "1", tombol [-] kiri [+] kanan (masing-masing 32px)
Kol kanan: "Deadline Ilustrasi *" 13px Medium #4b5563
  Date input 100%, 44px, 1px #e5e7eb, [lucide: calendar] 16px #9ca3af kanan
  Value: "30-06-2026"

Row 3:
Label "Catatan untuk Ilustrator" 13px Medium #4b5563 + "(opsional)" 12px #9ca3af
Textarea 100%, 88px, 8px radius, 1px #e5e7eb, placeholder "Tambahkan catatan jika deskripsi gambar perlu klarifikasi..."
Counter "0/500" 12px #9ca3af kanan bawah

Modal footer:
"← Kembali" secondary white 44px | "Simpan Penugasan" primary #0db8e8 44px
(Simpan disabled: #e5e7eb bg #9ca3af text — karena Ilustrator belum dipilih dalam contoh ini)

---

### SCREEN A-05 | Modal Detail Kode Soal (dari ikon view di tabel)

Context: Admin klik [lucide: eye] di baris tabel A-01. Modal detail muncul, menampilkan informasi lengkap satu kode soal dan progress penugasannya.

Modal (600px wide, white, 12px radius, centered):

Modal header:
"Detail Penugasan Ilustrasi" 16px Bold #111827 | [lucide: x] kanan

Modal body (24px padding):

Section 1 — Info Kode Soal (#f9fafb bg, 8px radius, 16px padding, margin-bottom 20px):
Row: "Kode Soal" 12px Medium #9ca3af | "26FISKALKLPF10SA-000000-0035" 13px Medium #111827
Row: "Penulis Soal" 12px Medium #9ca3af | "Wahyu Adam" 13px #111827
Row: "Mata Pelajaran" 12px Medium #9ca3af | "Fisika" 13px #111827
Row: "Status" 12px Medium #9ca3af | badge "Siap Dikerjakan" #e0f7fd #0db8e8 pill
Row: "Ilustrator" 12px Medium #9ca3af | "Gabbie" 13px #111827 Bold
Row: "Deadline" 12px Medium #9ca3af | "30 Jun 2026" 13px #111827
Row: "Ditugaskan" 12px Medium #9ca3af | "26 Jun 2026, 10:45 oleh hawarie" 13px #4b5563

Divider 1px #e5e7eb, 12px V margin

Section 2 — Deskripsi Ilustrasi:
Label "Deskripsi Ilustrasi" 13px SemiBold #111827, margin-bottom 8px
"Buat gambar panci seperti pada referensi namun konteksnya sedang memasak sayur wortel, jadi ada beberapa potong wortel yang naik dari dasar panci ke permukaan setelah dipanaskan, ada juga potongan wortel (lebih sedikit) yang sedang turun dari permukaan air yang mendidih menuju dasar panci." 13px Regular #4b5563

Label "Referensi Gambar" 12px Medium #9ca3af, margin-top 12px
[lucide: external-link] 14px #0db8e8 + "Lihat referensi gambar ↗" 13px Medium #0db8e8 (link)

Section 3 — Riwayat (divider atas 1px #e5e7eb, margin-top 16px):
Label "Riwayat Aktivitas" 13px SemiBold #111827
Timeline item: [lucide: check-circle] 14px #0db8e8 | "Ditugaskan ke Gabbie" 13px #111827 | "26 Jun 2026, 10:45 · hawarie" 12px #9ca3af
Timeline item: [lucide: plus-circle] 14px #9ca3af | "Penugasan dibuat" 13px #111827 | "26 Jun 2026, 10:30 · hawarie" 12px #9ca3af

Modal footer (border-top 1px #e5e7eb, 20px padding):
Dropdown "Perbarui Status" secondary [lucide: chevron-down] kanan (options: Sedang Dikerjakan, Selesai) | "Edit Penugasan" secondary | [spacer] | "Tutup" primary #0db8e8

---

### SCREEN A-06 | Toast Notifications + Confirmation Dialog

Context: Komponen feedback yang muncul setelah berbagai aksi. Tampilkan dalam satu frame: A-01 sebagai background + 1 toast aktif + 1 mini confirmation dialog.

TOAST (fixed bottom-right, 20px margin, 320px wide, white, 12px radius, 0 4px 12px rgba(0,0,0,0.15) shadow, 16px padding):
- [lucide: check-circle] 18px #16a34a kiri
- "Penugasan berhasil disimpan" 14px Medium #111827
- "Gabbie ditugaskan ke 26ANTPANPDAA22SA-000000-0078" 12px Regular #4b5563
- Left accent stripe 4px #16a34a
- [lucide: x] 14px #9ca3af kanan atas

CONFIRMATION MINI-DIALOG (muncul inline dari action dropdown status, floating card bukan full modal):
Card: white, 8px radius, 1px #e5e7eb border, shadow 0 4px 12px rgba(0,0,0,0.15), 240px wide, 16px padding
Posisi: di atas/dekat dropdown trigger di tabel
"Tandai sebagai Selesai?" 14px Medium #111827
"Aksi ini tidak dapat diubah kembali." 12px Regular #4b5563
Buttons: "Batal" 13px #4b5563 ghost | "Ya, Selesai" 13px Medium #0db8e8 (text button)
[lucide: x] 14px #9ca3af kanan atas card

---

# SECTION 5 — OUTPUT CHECKLIST

- [ ] A-01: Halaman Penugasan + tab "Penugasan Ilustrasi" — sidebar #1a2332 exact, primary #0db8e8 exact, tab bar, tabel 4 row example, paginasi
- [ ] A-02: Dropdown "+ Tambah Penugasan" expanded — 4 items dengan separator, item "Tambah Ilustrasi" cyan + ikon
- [ ] A-03: Modal Wizard Step 1 — step indicator, tabel pilih kode soal, selection counter, footer navigation
- [ ] A-04: Modal Wizard Step 2 — step 1 selesai (hijau check), form assign, summary kode soal terpilih
- [ ] A-05: Modal Detail — info read-only, deskripsi lengkap, riwayat aktivitas, footer aksi
- [ ] A-06: Toast sukses + confirmation mini-dialog inline

Global checks:
- [ ] File ini mencakup SATU modul saja: MOD-ILUSTRATOR
- [ ] File ini mencakup SATU platform saja: Admin Web 1366×900px
- [ ] brand_primary dalam context block = #0db8e8 (SIAP actual, bukan A'raf DS default)
- [ ] sidebar_bg = #1a2332 konsisten di semua screen
- [ ] Tombol "Tambah Ilustrasi" hanya ada di dropdown "+ Tambah Penugasan" — BUKAN menu sidebar
- [ ] Tab bar "Penugasan Penulisan" | "Penugasan Ilustrasi" ada di A-01
- [ ] Screen IDs: A-01 s/d A-06 — tidak ada menu prefix
- [ ] Tidak ada emoji sebagai ikon — semua [lucide: icon-name]
- [ ] Action icons tabel: eye #0db8e8, edit #f59e0b, trash #ef4444 — sesuai existing
- [ ] Status badge "Siap Dikerjakan" menggunakan #e0f7fd bg #0db8e8 text (bukan #eff6ff #0069d2)
- [ ] Semua copy dalam Bahasa Indonesia
- [ ] Spec labels dalam Bahasa Inggris, copy dalam Bahasa Indonesia

---

# SECTION 6 — DELTA PROMPTS

### Delta 1 — Add: Filter Expanded State (dari tombol "Filter" di A-01)

ADMIN WEB — Add Filter expanded panel di A-01.
Context: Admin klik tombol "Filter" — panel filter muncul di bawah action bar (accordion style, bukan dropdown).
Filter panel (white bg, border 1px #e5e7eb, 12px radius, 16px padding, margin-top 8px):
  Row: Label "Status" | chips horizontal: [Semua] [Belum Ditugaskan] [Siap Dikerjakan] [Sedang Dikerjakan] [Selesai]
    Chip style: 32px height, 12px H pad, 8px radius | inactive: white + #e5e7eb border + #4b5563 text | active: #e0f7fd bg + #0db8e8 border + #0db8e8 text 12px Medium
  Row: Label "Mata Pelajaran" | dropdown multi-select 200px
  Row: Label "Ilustrator" | dropdown single-select 200px, searchable
  Row: Label "Deadline" | date range picker: dari [date] sampai [date]
  Footer panel: "Reset Filter" ghost #0db8e8 kiri | "Terapkan Filter" primary #0db8e8 kanan

### Delta 2 — Add: Bulk Assign via Checkbox Selection

ADMIN WEB — Add bulk action bar di A-01 saat ada row terseleksi.
Context: Admin centang 2+ row di tabel, action bar khusus muncul menggantikan action bar biasa.
Bulk action bar (white bg, border-bottom 1px #e5e7eb, 12px padding, height 44px):
  Left: checkbox "semua" + "3 kode soal dipilih" 13px Medium #111827
  Right: "Tugaskan ke Ilustrator yang Sama" primary #0db8e8 [lucide: user-check] kiri | "Batalkan Pilihan" ghost #4b5563
Modal bulk assign: sama struktur A-04, tapi summary menampilkan list 3 kode soal + note peringatan #ba7517

### Delta 3 — Add: Validasi Error di Modal Step 2

ADMIN WEB — Add error state di A-04 saat Admin klik "Simpan Penugasan" dengan field kosong.
Dropdown Ilustrator: border 1.5px #dc2626, bg #fef2f2
  Error message: [lucide: alert-circle] 12px #dc2626 + "Pilih ilustrator terlebih dahulu" 12px #dc2626, di bawah dropdown
Date picker: border 1.5px #dc2626 jika kosong
  Error message: "Deadline ilustrasi wajib diisi" 12px #dc2626
Tombol "Simpan Penugasan" tetap aktif (user dapat retry setelah isi field)
Scroll otomatis ke field pertama yang error

### Delta 4 — Add: Deadline Merah (Overdue Warning) di Tabel A-01

ADMIN WEB — Add overdue indicator di kolom Deadline tabel A-01.
Trigger: tanggal hari ini > deadline AND status bukan Selesai.
Kolom Deadline cell: teks tanggal warna #dc2626 (bukan #111827) + [lucide: alert-circle] 12px #dc2626 kiri teks
Row background: #fef2f2 sangat subtle (opacity rendah, hanya row yang overdue)
Tooltip on hover deadline cell: "Deadline sudah terlewat X hari" 12px white, #111827 bg, 6px radius

### Delta 5 — Fix: Step 1 Multi-Select (lebih dari 1 kode soal)

ADMIN WEB — Fix A-03 untuk menampilkan state ketika Admin memilih 2+ kode soal.
Selection counter berubah: "3 kode soal dipilih" 13px Medium #0db8e8
Info banner berubah dari blue ke amber #fefce8 bg #ba7517 border:
  [lucide: info] #ba7517 + "Ilustrator dan deadline yang sama akan diterapkan ke 3 kode soal terpilih." 12px #ba7517
Tombol "Lanjut →" tetap enabled.
Di A-04, summary section berubah: tampilkan list 3 kode soal (scrollable 120px height jika lebih dari 3), dengan satu [lucide: edit-2] untuk "Kembali ubah pilihan".

### Delta 6 — Add: Empty State Tab "Penugasan Ilustrasi"

ADMIN WEB — Add empty state di A-01 ketika belum ada data penugasan ilustrasi sama sekali.
Replace area tabel dengan:
  [lucide: image] 48px #e5e7eb, centered
  "Belum ada penugasan ilustrasi" 16px Bold #111827 center
  "Tambahkan penugasan ilustrasi pertama melalui tombol 'Tambah Penugasan' di atas" 14px Regular #4b5563 center (280px max-width)
  Arrow indicator animasi mengarah ke tombol "+ Tambah Penugasan" di kanan atas (subtle, dashed line atau ikon panah)

---

# OPEN ITEMS & ASUMSI (v2)

## Perubahan dari v1:
- ✅ Entry point diubah: bukan menu sidebar, tapi dropdown "+ Tambah Penugasan" → opsi "Tambah Ilustrasi"
- ✅ Brand colors diupdate: sidebar #1a2332, primary #0db8e8 (dari screenshot existing)
- ✅ Penugasan Ilustrasi diimplementasikan sebagai TAB baru di halaman Penugasan existing
- ✅ Action icons tabel disesuaikan: eye cyan, edit amber, delete red (sesuai existing)
- ✅ Status badge "Siap Dikerjakan" menggunakan warna cyan (#e0f7fd / #0db8e8) bukan biru (#eff6ff / #0069d2)
- ✅ OI-08 diselesaikan: tidak ada menu baru di sidebar

## Asumsi yang masih perlu dikonfirmasi:

| ID | Asumsi | Dampak jika Salah |
|---|---|---|
| OI-01 | Admin yang mengupdate status, bukan Ilustrator sendiri | Perlu role/view terpisah untuk Ilustrator |
| OI-02 | Ilustrator tidak punya akses login ke SIAP | Perlu notifikasi saat ditugaskan |
| OI-03 | 1 kode soal = 1 Ilustrator (tidak split per gambar) | Struktur data dan UI berubah signifikan |
| OI-04 | Daftar Ilustrator tersedia di Master Data SIAP | Jika belum ada, perlu scope tambahan |
| OI-05 | Status tidak bisa mundur kecuali re-assign | Tambah confirmation dialog untuk transisi mundur |
| OI-09 (baru) | Tab dibuat di halaman Penugasan yang sama, bukan route/halaman baru | Jika harus halaman baru, perlu update sidebar navigation |
| OI-10 (baru) | Warna cyan brand = #0db8e8 (diestimasi dari screenshot) | Konfirmasi hex exact ke developer — bisa jadi #13bae8, #0ab5e5, dll |

## Pertanyaan untuk Developer:
- Hex exact brand color SIAP? (untuk memastikan #0db8e8 akurat)
- Apakah ada API untuk kode soal yang memiliki flag "memerlukan ilustrasi"?
- Apakah Ilustrator sudah ada sebagai role di tabel users?
- Apakah implementasinya sebagai tab di halaman existing bisa dilakukan, atau perlu route baru?
