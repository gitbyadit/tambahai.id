# TambahAI 🚀

**Platform konsultasi bisnis berbasis AI.** Ceritakan masalah bisnismu secara santai — TambahAI mendengar, menganalisa, dan menyusun langkah solusi konkret yang bisa langsung kamu jalankan.

> Demo interactive web app untuk menunjukkan alur produk: dari landing page hingga dashboard, konsultasi AI, laporan analisa, dan manajemen user.

---

## ✨ Fitur

| Fitur | Deskripsi |
|-------|-----------|
| 💬 **Konsultasi Chat AI** | Interface chat dengan simulasi AI business consultant. Ketik masalah → dapat solusi terstruktur dalam langkah-langkah. |
| 📈 **Laporan Analisa Bisnis** | Dashboard visual: KPI, bar chart, donut chart distribusi channel, dan insight otomatis. Filter 30 hari / 3 bulan / 1 tahun. |
| 📋 **Riwayat Konsultasi** | List semua konsultasi dengan filter status & kategori, detail solusi expandable. |
| 🔐 **Auth & Role System** | Login/Register dengan 3 role: **Admin**, **Operator**, **Viewer**. |
| 🛠️ **Admin Panel** | Manajemen user & role (tambah/edit/hapus, assign role, aktif/nonaktif). Khusus Admin. |
| 👤 **Profil & Pengaturan** | Edit info pribadi, keamanan (2FA, ganti password), notifikasi, hapus akun. |
| 🎯 **Landing Page** | Halaman marketing bergaya minimalis Apple untuk memperkenalkan produk. |

---

## 📁 Struktur Project

```
tambahai.id/
├── index.html          ← Bird's eye navigation hub (menu sentral semua halaman)
├── plan.md             ← Project plan & roadmap development
├── package.json        ← Dependencies (http-server, ai-connect)
├── .gitignore
└── preview/
    ├── index.html      ← Landing page marketing
    ├── login.html      ← Login / Register + pilih role
    ├── dashboard.html  ← Dashboard overview & quick actions
    ├── consult.html    ← Chat konsultasi AI
    ├── history.html    ← Riwayat konsultasi + filter
    ├── report.html     ← Laporan analisa bisnis (grafik + insight)
    ├── admin.html      ← Admin panel (admin-only)
    └── profile.html    ← Profil & pengaturan akun
```

---

## 🧭 Alur User

```
Bird's Eye Hub (index.html)
        │
        ▼
Landing Page ──→ Login/Register (pilih role)
                        │
                        ▼
                   Dashboard
        ┌──────────┬────┴─────┬──────────┐
        ▼          ▼          ▼          ▼
   Consult     Report     History    Profile
   (chat AI)  (analisa)  (riwayat)  (akun)
        │
        ▼
   Admin Panel (hanya role Admin)
```

## 🔐 Role & Permission

| Role | Akses |
|------|-------|
| **Admin** | Semua fitur + Admin Panel (kelola user & role) + laporan penuh |
| **Operator** | Konsultasi, laporan penuh, riwayat, profil |
| **Viewer** | Ringkasan laporan saja, riwayat, profil — tidak bisa akses admin panel atau laporan penuh |

Role-lock diterapkan: halaman `admin.html` dan `report.html` memvalidasi role dari `localStorage` dan menampilkan peringatan "Akses dibatasi" jika tidak berwenang.

---

## 🚀 Cara Menjalankan

Demo ini murni **frontend statis** (HTML/CSS/JS murni + localStorage) — tidak perlu backend.

```bash
# Masuk ke folder project
cd /home/fast

# Jalankan server (gunakan http-server dari node_modules)
npx http-server . -p 3000
```

Lalu buka **http://localhost:3000** di browser.

### Tips demo
1. Buka root `index.html` → bird's eye hub semua halaman
2. Masuk/daftar lewat `login.html`, **pilih role saat mendaftar**
3. Login sebagai **Admin** untuk coba akses penuh ke Admin Panel & Report
4. Login sebagai **Viewer** untuk lihat perbedaan permission (banyak fitur diblokir)

---

## 🛠️ Tech Stack

- **Frontend:** HTML5, CSS3 (inline, tema minimalis Apple), Vanilla JavaScript
- **Font:** Inter (Google Fonts)
- **Data:** `localStorage` untuk autentikasi demo & user session
- **Dependencies:** `http-server` (serve lokal), `@idcloudhost/ai-connect` (ready untuk integrasi AI masa depan)

> Catatan: Fitur AI pada `consult.html` saat ini berupa **respons demo/placeholder**. Integrasi dengan model AI sungguhan lewat `@idcloudhost/ai-connect` dijadwalkan pada fase berikutnya (lihat `plan.md`).

---

## 🗺️ Roadmap (dari plan.md)

| Fase | Status | Deskripsi |
|------|--------|-----------|
| **Fase 1 — Landing Page** | ✅ Selesai | Halaman marketing + preview demo |
| **Fase 2 — Backend API** | ⬜ Belum | Hono + SQLite + JWT, role/permission, AI consult flow, dashboard API |
| **Fase 3 — Frontend App** | ⬜ Belum | React + Vite, integrasi login asli |
| **Fase 4 — Integrasi AI** | ⬜ Belum | Hubungkan `@idcloudhost/ai-connect` ke `/api/consult` |

---

## 📄 Lisensi

© 2026 TambahAI. Hak cipta dilindungi. Dibuat untuk tujuan pengembangan & demo.

---

## 🤝 Kontribusi / Kontak

Project dikelola sebagai demo untuk platform **tambahai.id**. Untuk pertanyaan atau kontribusi, hubungi melalui repository GitHub.
