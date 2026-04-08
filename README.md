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
