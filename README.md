# Grand Horizon Hotel Booking System

A full-featured hotel booking system built with the MERN stack (MongoDB, Express, React, Node.js) featuring role-based access control, room management, booking workflows, Stripe payments, promo codes, and email notifications.

## Features

### For Customers
- Browse available rooms with filters (category, price range, capacity)
- View detailed room information with images, amenities, and reviews
- Book rooms with date selection and guest count
- Apply promo codes for discounts during checkout
- Secure payment processing via Stripe
- View booking history and status
- Leave reviews for completed stays
- Email confirmations for bookings

### For Managers
- Dashboard with real-time statistics
- View and manage all bookings
- Update booking statuses (pending, confirmed, checked_in, checked_out, cancelled)
- Today's check-ins and check-outs view
- Access booking analytics

### For Administrators
- Full room management (create, edit, delete rooms with images)
- Room statistics by category (total, available, occupied)
- Promo code management (create, edit, toggle, delete)
- User management across all roles
- System-wide analytics and reporting
- Manage all bookings and reviews

## Tech Stack

- **Frontend:** React 18, TypeScript, TailwindCSS, Shadcn/UI, TanStack Query, Wouter
- **Backend:** Node.js, Express, TypeScript
- **Database:** MongoDB Atlas with Mongoose ODM
- **Authentication:** JWT tokens with bcrypt password hashing
- **Payments:** Stripe integration (test mode)
- **Email:** Nodemailer with Gmail SMTP

## Room Categories

| Category | Description |
|----------|-------------|
| Standard | Budget-friendly options for comfortable stays |
| Deluxe | Enhanced comfort with premium amenities |
| Suite | Spacious accommodations with separate living areas |
| Executive | Business-focused with lounge access |
| Family | Designed for families with kids' amenities |
| Presidential | Luxury suites with butler service |
| Penthouse | Top-floor premium accommodations |

## Booking Statuses

| Status | Description |
|--------|-------------|
| `pending` | Booking created, awaiting payment |
| `confirmed` | Payment received, reservation confirmed |
| `checked_in` | Guest has arrived and checked in |
| `checked_out` | Stay completed |
| `cancelled` | Booking cancelled |

## Promo Code System

The system supports flexible promo codes with:
- **Discount Types:** Percentage (%) or Fixed amount ($)
- **Usage Limits:** Optional maximum usage count
- **Date Ranges:** Valid from/to dates
- **Minimum Spend:** Optional minimum booking amount requirement
- **Max Discount Cap:** Optional maximum discount limit for percentage codes

---

## Running Locally on Windows

Run the Application

**Option A: Using PowerShell (Recommended)**
```powershell
$env:NODE_ENV="development"; npx tsx server/index.ts
```

The application will start and be available at: **http://localhost:5000**


---

## Test Accounts

Use these accounts to test the application:

**Password for all accounts:** `Test@123`

| Role | Email | Access Level |
|------|-------|--------------|
| Admin | `admin@grandhorizon.com` | Full system access, room management, promo codes, user management |
| Manager | `manager@grandhorizon.com` | Booking management, status updates, dashboard |
| Customer | `guest@grandhorizon.com` | Room browsing, booking, reviews |

---

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | User login |
| GET | `/api/auth/me` | Get current user |

### Rooms
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/rooms` | List all rooms with reviews |
| GET | `/api/rooms/:id` | Get room details |
| POST | `/api/admin/rooms` | Create room (admin) |
| PUT | `/api/admin/rooms/:id` | Update room (admin) |
| DELETE | `/api/admin/rooms/:id` | Delete room (admin) |

### Bookings
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/bookings/my` | Get user's bookings |
| POST | `/api/bookings` | Create booking |
| POST | `/api/bookings/validate-promo` | Validate promo code |
| POST | `/api/bookings/:id/confirm-payment` | Confirm payment |
| PATCH | `/api/bookings/:id/cancel` | Cancel booking |

### Manager Routes
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/manager/bookings` | All bookings |
| GET | `/api/manager/bookings/today` | Today's check-ins |
| GET | `/api/manager/stats` | Dashboard statistics |
| PATCH | `/api/manager/bookings/:id/status` | Update booking status |

### Admin Routes
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/admin/stats` | Room statistics |
| GET | `/api/admin/promo-codes` | List promo codes |
| POST | `/api/admin/promo-codes` | Create promo code |
| PUT | `/api/admin/promo-codes/:id` | Update promo code |
| DELETE | `/api/admin/promo-codes/:id` | Delete promo code |
| PATCH | `/api/admin/promo-codes/:id/toggle` | Toggle promo code active status |

### Reviews
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/reviews` | Create review (after checkout) |

---

## Project Structure

```
grand-horizon-hotel/
├── client/                     # React frontend
│   ├── src/
│   │   ├── components/         # Reusable UI components
│   │   │   └── ui/             # Shadcn UI components
│   │   ├── pages/              # Page components
│   │   │   ├── admin/          # Admin dashboard pages
│   │   │   ├── manager/        # Manager dashboard pages
│   │   │   └── auth/           # Login/Register pages
│   │   ├── lib/                # Utilities (auth, api, query client)
│   │   └── hooks/              # Custom React hooks
│   └── index.html
├── server/                     # Express backend
│   ├── db/
│   │   ├── models/             # Mongoose models (User, Room, Booking, Review, PromoCode)
│   │   └── connection.ts       # MongoDB connection
│   ├── routes/                 # API route handlers
│   │   ├── auth.ts             # Authentication routes
│   │   ├── rooms.ts            # Room routes
│   │   ├── bookings.ts         # Booking routes
│   │   ├── manager.ts          # Manager routes
│   │   ├── admin.ts            # Admin routes
│   │   └── reviews.ts          # Review routes
│   ├── middleware/             # Express middleware (auth)
│   ├── services/               # Business logic (email service)
│   ├── scripts/                # Utility scripts (seed)
│   └── index.ts                # Server entry point
├── shared/                     # Shared types and schemas
│   └── schema.ts               # Zod schemas and types
├── uploads/                    # Uploaded room images
├── .env.example                # Example environment variables
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── vite.config.ts
└── README.md
```

---

## Troubleshooting

### Common Issues

1. **MongoDB Connection Fails**
   - Verify your `MONGODB_URI` is correct
   - Check if your IP is whitelisted in MongoDB Atlas
   - Ensure the database user has proper permissions

2. **Email Not Sending**
   - For Gmail, ensure you're using an App Password (not your regular password)
   - Check if 2-Step Verification is enabled on your Google account
   - Verify SMTP settings are correct

3. **Stripe Payments Not Working**
   - Ensure you're using test mode keys (start with `sk_test_` and `pk_test_`)
   - Check that your Stripe account is properly set up

4. **Images Not Uploading**
   - Ensure the `uploads/` directory exists and has write permissions
   - Check file size limits (max 5MB per image)
