# AgriHub

AgriHub is a full-stack agricultural platform that combines an online marketplace, labor booking, service and equipment rentals, wallet-based payments and refunds, logistics simulation, role verification, and an administrative control center in one website.

The project is organized as a workspace with:

- `frontend/` for the React + TypeScript + Vite client
- `backend/` for the Node.js + Express + MongoDB API

## What The Website Does

AgriHub supports multiple user flows inside one system:

- buyers can browse and order agricultural products
- sellers can publish listings, manage orders, and generate waybills
- laborers can publish labor offers and receive bookings
- service or rental providers can publish listings and manage bookings
- users can maintain a wallet, receive refunds, and request cash-out
- admins can review verifications, manage users, monitor orders, and control logistics simulation

## Main Features

### Authentication and Account Management

- Email and password login
- Google sign-in
- Email verification during registration
- Forgot-password request, verification, and reset flow
- Email-change and phone-change verification flows
- Strong password rules for registration and password reset
- Profile editing with avatar upload

### Marketplace

- Marketplace listing creation and editing
- Product varieties, pricing, stock, and seller details
- Buyer product browsing and checkout
- Seller order management
- Buyer order details with parcel timeline
- Waybill generation and download
- Refund request flow
- Review submission flow
- Protection against sellers buying their own listings

### Logistics and Tracking

- Admin logistics simulation controls
- Rider pickup trigger
- Route-progress slider for simulated delivery movement
- Buyer and seller order-details map
- Delivery timeline states such as:
  - order placed
  - preparing
  - ready for pickup
  - picked up
  - in transit
  - arrived at delivery hub
  - out for delivery
  - order received
  - cancelled

### Labor Booking

- Labor offer publishing
- Labor browsing for customers
- Labor booking flow
- Labor payment checkout
- On-the-way and complete status handling
- Labor reviews

### Services and Rentals

- Rental or service listing publishing
- Service browsing and booking
- Service payment checkout
- Pickup, cancel, and completion flows

### Wallet and Payment Features

- Wallet summary and transaction history
- Marketplace, labor, and rental payment handling
- Refund-to-wallet behavior for eligible cancellations
- Wallet cash-out request flow

### Roles and Verification

- Buyer, seller, laborer, service/provider, admin, and super admin flows
- Verification-document upload
- Role application workflow
- Verification approval and rejection from admin

### Admin Features

- Admin overview dashboard
- User access management
- User disable and restore actions
- User penalties
- Marketplace listing moderation
- Marketplace refund review
- Labor booking status administration
- Service booking status administration
- Logistics simulation for marketplace orders

## Tech Stack

### Frontend

- React 19
- TypeScript
- Vite
- React Router
- Tailwind CSS
- Radix UI
- Lucide React
- Recharts

### Backend

- Node.js
- Express.js
- MongoDB Atlas
- Mongoose
- JWT
- bcryptjs
- Nodemailer

### External Services and APIs

- Google Cloud Run
- Google Artifact Registry
- Google Compute Engine VM instances
- MongoDB Atlas
- Supabase Storage
- Xendit
- Google Identity Services / Google OAuth
- Google Maps JavaScript API
- Google Places API
- OpenRouteService
- OSRM
- GraphHopper
- Planner / OptaPlanner-compatible route optimization service
- Brevo Email API
- Gmail SMTP fallback

## Project Structure

```text
SysArch/
  frontend/
    src/
      app/
      features/
      shared/
    package.json
    vite.config.ts
  backend/
    src/
      config/
      controllers/
      middleware/
      models/
      routes/
      utils/
    Dockerfile
    package.json
  outputs/
  tools/
  package.json
  package-lock.json
```

## Available Scripts

Run these from the repo root:

```bash
npm install
npm run dev
```

Other useful scripts:

```bash
npm run dev:frontend
npm run dev:backend
npm run build
npm run start
```

## Local Development

1. Install dependencies:

```bash
npm install
```

2. Create a root `.env` file.

3. Start both apps:

```bash
npm run dev
```

4. Open the frontend:

- `http://localhost:5173`

5. Local API base:

- `http://localhost:5000/api/v1`

## Environment Variables

This project can read environment variables from the root `.env` file during local development.

Use [.env.example](C:/Users/earlj/OneDrive/Desktop/SysArch/.env.example) as the starting template and update it for your own setup.

### Backend

```env
PORT=5000
CLIENT_URL=http://localhost:5173
CLIENT_URLS=http://localhost:5173
ALLOW_VERCEL_PREVIEWS=false

MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
GOOGLE_CLIENT_ID=your_google_client_id

SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
SUPABASE_STORAGE_BUCKET=verification-documents
SUPABASE_PROFILE_BUCKET=profile-pictures
SUPABASE_MARKETPLACE_BUCKET=marketplace-listings
SUPABASE_REVIEW_BUCKET=reviews-picture
SUPABASE_MARKETPLACE_REFUND_BUCKET=marketplace-refund
SUPABASE_RENTALS_BUCKET=Rentals-picture

BREVO_API_KEY=your_brevo_api_key
BREVO_SENDER=your_verified_sender
EMAIL_FROM=AgriHub <noreply@example.com>
SMTP_FROM=AgriHub <noreply@example.com>
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_smtp_user
SMTP_PASS=your_smtp_password_or_gmail_app_password

XENDIT_SECRET_KEY=your_xendit_secret_key
XENDIT_WEBHOOK_CALLBACK_TOKEN=your_xendit_callback_token
XENDIT_API_BASE_URL=https://api.xendit.co

ORS_BASE_URL=http://127.0.0.1:8080/ors
ORS_API_KEY=your_ors_api_key
GRAPHHOPPER_BASE_URL=http://127.0.0.1:8989
GRAPHHOPPER_API_KEY=your_graphhopper_api_key
OSRM_BASE_URL=http://127.0.0.1:5001
OPTAPLANNER_BASE_URL=http://127.0.0.1:8090
ROUTING_REQUEST_TIMEOUT_MS=4000
SUPABASE_REQUEST_TIMEOUT_MS=4000

ENABLE_DEMO_DATA=false
```

### Frontend

```env
VITE_API_BASE_URL=http://localhost:5000/api/v1
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

## API Overview

Main API root:

- `/api/v1`

Main route groups:

- `/api/v1/auth/*`
- `/api/v1/data/*`
- `/api/v1/admin/*`
- `/api/v1/payments/*`
- `/api/v1/planner/*`
- `/api/v1/health`

Key examples:

- `POST /api/v1/auth/register`
- `POST /api/v1/auth/register/verify`
- `POST /api/v1/auth/login`
- `GET /api/v1/data/me`
- `GET /api/v1/data/dashboard`
- `GET /api/v1/data/marketplace`
- `POST /api/v1/data/marketplace/payment/checkout`
- `PATCH /api/v1/data/marketplace/orders/:orderId/receive`
- `GET /api/v1/data/labor`
- `GET /api/v1/data/services`
- `GET /api/v1/admin/overview`
- `POST /api/v1/payments/xendit/webhook`
- `GET /api/v1/planner/health`

## Deployment

Current recommended production setup for this project:

- `frontend/` deploy to Vercel or another static host
- `backend/` deploy to Google Cloud Run
- container images store in Google Artifact Registry
- optional routing / planner support services can run on Google Compute Engine VM instances
- MongoDB host on MongoDB Atlas
- file uploads and media on Supabase Storage

### 1. MongoDB Atlas

1. Create a cluster in Atlas.
2. Create a database user with read/write access.
3. In `Network Access`, allow the backend egress IP or use `0.0.0.0/0` if needed.
4. Copy the connection string and set `MONGODB_URI`.

Example:

```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/agrihub?retryWrites=true&w=majority
```

### 2. Backend on Google Cloud Run

The backend is containerized through [backend/Dockerfile](C:/Users/earlj/OneDrive/Desktop/SysArch/backend/Dockerfile).

Typical flow:

1. Build the backend image.
2. Push the image to Google Artifact Registry.
3. Deploy the image to Cloud Run.
4. Set backend environment variables.
5. Verify `/api/v1/health`.

Important notes:

- The Docker image installs Python and `reportlab` because deployed waybill generation uses them.
- Set `min instances` to `1` if you want to reduce cold starts.
- Keep Cloud Run close to MongoDB Atlas for better performance.

Health check example:

```bash
GET https://your-backend-domain/api/v1/health
```

Expected response:

```json
{
  "status": "ok",
  "service": "backend"
}
```

### 3. Google Artifact Registry

Use Artifact Registry to store the backend container image versions used by Cloud Run revisions.

This is useful for:

- build history
- controlled redeployments
- rollback to previous backend images

### 4. Google Compute Engine VM Instances

If you self-host support services for logistics or route planning, VM instances can be used for:

- OSRM
- GraphHopper
- planner / optimization services
- other auxiliary backend tools

### 5. Frontend on Vercel

Deploy the `frontend/` directory as the Vercel project root.

Suggested settings:

- Framework Preset: `Vite`
- Root Directory: `frontend`
- Build Command: `npm run build`
- Output Directory: `dist`

Set these frontend environment variables:

```env
VITE_API_BASE_URL=https://your-backend-domain/api/v1
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### 6. Production Checks

- Verify email registration and verification works
- Verify Google sign-in works
- Verify forgot-password flow works
- Verify marketplace checkout works
- Verify labor and service booking flows work
- Verify Supabase uploads work
- Verify wallet and refund flows work
- Verify admin dashboard access works
- Verify waybill download works on the deployed backend
- Verify `/api/v1/health` and `/api/v1/planner/health`

## Data and Startup Behavior

- The backend checks demo data during startup through `seedDemoData()`
- If `ENABLE_DEMO_DATA=true`, demo accounts and demo records are created
- If demo data is disabled, demo records are cleaned up
- Registration now stores pending signup data first and only creates the final user after email verification succeeds

## Notes

- Frontend source lives in `frontend/src`
- Backend source lives in `backend/src`
- The backend expects MongoDB, Supabase, Xendit, and email delivery settings for the full experience
- Google Maps functionality requires `VITE_GOOGLE_MAPS_API_KEY`
- Some interfaces are role-aware, so buyers, sellers, laborers, providers, admins, and super admins see different flows
- Marketplace logistics and order tracking behavior depend on the configured routing services and admin logistics simulation actions
