# 📝 Mini Task Manager – Full-Stack CRUD Application

A modern, responsive task management application built with **Next.js**, **React**, and **Tailwind CSS**. It offers a clean UI with full **CRUD operations**, **real-time feedback**, and **smooth animations**. Data is managed via a mock API with localStorage, simulating a full backend.

---

## 📋 Features

### ✅ Core Functionality (CRUD Operations)
- **Create**: Add new tasks with validation
- **Read**: View all tasks with filters (All / Pending / Done)
- **Update**: Edit task titles and toggle status
- **Delete**: Remove tasks with confirmation

### 🎨 UI/UX Features
- Responsive design for all screen sizes
- Clean interface with Tailwind CSS
- Hover effects, animations, and loading states
- Success/error notifications
- Live statistics dashboard

### 🔧 Technical Features
- Modular React components
- State management with `useState` & `useEffect`
- API simulation with delay and error handling
- Data persistence with `localStorage`

---

## 🛠️ Tech Stack

- **Frontend**: Next.js 14, React 18
- **Styling**: Tailwind CSS
- **Icons**: Lucide React
- **State**: React Hooks
- **Data Storage**: localStorage (mocking PostgreSQL)
- **Routing/API**: Next.js API routes

---

## 📁 Project Structure

mini-task-manager/
├── pages/

│ ├── api/
│ │ └── tasks/
│ │ ├── index.js # GET/POST /api/tasks
│ │ └── [id].js # GET/PUT/DELETE /api/tasks/:id
│ ├── _app.js # App wrapper
│ └── index.js # Main page
├── components/
│ ├── TaskCard.js # Task UI
│ ├── AddTaskForm.js # Task input form
│ └── Notification.js # Toast messages
├── styles/
│ └── globals.css # Tailwind imports
├── public/
│ └── favicon.ico
├── tailwind.config.js
├── next.config.js
├── package.json
└── README.md

yaml
Copy
Edit

---

## 🚀 Quick Start

### 🔧 Prerequisites
- Node.js (v16+)
- npm or yarn

### 🔌 Installation

```bash
git clone https://github.com/your-username/mini-task-manager.git
cd mini-task-manager
npm install   # or yarn install
npm run dev   # or yarn dev
Navigate to http://localhost:3000 in your browser.

🏗️ Build for Production
bash
Copy
Edit
npm run build
npm start
🔌 API Endpoints
Base URL: /api/tasks

1. Get All Tasks
GET /api/tasks

2. Create New Task
POST /api/tasks

json
Copy
Edit
{
  "title": "New task title"
}
3. Get Single Task
GET /api/tasks/:id

4. Update Task
PUT /api/tasks/:id

json
Copy
Edit
{
  "title": "Updated title",
  "status": "done"
}
5. Delete Task
DELETE /api/tasks/:id

Error Response
json
Copy
Edit
{
  "success": false,
  "error": "Error message"
}
🧱 Architecture & Design Decisions
Next.js Full-Stack for frontend + API in one project

Mock Backend simulating realistic delays/errors

Component-based UI with clean separation of concerns

Error Boundaries and client-side validations

State & UI separation with controlled hooks

🛡️ Error Handling & Edge Cases
Handled:

Empty/invalid task titles

Invalid/missing task IDs

Duplicate/rapid actions

Browser reload (state persists via localStorage)

🔒 Security Considerations (Production)
✅ Already:

Input validation

XSS prevention (React escaping)

CSRF via Next.js

🚀 Needed:

Auth (NextAuth.js, JWT)

DB security (SQL injection prevention, encryption)

CORS, rate limiting, secure headers

🌱 Future Improvements
🔥 High Priority
PostgreSQL + Prisma

Authentication (NextAuth, OAuth)

Tags, due dates, reminders

🚀 Medium Priority
Server-side optimizations

Dark mode, keyboard shortcuts

💡 Nice to Have
Real-time sync (WebSockets)

Task templates

Analytics dashboard

🧪 Testing Strategy
Unit Tests: Components, utilities, API

Integration: User flow + data management

E2E: Cypress for full journey tests

📱 Responsive Design
Mobile: 320–768px

Tablet: 768–1024px

Desktop: 1024+px

Responsive layout, scaling typography, touch-friendly buttons

🎨 Design System
Colors:

Primary: #2563eb

Success: #16a34a

Warning: #ea580c

Error: #dc2626

Neutral: Grayscale

Typography:

Heading: 600–700

Body: 400

Caption: 500

📊 Performance Metrics (Dev Mode)
FCP: < 1.5s

LCP: < 2.5s

CLS: < 0.1

TTI: < 3.5s

🔄 Deployment
Recommended: Vercel
Also supported: Netlify, Railway, Heroku

.env Variables (Production)
ini
Copy
Edit
NODE_ENV=production
DATABASE_URL=your_database_url
NEXTAUTH_SECRET=your_auth_secret
NEXTAUTH_URL=https://your-app.vercel.app
🤝 Contributing
Fork the repo

Create a new branch

Commit changes with clear messages

Open a pull request with details

📄 License
Licensed under the MIT License – feel free to use and modify.
