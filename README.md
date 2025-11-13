IBM-NJ-To-Do-App (React Hooks)
Project Overview
IBM-NJ To-Do App is a lightweight task management application built using React Hooks.
This repository documents the project development in 5 phases:

Problem Understanding & Requirements
Solution Design & Architecture
MVP Implementation
Enhancements & Deployment
Demonstration & Documentation
Phase 1 – Problem Understanding & Requirements
Problem Statement
Managing tasks effectively is a common challenge.
Users need a simple, responsive, and lightweight web-based To-Do App.

Scope
Add, update, delete, complete tasks
Store tasks in React state (local only for now)
Deliverable
Requirements document (PDF included in /docs)
Phase 1 Document

Tech Stack (Planned)
React (with Hooks)
JavaScript (ES6)
CSS for styling
Roadmap
Phase 2: Solution Design & Architecture

Phase 3: Basic MVP implementation

Phase 4: Enhancements & deployment

Phase 5: Documentation & demo

 PROBLEM STATEMENT:

Users today need simple, fast, and responsive tools to manage their tasks effectively. While many apps exist, they often include bloated features or lack responsiveness on different devices. The goal of the "Do App" is to provide users with a lightweight, intuitive task management tool that allows them to create, edit, complete, and delete tasks—quickly and efficiently.

 USER & STACKEHOLDERS:

Role Description User Anyone who needs to track and manage tasks (students, professionals, etc.) Product Owner You or your client/instructor who defines features and priorities Developers Frontend and backend developers (could be just you) Tester Person responsible for validating features against criteria.

 USER STORIES:

ID As a... I want to... So that... US1 User Create a new task I can remember what I need to do US2 User View a list of my tasks I can see what I need to complete US3 User Mark a task as completed I know I’ve finished it US4 User Edit a task I can correct or update task details US5 User Delete a task I can remove tasks I no longer need

 MVP FEATURES: The following features define the Minimum Viable Product (MVP): • ✅ Add new tasks • ✅ View all tasks • ✅ Mark tasks as completed/uncompleted • ✅ Edit existing tasks • ✅ Delete tasks • ✅ Store data via REST API (Node.js backend with a database)

 WIREFRAMES / API ENDPOINT LIST: A. Wireframes Sketch simple screens (or describe layout):

Main Screen: o Task Input (Text box + Add Button) o List of Tasks  Task Text  Checkbox for complete  Edit & Delete icons.

Edit Modal (optional): o Input field prefilled with task text o Save button You can use Figma, Balsamiq, or even hand-draw wireframes.

Method Endpoint Description GET /api/tasks Get all tasks POST /api/tasks Create a new task PUT /api/tasks/:id Update a task PATCH /api/tasks/:id/complete Mark as complete/incomplete DELETE /api/tasks/:id Delete a task

 ACCEPTANCE CRITERIA:

Feature Criteria Create Task When I type and click "Add", a new task appears in the list View Tasks On page load, I see all my tasks retrieved from the API Edit Task I can edit a task’s text and see the updated value Delete Task Clicking delete removes a task from the UI and DB Complete Task Clicking checkbox toggles completion visually and in DB Responsive Design The app works well on both mobile and desktop devices

 TECH STACK SELECTION:

• Frontend (UI): o React.js (with Hooks), Tailwind CSS or Material UI for clean, maintainable UI. • Backend (API Layer): o Node.js/Express or Java Spring Boot for RESTful API support (optional for To-Do apps needing persistence and multi-user features). • Database: o MongoDB for storing tasks; o Redis for caching active user sessions if scaling to multi-user. • Authentication & Security: o JWT (JSON Web Tokens) for session management OAuth2.0 if third-party login is need. • Deployment & Infrastructure: o Docker and Kubernetes (or OpenShift) for container orchestration; CI/CD with GitHub Actions/Jenkins.

 UI STRUCTURE / API SCHEMA DESIGN :

UI Structure (Page Components) • Home Page : Task list, task categories/filters, search. • Task Details Page: Task info, edit task, mark complete/incomplete. • Add/Edit Task Page: Add new or update existing task. • User Profile/Settings Page: Manage user info (if app is multi-user).

API Schema (RESTful) • POST /api/auth/login – User login. • POST /api/auth/register – User signup. • GET /api/tasks – Fetch all tasks (support pagination, filters). • GET /api/tasks/:id – Fetch task details. • POST /api/tasks – Add new task. • PUT /api/tasks/:id – Update task. • DELETE /api/tasks/:id – Delete task.  DATA HANDLING APPROACH:

• Tasks Data: MongoDB stores all To-Do tasks. Use schemas for task attributes (title, description, status).[5] • Sessions: Optional Redis caching for logged-in user sessions. User Data: Store securely in MongoDB with hashed passwords.

• Concurrency: Use optimistic locking for simultaneous task edits. • Data Security: SSL/TLS for all network traffic; implement basic security standards even in small apps.

App Section React Component(s) Backend Module Database Collection Header/Nav HeaderNav Task List TaskList, TaskItem Task Controller Tasks Add/Edit Task AddTask, EditTask Task Controller Tasks User Authentication Login, Register Auth Controller Users  COMPONENT / MODULE DIAGRAM:

 BASIC FLOW DIAGRAM:

User opens app → UI calls GET /api/tasks
User adds new task → POST /api/tasks
Task added to MongoDB (optionally cached in Redis)
User marks as completed/edits task → PUT /api/tasks/:id
User deletes task → DELETE /api/tasks/:id
Confirm changes reflected on UI.
 React Hooks Implementation Example:

import React, { useState, useEffect } from "react"; function TaskList() { const [tasks, setTasks] = useState([]); useEffect(() => { fetch("/api/tasks").then(res => res.json()).then(setTasks); }, []); return (

{tasks.map(task =>
{task.title}
)}
); }
