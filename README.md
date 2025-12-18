# Paracetamol

A comprehensive project documentation for the Paracetamol application.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [API Endpoints](#api-endpoints)
- [Usage Examples](#usage-examples)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)
- [Support](#support)

## 🎯 Project Overview

Paracetamol is a robust application designed to provide efficient solutions for [your project purpose]. This project leverages modern development practices and technologies to deliver a scalable, maintainable, and user-friendly application.

### Key Objectives

- Provide reliable and efficient functionality
- Ensure code quality and maintainability
- Facilitate easy integration and deployment
- Support comprehensive API access
- Enable seamless user experience

## ✨ Features

- **Feature 1**: Core functionality for [description]
- **Feature 2**: Advanced capabilities including [description]
- **Feature 3**: Real-time processing and monitoring
- **Feature 4**: Comprehensive error handling and logging
- **Feature 5**: RESTful API for easy integration
- **Feature 6**: Authentication and authorization support
- **Feature 7**: Database integration and management
- **Feature 8**: Scalable architecture

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v14.x or higher) / **Python** (v3.8 or higher) - [Choose based on your tech stack]
- **npm** (v6.x or higher) / **pip** (v20.x or higher)
- **Git** (v2.25 or higher)
- **Docker** (optional, for containerized deployment)
- **Database**: PostgreSQL 12+ or MongoDB 4.4+

### System Requirements

- **OS**: Linux, macOS, or Windows
- **RAM**: Minimum 2GB (4GB recommended)
- **Disk Space**: At least 500MB available

## 🚀 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/nn98-star/Paracetamol-.git
cd Paracetamol-
```

### Step 2: Install Dependencies

#### For Node.js/npm projects:

```bash
npm install
```

#### For Python projects:

```bash
pip install -r requirements.txt
```

### Step 3: Environment Configuration

Create a `.env` file in the project root directory:

```bash
cp .env.example .env
```

Edit the `.env` file with your configuration:

```env
# Application Configuration
NODE_ENV=development
PORT=3000
APP_NAME=Paracetamol

# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=paracetamol_db
DB_USER=postgres
DB_PASSWORD=your_password

# API Keys and Tokens
API_KEY=your_api_key_here
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRATION=24h

# Logging
LOG_LEVEL=info
LOG_FORMAT=json
```

### Step 4: Database Setup

#### PostgreSQL:

```bash
# Create database
createdb paracetamol_db

# Run migrations
npm run migrate
# or for Python
python manage.py migrate
```

#### MongoDB:

```bash
# MongoDB will auto-create the database on first connection
# Ensure MongoDB service is running
mongod
```

### Step 5: Start the Application

#### Development Mode:

```bash
npm run dev
# or for Python
python manage.py runserver
```

#### Production Mode:

```bash
npm run start
# or for Python
gunicorn app:app
```

#### Using Docker:

```bash
docker build -t paracetamol .
docker run -p 3000:3000 --env-file .env paracetamol
```

The application should now be running at `http://localhost:3000`

## ⚙️ Configuration

### Application Settings

Key configuration options available in `.env`:

| Variable | Description | Default |
|----------|-------------|---------|
| `NODE_ENV` | Environment (development/production) | development |
| `PORT` | Application port | 3000 |
| `DB_HOST` | Database host | localhost |
| `DB_PORT` | Database port | 5432 |
| `LOG_LEVEL` | Logging level (debug/info/warn/error) | info |
| `JWT_EXPIRATION` | JWT token expiration | 24h |

### Advanced Configuration

For advanced configurations, refer to the `config/` directory in the project root.

## 🔌 API Endpoints

### Base URL

```
http://localhost:3000/api/v1
```

### Authentication

All endpoints require authentication via JWT token in the `Authorization` header:

```
Authorization: Bearer <your_jwt_token>
```

### Endpoints

#### 1. **Health Check**

- **Method**: `GET`
- **Endpoint**: `/health`
- **Description**: Check application status
- **Authentication**: Not required
- **Response**:
```json
{
  "status": "ok",
  "timestamp": "2025-12-18T20:44:03Z",
  "version": "1.0.0"
}
```

---

#### 2. **User Management**

##### Get All Users

- **Method**: `GET`
- **Endpoint**: `/users`
- **Description**: Retrieve all users (admin only)
- **Query Parameters**:
  - `page` (integer): Page number (default: 1)
  - `limit` (integer): Results per page (default: 10)
  - `search` (string): Search term
- **Response**:
```json
{
  "success": true,
  "data": [
    {
      "id": "uuid",
      "username": "john_doe",
      "email": "john@example.com",
      "createdAt": "2025-12-18T20:44:03Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 100
  }
}
```

##### Get User by ID

- **Method**: `GET`
- **Endpoint**: `/users/:id`
- **Description**: Retrieve a specific user
- **Response**:
```json
{
  "success": true,
  "data": {
    "id": "uuid",
    "username": "john_doe",
    "email": "john@example.com",
    "profile": {
      "firstName": "John",
      "lastName": "Doe",
      "avatar": "https://example.com/avatar.jpg"
    }
  }
}
```

##### Create User

- **Method**: `POST`
- **Endpoint**: `/users`
- **Description**: Create a new user
- **Request Body**:
```json
{
  "username": "jane_doe",
  "email": "jane@example.com",
  "password": "securePassword123",
  "firstName": "Jane",
  "lastName": "Doe"
}
```
- **Response**:
```json
{
  "success": true,
  "data": {
    "id": "uuid",
    "username": "jane_doe",
    "email": "jane@example.com"
  }
}
```

##### Update User

- **Method**: `PUT`
- **Endpoint**: `/users/:id`
- **Description**: Update user information
- **Request Body**:
```json
{
  "username": "jane_doe_updated",
  "email": "jane.updated@example.com",
  "profile": {
    "firstName": "Jane",
    "lastName": "Smith"
  }
}
```
- **Response**: Updated user object

##### Delete User

- **Method**: `DELETE`
- **Endpoint**: `/users/:id`
- **Description**: Delete a user
- **Response**:
```json
{
  "success": true,
  "message": "User deleted successfully"
}
```

---

#### 3. **Authentication**

##### Login

- **Method**: `POST`
- **Endpoint**: `/auth/login`
- **Description**: Authenticate user and receive JWT token
- **Authentication**: Not required
- **Request Body**:
```json
{
  "username": "john_doe",
  "password": "password123"
}
```
- **Response**:
```json
{
  "success": true,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIs...",
    "user": {
      "id": "uuid",
      "username": "john_doe",
      "email": "john@example.com"
    }
  }
}
```

##### Register

- **Method**: `POST`
- **Endpoint**: `/auth/register`
- **Description**: Create new user account
- **Authentication**: Not required
- **Request Body**:
```json
{
  "username": "new_user",
  "email": "newuser@example.com",
  "password": "securePassword123",
  "passwordConfirm": "securePassword123"
}
```
- **Response**: User object with token

##### Logout

- **Method**: `POST`
- **Endpoint**: `/auth/logout`
- **Description**: Logout and invalidate token
- **Response**:
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

##### Refresh Token

- **Method**: `POST`
- **Endpoint**: `/auth/refresh`
- **Description**: Get a new JWT token
- **Response**:
```json
{
  "success": true,
  "data": {
    "token": "new_jwt_token"
  }
}
```

---

#### 4. **Data Management**

##### Get All Records

- **Method**: `GET`
- **Endpoint**: `/records`
- **Description**: Retrieve all records
- **Query Parameters**:
  - `page` (integer): Page number
  - `limit` (integer): Results per page
  - `sort` (string): Sort field
  - `order` (string): Sort order (asc/desc)
- **Response**:
```json
{
  "success": true,
  "data": [
    {
      "id": "uuid",
      "title": "Record Title",
      "description": "Record description",
      "status": "active",
      "createdAt": "2025-12-18T20:44:03Z"
    }
  ]
}
```

##### Create Record

- **Method**: `POST`
- **Endpoint**: `/records`
- **Description**: Create a new record
- **Request Body**:
```json
{
  "title": "New Record",
  "description": "Record description",
  "data": {}
}
```
- **Response**: Created record object

##### Update Record

- **Method**: `PUT`
- **Endpoint**: `/records/:id`
- **Description**: Update a record
- **Response**: Updated record object

##### Delete Record

- **Method**: `DELETE`
- **Endpoint**: `/records/:id`
- **Description**: Delete a record
- **Response**:
```json
{
  "success": true,
  "message": "Record deleted successfully"
}
```

---

### Error Handling

All endpoints follow consistent error response format:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {}
  }
}
```

### Common HTTP Status Codes

| Status | Description |
|--------|-------------|
| 200 | OK - Request successful |
| 201 | Created - Resource successfully created |
| 400 | Bad Request - Invalid input |
| 401 | Unauthorized - Authentication required |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource not found |
| 500 | Internal Server Error |

## 📚 Usage Examples

### Example 1: User Registration and Login

```bash
# Register a new user
curl -X POST http://localhost:3000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "email": "test@example.com",
    "password": "SecurePass123",
    "passwordConfirm": "SecurePass123"
  }'

# Login
curl -X POST http://localhost:3000/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "password": "SecurePass123"
  }'
```

### Example 2: Create and Manage Records

```bash
# Create a record (requires authentication)
curl -X POST http://localhost:3000/api/v1/records \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Sample Record",
    "description": "This is a test record",
    "data": {"key": "value"}
  }'

# Get all records
curl -X GET http://localhost:3000/api/v1/records?page=1&limit=10 \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"

# Update a record
curl -X PUT http://localhost:3000/api/v1/records/RECORD_ID \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Updated Record",
    "description": "Updated description"
  }'
```

### Example 3: Using with JavaScript/Node.js

```javascript
const axios = require('axios');

const API_URL = 'http://localhost:3000/api/v1';
let token = '';

// Login
async function login(username, password) {
  try {
    const response = await axios.post(`${API_URL}/auth/login`, {
      username,
      password
    });
    token = response.data.data.token;
    console.log('Login successful');
    return response.data;
  } catch (error) {
    console.error('Login failed:', error.response.data);
  }
}

// Create record
async function createRecord(title, description) {
  try {
    const response = await axios.post(
      `${API_URL}/records`,
      { title, description },
      {
        headers: {
          'Authorization': `Bearer ${token}`,
          'Content-Type': 'application/json'
        }
      }
    );
    return response.data;
  } catch (error) {
    console.error('Failed to create record:', error.response.data);
  }
}

// Usage
(async () => {
  await login('testuser', 'SecurePass123');
  await createRecord('My Record', 'Record description');
})();
```

## 📁 Project Structure

```
Paracetamol-/
├── src/
│   ├── api/
│   │   ├── routes/
│   │   │   ├── auth.js
│   │   │   ├── users.js
│   │   │   └── records.js
│   │   ├── controllers/
│   │   ├── middleware/
│   │   └── validators/
│   ├── models/
│   │   ├── User.js
│   │   └── Record.js
│   ├── services/
│   ├── utils/
│   ├── config/
│   └── app.js
├── tests/
│   ├── unit/
│   ├── integration/
│   └── fixtures/
├── migrations/
├── .env.example
├── .gitignore
├── .dockerignore
├── Dockerfile
├── docker-compose.yml
├── package.json
├── README.md
└── LICENSE
```

## 🤝 Contributing

We welcome contributions to Paracetamol! Please follow these guidelines:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/your-feature-name`
3. **Make your changes** and commit: `git commit -am 'Add new feature'`
4. **Push to the branch**: `git push origin feature/your-feature-name`
5. **Submit a Pull Request** with a clear description

### Code Standards

- Follow the existing code style
- Write meaningful commit messages
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting PR

### Running Tests

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm test -- filename.test.js
```

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## 💬 Support

For support, please:

1. Check the [Documentation](./docs) folder
2. Search existing [Issues](https://github.com/nn98-star/Paracetamol-/issues)
3. Create a new issue with detailed information
4. Contact the maintainers

### Useful Resources

- [API Documentation](./docs/API.md)
- [Installation Guide](./docs/INSTALLATION.md)
- [Contributing Guidelines](./CONTRIBUTING.md)
- [Changelog](./CHANGELOG.md)

---

**Last Updated**: 2025-12-18  
**Version**: 1.0.0  
**Maintainer**: [nn98-star](https://github.com/nn98-star)
