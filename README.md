# VoltIQ — Setup Guide

## 🔥 Firebase Console Setup (Required before using the app)

### 1. Enable Authentication
- Go to Firebase Console → Authentication → Sign-in method
- Enable **Email/Password**

### 2. Set Firestore Security Rules
- Go to Firebase Console → Firestore Database → Rules
- Paste the contents of `firestore.rules` and publish

### 3. Create Your Admin Account
- Open `login.html` in a browser
- Select **Admin** role
- Click **Sign Up**
- Enter your name, email, password
- Enter the Admin Secret Key: `VOLTIQ_ADMIN_2025`
- ⚠️ **Change this key** in `login.html` (search for `VOLTIQ_ADMIN_2025`)

### 4. Firestore Indexes (Optional — for history log sorting)
If you want the station update history to load sorted from Firestore:
- Go to Firestore → Indexes → Add composite index
- Collection: `station_updates`
- Fields: `ownerId` (Ascending), `timestamp` (Descending)

---

## 📁 File Overview

| File | Purpose | Access |
|------|---------|--------|
| `dashboard.html` | Public map, charts, stations, reviews | Everyone |
| `login.html` | Auth — User / Station Owner / Admin | Everyone |
| `pricing.html` | Subscription plans (₹300 Basic / ₹500 Pro) | Everyone |
| `station-owner.html` | Station telemetry & management panel | Station Owners only |
| `admin.html` | Full platform admin — users, approvals, revenue | Admins only |

---

## 🔄 User Flow

```
New User      → login.html (Sign Up as User)      → dashboard.html
Station Owner → login.html (Sign Up as Owner)     → Pending screen (await admin approval)
Admin         → login.html (Approve owner)        → admin.html → Approve → Owner gets access
Owner         → login.html (Log In as Owner)      → station-owner.html
```

---

## ⚠️ Security Checklist
- [ ] Change `VOLTIQ_ADMIN_2025` to a strong secret in `login.html`
- [ ] Apply Firestore security rules from `firestore.rules`
- [ ] Enable only Email/Password auth (disable others unless needed)
- [ ] Review Firestore indexes if history log has issues

---

## 🛠️ Tech Stack
- **Frontend**: Vanilla HTML/CSS/JS (5 self-contained files)
- **Auth**: Firebase Authentication (Email/Password)
- **Database**: Cloud Firestore
- **Maps**: Leaflet.js + CartoDB dark tiles
- **Charts**: Chart.js 4.4
- **Fonts**: Google Fonts (Rajdhani, Space Mono, Inter)
