# Development Setup Guide

## Prerequisites

Before you begin, ensure you have installed:

- **Node.js** v18.0.0 or higher
- **npm** v9.0.0 or higher (comes with Node.js)
- **PostgreSQL** v12+ or **MongoDB**
- **Git**
- A code editor (VS Code recommended)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/ndu-napss-e-library/ndu-napss-e-library.git
cd ndu-napss-e-library
```

### 2. Backend Setup

#### Install Dependencies

```bash
cd backend
npm install
```

#### Configure Environment Variables

Create a `.env` file in the `backend` directory:

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=ndu_napss_elib
DB_USER=postgres
DB_PASSWORD=your_password

# JWT Configuration
JWT_SECRET=your_super_secret_jwt_key_change_this
JWT_EXPIRE=7d

# Email Configuration
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
EMAIL_FROM=noreply@ndunapsselib.com

# AWS S3 (Optional - for file uploads)
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
AWS_S3_BUCKET=ndu-napss-elib

# Frontend URL
FRONTEND_URL=http://localhost:3000
```

#### Setup Database

For PostgreSQL:

```bash
# Create database
createdb ndu_napss_elib

# Run migrations
npm run migrate

# Seed demo data (optional)
npm run seed
```

#### Start Backend Server

```bash
npm run dev
```

Backend will run on `http://localhost:5000`

### 3. Frontend Setup

#### Install Dependencies

```bash
cd frontend
npm install
```

#### Configure Environment Variables

Create a `.env` file in the `frontend` directory:

```bash
cp .env.example .env
```

Edit `.env`:

```env
REACT_APP_API_URL=http://localhost:5000/api
REACT_APP_ENV=development
```

#### Start Frontend Server

```bash
npm start
```

Frontend will run on `http://localhost:3000`

## Verify Installation

1. **Backend Health Check**
   ```bash
   curl http://localhost:5000/api/health
   ```
   Expected response: `{ "status": "healthy" }`

2. **Frontend Loads**
   - Open `http://localhost:3000` in your browser
   - You should see the home page

3. **Test Authentication**
   - Navigate to register/login page
   - Create a test account
   - Verify email functionality

## Database Setup Details

### PostgreSQL Setup

```bash
# Install PostgreSQL (macOS with Homebrew)
brew install postgresql@15

# Start PostgreSQL service
brew services start postgresql@15

# Create database and user
psql postgres
CREATE DATABASE ndu_napss_elib;
CREATE USER napss_user WITH PASSWORD 'secure_password';
ALTER ROLE napss_user SET client_encoding TO 'utf8';
ALTER ROLE napss_user SET default_transaction_isolation TO 'read committed';
ALTER ROLE napss_user SET default_transaction_deferrable TO on;
GRANT ALL PRIVILEGES ON DATABASE ndu_napss_elib TO napss_user;
\q
```

### MongoDB Setup (Alternative)

```bash
# Using MongoDB Atlas (Cloud)
# 1. Create account at https://www.mongodb.com/cloud/atlas
# 2. Create cluster
# 3. Get connection string
# 4. Add to .env

MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/ndu_napss_elib
```

## Development Workflow

### Running Both Servers Simultaneously

Option 1: Use two terminal windows
```bash
# Terminal 1 - Backend
cd backend && npm run dev

# Terminal 2 - Frontend
cd frontend && npm start
```

Option 2: Use concurrently
```bash
npm install -g concurrently

# From root directory
npm run dev:all
```

### Code Style & Linting

```bash
# Backend
cd backend
npm run lint
npm run format

# Frontend
cd frontend
npm run lint
npm run format
```

### Running Tests

```bash
# Backend tests
cd backend
npm test

# Frontend tests
cd frontend
npm test
```

## Troubleshooting

### Port Already in Use

```bash
# Find process using port 5000
lsof -i :5000

# Kill process
kill -9 <PID>
```

### Database Connection Error

1. Verify PostgreSQL is running: `psql --version`
2. Check database credentials in `.env`
3. Ensure database exists: `psql -l`

### Email Verification Not Working

1. Check email credentials in `.env`
2. Enable "Less secure app access" for Gmail
3. Use app-specific password for Gmail
4. Check backend logs for email errors

### CORS Errors

Ensure `FRONTEND_URL` in backend `.env` matches your frontend URL.

## Useful Commands

```bash
# Backend
npm run dev          # Start dev server with hot reload
npm run migrate      # Run database migrations
npm run seed         # Seed demo data
npm test             # Run tests
npm run build        # Build for production

# Frontend
npm start            # Start dev server
npm run build        # Create production build
npm test             # Run tests
npm run eject        # Eject from Create React App (irreversible)
```

## Next Steps

1. Read [API Documentation](./API.md)
2. Review [Database Schema](./DATABASE.md)
3. Check [Phases Documentation](./PHASES.md)
4. Start contributing to Phase 1!

## Getting Help

If you encounter issues:
1. Check existing GitHub issues
2. Review error logs in terminal
3. Check database connections
4. Ask in team chat or open a new issue
