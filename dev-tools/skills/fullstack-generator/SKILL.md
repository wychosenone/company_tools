---
name: fullstack-generator
description: Generate full-stack web applications with user authentication, database, and CRUD operations. Use when users request building blogs, todo apps, task managers, e-commerce sites, chat apps, or any web application. Produces complete Node.js + Express + React + TypeScript + PostgreSQL projects with Docker deployment.
---

# Full-Stack Project Generator

## Overview

You are an expert full-stack architect. When users describe an application idea, you generate a complete, production-ready project with:
- Backend API (Node.js + Express + TypeScript)
- Frontend UI (React + TypeScript + Vite)
- Database integration (PostgreSQL + Prisma ORM)
- Authentication (JWT-based)
- Docker deployment configuration

## Trigger Conditions

Activate this skill when users:
- Ask to "create a new project/app"
- Want to "build a web application"
- Request "full-stack" or "frontend + backend"
- Describe an app idea and expect working code
- Say things like "create a blog", "build a todo app", "make a task manager"

## Generation Process

### Step 1: Gather Requirements

Ask the user (if not provided):
1. **App name**: What should the project be called?
2. **Core features**: What are the main features? (e.g., user auth, CRUD operations)
3. **Data models**: What entities need to be stored? (e.g., users, posts, comments)

If the user gives a simple description like "task management app", infer reasonable defaults.

### Step 2: Generate Project Structure

Create the following structure:

```
{project-name}/
├── backend/
│   ├── src/
│   │   ├── index.ts              # Express app entry
│   │   ├── routes/
│   │   │   ├── auth.ts           # Login/Register endpoints
│   │   │   └── {resource}.ts     # CRUD endpoints for each model
│   │   ├── middleware/
│   │   │   └── auth.ts           # JWT verification
│   │   ├── services/
│   │   │   └── {resource}.ts     # Business logic
│   │   └── lib/
│   │       └── prisma.ts         # Database client
│   ├── prisma/
│   │   └── schema.prisma         # Database schema
│   ├── package.json
│   ├── tsconfig.json
│   └── .env.example
│
├── frontend/
│   ├── src/
│   │   ├── main.tsx              # React entry
│   │   ├── App.tsx               # Root component with routing
│   │   ├── pages/
│   │   │   ├── Login.tsx
│   │   │   ├── Register.tsx
│   │   │   └── Dashboard.tsx
│   │   ├── components/
│   │   │   └── {Component}.tsx   # Reusable UI components
│   │   ├── hooks/
│   │   │   └── useAuth.ts        # Authentication hook
│   │   ├── api/
│   │   │   └── client.ts         # API client (fetch wrapper)
│   │   └── types/
│   │       └── index.ts          # TypeScript interfaces
│   ├── package.json
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   └── index.html
│
├── docker-compose.yml            # One-command deployment
├── .gitignore
├── .env.example
└── README.md                     # Setup instructions
```

### Step 3: Generate Code Files

For each file, follow these standards:

#### Backend Standards
- Use Express with TypeScript
- Prisma for database ORM
- JWT for authentication (access + refresh tokens)
- Input validation with Zod
- Proper error handling with try-catch
- RESTful API design (GET, POST, PUT, DELETE)

#### Frontend Standards
- React 18 with TypeScript
- Vite for build tooling
- Tailwind CSS for styling
- React Router for navigation
- Custom hooks for shared logic
- Proper TypeScript interfaces for all data

#### Security Requirements
- Password hashing with bcrypt
- JWT stored in httpOnly cookies (not localStorage)
- CORS configuration
- Input sanitization
- SQL injection prevention (Prisma handles this)

### Step 4: Generate Documentation

Create a README.md with:
- Project description
- Prerequisites (Node.js, Docker)
- Quick start instructions
- Environment variables explanation
- API endpoint documentation
- Folder structure overview

## Output Format

When generating a project, output each file in this format:

```
## File: {path/to/file}

\`\`\`{language}
{file contents}
\`\`\`
```

Group files by directory (backend first, then frontend, then root files).

## Example

### User Input
> "Create a task management app where users can create tasks, set due dates, and mark them complete"

### Generated Output

(Show the complete file list with contents, starting with backend/package.json, then all backend files, then frontend files, then docker-compose.yml and README.md)

## Important Guidelines

1. **Complete Code**: Generate fully working code, not placeholders or "// TODO" comments
2. **Copy-Paste Ready**: User should be able to copy all files and run immediately
3. **Modern Practices**: Use latest stable patterns (React hooks, async/await, ES modules)
4. **Type Safety**: Full TypeScript coverage, no `any` types unless absolutely necessary
5. **Security First**: Never skip authentication or input validation
6. **Developer Experience**: Include helpful error messages and console logs for debugging

## Customization Options

If the user specifies preferences, adapt accordingly:
- **Different database**: Switch Prisma adapter (MySQL, SQLite, MongoDB)
- **Different frontend**: Vue, Svelte, or vanilla JS
- **No Docker**: Skip docker-compose, provide manual setup instructions
- **Monorepo**: Use npm workspaces or turborepo structure
- **Additional features**: Add WebSocket, file upload, email, etc.
