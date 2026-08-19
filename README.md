# AI-Powered Verified Digital Proof Vault

A production-ready **AI-Powered Verified Digital Proof Vault** designed to securely store bills, receipts, invoices, warranty cards, and insurance policies while executing multi-vector **invoice authenticity analysis** (Authenticity Confidence Score 0–100%).

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Node](https://img.shields.io/badge/Node.js-18.x-green.svg)
![React](https://img.shields.io/badge/React-18.x-indigo.svg)
![Docker](https://img.shields.io/badge/Docker-Ready-cyan.svg)

---

## 🌟 Core Highlights

- **Multi-Factor Authenticity Engine (0–100%)**: Evaluates document validity across 7 verification vectors:
  1. **GST Format & Checksum Verification** (Indian GSTIN regex & Mod-36 checksum calculation)
  2. **QR Code Payload Cross-Matching** (Decodes embedded invoice QR code and cross-references against printed text)
  3. **File Metadata & EXIF Analysis** (Detects Adobe Photoshop, PDF editors, Canva, and file creation date vs modification date gaps)
  4. **Vault Duplicate Detection** (Prevents duplicate uploads matching invoice number, order ID, seller, and amount)
  5. **Physical Hardware Identifier Verification** (Matches invoice Serial Numbers / IMEIs with registered physical user devices)
  6. **Merchant & Seller Entity Verification**
  7. **Typography & Layout Consistency Check**
- **AI OCR & Classification Engine**: Extracts 14+ invoice fields automatically using Tesseract OCR, PDF Parser, and Google Gemini API (with zero-config heuristic NLP fallback).
- **Conversational Natural Language Search**: Query like `"Show my laptop bill from 2026"` or `"Insurance expiring this month"`.
- **Warranty Reminder System**: Automated background cron notifications at 30, 15, 7, and 1 day before document expiration.
- **Admin Control Panel**: View system health metrics, storage allocation, user accounts, and suspicious fraud reports.
- **DevOps & CI/CD**: Fully Dockerized with Nginx reverse proxy and a 12-stage Jenkins pipeline.

---

## 🛠 Tech Stack

### Frontend
- **Framework**: React.js (Vite) + React Router v6
- **Styling**: Tailwind CSS (Glassmorphism dark theme `#0B0F19`)
- **Animations**: Framer Motion
- **Charts**: Chart.js / `react-chartjs-2`
- **Icons**: Lucide React
- **HTTP Client**: Axios

### Backend
- **Runtime**: Node.js & Express.js
- **Database**: MongoDB (Mongoose ORM with automatic `mongodb-memory-server` out-of-the-box fallback)
- **AI & OCR**: `@google/genai` (Google Gemini API), Tesseract.js, pdf-parse, jsQR, sharp, exif-parser
- **Auth**: JWT & BcryptJS
- **Scheduler**: `node-cron` & Nodemailer

### DevOps
- Docker & Docker Compose
- Nginx (Reverse Proxy)
- Jenkins (12-stage CI/CD Pipeline)

---

## 📁 Folder Structure

```
verified-digital-proof-vault/
├── client/                     # React + Vite + Tailwind CSS Frontend
│   ├── src/
│   │   ├── components/         # Glassmorphic Navbar, Sidebar, RiskBadge, ScoreGauge
│   │   ├── context/            # AuthContext
│   │   ├── pages/              # Landing, Dashboard, Upload, DocumentDetails, Search, Devices, Admin
│   │   ├── services/           # Axios API Client
│   │   └── index.css           # Glassmorphism & custom utility classes
│   ├── Dockerfile
│   └── package.json
├── server/                     # Node.js + Express API Backend
│   ├── src/
│   │   ├── config/             # DB & Env configuration
│   │   ├── controllers/        # Auth, Document, Authenticity, Search, Device, Admin controllers
│   │   ├── models/             # User, Document, AuthenticityReport, Device, Notification, AuditLog
│   │   ├── services/           # OCR, AI Service, GST Validator, Metadata Analyzer, QR Service, Authenticity Engine
│   │   └── app.js              # Main Express Application entrypoint
│   ├── seed.js                 # Realistic demo data seeding script
│   ├── Dockerfile
│   └── package.json
├── nginx/
│   └── default.conf            # Nginx Reverse Proxy Configuration
├── docker-compose.yml          # Full-Stack Container Orchestration
├── Jenkinsfile                 # 12-Stage CI/CD Pipeline Script
└── README.md                   # Project Documentation
```

---

## 🚀 Quick Start (Local Development)

### 1. Clone & Install Dependencies

```bash
# Navigate into server and install packages
cd server
npm install

# Seed demo data (Users, Documents, Authenticity Reports, Devices)
npm run seed

# Start Express Backend API (Port 5000)
npm run dev
```

In a new terminal window:

```bash
# Navigate into client and install packages
cd client
npm install

# Start React Vite Client (Port 3000)
npm run dev
```

Open your browser at `http://localhost:3000`.

### 🔑 Demo Login Credentials
- **Demo User**: `user@proofvault.io` / `userpassword123`
- **Admin User**: `admin@proofvault.io` / `adminpassword123`

---

## 🐳 Docker Deployment

To launch the complete application stack (MongoDB + Express Backend + Nginx React Frontend):

```bash
docker compose up --build -d
```

Access the application at `http://localhost`.

---

## ⚙️ 12-Stage Jenkins CI/CD Pipeline

The included `Jenkinsfile` executes:
1. **Pull GitHub Repository**
2. **Install Dependencies**
3. **Run ESLint Syntax Validation**
4. **Execute Unit Tests**
5. **Build React Application**
6. **Build Backend API**
7. **Build Docker Images**
8. **Push Docker Images**
9. **Deploy Automatically via Docker Compose**
10. **Restart Containers**
11. **Health Check Verification (`/api/health`)**
12. **Deployment Notification**

---

## ⚠️ Important Security Disclaimer

This platform performs **risk-based authenticity analysis** using algorithmic OCR extraction, GST format logic, QR payload inspection, EXIF metadata analysis, duplicate scanning, and physical serial matching. It does **not** guarantee that an invoice is genuine in legal terms; rather, it outputs an **Authenticity Confidence Score** with itemized reasons to flag suspicious modifications or high-risk uploads.

---

## 📄 License

This project is licensed under the MIT License.
