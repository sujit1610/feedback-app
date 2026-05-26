# Feedback Management App (Spring Boot + React)

A simple fresher-level full-stack project.

## Features
1. **Registration** – new users sign up (name, email, password).
2. **Login** – for both users and admin.
3. **Add / Edit feedback** – a user sees their previously submitted feedback, or an add form if they haven't submitted yet. Each user has one feedback they can edit.
4. **Admin Dashboard** – admin can view, edit and delete (CRUD) all feedback.

## Tech stack
- **Backend:** Spring Boot 3.4 · Java 21 · Spring Data JPA · H2 (default) / PostgreSQL
- **Frontend:** React 18 · Vite

## Default admin login
```
email:    admin@app.com
password: admin123
```
(Created automatically on first startup.)

---

## How to run

### 1. Backend (port 8080)
```bash
cd backend
./mvnw spring-boot:run      # on Windows: mvnw spring-boot:run
```
Uses an in-memory H2 database by default, so no DB install is needed.
H2 console: http://localhost:8080/h2-console (JDBC URL: `jdbc:h2:mem:feedbackdb`, user `sa`, no password).

### 2. Frontend (port 5173)
```bash
cd frontend
npm install
npm run dev
```
Open http://localhost:5173

---

## Switching to PostgreSQL
In `backend/src/main/resources/application.properties`, comment out the H2 block
and uncomment the PostgreSQL block, then set your database name, user and password.

## API endpoints
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/api/auth/register` | Register a user |
| POST | `/api/auth/login` | Login |
| GET  | `/api/feedback/me/{userId}` | Get a user's own feedback |
| POST | `/api/feedback` | Add or update own feedback |
| GET  | `/api/feedback` | (Admin) list all feedback |
| PUT  | `/api/feedback/{id}` | (Admin) update feedback |
| DELETE | `/api/feedback/{id}` | (Admin) delete feedback |

## Notes for improvement (good things to mention in a review/viva)
- Passwords are stored as plain text for simplicity — use **BCrypt** hashing in a real app.
- There's no token/session security yet — add **Spring Security + JWT** to protect admin routes.
- Add server-side checks so only an admin can hit the admin endpoints.
