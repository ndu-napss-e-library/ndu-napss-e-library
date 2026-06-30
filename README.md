# NDU NAPSS E-Library 📚

Official Digital Library for the National Association of Political Science Students, Niger Delta University.

## 🎯 Project Overview

A comprehensive digital library platform designed specifically for Political Science students at NDU. It provides easy access to:
- Course materials organized by academic level (100-400)
- Books and lecture notes
- Past examination questions
- Research papers and journals
- NAPSS official documents
- Leadership resources

## 🛠 Tech Stack

### Frontend
- **React** 18.x - UI library
- **Tailwind CSS** - Styling
- **React Router** - Navigation
- **Axios** - API client
- **React Query** - Data fetching
- **Framer Motion** - Animations

### Backend
- **Node.js** 18.x - Runtime
- **Express.js** 4.x - Web framework
- **PostgreSQL** - Database
- **Sequelize** - ORM
- **JWT** - Authentication
- **Bcrypt** - Password hashing
- **Multer** - File uploads
- **Nodemailer** - Email verification

### DevOps
- **Frontend Deployment** - Vercel
- **Backend Deployment** - Render
- **Database** - PostgreSQL (Cloud provider)

## 🎨 Design Theme

- **Primary Color**: Royal Blue (#4169E1)
- **Secondary Color**: Sky Blue (#87CEEB)
- **Background**: White (#FFFFFF)
- **NAPSS Logo**: Integrated throughout

## 📁 Project Structure

```
ndu-napss-e-library/
├── frontend/                 # React application
│   ├── src/
│   │   ├── components/      # Reusable components
│   │   ├── pages/           # Page components
│   │   ├── services/        # API services
│   │   ├── hooks/           # Custom hooks
│   │   ├── context/         # React context
│   │   ├── styles/          # Tailwind config
│   │   └── App.jsx
│   ├── package.json
│   └── .env.example
│
├── backend/                  # Express API
│   ├── src/
│   │   ├── routes/          # API routes
│   │   ├── controllers/     # Request handlers
│   │   ├── models/          # Database models
│   │   ├── middleware/      # Auth, validation
│   │   ├── services/        # Business logic
│   │   ├── utils/           # Utilities
│   │   ├── config/          # Configuration
│   │   └── server.js
│   ├── uploads/             # File storage
│   ├── package.json
│   └── .env.example
│
└── database/                # Database setup
    ├── migrations/          # Schema migrations
    └── seeders/            # Demo data
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18.x
- PostgreSQL 12.x
- npm or yarn

### Frontend Setup
```bash
cd frontend
npm install
npm start
```

### Backend Setup
```bash
cd backend
npm install
npm run migrate
npm start
```

## 📚 Features

### User Roles
- **Students** - Browse, search, download materials
- **Administrators** - Upload, manage, analytics
- **Super Admin** - Full system control

### Core Features
- ✅ User authentication (JWT)
- ✅ Book/material search and filtering
- ✅ Online reading capability
- ✅ PDF downloads
- ✅ Bookmarking system
- ✅ User dashboard
- ✅ Admin panel
- ✅ Email notifications
- ✅ Download analytics
- ✅ Responsive design

## 🔐 Security

- JWT token-based authentication
- Bcrypt password hashing
- Email verification
- Role-based access control (RBAC)
- Protected file uploads
- Input validation & sanitization
- CORS configuration
- Rate limiting

## 📱 Responsive Design

Fully optimized for:
- Desktop (1920px+)
- Tablet (768px - 1024px)
- Mobile (320px - 767px)
  - iOS devices
  - Android devices

## 🌐 Deployment

### Frontend (Vercel)
```bash
npm run build
vercel deploy
```

### Backend (Render)
- Connect GitHub repository
- Set environment variables
- Deploy with auto-restart on git push

### Database (PostgreSQL)
- Cloud hosted on AWS RDS, Heroku, or Supabase

## 📖 Documentation

- [Frontend Setup Guide](./frontend/README.md)
- [Backend Setup Guide](./backend/README.md)
- [API Documentation](./backend/API.md)
- [Database Schema](./database/SCHEMA.md)

## 👥 Team

NDU NAPSS E-Library Development Team

## 📄 License

MIT License - See LICENSE file for details

## 🤝 Contributing

We welcome contributions! Please follow the contributing guidelines.

## 📞 Support

For issues or questions, please open an issue on GitHub.

---

**Made with ❤️ for NDU NAPSS**
