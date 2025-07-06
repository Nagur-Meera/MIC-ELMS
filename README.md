# <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTT8EqzjhTM2m8tvUxSKxLeMqG8liK9JV0CKA&s" style="vertical-align: middle; margin-right: 10px;"> MIC-ELMS Setup Guide

## 📋 Project Description
**MIC College of Technology Employee Leave Management System (MIC-ELMS)** - A MERN stack application with role-based authentication for managing employee leave applications.

## 📁 Project Structure
```
MIC-ELMS/
├── backend/                    # Node.js Backend
│   ├── models/                 # Database models
│   ├── routes/                 # API routes
│   ├── middleware/             # Custom middleware
│   ├── config.env              # Environment variables
│   ├── server.js               # Express server
│   ├── seed.js                 # Database seeding
│   └── package.json            # Backend dependencies
├── frontend/                   # React Frontend
│   ├── src/                    # Source code
│   ├── public/                 # Public assets
│   ├── package.json            # Frontend dependencies
│   └── vite.config.js          # Vite configuration
└── README.md                   # Project overview
```

## 🔧 Prerequisites
- **Node.js** (v16+)
- **MongoDB** (v5.0+)
- **Git**

## 🚀 Setup Instructions

### Step 1: Clone/Download Project
```bash
# Option 1: Clone from GitHub
git clone https://github.com/YOUR_USERNAME/MIC-ELMS.git
cd MIC-ELMS

# Option 2: Download and extract the provided folder
# (node_modules folders are excluded - you'll install them next)
```

### Step 2: Environment Configuration
Create `backend/config.env` file:
```env
NODE_ENV=development
PORT=5000
MONGODB_URI=mongodb://localhost:27017/mic-elms
JWT_SECRET=your-super-secret-jwt-key-here-make-it-long-and-secure
JWT_EXPIRE=7d
BCRYPT_SALT_ROUNDS=12
CORS_ORIGIN=http://localhost:5173
```

### Step 3: Install Dependencies
```bash
# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### Step 4: Database Setup & Seeding
```bash
# Start MongoDB service
# Windows: net start MongoDB
# macOS/Linux: sudo systemctl start mongod

# Seed the database
cd backend
node seed.js
```

### Step 5: Start Application
```bash
# Terminal 1 - Start Backend Server
cd backend
npm start
# Backend runs on: http://localhost:5000

# Terminal 2 - Start Frontend Server
cd frontend
npm run dev
# Frontend runs on: http://localhost:5173
```

## 🔐 Login Credentials

| Role | Email | Password |
|------|-------|----------|
| **Admin** | admin@mic.edu | admin123 |
| **HOD** | hod@mic.edu | hod123 |
| **Employee** | employee@mic.edu | employee123 |

## ✅ Verification
1. Open browser: `http://localhost:5173`
2. Login with any of the above credentials
3. Test the dashboard and leave management features

## 🔧 Common Issues
- **MongoDB not running**: Start MongoDB service
- **Port in use**: Kill process using port 5000/5173
- **Dependencies error**: Delete `node_modules` and run `npm install` again

---

**🎓 MIC College of Technology - Employee Leave Management System**
