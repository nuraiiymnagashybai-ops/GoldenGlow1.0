# Luxe Cuts & Beauty Studio

> Dublin's premier luxury hair and beauty studio website — built with Hono + TypeScript + Tailwind CSS

**Live URL:** `https://3000-io0i2h71sbhxbg8ko65s7-3844e1b6.sandbox.novita.ai`

---

## Overview

A complete, client-ready full-stack web application for **Luxe Cuts & Beauty Studio**, a high-end beauty salon based in Dublin, Ireland. The site features a premium dark luxury design aesthetic with gold accents, smooth animations, and a fully functional booking system.

---

## Features Implemented ✅

### Frontend Pages
- **Homepage** — Hero section, services overview, about preview, testimonials, gallery preview, CTA banner, contact info
- **About Page** — Salon story, team profiles, values, awards & press
- **Services Page** — All services with category filtering, pricing, duration, popular badges
- **Booking System** — Full 5-step booking wizard with availability checking
- **Gallery Page** — Masonry grid with lightbox preview, category filtering
- **Contact Page** — Contact form, business hours table, Google Maps embed
- **Admin Panel** — Full CRUD dashboard with authentication

### Booking System (Core)
- Step 1: Select service (with category filter)
- Step 2: Choose specialist
- Step 3: Calendar date picker + real-time availability
- Step 4: Customer details form with GDPR consent
- Step 5: Booking review and confirmation
- **Double-booking prevention** — backend validation
- Booking reference ID generated
- Email confirmation ready (SendGrid/Mailgun hookup point)

### Admin Dashboard
- JWT-style session authentication (admin / luxe2024)
- **Bookings** — View all, filter by status, cancel bookings
- **Services** — Add, edit, delete services with full modal form
- **Team** — Add, edit, delete team members
- **Gallery** — Add, remove gallery images
- **Dashboard stats** — Total bookings, confirmed, pending, revenue

### Design & UX
- Premium luxury dark theme (black, charcoal, gold)
- Cormorant Garamond (serif) + Jost (sans-serif) typography
- Smooth CSS animations (fade-up, reveal on scroll, marquee)
- Fully responsive — mobile-first design
- Loading states, toast notifications, error handling
- SEO meta tags, Open Graph tags
- GDPR consent checkboxes on all forms

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Runtime | Cloudflare Workers (via Hono) |
| Framework | Hono v4 |
| Frontend | Vanilla JS + Tailwind CSS (CDN) |
| Typography | Google Fonts (Cormorant Garamond + Jost) |
| Build | Vite + @hono/vite-build |
| Deploy | Cloudflare Pages |

---

## Project Structure

```
webapp/
├── src/
│   ├── index.tsx         # Main app — all pages + SPA logic + CSS
│   ├── renderer.tsx      # Hono JSX renderer
│   ├── routes/
│   │   └── api.ts        # All API routes (REST endpoints)
│   └── data/
│       └── salonData.ts  # Dummy data — services, team, testimonials, gallery
├── public/               # Static assets
├── dist/                 # Built output (generated)
├── ecosystem.config.cjs  # PM2 config
├── wrangler.jsonc        # Cloudflare Workers config
├── vite.config.ts        # Vite build config
├── package.json
└── README.md
```

---

## API Routes

### Public Endpoints
| Method | Route | Description |
|--------|-------|-------------|
| GET | `/api/health` | Health check |
| GET | `/api/salon-info` | Salon details |
| GET | `/api/services` | All services (filter: `?category=Hair`) |
| GET | `/api/services/:id` | Single service |
| GET | `/api/team` | All team members |
| GET | `/api/team/:id` | Single team member |
| GET | `/api/testimonials` | All testimonials |
| GET | `/api/gallery` | Gallery images (filter: `?category=Hair`) |
| GET | `/api/bookings/availability` | Available slots `?date=YYYY-MM-DD&staffId=t1` |
| POST | `/api/bookings` | Create booking |
| POST | `/api/contact` | Submit contact form |

### Admin Endpoints (requires `x-session-token` header)
| Method | Route | Description |
|--------|-------|-------------|
| POST | `/api/auth/login` | Admin login |
| POST | `/api/auth/logout` | Admin logout |
| GET | `/api/auth/verify` | Verify session |
| GET | `/api/bookings` | List all bookings |
| PUT | `/api/bookings/:id` | Update booking |
| DELETE | `/api/bookings/:id` | Cancel booking |
| POST | `/api/services` | Create service |
| PUT | `/api/services/:id` | Update service |
| DELETE | `/api/services/:id` | Delete service |
| POST | `/api/team` | Add team member |
| PUT | `/api/team/:id` | Update team member |
| DELETE | `/api/team/:id` | Remove team member |
| POST | `/api/gallery` | Add gallery image |
| DELETE | `/api/gallery/:id` | Remove gallery image |

---

## Admin Login

Navigate to `/` → scroll to footer → click **Admin** link

**Credentials:**
- Username: `admin`
- Password: `luxe2024`

---

## Data Models

### Booking
```json
{
  "id": "b001",
  "serviceId": "h1",
  "serviceName": "Signature Cut & Style",
  "staffId": "t1",
  "staffName": "Siobhán O'Brien",
  "date": "2025-04-10",
  "time": "11:00",
  "customerName": "Emma Sheehan",
  "customerEmail": "emma@email.ie",
  "customerPhone": "+353 87 000 0000",
  "notes": "",
  "status": "confirmed",
  "price": 85,
  "gdprConsent": true,
  "createdAt": "2025-03-24T00:00:00.000Z"
}
```

---

## Local Development

```bash
# Install dependencies
npm install

# Build
npm run build

# Start dev server
pm2 start ecosystem.config.cjs

# Or run directly
npx wrangler pages dev dist --ip 0.0.0.0 --port 3000
```

---

## Deployment to Cloudflare Pages

```bash
# Install Wrangler
npm install -g wrangler

# Login to Cloudflare
wrangler login

# Build
npm run build

# Create project
npx wrangler pages project create luxe-cuts-beauty --production-branch main

# Deploy
npx wrangler pages deploy dist --project-name luxe-cuts-beauty
```

---

## Production Upgrades (Recommended)

To move from in-memory to persistent storage, connect:

| Feature | Upgrade |
|---------|---------|
| Data persistence | Cloudflare D1 (SQLite) |
| Image uploads | Cloudflare R2 |
| Email confirmations | Resend or SendGrid API |
| SMS notifications | Twilio API |
| Payment deposits | Stripe API |
| Authentication | JWT with secure signing |

---

## Business Details (Dummy Data)

- **Location:** 14 Grafton Quarter, Dublin 2, D02 VH98, Ireland
- **Phone:** +353 1 234 5678
- **Email:** hello@luxecutsdublin.ie
- **Currency:** Euro (€)
- **GDPR:** Consent checkboxes on all forms

---

*Built with Hono + TypeScript + Tailwind CSS · Deployed on Cloudflare Pages*
