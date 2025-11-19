# MicroBiz Inventory & Sales Tracker

A modern, full-stack inventory and sales management system designed for small businesses and multi-branch stores with offline-first capabilities and real-time synchronization.

## 📋 Table of Contents

- Overview
- Features
- Tech Stack
- Project Structure
- Getting Started
- Installation
- Configuration
- Running the Application
- API Documentation
- Database Schema
- Usage Guide
- Development
- Deployment
- Contributing
- License

---

## Overview

**MicroBiz** is a comprehensive inventory management and point-of-sale (POS) solution tailored for small retail businesses, kiosks, and multi-store operations. It provides real-time inventory tracking, sales recording, revenue analytics, and low-stock alerts—all with a clean, modern interface and graceful offline functionality.

### Key Highlights

- 🏪 **Multi-Store Support**: Manage single or multiple store locations from one dashboard
- 📊 **Real-Time Analytics**: View sales trends, revenue summaries, and inventory health at a glance
- 🔔 **Inventory Alerts**: Automatic notifications for low-stock items
- 📱 **Responsive Design**: Seamless experience across desktop and mobile devices
- 🔐 **Secure Authentication**: JWT-based user authentication with password hashing
- 🌐 **Offline-Ready**: Built to handle intermittent connectivity gracefully
- ⚡ **Fast & Modern**: React 18, Express.js, MongoDB with optimized queries

---

## Features

### Core Functionality

#### **Dashboard**
- Quick overview of total sales, revenue, product count, and low-stock items
- Recent sales activity feed
- Sales trend visualization (7-day rolling average)
- Key performance indicators (KPIs) at a glance

#### **Inventory Management**
- Add, edit, and archive products
- Track product SKU, category, quantity, and unit price
- Set low-stock thresholds and receive alerts
- Bulk operations and search/filter capabilities

#### **Sales Recording**
- Quick sale entry with product selection
- Quantity and price validation
- Automatic inventory deduction
- Payment method tracking (cash, card, etc.)
- Sales history with detailed timestamps

#### **Reports & Analytics**
- Sales summary (revenue, count, trends)
- Product performance metrics
- Low-stock and reorder recommendations
- Extensible reporting framework for future enhancements
- Export-ready data structures

#### **User Management**
- User registration and login
- Profile management
- Business/store information
- Role-based access (foundation for future enhancements)
- Secure JWT token authentication

---

## Tech Stack

### **Frontend**
| Technology | Purpose |
|------------|---------|
| **React 18** | UI framework with hooks and context API |
| **React Router v6** | Client-side routing and navigation |
| **Axios** | HTTP client with request/response interceptors |
| **Vite** | Build tool and dev server (blazing fast) |
| **Tailwind CSS** | Utility-first styling |

### **Backend**
| Technology | Purpose |
|------------|---------|
| **Node.js & Express.js** | Server runtime and web framework |
| **MongoDB & Mongoose** | NoSQL database with schema validation |
| **JWT (jsonwebtoken)** | Stateless authentication |
| **bcryptjs** | Password hashing and comparison |
| **CORS** | Cross-origin resource sharing |
| **dotenv** | Environment variable management |

### **Development Tools**
| Tool | Purpose |
|------|---------|
| **Nodemon** | Auto-restart server on file changes |
| **Vite** | Lightning-fast HMR development |
| **ESLint** (optional) | Code linting |

---

## Project Structure

```
microbiz-inventory/
│
├── Client/                          # React frontend application
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── auth/                # LoginForm, RegisterForm, AuthLayout
│   │   │   ├── common/              # Button, Input, Loader, MetricCard
│   │   │   ├── layout/              # Sidebar, TopBar, Layout, OfflineBanner
│   │   │   ├── products/            # ProductForm, ProductTable
│   │   │   └── sales/               # SaleForm, SalesTable
│   │   ├── context/
│   │   │   └── ToastContext.jsx     # Global toast notifications
│   │   ├── hooks/
│   │   │   ├── useAuth.jsx          # Authentication context and logic
│   │   │   └── useOnlineStatus.js   # Online/offline detection
│   │   ├── pages/
│   │   │   ├── DashboardPage.jsx    # Main dashboard
│   │   │   ├── ProductsPage.jsx     # Inventory management
│   │   │   ├── SalesPage.jsx        # Sales history
│   │   │   ├── ReportsPage.jsx      # Analytics & reports
│   │   │   ├── SettingsPage.jsx     # User settings
│   │   │   ├── LoginPage.jsx        # Login page
│   │   │   └── RegisterPage.jsx     # Registration page
│   │   ├── services/
│   │   │   ├── apiClient.js         # Configured axios instance
│   │   │   └── reportService.js     # Report API service
│   │   ├── utils/
│   │   │   └── currency.js          # Currency formatting utilities
│   │   ├── api/
│   │   │   └── axios.js             # Alternative axios setup
│   │   ├── App.jsx                  # Main app component with routes
│   │   ├── main.jsx                 # React DOM entry point
│   │   └── index.css                # Global styles and design system
│   ├── index.html                   # HTML entry point
│   ├── vite.config.js               # Vite configuration
│   ├── package.json                 # Dependencies and scripts
│   ├── .env                         # Local environment variables
│   └── .env.example                 # Environment template
│
├── Server/                          # Express.js backend application
│   ├── src/
│   │   ├── config/
│   │   │   └── db.js                # MongoDB connection setup
│   │   ├── controllers/
│   │   │   ├── authController.js    # Auth logic (register, login, getMe)
│   │   │   ├── productController.js # Product CRUD operations
│   │   │   ├── saleController.js    # Sale CRUD operations
│   │   │   ├── metricsController.js # Dashboard metrics aggregation
│   │   │   ├── reportController.js  # Report data generation
│   │   │   └── storeController.js   # Store management (multi-store)
│   │   ├── middleware/
│   │   │   ├── authMiddleware.js    # JWT verification (Bearer token)
│   │   │   ├── auth.js              # Alternative auth (cookie + header)
│   │   │   ├── logger.js            # Request logging middleware
│   │   │   └── errorHandler.js      # Error handling middleware
│   │   ├── models/
│   │   │   ├── User.js              # User schema with password hashing
│   │   │   ├── Product.js           # Product schema with inventory tracking
│   │   │   ├── Sale.js              # Sale schema with transaction details
│   │   │   └── Store.js             # Store schema (multi-store support)
│   │   ├── routes/
│   │   │   ├── authRoutes.js        # /api/auth endpoints
│   │   │   ├── productRoutes.js     # /api/products endpoints
│   │   │   ├── saleRoutes.js        # /api/sales endpoints
│   │   │   ├── metricsRoutes.js     # /api/metrics endpoints
│   │   │   ├── reportRoutes.js      # /api/reports endpoints
│   │   │   └── storeRoutes.js       # /api/stores endpoints
│   │   ├── scripts/
│   │   │   └── seedDemoData.js      # Demo data seeding script
│   │   ├── utils/
│   │   │   └── generateToken.js     # JWT token generation utility
│   │   └── server.js                # Express app initialization and routes
│   ├── package.json                 # Dependencies and scripts
│   ├── .env                         # Local environment variables
│   └── .env.example                 # Environment template
│
└── README.md                        # This file
```

---

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v16 or higher) – [Download](https://nodejs.org/)
- **MongoDB** – [Community Edition](https://www.mongodb.com/try/download/community) or [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) (cloud)
- **npm** or **yarn** – Comes with Node.js
- **Git** – [Download](https://git-scm.com/)

### Quick Start (5 minutes)

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/microbiz-inventory.git
cd microbiz-inventory

# 2. Setup Backend
cd Server
cp .env.example .env
# Edit .env with your MongoDB URI and JWT secret
npm install
npm run dev

# 3. Setup Frontend (in a new terminal)
cd Client
cp .env.example .env
# Verify VITE_API_URL points to http://localhost:4000/api
npm install
npm run dev

# 4. Open in browser
# Navigate to http://localhost:5173
# Login with test@example.com / password (or register a new account)
```

---

## Installation

### Backend Setup

#### Step 1: Navigate to Server Directory

```bash
cd Server
```

#### Step 2: Install Dependencies

```bash
npm install
```

This will install all required packages listed in `Server/package.json`:
- `express` – Web framework
- `mongoose` – MongoDB ODM
- `jsonwebtoken` – JWT authentication
- `bcryptjs` – Password hashing
- `cors` – Cross-origin requests
- `dotenv` – Environment variables
- `nodemon` – Development auto-reload

#### Step 3: Create Environment File

```bash
cp .env.example .env
```

Then edit `Server/.env` with your configuration (see Configuration).

### Frontend Setup

#### Step 1: Navigate to Client Directory

```bash
cd Client
```

#### Step 2: Install Dependencies

```bash
npm install
```

This will install all required packages listed in `Client/package.json`:
- `react` – UI framework
- `react-router-dom` – Routing
- `axios` – HTTP client
- `@vitejs/plugin-react` – Vite React plugin

#### Step 3: Create Environment File

```bash
cp .env.example .env
```

Verify the `Client/.env` file has the correct API URL.

---

## Configuration

### Backend Configuration (.env)

Create or update `Server/.env` with the following variables:

```bash
# Server Port
PORT=4000

# MongoDB Connection URI
# For local MongoDB:
# MONGO_URI=mongodb://localhost:27017/microbiz
# For MongoDB Atlas (cloud):
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/microbiz?retryWrites=true&w=majority

# JWT Secret for token signing (use a strong, random string)
JWT_SECRET=your_super_secret_jwt_key_here_change_in_production

# CORS Origin (frontend URL)
CORS_ORIGIN=http://localhost:5173
```

### Frontend Configuration (.env)

Create or update `Client/.env` with:

```bash
# Backend API Base URL
VITE_API_URL=http://localhost:4000/api
```

### MongoDB Atlas Setup (Optional)

If using MongoDB Atlas:

1. Go to [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free cluster
3. Add a database user with username and password
4. Whitelist your IP address
5. Copy the connection string and paste into `Server/.env` as `MONGO_URI`

---

## Running the Application

### Development Mode

#### Terminal 1: Start Backend

```bash
cd Server
npm run dev
```

Expected output:
```
🚀 Server running on http://localhost:4000
✅ MongoDB connected: localhost
```

#### Terminal 2: Start Frontend

```bash
cd Client
npm run dev
```

Expected output:
```
VITE v6.0.1  ready in 123 ms

➜  Local:   http://localhost:5173/
➜  press h + enter to show help
```

#### Terminal 3 (Optional): Seed Demo Data

```bash
cd Server
npm run seed
```

This will:
- Create demo products (rice, oil, soft drinks, noodles, soap)
- Create demo sales for the last 7 days
- Populate the database for testing

### Production Build

#### Build Frontend

```bash
cd Client
npm run build
```

Output: `Client/dist/` directory ready for deployment.

#### Start Backend (Production)

```bash
cd Server
npm start
```

---

## API Documentation

### Authentication Endpoints

#### **POST /api/auth/register**
Register a new user account.

**Request:**
```json
{
  "name": "John Doe",
  "email": "john@store.com",
  "password": "securePassword123",
  "businessName": "John's Store"
}
```

**Response (201):**
```json
{
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "name": "John Doe",
    "email": "john@store.com",
    "businessName": "John's Store",
    "defaultStore": "Main Store"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

---

#### **POST /api/auth/login**
Authenticate and receive a JWT token.

**Request:**
```json
{
  "email": "john@store.com",
  "password": "securePassword123"
}
```

**Response (200):**
```json
{
  "user": { /* user object */ },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Headers (All Protected Routes):**
```
Authorization: Bearer {token}
```

---

#### **GET /api/auth/me**
Get current authenticated user.

**Response (200):**
```json
{
  "user": {
    "_id": "507f1f77bcf86cd799439011",
    "name": "John Doe",
    "email": "john@store.com",
    "businessName": "John's Store",
    "defaultStore": "Main Store"
  }
}
```

---

### Product Endpoints

#### **GET /api/products**
Retrieve all products for the authenticated user.

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439012",
      "name": "Premium Rice (50kg)",
      "sku": "RICE-50",
      "category": "Grains",
      "quantity": 40,
      "unitPrice": 32000,
      "lowStockThreshold": 5,
      "owner": "507f1f77bcf86cd799439011",
      "createdAt": "2024-01-15T10:30:00Z"
    }
  ]
}
```

---

#### **POST /api/products**
Create a new product.

**Request:**
```json
{
  "name": "Product Name",
  "sku": "SKU-001",
  "category": "Category",
  "quantity": 100,
  "unitPrice": 5000
}
```

**Response (201):**
```json
{
  "success": true,
  "data": { /* product object */ }
}
```

---

### Sales Endpoints

#### **GET /api/sales**
Retrieve all sales for the authenticated user (last 100).

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439013",
      "product": "507f1f77bcf86cd799439012",
      "productName": "Premium Rice (50kg)",
      "quantity": 2,
      "unitPrice": 32000,
      "totalAmount": 64000,
      "date": "2024-01-15T14:30:00Z",
      "paymentMethod": "cash",
      "owner": "507f1f77bcf86cd799439011"
    }
  ]
}
```

---

#### **POST /api/sales**
Record a new sale.

**Request:**
```json
{
  "productId": "507f1f77bcf86cd799439012",
  "quantity": 2,
  "unitPrice": 32000,
  "date": "2024-01-15T14:30:00Z"
}
```

**Response (201):**
```json
{
  "success": true,
  "data": { /* sale object */ }
}
```

---

### Metrics Endpoint

#### **GET /api/metrics/overview**
Get dashboard metrics and key performance indicators.

**Response (200):**
```json
{
  "totals": {
    "totalSalesAmount": 450000,
    "totalSalesCount": 15,
    "productCount": 5,
    "lowStockCount": 2
  },
  "recentSales": [
    {
      "id": "507f1f77bcf86cd799439013",
      "productName": "Premium Rice (50kg)",
      "quantity": 2,
      "totalAmount": 64000,
      "date": "2024-01-15T14:30:00Z"
    }
  ],
  "salesTrend": [
    { "date": "01-09", "totalAmount": 120000 },
    { "date": "01-10", "totalAmount": 95000 },
    /* ... last 7 days ... */
  ]
}
```

---

### Reports Endpoint

#### **GET /api/reports/summary**
Get a basic reports summary.

**Response (200):**
```json
{
  "totalSalesCount": 15,
  "totalProductsCount": 5,
  "message": "Basic reports summary. Extend this later with more detailed analytics."
}
```

---

## Database Schema

### User Model

```javascript
{
  _id: ObjectId,
  name: String (required),
  email: String (required, unique),
  passwordHash: String (required, bcrypted),
  businessName: String,
  defaultStore: String,
  createdAt: Date,
  updatedAt: Date
}
```

**Methods:**
- `matchPassword(plainPassword)` – Compare plain password with hash

---

### Product Model

```javascript
{
  _id: ObjectId,
  owner: ObjectId (ref: User),
  store: ObjectId (ref: Store, optional),
  name: String (required),
  sku: String,
  category: String,
  quantity: Number (default: 0, min: 0),
  unitPrice: Number (default: 0, min: 0),
  lowStockThreshold: Number (default: 5),
  isArchived: Boolean (default: false),
  createdAt: Date,
  updatedAt: Date
}
```

---

### Sale Model

```javascript
{
  _id: ObjectId,
  owner: ObjectId (ref: User),
  store: ObjectId (ref: Store, optional),
  product: ObjectId (ref: Product, optional),
  productName: String (required),
  quantity: Number (required, min: 1),
  unitPrice: Number (required, min: 0),
  totalAmount: Number (required, min: 0),
  date: Date (default: now),
  paymentMethod: String (default: "cash"),
  createdAt: Date,
  updatedAt: Date
}
```

---

### Store Model

```javascript
{
  _id: ObjectId,
  name: String (required),
  owner: ObjectId (ref: User, required),
  type: String (enum: ["single", "multi"], default: "single"),
  currency: String (default: "NGN"),
  isDefault: Boolean (default: false),
  createdAt: Date,
  updatedAt: Date
}
```

---

## Usage Guide

### First-Time Setup

1. **Register Account**
   - Go to http://localhost:5173/register
   - Enter your name, email, and password
   - Click "Create MicroBiz workspace"

2. **Add Products**
   - Navigate to **Products** page
   - Fill in product details (name, SKU, category, quantity, price)
   - Click **Add**

3. **Record Sales**
   - Go to **Sales** page
   - Select a product from the dropdown
   - Enter quantity and confirm
   - Transaction is recorded and inventory is updated

4. **View Dashboard**
   - **Dashboard** page shows:
     - Total revenue
     - Total sales count
     - Product inventory count
     - Low-stock alerts
     - Recent sales activity
     - 7-day sales trend

5. **Generate Reports**
   - **Reports** page displays:
     - Total sales by category (expandable)
     - Profit/loss summaries
     - Low-stock recommendations

### Demo Data

To populate with demo data:

```bash
cd Server
npm run seed
```

Then login with:
- **Email**: `test@example.com`
- **Password**: You'll need to register first, or update the seed script

---

## Development

### Project Commands

#### **Backend**

```bash
# Start development server (auto-reload)
npm run dev

# Start production server
npm start

# Seed demo data
npm run seed
```

#### **Frontend**

```bash
# Start development server with HMR
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### Code Style & Best Practices

- **Components**: Functional components with hooks
- **State Management**: React Context API for auth and toasts
- **API Calls**: Axios with interceptors for token injection
- **Error Handling**: Try-catch blocks with user-friendly toast messages
- **Validation**: Client-side form validation + server-side schema validation

### Extending the Application

#### Adding a New Feature (e.g., Discount System)

1. **Backend**:
   - Add fields to Product/Sale schema in `Server/src/models`
   - Create controller methods in `Server/src/controllers`
   - Add routes in `Server/src/routes`

2. **Frontend**:
   - Create component in `Client/src/components`
   - Add API service method in `Client/src/services/apiClient.js`
   - Create page/hook in `Client/src/pages` or `Client/src/hooks`
   - Add route in `Client/src/App.jsx`

3. **Testing**:
   - Test API with Postman or curl
   - Test UI in browser with React DevTools

---

## Deployment

### Deploying to Heroku/Railway/Render

#### Backend

1. **Prepare for Production**
   ```bash
   cd Server
   npm install
   ```

2. **Set Environment Variables** on your hosting platform:
   ```
   PORT=4000
   MONGO_URI=<your-mongodb-atlas-uri>
   JWT_SECRET=<strong-random-secret>
   CORS_ORIGIN=<your-frontend-url>
   ```

3. **Deploy** using your platform's CLI or Git integration

#### Frontend

1. **Build**
   ```bash
   cd Client
   npm run build
   ```

2. **Deploy** the `dist/` folder to Vercel, Netlify, or your static hosting

3. **Update Environment**:
   ```
   VITE_API_URL=<your-backend-url>/api
   ```

---

## Contributing

Contributions are welcome! Here's how:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Reporting Issues

Please use the [GitHub Issues](https://github.com/yourusername/microbiz-inventory/issues) tab to report bugs with:
- Clear description
- Steps to reproduce
- Expected vs. actual behavior
- Screenshots/logs if applicable

---

## License

This project is licensed under the **MIT License** – see the LICENSE file for details.

---

## Support & Contact

- 📧 **Email**: support@microbiz.app
- 💬 **Discord**: [Join Community](https://discord.gg/microbiz)
- 📖 **Docs**: [Full Documentation](https://docs.microbiz.app)
- 🐛 **Issues**: [GitHub Issues](https://github.com/yourusername/microbiz-inventory/issues)

---

## Acknowledgments

- **MongoDB** for robust NoSQL database
- **Express.js** for lightweight web framework
- **React** for reactive UI
- **Vite** for blazing-fast build tooling
- **Tailwind CSS** for utility-first styling

---

## Roadmap

### Phase 2 (Q2 2025)
- [ ] Multi-user roles (Manager, Cashier, Admin)
- [ ] Barcode scanning
- [ ] Supplier management
- [ ] Purchase orders

### Phase 3 (Q3 2025)
- [ ] Mobile app (React Native)
- [ ] Advanced reporting & exports
- [ ] Accounting integration
- [ ] SMS/Email notifications

### Phase 4 (Q4 2025)
- [ ] AI-powered demand forecasting
- [ ] Automated reordering
- [ ] Multi-currency support
- [ ] API for third-party integrations

---

**Made with ❤️ for small business owners worldwide.**

Last Updated: **November 2025**  
Version: **1.0.0**
