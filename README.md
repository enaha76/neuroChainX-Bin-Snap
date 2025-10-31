# 🌍 NeuroChainX-Bin-Snap

![Version](https://img.shields.io/badge/version-1.0.0-green)
![License](https://img.shields.io/badge/license-MIT-blue)
![Hedera](https://img.shields.io/badge/blockchain-Hedera-purple)
![React](https://img.shields.io/badge/frontend-React-blue)
![Node.js](https://img.shields.io/badge/backend-Node.js-green)

**NeuroChainX-Bin-Snap** is a complete blockchain-powered waste management ecosystem consisting of two integrated applications that revolutionize urban waste management through citizen engagement and blockchain rewards.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Understanding Git Submodules](#-understanding-git-submodules)
- [Project Architecture](#-project-architecture)
- [Submodules](#-submodules)
- [Quick Start](#-quick-start)
- [Technology Stack](#-technology-stack)
- [Setup Instructions](#-setup-instructions)
- [Development Workflow](#-development-workflow)
- [How They Work Together](#-how-they-work-together)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

NeuroChainX-Bin-Snap is a comprehensive waste management platform that incentivizes citizens to report waste issues and helps municipalities maintain cleaner cities.

### The Platform Consists Of:

1. **EcoClean (User App)** - Citizen-facing mobile-first web app where users report overflowing waste bins and earn cryptocurrency rewards
2. **EcoWatch (Admin Dashboard)** - Administrative dashboard for managing reports, coordinating cleanup teams, and tracking operations

Both applications are powered by:
- **Hedera blockchain** for transparent and instant reward distribution
- **AI-powered image analysis** (DeepSeek) to automatically assess waste urgency levels

### Key Benefits

- 🎯 **For Citizens**: Earn crypto rewards (ECO tokens/HBAR) for reporting waste issues
- 🏛️ **For Municipalities**: Real-time awareness of waste issues with proactive management
- 🤖 **For Efficiency**: AI-powered prioritization and blockchain-verified reporting
- 🌱 **For Environment**: Faster cleanup response times lead to cleaner cities

---

## 📦 Understanding Git Submodules

This project uses **Git submodules** to organize code into separate repositories while maintaining them as part of a single ecosystem.

### What Are Git Submodules?

Git submodules allow you to keep a Git repository as a subdirectory of another Git repository. This lets you clone another repository into your project and keep your commits separate.

### Why Use Submodules Here?

- **Modularity**: Each application (user app and admin dashboard) is independently developed
- **Reusability**: Submodules can be used in multiple parent projects
- **Version Control**: Each submodule has its own Git history
- **Team Collaboration**: Different teams can work on different submodules simultaneously
- **Deployment Flexibility**: Each submodule can be deployed independently

### Project Structure

```
neuroChainX-Bin-Snap/                    # Parent repository
├── .gitmodules                          # Submodule configuration file
├── README.md                            # This file
└── modules/                             # Submodules directory
    ├── user-app-bin/                    # User application (EcoClean)
    │   ├── src/                         # React frontend
    │   ├── backend/                     # Node.js + Express backend
    │   ├── package.json
    │   └── README.md                    # Detailed user app docs
    └── admin-dashboear-cibe/            # Admin dashboard (EcoWatch)
        ├── src/                         # React frontend
        ├── backend/                     # Express + TypeScript + Prisma
        ├── package.json
        └── README.md                    # Detailed admin docs
```

### Submodule Configuration (`.gitmodules`)

```ini
[submodule "modules/user-app-bin"]
    path = modules/user-app-bin
    url = git@github.com:enaha76/user-app-bin.git

[submodule "modules/admin-dashboear-cibe"]
    path = modules/admin-dashboear-cibe
    url = git@github.com:enaha76/admin-dashboear-cibe.git
```

### Working with Submodules - Essential Commands

**Clone repository with all submodules:**
```bash
git clone --recurse-submodules git@github.com:enaha76/neuroChainX-Bin-Snap.git
```

**If already cloned without submodules:**
```bash
git submodule init
git submodule update
```

**Update all submodules to latest:**
```bash
git submodule update --remote --merge
```

**Navigate and work in a submodule:**
```bash
cd modules/user-app-bin
# Now you're inside the submodule's independent repository
git status
git log
# Make changes, commit, and push as normal
```

**Update parent repo after submodule changes:**
```bash
cd modules/user-app-bin
# Make changes
git add .
git commit -m "Update features"
git push origin main
cd ../..
# Update parent to track new submodule commit
git add modules/user-app-bin
git commit -m "Update user-app-bin submodule"
git push
```

---

## 🏗️ Project Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                  NEUROCHAINX-BIN-SNAP                       │
│                   (Parent Repository)                        │
└─────────────────────────────────────────────────────────────┘
                            │
            ┌───────────────┴───────────────┐
            │                               │
            ▼                               ▼
┌───────────────────────┐       ┌───────────────────────┐
│   USER APP (EcoClean) │       │ ADMIN DASHBOARD       │
│                       │       │   (EcoWatch)          │
│  ┌─────────────────┐ │       │  ┌─────────────────┐  │
│  │ React Frontend  │ │       │  │ React Frontend  │  │
│  │  (Port 5173)    │ │       │  │  (Port 8080)    │  │
│  └─────────────────┘ │       │  └─────────────────┘  │
│          │            │       │          │            │
│  ┌─────────────────┐ │       │  ┌─────────────────┐  │
│  │ Express Backend │ │       │  │ Express Backend │  │
│  │  (Port 3001)    │ │       │  │  (Port 3000)    │  │
│  └─────────────────┘ │       │  └─────────────────┘  │
│          │            │       │          │            │
│  ┌─────────────────┐ │       │  ┌─────────────────┐  │
│  │    MongoDB      │ │       │  │   PostgreSQL    │  │
│  └─────────────────┘ │       │  └─────────────────┘  │
└───────────────────────┘       └───────────────────────┘
            │                               │
            └───────────────┬───────────────┘
                            │
                            ▼
            ┌───────────────────────────┐
            │   HEDERA BLOCKCHAIN       │
            │   (Testnet/Mainnet)       │
            │   - ECO Token (HTS)       │
            │   - HBAR Rewards          │
            └───────────────────────────┘
                            │
                            ▼
            ┌───────────────────────────┐
            │   OPENROUTER AI API       │
            │   (DeepSeek Vision)       │
            │   - Image Analysis        │
            │   - Urgency Detection     │
            └───────────────────────────┘
```

### Data Flow

1. User reports waste via EcoClean app
2. Image uploaded and analyzed by AI (urgency detected)
3. Report saved to MongoDB
4. Backend checks if first reporter
5. If first reporter: Hedera transfers ECO tokens
6. Admin views report in EcoWatch dashboard (PostgreSQL)
7. Admin assigns cleanup team
8. Team cleans bin and marks as complete
9. Both databases updated
10. Next reporter becomes eligible for rewards

---

## 📱 Submodules

### 1. User App - EcoClean

**Repository**: [enaha76/user-app-bin](https://github.com/enaha76/user-app-bin)  
**Location**: `modules/user-app-bin`  
**Purpose**: Citizen-facing application for reporting waste issues

#### What is EcoClean?

A revolutionary civic engagement platform that gamifies waste management by rewarding citizens with blockchain-based cryptocurrency (ECO tokens) for reporting overflowing or dirty waste bins.

#### Key Features

- 🤖 **AI-Powered Detection** - Automatic waste urgency analysis using DeepSeek AI
- 💰 **Blockchain Rewards** - Instant ECO token payments via Hedera
- 📍 **Location Services** - GPS-based bin detection + QR code scanning
- 📊 **User Dashboard** - Track reports, earnings, and environmental impact
- 🔐 **Smart Verification** - First-reporter system prevents spam
- 📸 **Image Upload** - Photo upload for AI analysis
- 🎯 **Multi-step Form** - Intuitive wizard-style report submission

#### Tech Stack

**Frontend**: React 18 + TypeScript + Vite + TailwindCSS + shadcn/ui + TanStack Query  
**Backend**: Node.js + Express + MongoDB + Mongoose  
**Blockchain**: Hedera SDK + ECO Token (HTS)  
**AI**: OpenRouter API + DeepSeek Vision

**Ports**: Frontend `5173` | Backend `3001`

#### Reward System

| Urgency | ECO Tokens |
|---------|-----------|
| Critical | 75 ECO |
| High | 50 ECO |
| Medium | 25 ECO |
| Low | 10 ECO |

#### Quick Start

```bash
cd modules/user-app-bin

# Backend
cd backend && npm install && cp .env.example .env
# Configure .env with Hedera credentials
node scripts/create-token.js  # Create ECO token
npm run dev  # Port 3001

# Frontend (new terminal)
cd modules/user-app-bin && npm install && cp .env.local.example .env.local
npm run dev  # Port 5173
```

#### API Endpoints

```
POST   /api/reports                  Submit waste report
GET    /api/reports/:reportId        Get report by ID
GET    /api/reports/user/:userId     Get user's reports
GET    /api/bins/:binId/status       Check bin status
PATCH  /api/reports/bin/:binId/clean Mark bin cleaned
GET    /api/rewards/balance/:walletId Get token balance
```

**📚 Full Documentation**: See `modules/user-app-bin/README.md`

---

### 2. Admin Dashboard - EcoWatch

**Repository**: [enaha76/admin-dashboear-cibe](https://github.com/enaha76/admin-dashboear-cibe)  
**Location**: `modules/admin-dashboear-cibe`  
**Purpose**: Administrative dashboard for managing operations

#### What is EcoWatch?

A comprehensive admin dashboard for municipal administrators and team leaders to manage citizen-submitted waste reports, coordinate cleanup teams, and track operations.

#### Key Features

- 📊 **Dashboard Overview** - Real-time statistics, KPIs, charts
- 📝 **Report Management** - View, filter, verify, assign reports
- 👥 **Team Management** - Create teams, assign members
- 📈 **Analytics** - Advanced data visualization with Recharts
- 🔐 **Authentication** - JWT-based auth with RBAC (Admin/Leader/User roles)
- 🎨 **Modern UI** - Responsive design + dark mode
- 🔍 **Advanced Filtering** - Status, urgency, date range, team filters

#### Tech Stack

**Frontend**: React 18 + TypeScript + Vite + TailwindCSS + shadcn/ui + Recharts  
**Backend**: Node.js + Express + TypeScript + Prisma ORM + PostgreSQL  
**Auth**: JWT + bcrypt + express-validator

**Ports**: Frontend `8080` | Backend `3000` | Prisma Studio `5555`

#### User Roles

| Role | Permissions |
|------|------------|
| ADMIN | Full access - manage users, reports, teams |
| TEAM_LEADER | Manage assigned team, update status |
| USER | Submit reports, view own reports |

#### Status Workflow

```
PENDING → VERIFIED → CLEANING → COMPLETED
            ↓
         REJECTED
```

#### Quick Start

```bash
cd modules/admin-dashboear-cibe

# Automated setup
./setup.sh

# Or manual:
cd backend && npm install && cp .env.example .env
# Configure .env with PostgreSQL
npm run prisma:generate && npm run prisma:migrate && npm run prisma:seed
npm run dev  # Port 3000

# Frontend (new terminal)
cd modules/admin-dashboear-cibe && npm install
npm run dev  # Port 8080
```

#### Default Login

```
Admin: admin@ecowatch.com / admin123
Team Leader: leader@ecowatch.com / leader123
User: sarah.johnson@example.com / user123
```

#### API Endpoints

```
POST   /api/auth/login              Login
GET    /api/auth/me                 Get current user
GET    /api/reports                 Get all reports (filtered)
PATCH  /api/reports/:id/status      Update status
PATCH  /api/reports/:id/assign      Assign team
GET    /api/teams                   Get all teams
POST   /api/teams                   Create team
GET    /api/dashboard/stats         Get statistics
```

**📚 Full Documentation**: See `modules/admin-dashboear-cibe/README.md`

---

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- MongoDB (local or Atlas)
- PostgreSQL 14+
- Hedera testnet account ([Get free](https://portal.hedera.com/))
- OpenRouter API key ([Get key](https://openrouter.ai/))

### 1. Clone with Submodules

```bash
git clone --recurse-submodules git@github.com:enaha76/neuroChainX-Bin-Snap.git
cd neuroChainX-Bin-Snap

# If already cloned without submodules:
git submodule init && git submodule update
```

### 2. Setup Hedera

1. Create account at https://portal.hedera.com/
2. Get Account ID (`0.0.xxxxx`) and Private Key
3. Fund via testnet faucet
4. Create ECO token:
```bash
cd modules/user-app-bin/backend
npm install && cp .env.example .env
# Add Hedera credentials to .env
node scripts/create-token.js
```

### 3. Start User App

**Terminal 1 - Backend:**
```bash
cd modules/user-app-bin/backend
npm run dev  # Port 3001
```

**Terminal 2 - Frontend:**
```bash
cd modules/user-app-bin
npm install && cp .env.local.example .env.local
npm run dev  # Port 5173
```

### 4. Start Admin Dashboard

**Terminal 3 - Backend:**
```bash
cd modules/admin-dashboear-cibe/backend
npm install && cp .env.example .env
# Configure PostgreSQL in .env
npm run prisma:generate && npm run prisma:migrate && npm run prisma:seed
npm run dev  # Port 3000
```

**Terminal 4 - Frontend:**
```bash
cd modules/admin-dashboear-cibe
npm install
npm run dev  # Port 8080
```

### 5. Access Applications

| Application | URL | Credentials |
|-------------|-----|-------------|
| **User App** | http://localhost:5173 | N/A |
| **Admin Dashboard** | http://localhost:8080 | admin@ecowatch.com / admin123 |
| **User API** | http://localhost:3001 | N/A |
| **Admin API** | http://localhost:3000 | N/A |
| **Prisma Studio** | http://localhost:5555 | Run: `cd backend && npm run prisma:studio` |

---

## 🛠️ Technology Stack

### Frontend

| Tech | Version | Purpose |
|------|---------|---------|
| React | 18.3.1 | UI framework |
| TypeScript | 5.5+ | Type safety |
| Vite | 6.2+ | Build tool |
| TailwindCSS | 3.4+ | Styling |
| shadcn/ui | Latest | UI components |
| React Router | 6.26+ | Routing |
| TanStack Query | 5.56+ | Data fetching |
| Recharts | 2.12+ | Charts |
| Framer Motion | 12.6+ | Animations |

### Backend

| Tech | Version | Purpose |
|------|---------|---------|
| Node.js | 18+ | Runtime |
| Express | 4.18+ | Web framework |
| MongoDB | 8.0+ | Database (User App) |
| PostgreSQL | 14+ | Database (Admin) |
| Prisma | 5.20+ | ORM (Admin) |
| Mongoose | 8.0+ | ODM (User App) |
| JWT | 9.0+ | Authentication |
| bcrypt | 5.1+ | Password hashing |

### Blockchain & AI

- **Hedera Hashgraph** - Blockchain network
- **Hedera Token Service** - ECO token
- **OpenRouter API** - AI gateway
- **DeepSeek v3.1** - Vision AI model

---

## 📖 Setup Instructions

### Environment Variables

#### User App Backend (`backend/.env`)

```env
# Hedera Configuration
HEDERA_NETWORK=testnet
HEDERA_OPERATOR_ID=0.0.YOUR_ACCOUNT_ID
HEDERA_OPERATOR_KEY=YOUR_PRIVATE_KEY
HEDERA_TREASURY_ID=0.0.YOUR_ACCOUNT_ID
HEDERA_TREASURY_KEY=YOUR_PRIVATE_KEY
ECO_TOKEN_ID=0.0.TOKEN_ID

# Database
MONGODB_URI=mongodb://localhost:27017/ecoclean

# Server
PORT=3001
FRONTEND_URL=http://localhost:5173

# AI
OPENROUTER_API_KEY=sk-or-v1-your-key
```

#### User App Frontend (`.env.local`)

```env
VITE_API_URL=http://localhost:3001/api
VITE_OPENROUTER_API_KEY=sk-or-v1-your-key
```

#### Admin Backend (`backend/.env`)

```env
DATABASE_URL="postgresql://user:pass@localhost:5432/ecowatch_db?schema=public"
PORT=3000
NODE_ENV=development
JWT_SECRET=your-secret-key-min-32-chars
JWT_EXPIRES_IN=7d
CORS_ORIGIN=http://localhost:8080
```

#### Admin Frontend (`.env`)

```env
VITE_API_URL=http://localhost:3000/api
```

### Database Setup

**MongoDB (User App):**
```bash
# Ubuntu/Debian
sudo apt install mongodb
sudo systemctl start mongodb

# macOS
brew install mongodb-community
brew services start mongodb-community

# Or use MongoDB Atlas cloud service
```

**PostgreSQL (Admin):**
```bash
# Ubuntu/Debian
sudo apt install postgresql
sudo systemctl start postgresql
sudo -u postgres createdb ecowatch_db

# macOS
brew install postgresql@14
brew services start postgresql@14
createdb ecowatch_db
```

---

## 💻 Development Workflow

### Development Scripts

**User App:**
```bash
cd modules/user-app-bin
npm run dev          # Start frontend
npm run build        # Build for production
npm run typecheck    # Type checking

cd backend
npm run dev          # Start backend (nodemon)
```

**Admin Dashboard:**
```bash
cd modules/admin-dashboear-cibe
npm run dev              # Start frontend
npm run build            # Build for production

cd backend
npm run dev              # Start backend with hot reload
npm run prisma:studio    # Open Prisma Studio (DB GUI)
npm run prisma:migrate   # Run migrations
npm run db:reset         # Reset database
```

### Git Workflow

**Pull latest changes:**
```bash
git pull
git submodule update --remote --merge
```

**Update a submodule:**
```bash
cd modules/user-app-bin
git checkout main
git pull
# Make changes
git add . && git commit -m "Changes" && git push
cd ../..
git add modules/user-app-bin
git commit -m "Update submodule"
git push
```

---

## 🔄 How They Work Together

### Integration Points

1. **Shared Blockchain** - Both apps use same Hedera network and ECO token
2. **Synchronized Reports** - Reports from EcoClean visible in EcoWatch
3. **Status Updates** - Admin status changes affect user app
4. **Reward Distribution** - Tracked in both systems

### Complete Workflow

```
1. Citizen opens EcoClean app
2. Takes photo of overflowing bin
3. GPS captures location
4. AI analyzes image → determines urgency
5. Report submitted to MongoDB
6. Backend checks: First reporter?
7. If YES: Hedera transfers ECO tokens
8. Admin sees report in EcoWatch
9. Admin verifies and assigns team
10. Team cleans and marks complete
11. Bin status updated → allows new reports
```

---

## 🤝 Contributing

### For Parent Repository

```bash
git clone --recurse-submodules git@github.com:enaha76/neuroChainX-Bin-Snap.git
cd neuroChainX-Bin-Snap
git checkout -b feature/my-feature
# Make changes
git commit -m "Add feature"
git push origin feature/my-feature
# Create pull request
```

### For Submodules

```bash
cd modules/user-app-bin  # or admin-dashboear-cibe
git checkout -b feature/my-feature
# Make changes
git commit -m "Add feature"
git push origin feature/my-feature
# Create pull request in submodule repo
```

---

## 📄 License

This project is licensed under the MIT License. See individual submodule LICENSE files for details.

---

## 📞 Support & Documentation

- **User App Docs**: `modules/user-app-bin/README.md`
- **Admin Docs**: `modules/admin-dashboear-cibe/README.md`
- **API Documentation**: See individual README files
- **Architecture Docs**: `modules/user-app-bin/ARCHITECTURE.md`
- **Integration Guide**: `modules/user-app-bin/INTEGRATION_GUIDE.md`

---

## 🙏 Acknowledgments

- **Hedera Hashgraph** - Blockchain infrastructure
- **OpenRouter** - AI API gateway
- **DeepSeek** - Vision AI model
- **shadcn/ui** - UI components
- **TailwindCSS** - Styling framework

---

## 📈 Project Status

🟢 **Active Development** - Hackathon Project

**Version**: 1.0.0  
**Last Updated**: October 2025

---

<div align="center">

### Made with 🌱 for a cleaner planet

**NeuroChainX-Bin-Snap** | Blockchain-Powered Waste Management

</div>