# De-HaaT — Modern Grocery eCommerce Platform

> Full-stack, multi-vendor grocery & daily essentials platform built with Next.js 14, TypeScript, Prisma, and modern UI/UX principles.

---

## Features

- **Customer Dashboard** — Browse, search, cart, wishlist, orders
- **Delivery Partner Portal** — Accept deliveries, track earnings, manage availability
- **Admin Dashboard** — Manage products, users, orders, analytics
- **Real-time Order Tracking** — Live status updates via Socket.io
- **Secure Authentication** — JWT-based with role-based access control
- **Payment Ready** — Razorpay, Stripe, UPI, COD, Wallet integration architecture
- **Responsive Design** — Mobile-first, glassmorphism UI
- **Modern Tech Stack** — Next.js 14, TypeScript, Tailwind CSS, Prisma

---

## Tech Stack

### Frontend
- Next.js 14 (App Router)
- React 18 with TypeScript
- Tailwind CSS 3.4 with custom De-HaaT theme
- Framer Motion — animations
- React Hook Form + Zod — form validation
- Zustand — state management
- Axios — HTTP client
- Lucide React — icons
- Recharts — analytics charts

### Backend
- Next.js API Routes
- Prisma ORM
- PostgreSQL / MySQL
- JWT + bcryptjs — authentication
- Socket.io — real-time updates

---

## Project Structure

```
de-haat/
├── src/
│   ├── app/                  # Next.js app directory
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── api/              # API routes
│   │   ├── auth/             # Auth pages
│   │   ├── products/         # Product pages
│   │   ├── cart/             # Cart page
│   │   ├── customer/         # Customer dashboard
│   │   ├── delivery/         # Delivery partner dashboard
│   │   └── admin/            # Admin dashboard
│   ├── components/
│   │   ├── ui/               # Reusable UI components
│   │   │   ├── Button.tsx
│   │   │   ├── Input.tsx
│   │   │   ├── Card.tsx
│   │   │   └── Badge.tsx
│   │   └── layout/           # Layout components
│   │       ├── Navbar.tsx
│   │       └── Footer.tsx
│   ├── lib/
│   │   ├── auth.ts           # Authentication utilities
│   │   ├── db.ts             # Prisma client
│   │   └── utils.ts          # Helper functions
│   ├── store/                # Zustand stores
│   │   ├── authStore.ts
│   │   └── cartStore.ts
│   ├── services/
│   │   └── api.ts            # API services
│   ├── hooks/                # Custom React hooks
│   │   ├── useAuth.ts
│   │   └── useLocalStorage.ts
│   ├── types/
│   │   └── index.ts          # TypeScript types
│   └── middleware.ts         # Next.js middleware
├── prisma/
│   ├── schema.prisma         # Database schema
│   └── seed.ts               # Seed data
├── public/                   # Static assets
├── .env.example
├── .env.local                # Local environment (gitignored)
├── next.config.js
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## Installation & Setup

### Prerequisites

- Node.js 18+
- npm or yarn
- PostgreSQL or MySQL

### 1. Clone the repository

```bash
git clone https://github.com/Anchitkumarr009/de-haat.git
cd de-haat
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

```bash
cp .env.example .env.local
```

Edit `.env.local`:

```env
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/dehaat"

# JWT
JWT_SECRET="your-super-secret-jwt-key"
JWT_REFRESH_SECRET="your-refresh-token-secret"

# API
NEXT_PUBLIC_API_URL="http://localhost:3000/api"

# Cloudinary (image uploads)
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME="your-cloud-name"
CLOUDINARY_API_KEY="your-api-key"
CLOUDINARY_API_SECRET="your-api-secret"

# Payment (optional)
RAZORPAY_KEY_ID="your-razorpay-key"
RAZORPAY_KEY_SECRET="your-razorpay-secret"
STRIPE_PUBLIC_KEY="your-stripe-key"
STRIPE_SECRET_KEY="your-stripe-secret"
```

### 4. Set up the database

```bash
npm run prisma:generate   # Generate Prisma client
npm run prisma:migrate    # Run migrations
npm run prisma:seed       # Seed sample data (optional)
```

### 5. Start the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## API Reference

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login user |
| POST | `/api/auth/logout` | Logout user |
| POST | `/api/auth/refresh` | Refresh JWT token |
| GET | `/api/auth/profile` | Get user profile |
| PUT | `/api/auth/profile` | Update profile |

### Products

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/products` | Get all products (with filtering) |
| GET | `/api/products/:id` | Get product details |
| GET | `/api/categories` | Get all categories |
| GET | `/api/products/search` | Search products |

### Orders

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/orders` | Create new order |
| GET | `/api/orders` | Get user orders |
| GET | `/api/orders/:id` | Get order details |
| PATCH | `/api/orders/:id/status` | Update order status |
| POST | `/api/orders/:id/cancel` | Cancel order |

### Delivery Partner

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/delivery/orders` | Get assigned orders |
| PATCH | `/api/delivery/:id/status` | Update delivery status |
| GET | `/api/delivery/earnings` | Get earnings |
| PATCH | `/api/delivery/availability` | Toggle online/offline |

### Admin

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/admin/dashboard` | Dashboard analytics |
| GET | `/api/admin/products` | Manage products |
| GET | `/api/admin/users` | Manage users |
| GET | `/api/admin/orders` | Manage orders |
| GET | `/api/admin/analytics` | Sales analytics |

---

## UI Components

Reusable components in `src/components/ui/`:

| Component | Variants |
|-----------|----------|
| `Button` | primary, secondary, outline, ghost |
| `Input` | with label, error, helper text |
| `Card` | elevated, glass, default |
| `Badge` | status indicators |
| `Modal` | dialog component |
| `Toast` | notifications |

---

## Authentication Flow

1. User registers or logs in
2. Server validates credentials and hashes password with bcrypt
3. JWT token is generated and sent to client
4. Token stored in `localStorage` and `httpOnly` cookie
5. Protected routes check token validity via middleware
6. Role-based access control applies (`customer`, `delivery`, `admin`)

---

## Database Models

| Model | Description |
|-------|-------------|
| `User` | Customer accounts |
| `DeliveryPartner` | Delivery partner accounts |
| `Admin` | Admin accounts |
| `Product` | Product catalog |
| `Category` | Product categories |
| `Order` | Customer orders |
| `Payment` | Payment transactions |
| `Delivery` | Delivery tracking |
| `Review` | Product reviews |

See `prisma/schema.prisma` for the complete schema.

---

## Available Scripts

```bash
npm run dev               # Start development server
npm run build             # Build for production
npm run start             # Start production server
npm run lint              # Run ESLint
npm run format            # Format code with Prettier
npm run prisma:generate   # Generate Prisma client
npm run prisma:migrate    # Run database migrations
npm run prisma:seed       # Seed sample data
```

---

## Deployment

### Vercel (recommended)

```bash
npm install -g vercel
vercel
```

### Docker

```bash
docker build -t de-haat .
docker run -p 3000:3000 de-haat
```

---

## Troubleshooting

**Database connection issues**
```bash
# Verify DATABASE_URL in .env.local, confirm PostgreSQL/MySQL is running, then:
npx prisma db push
```

**Build errors**
```bash
rm -rf .next
npm run build
```

**Port already in use**
```bash
npm run dev -- -p 3001
```

---

## Roadmap

- [ ] Live chat support
- [ ] AI-powered product recommendations
- [ ] Subscription delivery
- [ ] Multi-language support
- [ ] PWA app
- [ ] Analytics dashboard improvements
- [ ] Mobile app (React Native)

---

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

## Support

- GitHub Issues: [github.com/Anchitkumarr009/de-haat/issues](https://github.com/Anchitkumarr009/de-haat/issues)
- Email: nchtrai@gmail.com

---

## License

MIT License — free to use for commercial purposes.

---

*Made with ❤️ by the De-HaaT Team*
