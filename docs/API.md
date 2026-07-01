# API Documentation

NDU NAPSS E-Library REST API Documentation

## Base URL

```
http://localhost:5000/api
```

## Authentication

All protected endpoints require a JWT token in the Authorization header:

```
Authorization: Bearer <token>
```

## Response Format

All responses are in JSON format:

```json
{
  "success": true,
  "message": "Operation successful",
  "data": {},
  "error": null
}
```

---

## Authentication Endpoints

### Register User

**POST** `/auth/register`

Register a new student account.

**Request Body:**
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "SecurePass123!",
  "matNumber": "CS/2021/001",
  "phoneNumber": "+234801234567",
  "level": "100"
}
```

**Response:** `201 Created`
```json
{
  "success": true,
  "message": "Registration successful. Please verify your email.",
  "data": {
    "id": "user_id",
    "email": "john@example.com",
    "firstName": "John"
  }
}
```

### Login User

**POST** `/auth/login`

Authenticate user and get JWT token.

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "SecurePass123!"
}
```

**Response:** `200 OK`
```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "token": "eyJhbGc...",
    "refreshToken": "eyJhbGc...",
    "user": {
      "id": "user_id",
      "email": "john@example.com",
      "role": "student"
    }
  }
}
```

### Verify Email

**POST** `/auth/verify-email`

Verify email address with token.

**Request Body:**
```json
{
  "token": "verification_token"
}
```

**Response:** `200 OK`

### Password Reset Request

**POST** `/auth/forgot-password`

Request password reset email.

**Request Body:**
```json
{
  "email": "john@example.com"
}
```

### Reset Password

**POST** `/auth/reset-password`

**Request Body:**
```json
{
  "token": "reset_token",
  "newPassword": "NewSecurePass123!"
}
```

### Refresh Token

**POST** `/auth/refresh-token`

Get a new access token using refresh token.

**Request Body:**
```json
{
  "refreshToken": "eyJhbGc..."
}
```

---

## Books Endpoints

### Get All Books

**GET** `/books`

Retrieve paginated list of books.

**Query Parameters:**
- `page` (default: 1)
- `limit` (default: 10)
- `search` - Search by title, author, or course code
- `category` - Filter by category
- `level` - Filter by course level (100, 200, 300, 400)
- `sort` - Sort by: `newest`, `popular`, `title`

**Example:**
```
GET /books?page=1&limit=10&level=100&sort=newest
```

**Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "books": [
      {
        "id": "book_id",
        "title": "Political Theory",
        "author": "John Smith",
        "courseCode": "POL101",
        "level": "100",
        "category": "Theory",
        "coverImage": "url",
        "downloads": 150,
        "createdAt": "2026-01-01T00:00:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 10,
      "total": 45,
      "totalPages": 5
    }
  }
}
```

### Get Single Book

**GET** `/books/:id`

**Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "id": "book_id",
    "title": "Political Theory",
    "author": "John Smith",
    "description": "Comprehensive guide...",
    "pdf": "url_to_pdf",
    "coverImage": "url",
    "courseCode": "POL101",
    "level": "100",
    "category": "Theory",
    "downloads": 150,
    "rating": 4.5,
    "reviews": []
  }
}
```

### Upload Book (Admin Only)

**POST** `/books` (Protected)

**Headers:**
```
Content-Type: multipart/form-data
Authorization: Bearer <token>
```

**Form Data:**
- `title` - Book title
- `author` - Author name
- `description` - Book description
- `courseCode` - Associated course code
- `level` - Academic level (100, 200, 300, 400)
- `category` - Book category
- `pdf` - PDF file
- `coverImage` - Cover image file

**Response:** `201 Created`

### Download Book

**GET** `/books/:id/download` (Protected)

Download PDF file.

**Response:** PDF file

---

## Courses Endpoints

### Get All Courses

**GET** `/courses`

**Query Parameters:**
- `level` - Filter by level (100, 200, 300, 400)
- `search` - Search by course code or title

**Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "courses": [
      {
        "id": "course_id",
        "code": "POL101",
        "title": "Introduction to Political Science",
        "level": "100",
        "description": "...",
        "unit": 3,
        "lecturer": "Prof. Name"
      }
    ]
  }
}
```

### Get Course Materials

**GET** `/courses/:courseCode/materials`

Get all materials for a specific course.

**Query Parameters:**
- `type` - Filter by type: `book`, `lecture_note`, `past_question`, `journal`, `project`

---

## User Endpoints

### Get Current User Profile

**GET** `/users/profile` (Protected)

**Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "id": "user_id",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@example.com",
    "matNumber": "CS/2021/001",
    "level": "100",
    "role": "student",
    "profilePicture": "url",
    "joinedAt": "2026-01-01T00:00:00Z"
  }
}
```

### Update Profile

**PUT** `/users/profile` (Protected)

**Request Body:**
```json
{
  "firstName": "Jane",
  "phoneNumber": "+234801234567",
  "profilePicture": "image_file"
}
```

### Get Favourite Books

**GET** `/users/favourites` (Protected)

### Add to Favourites

**POST** `/users/favourites/:bookId` (Protected)

### Remove from Favourites

**DELETE** `/users/favourites/:bookId` (Protected)

---

## Admin Endpoints

### Get All Users

**GET** `/admin/users` (Admin Only)

**Query Parameters:**
- `role` - Filter by role
- `search` - Search by email or name

### Manage User

**PUT** `/admin/users/:userId` (Admin Only)

**Request Body:**
```json
{
  "role": "student",
  "status": "active"
}
```

### Get Analytics

**GET** `/admin/analytics` (Admin Only)

**Query Parameters:**
- `period` - `day`, `week`, `month`, `year`

**Response:**
```json
{
  "success": true,
  "data": {
    "totalDownloads": 1250,
    "totalUsers": 500,
    "totalBooks": 120,
    "topBooks": [],
    "userGrowth": []
  }
}
```

---

## Error Responses

### 400 Bad Request
```json
{
  "success": false,
  "message": "Validation error",
  "errors": {
    "email": "Invalid email format"
  }
}
```

### 401 Unauthorized
```json
{
  "success": false,
  "message": "Invalid or expired token"
}
```

### 403 Forbidden
```json
{
  "success": false,
  "message": "You do not have permission to perform this action"
}
```

### 404 Not Found
```json
{
  "success": false,
  "message": "Resource not found"
}
```

### 500 Internal Server Error
```json
{
  "success": false,
  "message": "Internal server error"
}
```

---

## Rate Limiting

API endpoints are rate-limited to prevent abuse:
- **Public endpoints**: 100 requests per 15 minutes
- **Authenticated endpoints**: 300 requests per 15 minutes
- **Admin endpoints**: 500 requests per 15 minutes

---

## Testing Endpoints

Use Postman or similar tools. Import the provided collection:
```
/postman/ndu-napss-elib.postman_collection.json
```
