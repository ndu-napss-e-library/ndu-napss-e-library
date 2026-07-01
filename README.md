# NDU NAPSS E-Library

**Official Digital Library for the National Association of Political Science Students, Niger Delta University**

A comprehensive digital platform for accessing Political Science educational resources, including textbooks, lecture notes, past questions, journals, and final year projects.

## 🎯 Project Overview

This project is divided into 5 development phases:

### **Phase 1 – User System**
- User Registration & Login (Student & Admin)
- Password Reset functionality
- Email Verification
- Role-based authentication

### **Phase 2 – Digital Library**
- Upload PDF books
- Read books online
- Download books
- Book covers & metadata
- Categories & organization
- Advanced Search (course code, title, author, level)

### **Phase 3 – Political Science Content**
- 100, 200, 300, 400 Level courses
- Lecture notes
- Past questions
- Journals & research papers
- Final year projects

### **Phase 4 – Admin Panel**
- Upload books & lecture notes
- Manage students & courses
- Announcements system
- Analytics & reporting

### **Phase 5 – Polish**
- Dark mode
- Reading progress tracking
- Favourite books
- Notifications
- Advanced PDF viewer
- Book recommendations

## 🗂️ Project Structure

```
ndu-napss-e-library/
├── frontend/                    # React frontend application
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navigation/      # Main navigation menu
│   │   │   ├── Auth/            # Authentication components
│   │   │   ├── Library/         # E-Library components
│   │   │   ├── Books/           # Book reader & viewer
│   │   │   ├── Content/         # Political Science content
│   │   │   ├── Admin/           # Admin panel components
│   │   │   └── Dashboard/       # User & Admin dashboards
│   │   ├── pages/               # Page routes
│   │   ├── styles/              # Global & dark mode styles
│   │   ├── utils/               # Helper functions
│   │   └── App.jsx
│   ├── public/
│   ├── package.json
│   └── .env.example
│
├── backend/                     # Node.js/Express backend
│   ├── src/
│   │   ├── routes/
│   │   │   ├── auth.js         # Authentication endpoints
│   │   │   ├── books.js        # Book management endpoints
│   │   │   ├── courses.js      # Course management endpoints
│   │   │   ├── users.js        # User management endpoints
│   │   │   └── admin.js        # Admin operations endpoints
│   │   ├── models/              # Database schemas
│   │   ├── controllers/         # Business logic
│   │   ├── middleware/          # Auth & validation middleware
│   │   ├── utils/               # Helper functions
│   │   └── server.js
│   ├── config/
│   │   └── database.js
│   ├── uploads/                 # File storage
│   ├── package.json
│   ├── .env.example
│   └── .gitignore
│
├── database/
│   ├── migrations/              # Database migration files
│   └── seeds/                   # Seed data for testing
│
├── docs/
│   ├── API.md                   # API documentation
│   ├── DATABASE.md              # Database schema documentation
│   ├── SETUP.md                 # Development setup guide
│   └── PHASES.md                # Detailed phase descriptions
│
├── .gitignore
└── README.md
```

## 🌐 Navigation Menu Structure

The application includes the following menu items organized as:

**Main Navigation (Public Access):**
- Home
- E-Library
- Courses
- Past Questions
- Journals
- Research Repository
- Announcements
- NAPSS Executives
- About NAPSS
- Contact

**User Navigation (Authenticated Users):**
- Student Portal (for students)
- Admin Portal (for super admins)

## 🛠️ Tech Stack

### Frontend
- **Framework**: React 18+
- **Styling**: Tailwind CSS
- **State Management**: Redux Toolkit
- **PDF Viewer**: React-PDF or similar
- **UI Components**: Shadcn/ui or Material-UI
- **Routing**: React Router v6

### Backend
- **Runtime**: Node.js 18+
- **Framework**: Express.js
- **Database**: PostgreSQL or MongoDB
- **Authentication**: JWT (JSON Web Tokens)
- **Password Hashing**: Bcrypt
- **File Storage**: AWS S3 or local storage
- **Email**: Nodemailer or SendGrid
- **ORM**: Sequelize or Mongoose

### DevOps
- **Version Control**: Git/GitHub
- **Hosting**: Vercel (Frontend), Render/Railway (Backend)
- **CI/CD**: GitHub Actions
- **Database Hosting**: AWS RDS / Supabase

## 🚀 Getting Started

### Prerequisites
- Node.js 16+ and npm/yarn
- PostgreSQL 12+ or MongoDB
- Git

### Installation

#### Clone the repository
```bash
git clone https://github.com/ndu-napss-e-library/ndu-napss-e-library.git
cd ndu-napss-e-library
```

#### Backend Setup
```bash
cd backend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run migrate
npm run dev
```

#### Frontend Setup
```bash
cd frontend
npm install
cp .env.example .env
# Edit .env with your API endpoint (http://localhost:5000)
npm start
```

For detailed setup instructions, see [SETUP.md](docs/SETUP.md)

## 📚 Documentation

- **[API Documentation](docs/API.md)** - REST API endpoints and usage
- **[Database Schema](docs/DATABASE.md)** - Database models and relationships
- **[Development Setup](docs/SETUP.md)** - Step-by-step setup guide
- **[Phase Details](docs/PHASES.md)** - Detailed breakdown of each development phase

## 👥 User Roles

1. **Student** - Access e-library, view courses, download materials, track reading progress
2. **Super Admin** - Manage users, upload content, view analytics, manage courses
3. **Guest** - Limited access to public content (Home, About, Contact)

## 🔐 Security Features

- Password hashing with bcrypt
- JWT-based authentication with refresh tokens
- Email verification for account creation
- Role-based access control (RBAC)
- Rate limiting on API endpoints
- CSRF protection
- Secure file upload validation
- Input sanitization & validation

## 📊 Features Status

- [x] Database & schema design
- [x] Project structure setup
- [x] Navigation menu planning
- [ ] Phase 1: User System
- [ ] Phase 2: Digital Library
- [ ] Phase 3: Political Science Content
- [ ] Phase 4: Admin Panel
- [ ] Phase 5: Polish & Enhancement

## 🤝 Contributing

1. Create a feature branch (`git checkout -b feature/amazing-feature`)
2. Commit your changes (`git commit -m 'Add amazing feature'`)
3. Push to the branch (`git push origin feature/amazing-feature`)
4. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📧 Contact

For inquiries or support, contact the NDU NAPSS E-Library team.

---

**Project Status**: Phase 1 - User System Setup
**Last Updated**: July 1, 2026
**Maintained by**: NDU NAPSS Development Team
