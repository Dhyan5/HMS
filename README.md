# Sahyadri Hostel — Complaint & Maintenance System

A full-stack web application designed to streamline hostel maintenance by enabling students to report issues, track complaint status in real time, and allowing administrators to manage maintenance requests through a centralized dashboard.

---

## Overview

Sahyadri Hostel is a complaint and maintenance management system developed for hostel environments where reporting and resolving maintenance issues can often be inefficient.

The application provides a transparent workflow that allows students to submit maintenance requests while enabling administrators to monitor, prioritize, and resolve complaints efficiently. The interface follows a modern dark theme inspired by Apple's design language to provide a clean and intuitive user experience.

---

## Features

### Student Portal

* Submit maintenance complaints with category, priority, and detailed description
* View assigned room number directly from the dashboard and sidebar
* Track complaint status in real time
* Receive toast notifications for application events
* Modern, responsive dark user interface

### Administrator Portal

* View all complaints across the hostel
* Search complaints by student name, category, or description
* Filter complaints by status (Pending, In Progress, Resolved)
* Update complaint status with a single click
* High-priority alert banner for urgent maintenance requests

### General Features

* Secure JWT-based authentication with 7-day sessions
* Full-screen animated loading screen
* Smooth page transitions using Framer Motion
* Desktop-first responsive design with mobile-compatible navigation

---

## Technology Stack

| Layer             | Technology                                              |
| ----------------- | ------------------------------------------------------- |
| Framework         | Next.js 15 (App Router)                                 |
| Database          | NeonDB (Serverless PostgreSQL)                          |
| Authentication    | JWT using `jose` with HTTP-only cookies                 |
| Password Security | bcrypt (Cost Factor: 12)                                |
| Styling           | Tailwind CSS v4                                         |
| Animations        | Framer Motion                                           |
| Icons             | Lucide React                                            |
| Notifications     | react-hot-toast                                         |
| Deployment        | Docker, Nginx                                           |
| CI/CD             | GitHub Actions → Docker Hub (`dhyan11/sahyadri-hostel`) |

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/Dhyan5/sKILL_lab2026.git
cd sKILL_lab2026/sahyadri-hostel
npm install
```

### 2. Configure Environment Variables

Create a `.env.local` file in the project root.

```env
DATABASE_URL=postgresql://your_user:your_password@your_host/your_db?sslmode=require
JWT_SECRET=your_super_secret_key_here
```

A free PostgreSQL database can be created using Neon.

### 3. Initialize the Database

Start the development server and visit:

```
http://localhost:3000/api/init
```

This endpoint automatically creates the required database tables (`users` and `complaints`). This step only needs to be performed once.

### 4. Run the Application

```bash
npm run dev
```

The application will be available at:

```
http://localhost:3000
```

---

## Docker Deployment

### Build and Run

```bash
docker build \
  --build-arg DATABASE_URL="your_neondb_url" \
  --build-arg JWT_SECRET="your_secret" \
  -t sahyadri-hostel:latest .

docker run -p 3000:3000 \
  -e DATABASE_URL="your_neondb_url" \
  -e JWT_SECRET="your_secret" \
  sahyadri-hostel:latest
```

### Using Docker Compose

```bash
cp .env.example .env
docker compose up --build
```

### Pull Pre-built Image

```bash
docker pull dhyan11/sahyadri-hostel:latest

docker run -p 3000:3000 \
  -e DATABASE_URL="..." \
  -e JWT_SECRET="..." \
  dhyan11/sahyadri-hostel:latest
```

---

## Project Structure

```text
sahyadri-hostel/
│
├── app/
│   ├── api/
│   │   ├── auth/
│   │   ├── complaints/
│   │   └── init/
│   │
│   ├── dashboard/
│   │   ├── student/
│   │   └── admin/
│   │
│   ├── login/
│   ├── register/
│   ├── layout.tsx
│   └── globals.css
│
├── components/
│   ├── Loader.tsx
│   ├── Sidebar.tsx
│   ├── Navbar.tsx
│   └── ComplaintCard.tsx
│
├── lib/
│   ├── db.ts
│   └── auth.ts
│
├── .github/workflows/
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
└── .env.example
```

---

## Authentication Workflow

1. Students and administrators register using their credentials.
2. Passwords are securely hashed using bcrypt.
3. A JWT is generated upon successful authentication.
4. The token is stored in an HTTP-only cookie and in local storage for authenticated API requests.
5. Protected routes verify the JWT and enforce role-based authorization.
6. Students can only access their own complaints, while administrators have access to all complaints and management functions.

---

## Room Number Integration

During registration, students provide their hostel room number (e.g., `A-204`).

The room number is displayed:

* In the sidebar beneath the user's profile
* On the student dashboard
* Alongside complaint details in the administrator dashboard to simplify maintenance assignments

---

## Contributing

This project was developed as part of a college Skill Lab project for Sahyadri Hostel.

Contributions, improvements, and adaptations for similar hostel management systems are welcome. Feel free to fork the repository and customize it to meet your requirements.

---

## License

This project is licensed under the MIT License.
