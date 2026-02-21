# PSS-portal
Official website for Panjim Shigmotsav Samiti featuring announcements, event details, schedules, and festival information for Shigmotsav celebrations in Panjim, Goa.


# PSS Portal – Panjim Shigmotsav Samiti

Full-stack web portal for Panjim Shigmotsav Samiti built with **Next.js**, **NestJS**, **PostgreSQL**, **Prisma**, and **Tailwind CSS**.

---

## 🗂️ Project Structure

```
pss-portal/
├── backend/                  # NestJS API Server
│   ├── prisma/
│   │   ├── schema.prisma     # Database schema
│   │   └── seed.ts           # Seed data
│   ├── src/
│   │   ├── main.ts
│   │   ├── app.module.ts
│   │   ├── prisma/           # Prisma service & module
│   │   ├── auth/             # JWT auth (login, strategy, guard)
│   │   ├── announcements/    # CRUD for announcements
│   │   ├── events/           # CRUD for events
│   │   └── carousel/         # Upload/delete carousel images
│   ├── uploads/              # Auto-created: uploaded images
│   ├── package.json
│   ├── tsconfig.json
│   └── .env.example
│
└── frontend/                 # Next.js App
    ├── src/
    │   ├── app/
    │   │   ├── layout.tsx
    │   │   ├── page.tsx          # Home page
    │   │   ├── announcements/    # Announcements listing
    │   │   ├── events/           # Events listing
    │   │   ├── contact/          # Contact page
    │   │   └── admin/            # Admin panel
    │   │       ├── page.tsx          # Login
    │   │       ├── layout.tsx        # Sidebar layout
    │   │       ├── dashboard/        # Dashboard
    │   │       ├── announcements/    # Manage announcements
    │   │       ├── events/           # Manage events
    │   │       └── carousel/         # Manage carousel images
    │   ├── components/
    │   │   ├── layout/
    │   │   │   ├── Header.tsx
    │   │   │   └── Footer.tsx
    │   │   └── home/
    │   │       ├── Carousel.tsx
    │   │       ├── CommitteeSection.tsx
    │   │       └── ContactSection.tsx
    │   ├── lib/
    │   │   └── api.ts
    │   └── types/
    │       └── index.ts
    ├── package.json
    ├── tailwind.config.js
    └── next.config.js
```

---

## 🗄️ Database Schema

| Table              | Key Fields |
|--------------------|------------|
| `admins`           | id, email, password |
| `committee_members`| id, name, designation, photoUrl, order |
| `announcements`    | id, title, description, photoUrl, date |
| `events`           | id, title, description, date, photoUrl, location |
| `carousel_images`  | id, imageUrl, altText, order |

---

## 🚀 Setup & Run

### Prerequisites
- Node.js 18+
- PostgreSQL running locally

### 1. Backend Setup

```bash
cd backend
cp .env.example .env
# Edit .env → set your DATABASE_URL, JWT_SECRET, ADMIN_EMAIL, ADMIN_PASSWORD

npm install
npx prisma generate
npx prisma migrate dev --name init
npx ts-node prisma/seed.ts     # Seeds admin + sample data
npm run start:dev
```

API runs at: **http://localhost:3001/api**

### 2. Frontend Setup

```bash
cd frontend
cp .env.local.example .env.local
# Edit if your backend runs on a different port

npm install
npm run dev
```

Frontend runs at: **http://localhost:3000**

---

## 🔐 Admin Access

- URL: `http://localhost:3000/admin`
- Email: `admin@pss.com` (or value set in ADMIN_EMAIL)
- Password: `Admin@123` (or value set in ADMIN_PASSWORD)

---

## 🎨 Color Scheme

| Name | Hex |
|------|-----|
| Primary – Deep Maroon | `#7A0E0E` |
| Secondary – Festival Yellow | `#F4B400` |
| Accent – Temple Gold | `#D4A017` |
| Support – Saffron Orange | `#E65100` |
| Background – Warm Off White | `#FFF8EE` |
| Text – Charcoal Black | `#1C1C1C` |

---

## 🔌 API Endpoints

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/api/auth/login` | ❌ | Admin login |
| GET | `/api/announcements` | ❌ | List all |
| POST | `/api/announcements` | ✅ | Create |
| PUT | `/api/announcements/:id` | ✅ | Update |
| DELETE | `/api/announcements/:id` | ✅ | Delete |
| GET | `/api/events` | ❌ | List all |
| POST | `/api/events` | ✅ | Create |
| PUT | `/api/events/:id` | ✅ | Update |
| DELETE | `/api/events/:id` | ✅ | Delete |
| GET | `/api/carousel` | ❌ | List images |
| POST | `/api/carousel` | ✅ | Upload image |
| DELETE | `/api/carousel/:id` | ✅ | Remove image |

✅ = Requires `Authorization: Bearer <token>` header


# Nextsjs initial setup
npx create-next-app@latest frontend
cd frontend
