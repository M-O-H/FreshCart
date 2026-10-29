# FreshCart Supermarket & Essentials 🛒🥦🧼

A production-ready, mobile-first MVP E-Commerce Web Application and Admin Management Dashboard specifically engineered for local supermarkets and grocery stores selling produce, household items (soaps, detergents), and daily essentials.

---

## 🌟 Key Supermarket Domain Innovations

1. **Direct Add-to-Cart Steppers:**
   Unlike traditional fashion or electronics e-commerce, supermarket shoppers buy 10–30 items per visit. Every product card features an instant `+ Add` button that transforms into an inline `[- 1 +]` stepper without navigating to a product detail page.
2. **Prominent Unit & Pack Pricing:**
   Clear unit labels on every product (e.g., `per 1 kg`, `500g pack`, `4-pack soap`, `1.5L bottle`, `12 jumbo roll pack`).
3. **Frictionless Local Checkout:**
   Guest checkout requiring no password creation. Supports customer full name, validated phone/WhatsApp number, delivery neighborhood zone selector (auto-calculating fees and delivery estimates), detailed street/apartment address, and delivery instructions.
4. **Local Payment Flexibility:**
   - **Cash on Delivery (COD):** Inspect groceries upon arrival and pay cash or card at the door.
   - **Bank Transfer / Mobile Money:** Shows bank account details, wire instructions, and reference/receipt tracking.
   - **Card Payment:** Integrated Stripe test simulation.
5. **WhatsApp Backup Channel:**
   Upon order confirmation, a 1-tap "Send Order via WhatsApp" pre-formats the entire receipt and items list to the supermarket's support line for backup priority packing.
6. **Live Step-by-Step Order Tracker (`/track-order`):**
   Visual progress timeline: `Pending` -> `Packing Items` -> `Out for Delivery` -> `Delivered`.
7. **Store Operations & Warehouse Picker Portal (`/admin`):**
   - **Overview & KPIs:** Today's Revenue, Total Orders, Pending Orders Needing Packing, and Low Stock Alerts (`stock <= 5`).
   - **Live Order Management:** Filter by status and payment status, view printable warehouse packing slips with interactive checkboxes for pickers, inspect payment proofs, and trigger one-click status transitions.
   - **Inventory CRUD & Quick Inline Editing:** Change daily market prices and toggle out-of-stock states directly in the table row without opening modals.
   - **Settings & Zones:** Manage product aisles and local delivery neighborhoods with flat delivery fees.

---

## 🛠️ Tech Stack & Architecture

- **Framework:** Next.js 15 (App Router, TypeScript)
- **Styling & UI:** Tailwind CSS, Lucide Icons, Custom Emerald/Slate Palette
- **Database & ORM:** PostgreSQL + Prisma ORM
- **State Management:** Zustand with `localStorage` persistence
- **Validation & Forms:** React Hook Form + Zod
- **Authentication & RBAC:** Edge-compatible Jose JWT & HTTP-Only secure cookies (`ADMIN`, `STAFF` roles)
- **Delight & Feedback:** Canvas Confetti celebration on checkout

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- Node.js (v18.18+ or v20+)
- PostgreSQL running locally or remotely

### 2. Environment Variables
Create a `.env` file (or use the included `.env`):
```env
DATABASE_URL="postgresql://mohamed@localhost:5432/supermarket_db"
JWT_SECRET="supermarket_super_secure_jwt_secret_key_2026_xyz"
NEXTAUTH_SECRET="supermarket_super_secure_jwt_secret_key_2026_xyz"
NEXT_PUBLIC_APP_URL="http://localhost:3000"
NEXT_PUBLIC_STORE_NAME="FreshCart Market & Essentials"
NEXT_PUBLIC_STORE_PHONE="+1 (555) 234-5678"
NEXT_PUBLIC_STORE_WHATSAPP="+15552345678"
```

### 3. Setup & Seeding
```bash
# Install dependencies
npm install --legacy-peer-deps

# Push schema to database
npx prisma db push

# Seed categories, 18+ products, delivery zones, sample orders, and admin credentials
npm run db:seed
```

### 4. Running the Application
```bash
# Development
npm run dev

# Production
npm run build
npm run start
```

---

## 🔐 Demo Credentials

| Role | Email | Password | Access |
| :--- | :--- | :--- | :--- |
| **Admin Director** | `admin@freshcart.com` | `admin123` | Full store control, inventory CRUD, zone management, orders |
| **Warehouse Staff** | `staff@freshcart.com` | `staff123` | Order fulfillment, packing checklist, status dispatch |

*Note: The login page at `/admin/login` features 1-click test login buttons for quick access.*

---

## 📁 Project Structure

```
├── prisma/
│   ├── schema.prisma       # Prisma models: Category, Product, Order, OrderItem, DeliveryZone, AdminUser
│   └── seed.cjs            # Realistic supermarket catalog and sample order seeder
├── src/
│   ├── app/
│   │   ├── page.tsx                             # Customer storefront with category filtering & search
│   │   ├── checkout/page.tsx                    # Single-page frictionless checkout
│   │   ├── order-confirmation/[orderNumber]/    # Confirmation receipt with WhatsApp backup channel
│   │   ├── track-order/page.tsx                 # Visual step progress tracker
│   │   ├── admin/
│   │   │   ├── page.tsx                         # Overview KPI Dashboard
│   │   │   ├── login/page.tsx                   # Staff/Admin portal login
│   │   │   ├── orders/page.tsx                  # Live order fulfillment & printable picker slips
│   │   │   ├── products/page.tsx                # Inventory CRUD & inline price/stock editor
│   │   │   └── settings/page.tsx                # Categories & Delivery Zones manager
│   │   └── api/                                 # REST API routes (orders, products, stats, zones, auth)
│   ├── components/
│   │   ├── layout/Navbar.tsx                    # Sticky header with live search & cart counter
│   │   ├── catalog/CategoryPills.tsx            # Horizontal scrolling category tabs
│   │   ├── catalog/PromoBanner.tsx              # Weekly supermarket deals banner
│   │   ├── catalog/ProductCard.tsx              # Card with direct add-to-cart stepper & unit badge
│   │   ├── catalog/ProductGrid.tsx              # Responsive mobile-first product grid
│   │   └── cart/CartDrawer.tsx                  # Slide-over cart with free shipping meter
│   ├── lib/
│   │   ├── prisma.ts                            # Prisma client singleton
│   │   ├── token.ts                             # Jose Edge-compatible JWT helpers
│   │   ├── auth.ts                              # Bcrypt & session utilities
│   │   └── utils.ts                             # Formatting & helper functions
│   ├── store/
│   │   └── useCartStore.ts                      # Persistent Zustand supermarket basket
│   └── types/                                   # TypeScript domain types
└── package.json
```
