# Byte Buddy

Low-connectivity food ordering & micro-credit platform for rural + urban India.

## Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌───────────────┐
│   React SPA     │────▶│  Express API     │────▶│  Firebase     │
│   (Vite + TW)   │     │  (Node.js)       │     │  (Auth + DB)  │
│   PWA + Offline  │     │  Razorpay/Twilio │     │  Firestore    │
└─────────────────┘     └──────────────────┘     └───────────────┘
```

**Frontend:** React 18, Vite, TailwindCSS, Framer Motion, i18next
**Backend:** Node.js, Express, Firebase Admin
**Database:** Firebase Firestore + Auth
**Payments:** Razorpay (test mode)
**SMS Fallback:** Twilio
**PWA:** Service worker + Workbox for offline support

## Features

- **Phone/OTP Login** via Firebase Auth
- **Restaurant Browsing** with veg/non-veg filters
- **Voice-to-Order** — speak in Hindi/Marathi, items auto-matched
- **Offline Support** — cached menus, queued orders via IndexedDB
- **Lite Mode** — auto-detects 2G/3G, disables images/animations
- **Wallet & Micro-Lending** — emergency meal credits with Trust Score
- **Vendor Dashboard** — order management, menu CRUD, earnings
- **Vendor Registration** — simple form for non-smartphone vendors
- **Admin Panel** — users, vendors, analytics, credit overview
- **Multi-language** — English, Hindi (हिन्दी), Marathi (मराठी)
- **Dark Mode** with system preference detection
- **PWA** — installable, works offline

## Setup

### Prerequisites
- Node.js 18+
- Firebase project with Auth + Firestore enabled

### 1. Clone & Install

```bash
cd ByteBuddy
cd client && npm install
cd ../server && npm install
```

### 2. Configure Environment

```bash
# Client
cp client/.env.example client/.env
# Edit client/.env with your Firebase config

# Server
cp server/.env.example server/.env
# Edit server/.env with your credentials
```

### 3. Run Development

```bash
# Terminal 1 - Server
cd server && npm run dev

# Terminal 2 - Client
cd client && npm run dev
```

Open http://localhost:5173

### 4. Build for Production

```bash
cd client && npm run build
```

### 5. Deploy to Firebase

```bash
firebase deploy
```

## Environment Variables

### Client (`client/.env`)
| Variable | Description |
|----------|-------------|
| `VITE_FIREBASE_API_KEY` | Firebase API key |
| `VITE_FIREBASE_AUTH_DOMAIN` | Firebase auth domain |
| `VITE_FIREBASE_PROJECT_ID` | Firebase project ID |
| `VITE_FIREBASE_STORAGE_BUCKET` | Firebase storage bucket |
| `VITE_FIREBASE_MESSAGING_SENDER_ID` | FCM sender ID |
| `VITE_FIREBASE_APP_ID` | Firebase app ID |

### Server (`server/.env`)
| Variable | Description |
|----------|-------------|
| `PORT` | Server port (default: 3001) |
| `RAZORPAY_KEY_ID` | Razorpay test key |
| `RAZORPAY_KEY_SECRET` | Razorpay test secret |
| `TWILIO_ACCOUNT_SID` | Twilio account SID |
| `TWILIO_AUTH_TOKEN` | Twilio auth token |
| `TWILIO_PHONE_NUMBER` | Twilio phone number |

## Project Structure

```
ByteBuddy/
├── client/
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/          # Route-level screens
│   │   ├── hooks/          # Custom React hooks
│   │   ├── context/        # Auth, Cart, Wallet, Theme, LiteMode
│   │   ├── services/       # Firebase, API client
│   │   ├── i18n/           # en, hi, mr translations
│   │   └── utils/          # Trust score, offline queue, voice parser
│   ├── tailwind.config.js
│   └── vite.config.js
├── server/
│   ├── routes/             # API endpoints
│   ├── middleware/          # Auth, rate limiting
│   ├── services/           # Twilio, Razorpay, trust score
│   └── index.js
└── firebase.json
```
