# 🚀 SmartLeads - Lead Management Dashboard

A full-stack Lead Management Dashboard built with the **MERN stack** (MongoDB, Express.js, React.js, Node.js) using **TypeScript** throughout. Features JWT authentication, role-based access control, advanced filtering, and a premium UI.

![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

---

## ✨ Features

### Core
- **JWT Authentication** - Secure register/login with bcrypt password hashing
- **RBAC** - Admin and Sales User roles with permission-based access
- **Lead CRUD** - Create, Read, Update, Delete leads with validation
- **Advanced Filtering** - Filter by status, source, search by name/email — all combinable
- **Backend Pagination** - Proper skip/limit with metadata (10 per page)
- **Debounced Search** - 400ms debounce on search input
- **CSV Export** - Export filtered leads as CSV
- **Dark Mode** - System-preference-aware with manual toggle

### UI/UX
- Premium glassmorphism design with gradient accents
- Responsive layout with collapsible sidebar
- Loading states, empty states, and error handling
- Animated transitions and micro-interactions
- Toast notifications for all actions

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 19, TypeScript, TailwindCSS v4, Vite |
| Backend | Node.js, Express.js, TypeScript |
| Database | MongoDB + Mongoose |
| Auth | JWT + bcrypt |
| DevOps | Docker + Docker Compose |

---

## 📁 Project Structure

```
├── client/                    # React Frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/        # Reusable components
│   │   │   ├── layout/        # Layout component
│   │   │   └── leads/         # Lead-specific components
│   │   ├── context/           # Auth & Theme contexts
│   │   ├── hooks/             # Custom hooks (useDebounce)
│   │   ├── pages/             # Page components
│   │   ├── services/          # API service layer
│   │   ├── types/             # TypeScript interfaces
│   │   └── App.tsx
│   ├── Dockerfile
│   └── nginx.conf
├── server/                    # Express Backend
│   ├── src/
│   │   ├── config/            # Database config
│   │   ├── controllers/       # Route controllers
│   │   ├── middleware/        # Auth, RBAC, error handling
│   │   ├── models/            # Mongoose models
│   │   ├── routes/            # API routes
│   │   ├── types/             # TypeScript interfaces
│   │   ├── validators/        # Request validators
│   │   └── server.ts
│   └── Dockerfile
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## 🚀 Setup Instructions

### Prerequisites
- Node.js v18+
- MongoDB (local or Atlas)
- npm or yarn

### 1. Clone the repository
```bash
git clone <repo-url>
cd smart-leads-dashboard
```

### 2. Setup Backend
```bash
cd server
cp ../.env.example .env    # Edit with your MongoDB URI & JWT secret
npm install
npm run dev
```

### 3. Setup Frontend
```bash
cd client
npm install
npm run dev
```

### 4. Docker Setup (Alternative)
```bash
docker-compose up --build
```
- Frontend: http://localhost:3000
- Backend: http://localhost:5000
- MongoDB: localhost:27017

---

## 🔑 Environment Variables

Copy `.env.example` and configure:

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port | 5000 |
| `MONGODB_URI` | MongoDB connection string | mongodb://localhost:27017/smart-leads |
| `JWT_SECRET` | JWT signing secret | (change in production!) |
| `JWT_EXPIRES_IN` | Token expiration | 7d |
| `CLIENT_URL` | Frontend URL for CORS | http://localhost:5173 |

---

## 📡 API Documentation

### Auth Endpoints

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| POST | `/api/auth/register` | Register new user | Public |
| POST | `/api/auth/login` | Login user | Public |
| GET | `/api/auth/me` | Get current user profile | Private |

### Lead Endpoints

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| GET | `/api/leads` | Get leads (paginated, filterable) | Private |
| GET | `/api/leads/:id` | Get single lead | Private |
| POST | `/api/leads` | Create new lead | Private |
| PUT | `/api/leads/:id` | Update lead | Private |
| DELETE | `/api/leads/:id` | Delete lead | Admin only |
| GET | `/api/leads/export/csv` | Export leads as CSV | Private |
| GET | `/api/leads/stats/overview` | Get dashboard stats | Private |

### Query Parameters (GET /api/leads)

| Param | Type | Description |
|-------|------|-------------|
| `status` | string | Filter: New, Contacted, Qualified, Lost |
| `source` | string | Filter: Website, Instagram, Referral |
| `search` | string | Search name or email |
| `sort` | string | latest (default) or oldest |
| `page` | number | Page number (default: 1) |
| `limit` | number | Records per page (default: 10) |

### Response Format
```json
{
  "success": true,
  "message": "Leads retrieved successfully.",
  "data": {
    "records": [...],
    "pagination": {
      "currentPage": 1,
      "totalPages": 5,
      "totalRecords": 48,
      "limit": 10,
      "hasNextPage": true,
      "hasPrevPage": false
    }
  }
}
```

---

## 👥 Role-Based Access

| Feature | Admin | Sales User |
|---------|-------|------------|
| View all leads | ✅ | ❌ (own only) |
| Create leads | ✅ | ✅ |
| Update leads | ✅ (all) | ✅ (own only) |
| Delete leads | ✅ | ❌ |
| Export CSV | ✅ | ✅ (own only) |
| Dashboard stats | ✅ (all) | ✅ (own only) |

---

## 🛠️ Development

```bash
# Backend (hot reload)
cd server && npm run dev

# Frontend (Vite dev server)
cd client && npm run dev
```
