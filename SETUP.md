# <img src="https://via.placeholder.com/40x40/1e40af/ffffff?text=MIC" alt="MIC College Logo" style="vertical-align: middle; margin-right: 10px;"> MIC-ELMS Setup Guide

## 📋 Overview
Complete setup instructions for the **MIC College of Technology Employee Leave Management System (MIC-ELMS)** - a comprehensive MERN stack application with role-based authentication and institutional branding.

## 🔧 Prerequisites
Before setting up MIC-ELMS, ensure you have the following installed:

| Software | Version | Purpose |
|----------|---------|---------|
| **Node.js** | v16+ | JavaScript runtime |
| **MongoDB** | v5.0+ | Database |
| **Git** | Latest | Version control |
| **Code Editor** | VS Code recommended | Development |

### Quick Installation Links
- [Node.js Download](https://nodejs.org/)
- [MongoDB Download](https://www.mongodb.com/try/download/community)
- [Git Download](https://git-scm.com/downloads)
- [VS Code Download](https://code.visualstudio.com/)

## 🚀 Installation Steps

### Step 1: Clone Repository
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/MIC-ELMS.git
cd MIC-ELMS
```

### Step 2: Backend Setup
```bash
# Navigate to backend directory
cd backend

# Install backend dependencies
npm install

# Create environment configuration file
cp config.env.example config.env
```

### Step 3: Environment Configuration
Create `backend/config.env` with the following variables:

```env
# Development Configuration
NODE_ENV=development
PORT=5000

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/mic-elms

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here-make-it-long-and-secure
JWT_EXPIRE=7d

# Security Configuration
BCRYPT_SALT_ROUNDS=12

# CORS Configuration (optional)
CORS_ORIGIN=http://localhost:5173
```

> **⚠️ Important:** Replace `JWT_SECRET` with a strong, unique secret key for production use.

### Step 4: Database Setup
```bash
# Start MongoDB service
# Windows users:
net start MongoDB

# macOS/Linux users:
sudo systemctl start mongod

# Verify MongoDB is running
# Check if port 27017 is listening
netstat -an | grep 27017
```

### Step 5: Database Seeding
```bash
# Navigate to backend directory (if not already there)
cd backend

# Run database seeding
node seed.js
```

**Expected Output:**
```
✅ MongoDB connected
✅ Database cleared
✅ Admin user created
✅ HOD user created
✅ Employee users created
✅ Database seeding completed successfully
```

### Step 6: Frontend Setup
```bash
# Navigate to frontend directory
cd ../frontend

# Install frontend dependencies
npm install
```

### Step 7: Start Development Servers

#### Terminal 1 - Backend Server
```bash
cd backend
npm start
```
**Expected Output:**
```
✅ MongoDB connected
🚀 Server running on port 5000
```

#### Terminal 2 - Frontend Server
```bash
cd frontend
npm run dev
```
**Expected Output:**
```
Local:   http://localhost:5173/
Network: http://192.168.x.x:5173/
```

## 🔐 Default Login Credentials

### Admin Account
- **Email:** `admin@mic.edu`
- **Password:** `admin123`
- **Permissions:** 
  - Full system administration
  - Employee management
  - Leave policy configuration
  - System reports and analytics

### HOD Account
- **Email:** `hod@mic.edu`
- **Password:** `hod123`
- **Permissions:**
  - Department management
  - Leave approval/rejection
  - Employee oversight
  - Department reports

### Employee Accounts
| Email | Password | Department |
|-------|----------|------------|
| `employee@mic.edu` | `employee123` | Computer Science |
| `jane.smith@mic.edu` | `employee123` | Computer Science |
| `mike.johnson@mic.edu` | `employee123` | Computer Science |

**Employee Permissions:**
- Leave application submission
- Profile management
- Leave history viewing
- Leave balance tracking

## ✅ Verification Steps

### 1. Backend Health Check
```bash
# Test backend API
curl http://localhost:5000/api/test
```
**Expected Response:** `{"success": true, "message": "API is working"}`

### 2. Database Connection Verification
Check console logs for:
```
✅ MongoDB connected
Database: mic-elms
```

### 3. Frontend Application Test
1. Open browser and navigate to `http://localhost:5173`
2. You should see the MIC-ELMS login page with:
   - MIC College branding
   - Professional login form
   - Demo credentials display

### 4. Authentication Test
1. Login with admin credentials: `admin@mic.edu` / `admin123`
2. Verify dashboard loads with admin features
3. Test navigation between different sections
4. Logout and test other user roles

### 5. Leave Management Test
1. Login as employee
2. Navigate to "Apply Leave"
3. Fill out leave application form
4. Submit application
5. Login as HOD and verify leave appears in pending requests

## 🔧 Common Issues & Solutions

### MongoDB Connection Error
```bash
# Check if MongoDB is running
# Windows:
net start MongoDB

# macOS/Linux:
sudo systemctl start mongod
sudo systemctl status mongod

# Check MongoDB logs
# Windows: Check Event Viewer
# macOS/Linux: journalctl -u mongod
```

### Port Already in Use
```bash
# Find process using port 5000
# Windows:
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# macOS/Linux:
lsof -ti:5000 | xargs kill -9
```

### Package Installation Issues
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# If still having issues, try:
npm install --legacy-peer-deps
```

### Database Seeding Failed
```bash
# Check MongoDB connection
mongo --eval "db.adminCommand('ismaster')"

# Verify environment variables
cat backend/config.env

# Clear database and reseed
mongo mic-elms --eval "db.dropDatabase()"
node seed.js
```

### Frontend Build Issues
```bash
# Clear Vite cache
rm -rf node_modules/.vite
npm run dev

# If dependencies issue:
npm install --force
```

## 📁 Project Structure
```
MIC-ELMS/
├── 📁 backend/                    # Node.js Backend
│   ├── 📁 models/                 # Database models
│   │   ├── User.js                # User model with roles
│   │   └── Leave.js               # Leave application model
│   ├── 📁 routes/                 # API routes
│   │   ├── auth.js                # Authentication routes
│   │   ├── users.js               # User management
│   │   ├── leaves.js              # Leave management
│   │   └── dashboard.js           # Dashboard data
│   ├── 📁 middleware/             # Custom middleware
│   │   ├── auth.js                # JWT authentication
│   │   └── errorHandler.js        # Error handling
│   ├── 📄 config.env              # Environment variables
│   ├── 📄 server.js               # Express server setup
│   ├── 📄 seed.js                 # Database seeding script
│   └── 📄 package.json            # Backend dependencies
├── 📁 frontend/                   # React Frontend
│   ├── 📁 src/
│   │   ├── 📁 components/         # Reusable components
│   │   │   ├── InstitutionalHeader.jsx
│   │   │   └── LeavePolicyReference.jsx
│   │   ├── 📁 pages/              # Application pages
│   │   │   ├── 📁 admin/          # Admin dashboard & features
│   │   │   ├── 📁 hod/            # HOD dashboard & features
│   │   │   ├── 📁 employee/       # Employee dashboard & features
│   │   │   └── Login.jsx          # Authentication page
│   │   ├── 📁 contexts/           # React contexts
│   │   │   └── AuthContext.jsx    # Authentication context
│   │   ├── 📁 layouts/            # Page layouts
│   │   │   ├── AdminLayout.jsx    # Admin layout
│   │   │   ├── HODLayout.jsx      # HOD layout
│   │   │   └── EmployeeLayout.jsx # Employee layout
│   │   ├── 📁 utils/              # Utility functions
│   │   ├── 📁 logo/               # MIC College logo
│   │   └── 📄 index.css           # Global styles with MIC branding
│   ├── 📄 index.html              # Entry point
│   ├── 📄 vite.config.js          # Vite configuration
│   └── 📄 package.json            # Frontend dependencies
├── 📄 SETUP.md                    # This setup guide
├── 📄 PROJECT_REPORT.md           # Project documentation
├── 📄 TECHNICAL_INFO.md           # Technical details
├── 📄 README.md                   # Project overview
└── 📄 .gitignore                  # Git ignore rules
```

## 🎯 Key Features Overview

### 🔐 Authentication System
- JWT-based authentication
- Role-based access control (Admin, HOD, Employee)
- Secure password hashing
- Session management

### 📝 Leave Management
- Multiple leave types (CL, SCL, EL, HPL, CCL)
- Half-year quota system
- Automatic working days calculation
- Leave balance tracking

### 🎨 MIC College Branding
- Official institutional colors
- MIC College logo integration
- Professional UI design
- Role-based color themes

### 📊 Dashboard Features
- Real-time leave statistics
- Recent applications tracking
- Quick action buttons
- Role-specific information

## 🚀 Next Steps

### For Developers
1. ✅ Complete setup verification
2. 🔍 Explore codebase structure
3. 🧪 Test all user roles and features
4. 📖 Review technical documentation
5. 🔧 Configure development environment

### For Users
1. 🔑 Login with provided credentials
2. 🏠 Explore role-specific dashboards
3. 📝 Test leave application workflow
4. 👥 Switch between different user roles
5. 📊 Review leave management features

### For Administrators
1. 🗄️ Configure production database
2. 🔐 Set up secure environment variables
3. 🌐 Configure production deployment
4. 📈 Set up monitoring and logging
5. 🔒 Implement additional security measures

## 📞 Support & Troubleshooting

### Getting Help
- 📋 Check console logs for detailed error messages
- 🔍 Verify all environment variables are correctly set
- 📦 Ensure all dependencies are installed properly
- 🧪 Test with different user roles to verify functionality

### Debug Mode
Enable debug mode for detailed logging:
```bash
# Backend debug mode
DEBUG=* npm start

# Frontend debug mode
npm run dev -- --debug
```

### Common Solutions
1. **Clear browser cache** if frontend issues persist
2. **Restart both servers** after configuration changes
3. **Check firewall settings** if connection issues occur
4. **Verify MongoDB service** is running and accessible
5. **Update Node.js** if version compatibility issues arise

## 📚 Additional Resources
- [Node.js Documentation](https://nodejs.org/docs/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [React Documentation](https://reactjs.org/docs/)
- [Express.js Documentation](https://expressjs.com/)
- [JWT Documentation](https://jwt.io/)

---

**🎓 MIC College of Technology - Employee Leave Management System**

*A professional, institutional-grade leave management solution built with modern web technologies.*