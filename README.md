# 🚻 NearLoo — Smart Public Toilet Locator

> AI-powered real-time public restroom finder for urban cities like Chennai and Coimbatore.

![NearLoo](https://img.shields.io/badge/NearLoo-v1.0.0-green)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)
![React](https://img.shields.io/badge/React-18-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Supabase-blue)

---

## 📌 Problem Statement

Citizens struggle to locate clean and accessible public toilets in cities like Chennai and Coimbatore, as Google Maps only shows static locations with no real-time data on cleanliness or occupancy. A web application is needed where municipal admins manage government public toilets, while citizens crowdsource cleanliness reports through a majority-voting mechanism, helping users instantly find the nearest suitable toilet through an interactive map.

---

## ✨ Features

### 🧍 Citizen Features
- 📍 Find nearby public toilets using GPS location
- 🗺 Interactive map with color-coded markers (Green = Clean, Red = Dirty, Grey = Closed)
- 🔍 Search toilets by name, area, or type "near me"
- 🚶 Get walking route directions (OSRM — no Google Maps API needed)
- 🔽 Filter by: Female Only / Accessible / Free / 24 Hours
- 📊 Report cleanliness (Clean / Dirty)
- ⭐ Rate toilets (1–5 stars + comment)
- ⚡ Real-time status updates via WebSocket

### 🏛 Municipality Admin Features
- ➕ Add / Edit / Delete public toilets
- 🔄 Manually update toilet status (Clean / Dirty / Closed / Maintenance)
- 🔔 Receive alerts when 5+ dirty reports are submitted
- 📋 View complaint dashboard and recent reports
- 📊 Toilet Health Overview (donut chart)
- 🗺 Mini map with all toilet markers

### ⚙️ System (Auto)
- 5+ dirty reports → status auto-changes to DIRTY
- WebSocket broadcasts live pin color changes to all users
- Admin receives instant notification

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js + Vite + Leaflet.js + OpenStreetMap |
| Backend | Spring Boot 3 + Spring Security + JWT |
| Real-time | WebSocket (STOMP) |
| Database | Supabase (PostgreSQL + PostGIS) |
| Routing | OSRM (Open Source Routing Machine) |
| Hosting | Vercel (Frontend) + Render (Backend) |
| Cost | ₹0 — Fully Free |

---

## 🗄 Database Tables

| Table | Purpose |
|---|---|
| users | Login + role (citizen / admin) |
| toilets | Toilet data + real-time status |
| toilet_reports | Crowdsource clean/dirty reports |
| ratings | Star ratings + comments |
| toilet_status_log | Admin status change history |
| notifications | Admin alerts |

---

## 🚀 Getting Started

### Prerequisites
- Java 21
- Node.js 18+
- Maven
- Supabase account (free)

---

### Backend Setup

```bash
# Clone the repository
git clone https://github.com/KanikaSuresh17/Nearloo_Backend.git
cd Nearloo_Backend

# Configure application.properties
spring.datasource.url=jdbc:postgresql://YOUR_SUPABASE_POOLER_URL:6543/postgres
spring.datasource.username=postgres.YOUR_PROJECT_REF
spring.datasource.password=YOUR_PASSWORD
jwt.secret=YOUR_JWT_SECRET
jwt.expiration=86400000
spring.datasource.hikari.data-source-properties.prepareThreshold=0
spring.datasource.hikari.data-source-properties.preferQueryMode=simple

# Run
mvn spring-boot:run
```

Backend runs on: `http://localhost:8080`

---

### Frontend Setup

```bash
# Clone the repository
git clone https://github.com/KanikaSuresh17/Nearloo_Frontend.git
cd Nearloo_Frontend

# Install dependencies
npm install

# Configure API URL in src/services/api.js
baseURL: 'http://localhost:8080/api'

# Run
npm run dev
```

Frontend runs on: `http://localhost:5173`

---

## 📡 API Endpoints

### Auth (Public)
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/auth/register | Register new citizen |
| POST | /api/auth/login | Login → returns JWT token |

### Toilets (Public)
| Method | Endpoint | Description |
|---|---|---|
| GET | /api/toilets/nearby?lat=&lng=&radius= | Find nearby toilets |
| GET | /api/toilets/{id} | Get toilet details |

### Reports & Ratings (JWT Required)
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/toilets/{id}/report?reportType= | Submit clean/dirty report |
| POST | /api/toilets/{id}/rating?stars=&comment= | Submit star rating |
| GET | /api/toilets/{id}/ratings | Get ratings + average |

### Admin (JWT + Admin Role Required)
| Method | Endpoint | Description |
|---|---|---|
| POST | /api/admin/toilets | Add new toilet |
| PUT | /api/admin/toilets/{id} | Update toilet info |
| PUT | /api/admin/toilets/{id}/status | Update toilet status |
| DELETE | /api/admin/toilets/{id} | Delete toilet |
| GET | /api/admin/notifications | Get admin alerts |

### WebSocket
| URL | Description |
|---|---|
| ws://host/ws | Connect |
| /topic/toilet-status | Subscribe for live status updates |

---

## 🌐 Deployment

### Backend → Render
```
Build Command: mvn clean package -DskipTests
Start Command: java -jar target/nearloo-backend-0.0.1-SNAPSHOT.jar
```

### Frontend → Vercel
```
Framework: Vite
Build Command: npm run build
Output Directory: dist
```

---

## 👥 Roles

| Role | Access |
|---|---|
| Citizen | Search, filter, report, rate toilets |
| Admin | Full CRUD, status management, notifications |

> Admin accounts are created via Postman only. All website registrations create citizen accounts.

---

## 🔄 Real-time Flow

```
User reports "Dirty" → 5+ reports received
        ↓
System auto-changes status to DIRTY
        ↓
WebSocket broadcasts to all connected clients
        ↓
Map pin color changes RED instantly
        ↓
Admin receives notification alert
        ↓
Admin cleans → marks "Clean" → pin turns GREEN
```

---

## 📱 Why NearLoo vs Google Maps?

| Feature | Google Maps | NearLoo |
|---|---|---|
| Toilet location | ✅ | ✅ |
| Real-time cleanliness | ❌ | ✅ |
| Occupancy status | ❌ | ✅ |
| Female only filter | ❌ | ✅ |
| Crowdsource reports | ❌ | ✅ |
| Municipality dashboard | ❌ | ✅ |
| Live WebSocket updates | ❌ | ✅ |

---

## 🏫 Project Info

- **Type:** Full Stack College Project
- **Cities Covered:*Coimbatore
- **Total Cost:** ₹0 (Fully Free Stack)

---
