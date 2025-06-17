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
// Frontend validation
if (!title.trim()) {
  showNotification('Task title cannot be empty', 'error');
  return;
}

// Backend validation
if (!title || typeof title !== 'string' || title.trim().length === 0) {
  return res.status(400).json({
    success: false,
    error: 'Title is required and must be a non-empty string'
  });
}
Network Error Handling
javascripttry {
  const response = await api.createTask(taskData);
  if (response.success) {
    showNotification('Task added successfully!');
  }
} catch (error) {
  showNotification('Failed to add task. Please try again.', 'error');
}
Additional Error Handling for Production
1. Network Resilience

Retry Logic: Automatic retry for failed requests (exponential backoff)
Offline Support: Service workers for offline functionality
Connection Status: Show network status to users

2. Data Integrity

Optimistic Updates: Update UI immediately, rollback on error
Conflict Resolution: Handle concurrent updates to the same task
Data Synchronization: Ensure consistency between client and server

3. User Experience

Error Boundaries: React error boundaries to catch component crashes
Graceful Degradation: App continues working even with some features broken
User Feedback: Clear, actionable error messages

4. Edge Cases Covered

Empty task titles
Invalid task IDs (non-numeric, negative)
Deleted tasks being updated
Browser refresh during operations
Rapid multiple clicks (debouncing)
Network timeouts


4. What security features would you add in production?
Authentication & Authorization
javascript// JWT-based authentication
const jwt = require('jsonwebtoken');

const authMiddleware = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'Access denied. No token provided.' });
  }
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    res.status(400).json({ error: 'Invalid token.' });
  }
};
Input Sanitization & Validation
javascriptconst Joi = require('joi');

const taskSchema = Joi.object({
  title: Joi.string().min(1).max(255).required().trim(),
  status: Joi.string().valid('pending', 'done')
});

const validateTask = (req, res, next) => {
  const { error } = taskSchema.validate(req.body);
  if (error) {
    return res.status(400).json({ error: error.details[0].message });
  }
  next();
};
Additional Security Measures
1. Data Protection

HTTPS Enforcement: Redirect all HTTP to HTTPS
Database Encryption: Encrypt sensitive data at rest
Environment Variables: Secure credential management

2. API Security

Rate Limiting: Prevent API abuse

javascriptconst rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});

CORS Configuration: Restrict allowed origins
Request Size Limits: Prevent large payload attacks

3. Content Security

Content Security Policy (CSP): Prevent XSS attacks
SQL Injection Prevention: Parameterized queries
NoSQL Injection Prevention: Input sanitization

4. Monitoring & Logging

Access Logs: Track API usage and suspicious activity
Error Monitoring: Real-time error tracking (Sentry)
Security Alerts: Automated alerts for security events


5. What would you improve if you had 1 full day?
Priority 1: Database Integration (4 hours)
javascript// Prisma schema
model Task {
  id        Int      @id @default(autoincrement())
  title     String
  status    Status   @default(PENDING)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  userId    Int
  user      User     @relation(fields: [userId], references: [id])
}
Benefits:

Real data persistence
Better performance with indexing
Relationship management
Data integrity constraints

Priority 2: User Authentication (2 hours)
javascript// NextAuth.js setup
import NextAuth from 'next-auth'
import GoogleProvider from 'next-auth/providers/google'

export default NextAuth({
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    })
  ],
  callbacks: {
    session: async ({ session, token }) => {
      session.userId = token.sub;
      return session;
    }
  }
})
Priority 3: Enhanced Features (1.5 hours)
Advanced Task Management

Categories/Tags: Organize tasks by project or category
Due Dates: Task scheduling with calendar integration
Priority Levels: High, Medium, Low priority tasks
Subtasks: Break down complex tasks

Improved UX

Drag & Drop: Reorder tasks by priority
Bulk Operations: Select and modify multiple tasks
Search & Filter: Find tasks quickly
Keyboard Shortcuts: Power user features

Priority 4: Performance & Testing (0.5 hours)
Performance Optimizations
javascript// React.memo for expensive components
const TaskCard = React.memo(({ task, onEdit, onDelete }) => {
  // Component logic
});

// useMemo for expensive calculations
const taskStats = useMemo(() => {
  return {
    pending: tasks.filter(t => t.status === 'pending').length,
    completed: tasks.filter(t => t.status === 'done').length
  };
}, [tasks]);
Testing Setup
javascript// Jest + React Testing Library
import { render, screen, fireEvent } from '@testing-library/react';
import TaskCard from '../components/TaskCard';

test('should toggle task status when button clicked', () => {
  const mockToggle = jest.fn();
  render(<TaskCard task={mockTask} onToggleStatus={mockToggle} />);
  
  fireEvent.click(screen.getByRole('button', { name: /mark as done/i }));
  expect(mockToggle).toHaveBeenCalledWith(mockTask.id);
});
Future Roadmap (Beyond 1 Day)

Real-time Collaboration: WebSocket integration for live updates
Mobile App: React Native version
Analytics: Task completion metrics and productivity insights
Integrations: Calendar, email, Slack notifications
AI Features: Smart task suggestions and auto-categorization
