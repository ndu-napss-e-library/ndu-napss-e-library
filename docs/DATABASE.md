# Database Schema Documentation

## Overview

The NDU NAPSS E-Library uses PostgreSQL as the primary database. This document outlines all database tables, relationships, and schemas.

## Entity Relationship Diagram

```
Users
  ├── StudentProfiles
  ├── Favourites
  ├── Downloads
  ├── Reviews
  └── ReadingProgress

Books
  ├── Categories
  ├── Reviews
  ├── Downloads
  └── ReadingProgress

Courses
  ├── CourseBooks
  ├── LectureNotes
  ├── PastQuestions
  └── Journals

Content
  ├── LectureNotes
  ├── PastQuestions
  ├── Journals
  └── Projects
```

## Tables

### 1. Users Table

Stores user account information.

```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  firstName VARCHAR(50) NOT NULL,
  lastName VARCHAR(50) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  role ENUM('student', 'admin', 'superadmin') DEFAULT 'student',
  profilePicture VARCHAR(255),
  phoneNumber VARCHAR(20),
  isEmailVerified BOOLEAN DEFAULT FALSE,
  emailVerificationToken VARCHAR(255),
  emailVerificationExpires TIMESTAMP,
  passwordResetToken VARCHAR(255),
  passwordResetExpires TIMESTAMP,
  lastLogin TIMESTAMP,
  status ENUM('active', 'inactive', 'suspended') DEFAULT 'active',
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  deletedAt TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role ON users(role);
```

### 2. StudentProfiles Table

Extended student information.

```sql
CREATE TABLE student_profiles (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  userId UUID NOT NULL UNIQUE,
  matNumber VARCHAR(20) UNIQUE NOT NULL,
  level ENUM('100', '200', '300', '400') NOT NULL,
  departmentId UUID,
  gpa DECIMAL(3, 2),
  enrollmentDate DATE,
  expectedGraduationDate DATE,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (userId) REFERENCES users(id) ON DELETE CASCADE
);

CREATE INDEX idx_student_profiles_matNumber ON student_profiles(matNumber);
```

### 3. Categories Table

Book and content categories.

```sql
CREATE TABLE categories (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(100) NOT NULL UNIQUE,
  slug VARCHAR(100) UNIQUE,
  description TEXT,
  icon VARCHAR(255),
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 4. Books Table

Main books collection.

```sql
CREATE TABLE books (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  author VARCHAR(255) NOT NULL,
  description TEXT,
  coverImage VARCHAR(255),
  filePath VARCHAR(255) NOT NULL,
  fileName VARCHAR(255),
  fileSize BIGINT,
  fileType VARCHAR(20) DEFAULT 'pdf',
  categoryId UUID,
  courseCode VARCHAR(20),
  level ENUM('100', '200', '300', '400'),
  isbn VARCHAR(20),
  publisher VARCHAR(255),
  publicationYear INT,
  pageCount INT,
  language VARCHAR(20) DEFAULT 'en',
  uploadedBy UUID NOT NULL,
  totalDownloads INT DEFAULT 0,
  avgRating DECIMAL(2, 1) DEFAULT 0,
  reviewCount INT DEFAULT 0,
  status ENUM('draft', 'published', 'archived') DEFAULT 'published',
  isActive BOOLEAN DEFAULT TRUE,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  deletedAt TIMESTAMP,
  FOREIGN KEY (categoryId) REFERENCES categories(id),
  FOREIGN KEY (uploadedBy) REFERENCES users(id)
);

CREATE INDEX idx_books_title ON books(title);
CREATE INDEX idx_books_author ON books(author);
CREATE INDEX idx_books_courseCode ON books(courseCode);
CREATE INDEX idx_books_level ON books(level);
CREATE INDEX idx_books_category ON books(categoryId);
```

### 5. Courses Table

Academic courses.

```sql
CREATE TABLE courses (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  code VARCHAR(20) UNIQUE NOT NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  level ENUM('100', '200', '300', '400') NOT NULL,
  unit INT DEFAULT 3,
  lecturer VARCHAR(255),
  prerequisiteCourses VARCHAR(255),
  semester VARCHAR(20),
  isActive BOOLEAN DEFAULT TRUE,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (lecturer) REFERENCES users(id)
);

CREATE INDEX idx_courses_code ON courses(code);
CREATE INDEX idx_courses_level ON courses(level);
```

### 6. CourseBooks Junction Table

Links books to courses.

```sql
CREATE TABLE course_books (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  courseId UUID NOT NULL,
  bookId UUID NOT NULL,
  isPrimary BOOLEAN DEFAULT FALSE,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (courseId) REFERENCES courses(id) ON DELETE CASCADE,
  FOREIGN KEY (bookId) REFERENCES books(id) ON DELETE CASCADE,
  UNIQUE(courseId, bookId)
);
```

### 7. Downloads Table

Track book downloads.

```sql
CREATE TABLE downloads (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  userId UUID NOT NULL,
  bookId UUID NOT NULL,
  downloadedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  userAgent VARCHAR(255),
  ipAddress VARCHAR(45),
  FOREIGN KEY (userId) REFERENCES users(id) ON DELETE CASCADE,
  FOREIGN KEY (bookId) REFERENCES books(id) ON DELETE CASCADE,
  UNIQUE(userId, bookId, downloadedAt)
);

CREATE INDEX idx_downloads_userId ON downloads(userId);
CREATE INDEX idx_downloads_bookId ON downloads(bookId);
CREATE INDEX idx_downloads_date ON downloads(downloadedAt);
```

### 8. Favourites Table

User favourite books.

```sql
CREATE TABLE favourites (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  userId UUID NOT NULL,
  bookId UUID NOT NULL,
  addedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (userId) REFERENCES users(id) ON DELETE CASCADE,
  FOREIGN KEY (bookId) REFERENCES books(id) ON DELETE CASCADE,
  UNIQUE(userId, bookId)
);
```

### 9. Reviews Table

Book reviews and ratings.

```sql
CREATE TABLE reviews (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  userId UUID NOT NULL,
  bookId UUID NOT NULL,
  rating INT CHECK (rating >= 1 AND rating <= 5),
  reviewText TEXT,
  isHelpful INT DEFAULT 0,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (userId) REFERENCES users(id) ON DELETE CASCADE,
  FOREIGN KEY (bookId) REFERENCES books(id) ON DELETE CASCADE,
  UNIQUE(userId, bookId)
);
```

### 10. ReadingProgress Table

Track user reading progress.

```sql
CREATE TABLE reading_progress (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  userId UUID NOT NULL,
  bookId UUID NOT NULL,
  currentPage INT DEFAULT 0,
  totalPages INT,
  progressPercentage INT DEFAULT 0,
  lastReadAt TIMESTAMP,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (userId) REFERENCES users(id) ON DELETE CASCADE,
  FOREIGN KEY (bookId) REFERENCES books(id) ON DELETE CASCADE,
  UNIQUE(userId, bookId)
);
```

### 11. LectureNotes Table

Course lecture notes.

```sql
CREATE TABLE lecture_notes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  courseId UUID NOT NULL,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  filePath VARCHAR(255) NOT NULL,
  fileName VARCHAR(255),
  uploadedBy UUID NOT NULL,
  totalDownloads INT DEFAULT 0,
  status ENUM('draft', 'published') DEFAULT 'published',
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (courseId) REFERENCES courses(id) ON DELETE CASCADE,
  FOREIGN KEY (uploadedBy) REFERENCES users(id)
);
```

### 12. PastQuestions Table

Past examination questions.

```sql
CREATE TABLE past_questions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  courseId UUID NOT NULL,
  title VARCHAR(255) NOT NULL,
  year INT NOT NULL,
  semester VARCHAR(20),
  filePath VARCHAR(255) NOT NULL,
  fileName VARCHAR(255),
  uploadedBy UUID NOT NULL,
  totalDownloads INT DEFAULT 0,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (courseId) REFERENCES courses(id) ON DELETE CASCADE,
  FOREIGN KEY (uploadedBy) REFERENCES users(id)
);
```

### 13. Journals Table

Research journals and papers.

```sql
CREATE TABLE journals (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  author VARCHAR(255) NOT NULL,
  abstract TEXT,
  keywords VARCHAR(500),
  filePath VARCHAR(255) NOT NULL,
  fileName VARCHAR(255),
  publicationDate DATE,
  publisher VARCHAR(255),
  courseIds UUID[],
  uploadedBy UUID NOT NULL,
  totalDownloads INT DEFAULT 0,
  status ENUM('draft', 'published') DEFAULT 'published',
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (uploadedBy) REFERENCES users(id)
);
```

### 14. Projects Table

Final year projects.

```sql
CREATE TABLE projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  author VARCHAR(255) NOT NULL,
  supervisorName VARCHAR(255),
  academicYear VARCHAR(20),
  description TEXT,
  filePath VARCHAR(255) NOT NULL,
  fileName VARCHAR(255),
  level ENUM('300', '400') NOT NULL,
  uploadedBy UUID NOT NULL,
  totalDownloads INT DEFAULT 0,
  status ENUM('draft', 'published') DEFAULT 'published',
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (uploadedBy) REFERENCES users(id)
);
```

### 15. Announcements Table

System announcements.

```sql
CREATE TABLE announcements (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  content TEXT NOT NULL,
  authorId UUID NOT NULL,
  priority ENUM('low', 'medium', 'high') DEFAULT 'medium',
  isPublished BOOLEAN DEFAULT TRUE,
  publishedAt TIMESTAMP,
  expiresAt TIMESTAMP,
  createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (authorId) REFERENCES users(id)
);
```

## Indexes for Performance

```sql
-- Search indexes
CREATE INDEX idx_books_search ON books USING GIN(
  to_tsvector('english', title || ' ' || author)
);

CREATE INDEX idx_courses_search ON courses USING GIN(
  to_tsvector('english', title)
);

-- Time-based queries
CREATE INDEX idx_downloads_dateRange ON downloads(downloadedAt);
CREATE INDEX idx_books_createdAt ON books(createdAt);

-- Foreign key optimization
CREATE INDEX idx_books_uploadedBy ON books(uploadedBy);
CREATE INDEX idx_students_userId ON student_profiles(userId);
```

## Data Relationships

1. **One-to-Many**: User → Books (user uploads multiple books)
2. **One-to-Many**: Course → Materials (course has multiple books, notes, etc.)
3. **Many-to-Many**: Books ↔ Courses (via course_books junction)
4. **One-to-Many**: User → Downloads (user can download multiple books)
5. **One-to-One**: User → StudentProfile (student has one profile)

## Constraints

- Email must be unique across users
- Material numbers must be unique for students
- Each user can have only one favourite per book
- Each user can have only one review per book
- Course codes must be unique

## Migrations

Database migrations are managed with Sequelize. Run migrations with:

```bash
cd backend
npm run migrate
```

## Backup & Recovery

```bash
# Backup database
pg_dump ndu_napss_elib > backup.sql

# Restore database
psql ndu_napss_elib < backup.sql
```
