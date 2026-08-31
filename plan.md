# TambahAI — Project Plan

## Overview
Platform AI business consultant: user bicara masalah bisnis → AI analisa → kasih solusi konkret. Bahasa Indonesia, target UMKM & pebisnis yang baru kenal AI.

---

## Fase 1 — Landing Page ✅ (selesai)
- `index.html` — single-file landing page
- Style: Apple-inspired (halus, whitespace besar, rounded corners)
- Section: Hero, Cara Kerja, Fitur, Testimoni, Harga, CTA, Footer
- Responsive mobile-friendly

---

## Fase 2 — Backend API (demo-ready)

### Tech Stack
| Component | Choice | Alasan |
|-----------|--------|--------|
| Framework | **Hono** | Ultra-light (~50KB), Express-like tapi lebih ringan |
| Database | **better-sqlite3** | File-based `.sqlite`, gak perlu install DB server |
| Auth | **bcrypt + jsonwebtoken** | Simple token-based auth |
| Environment | **dotenv** | Config management |

```json
{
  "dependencies": {
    "hono": "^4.x",
    "better-sqlite3": "^11.x",
    "bcrypt": "^5.x",
    "jsonwebtoken": "^9.x",
    "dotenv": "^16.x"
  }
}
```

### Core Features

#### 1. Auth System
- `POST /api/register` — registrasi dengan nama, email, password
- `POST /api/login` — login, return JWT token
- `GET /api/me` — cek profil pengguna (harus login)

#### 2. Role & Permission Model
```
Role hierarchy:
├── admin   → semua akses
├── operator → baca laporan, kirim konsultasi AI, kelola user
└── viewer  → hanya baca dashboard & hasil konsultasi
```

Middleware sederhana:
```javascript
// Cek role pada setiap route
const authorize = (...roles) => async (c, next) => {
  const user = getUserFromToken(c);
  if (!roles.includes(user.role)) return c.json({ error: 'Akses ditolak' }, 403);
  await next();
};
```

#### 3. AI Consultation Flow
- `POST /api/consult` — kirim masalah bisnis → simpan ke database → callback AI → kirim respon
- `GET /api/consult/history` — lihat riwayat konsultasi (role-filtered)
- `GET /api/consult/:id` — detail satu konsultasi

#### 4. Dashboard API
- `GET /api/dashboard/stats` — ringkasan data bisnis (jumlah user, total konsultasi, tren)

---

## Fase 3 — Frontend App (opsional, setelah backend siap)

Opsi cepat:
- **Nolabel**: Gunakan React + Vite langsung (sudah ada landing page HTML sebagai referensi design)
- **Minimalis**: Tambah halaman login/register di landing page yang sudah ada, sisanya SPA routing via Hono serve static files

---

## Fase 4 — Integrasi AI (`@idcloudhost/ai-connect`)
- Hubungkan endpoint `/api/consult` ke AI Connect SDK
- Kirim konteks masalah bisnis ke model AI
- Terima dan format respon sebagai solusi terstruktur

---

## Struktur Project

```
/home/fast/
├── index.html          ← Landing page (Fase 1)
├── plan.md             ← File ini
├── package.json
├── .env.example        ← Template environment
├── src/
│   ├── index.js        ← Entry point, setup Hono
│   ├── db.js           ← SQLite setup & migrations
│   ├── middleware/
│   │   ├── auth.js     ← JWT verification
│   │   └── role.js     ← Permission checker
│   ├── routes/
│   │   ├── auth.js     ← register, login, me
│   │   ├── consult.js  ← kirim masalah, histori, detail
│   │   └── dashboard.js← statistik
│   └── utils/
│       └── hash.js     ← bcrypt helpers
├── data/
│   └── tambahai.db     ← SQLite database (auto-created)
└── public/
    └── index.html      ← Clone landing page untuk serve static
```

---

## Timeline Estimasi

| Fase | Estimasi | Catatan |
|------|----------|---------|
| Setup Hono + SQLite | 30 menit | Routing dasar + DB init |
| Auth (register + login) | 1–2 jam | JWT + bcrypt |
| Role & permission | 1 jam | Middleware + seed data |
| Consult flow | 2–3 jam | CRUD + AI integration placeholder |
| Dashboard API | 1–2 jam | Statistik endpoints |
| Testing & polish | 1–2 jam | Postman collection + bug fix |

**Total: ~8–10 jam kerja** — bisa selesai dalam 2 hari santai.

---

## Notes
- Database `.sqlite` tinggal copy-paste antar mesin
- Gak perlu server eksternal untuk demo lokal
- Role seeding otomatis saat startup pertama
- Error handling konsisten: selalu return JSON `{ error, message }`
