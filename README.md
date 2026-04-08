# Advanced Authentication System with JWT, Refresh Token Rotation & Session Management

A secure backend authentication system built with **Node.js**, **Express.js**, and **MongoDB**, implementing **JWT-based authentication**, **refresh token rotation**, **session management**, and **cookie-based auth flow**.

This project demonstrates a more advanced authentication architecture than basic login/register systems by including:

- **Access Token + Refresh Token flow**
- **Refresh Token Rotation**
- **Session Tracking in Database**
- **Logout from Current Device**
- **Logout from All Devices**
- **Secure HTTP-only Cookie Storage**
- **Password Hashing**
- **Scalable Backend Folder Structure**

---

## 🚀 Features

### Authentication Features
- User Registration
- User Login
- Get Current Logged-in User (`get-me`)
- Refresh Access Token using Refresh Token
- Logout from Current Device
- Logout from All Devices

### Security Features
- JWT-based authentication
- Short-lived **Access Token** (`15 minutes`)
- Long-lived **Refresh Token** (`7 days`)
- Refresh token stored in **HTTP-only cookies**
- Refresh token **hashed before storing in DB**
- Session-based token validation
- Token rotation on refresh
- Session revocation support

### Session Management
- Stores each login session in MongoDB
- Tracks:
  - User ID
  - Refresh Token Hash
  - IP Address
  - User Agent
  - Revoked status
- Supports invalidating:
  - Single session
  - All sessions for a user

---

## 🛠️ Tech Stack

- **Node.js**
- **Express.js**
- **MongoDB**
- **Mongoose**
- **JWT (jsonwebtoken)**
- **cookie-parser**
- **Morgan**
- **dotenv**
- **crypto**

---

## 📁 Project Structure

```bash
advanced-auth-system/
│
├── src/
│   ├── config/
│   │   ├── config.js
│   │   └── database.js
│   │
│   ├── controllers/
│   │   └── auth.controller.js
│   │
│   ├── models/
│   │   ├── user.model.js
│   │   └── session.model.js
│   │
│   ├── routes/
│   │   └── auth.routes.js
│   │
│   └── app.js
│
├── .gitignore
├── package.json
├── package-lock.json
├── server.js
└── README.md
```


## ⚙️ Installation & Setup
### 1) Clone the repository
```bash
git clone https://github.com/patil-bhupendra/advanced-auth-system.git
cd advanced-auth-system
```
### 2) Install dependencies
```
npm install
```
### 3) Create a .env file in the root directory
```bash
MONGO_URI=mongodb://127.0.0.1:27017/advanced-auth-system
JWT_SECRET=your_super_secret_key
```
### 4) Start MongoDB

Make sure MongoDB is running locally.

### 5) Run the server
```bash
npm run dev
```

or

```bash
node server.js
```
## 🔐 Environment Variables

Create a .env file in the root directory and add:

```
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
```
## 📌 API Endpoints
Base URL
```
http://localhost:3000/api/auth
```
### 1. Register User

**Endpoint:**
```
POST /api/auth/register
```
**Request Body:**
```
{
  "username": "bhupendra",
  "email": "bhupendra@example.com",
  "password": "123456"
}
```
**Response:**
```
{
  "message": "User registered successfully",
  "user": {
    "username": "bhupendra",
    "email": "bhupendra@example.com"
  },
  "accessToken": "your_access_token"
}
```
### 2. Login User

**Endpoint:**
```
POST /api/auth/login
```
**Request Body:**
```
{
  "email": "bhupendra@example.com",
  "password": "123456"
}
```
**Response:**
```
{
  "message": "Logged in successfully",
  "user": {
    "username": "bhupendra",
    "email": "bhupendra@example.com"
  },
  "accessToken": "your_access_token"
}
```
### 3. Get Current User

**Endpoint:**
```
GET /api/auth/get-me
```
**Headers:**

Authorization: Bearer your_access_token

**Response:**
```
{
  "message": "User fetched successfully",
  "user": {
    "username": "bhupendra",
    "email": "bhupendra@example.com"
  }
}
```
### 4. Refresh Access Token

**Endpoint:**
```
GET /api/auth/refresh-token
```
**Requirement:**

Refresh token must be present in HTTP-only cookie

**Response:**
```
{
  "message": "Access token refreshed successfully",
  "accessToken": "new_access_token"
}
```
### 5. Logout (Current Device)

**Endpoint:**
```
GET /api/auth/logout
```
**Requirement:**

Refresh token must be present in HTTP-only cookie

**Response:**
```
{
  "message": "Logged out successfully"
}
```
### 6. Logout from All Devices

**Endpoint:**
```
GET /api/auth/logout-all
```
**Requirement:**

Refresh token must be present in HTTP-only cookie

**Response:**
```
{
  "message": "Logged out from all devices successfully"
}
```

## 🔄 Authentication Flow
### Access Token
- Generated on register and login
- Sent in the response body
- Used for protected routes
- Expires in 15 minutes
### Refresh Token
- Generated on register and login
- Stored in HTTP-only cookie
- Expires in 7 days
- Hashed before storing in database
- Used to generate a new access token
### Refresh Token Rotation

When /refresh-token is called:

- Existing refresh token is verified
- Session is checked in MongoDB
- A new refresh token is generated
- Old refresh token hash is replaced with new hash
- A new access token is returned
- New refresh token is set in cookie

This improves security by ensuring refresh tokens are rotated instead of reused.

## 🗃️ Database Models
### User Model

Stores:

- username
- email
- password (hashed)

### Session Model

Stores:

- user
- refreshTokenHash
- ip
- userAgent
- revoked
- createdAt
- updatedAt

## 🔒 Security Notes

This project includes important security concepts such as:

- JWT authentication
- Refresh token rotation
- Session storage in DB
- Token revocation
- Cookie-based refresh token handling
- Password hashing
- Device/session tracking

### Current Development Notes

- secure: false is currently used for cookies for localhost testing
- In production, it should be changed to:

```
secure: true

```
-sameSite and cookie configuration should be adjusted based on deployment environment

## ⚠️ Important Note

This project is built as a learning-focused advanced authentication system to understand real-world backend authentication concepts.

## Recommended Production Improvements

For production-grade implementation, the following upgrades are recommended:

- Use bcrypt instead of plain SHA-256 for password hashing
- Add input validation using express-validator or Zod
- Create reusable auth middleware
- Add centralized error handling middleware
- Use separate utility functions for token generation and cookie options
- Add rate limiting
- Add CSRF protection (if required based on frontend architecture)
  
## 📚 Learning Goals of This Project

This project was created to practice and demonstrate understanding of:

- Backend authentication architecture
- JWT token generation and verification
- Access token vs refresh token
- Refresh token rotation
- Session management with MongoDB
- Cookie-based authentication
- Device-based logout strategies
- Secure auth flow design in Express.js
  
## 🧪 Testing the API

You can test the API using:

- Postman
- Thunder Client

### Suggested Testing Flow
1. Register a user
2. Login
3. Copy the access token
4. Call get-me with Bearer token
5. Call refresh-token (cookie required)
7. Call logout
8. Login again
9. Call logout-all

## 📈 Future Enhancements

Planned improvements for this project:

- Email verification flow
- Forgot password / reset password
- Role-based authentication (User/Admin)
- Auth middleware for protected routes
- Device/session listing API
- Password strength validation
- Rate limiting for auth routes
- Deployment-ready environment config
- Unit & integration tests

## 👨‍💻 Author

**Bhupendra Patil**
Full Stack Developer (MERN Stack)

**GitHub:** patil-bhupendra
## ⭐ If you found this project useful

If this project helped you understand advanced authentication concepts:

- Star the repository
- Fork it
- Use it as a learning reference
  
## 📄 License

This project is for learning and educational purposes.
