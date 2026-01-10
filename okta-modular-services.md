# Okta Modular Services Architecture

This document identifies the major functionalities of the Tahdir legacy system that should be extracted into independent modules/services for the Okta platform re-architecture.

## Core / Platform Services

### Authentication & Authorization Service
**Service Type:** Platform  
**Description:** Handles user authentication, OTP verification, multi-account selection, and session management. Supports multiple account types (admin, school employee, guardian, student) with account switching capabilities.

### User Management Service
**Service Type:** Platform  
**Description:** Manages user profiles, identities, and basic user data across all account types. Handles user creation, updates, and profile management with support for multiple user roles and relationships.

### Roles & Permissions Service
**Service Type:** Platform  
**Description:** Manages role-based access control, permissions, and authorization policies. Supports school-specific roles, country-level permissions, and fine-grained permission definitions across the platform.

### Notifications Service
**Service Type:** Platform  
**Description:** Provides notification delivery infrastructure including push notifications (FCM), in-app notifications, and notification definitions. Supports customizable notification templates and delivery channels.

### Messaging Service
**Service Type:** Platform  
**Description:** Handles internal messaging and chat functionality between users. Manages chat rooms, message delivery, and communication threads across different user types.

### File Management Service
**Service Type:** Platform  
**Description:** Manages file storage, retrieval, and delivery. Handles document generation (PDFs, prints), file downloads, and secure file access with signature validation.

### Settings Service
**Service Type:** Platform  
**Description:** Manages system-wide and entity-specific settings. Supports hierarchical settings (platform, country, school) and configuration management for various system features.

### Location Service
**Service Type:** Platform  
**Description:** Manages geographical data including countries, regions, cities, districts, and sub-areas. Provides location-based services and data for school registration and user management.

### Subscription & Billing Service
**Service Type:** Platform  
**Description:** Handles subscription management, billing, transactions, and payment processing. Manages service subscriptions, packages, products, coupons, and subscription lifecycle (trials, activations, renewals).

## Business / Domain Services

### School Management Service
**Service Type:** Business  
**Description:** Manages school entities, school complexes, school registration, and school-level configurations. Handles school profiles, settings, device management, and school state management.

### Student Management Service
**Service Type:** Business  
**Description:** Manages student records, enrollment, student-school relationships, and student lifecycle. Handles student transfers, status changes, and student data import/export functionality.

### Guardian Management Service
**Service Type:** Business  
**Description:** Manages guardian accounts, guardian-student relationships, and representative management. Handles guardian authorization, representative roles, and guardian access to student information.

### Employee Management Service
**Service Type:** Business  
**Description:** Manages school employees, employee-school assignments, and employee roles. Handles employee lifecycle, role assignments, and employee permissions within schools.

### Attendance Management Service
**Service Type:** Business  
**Description:** Tracks student and employee attendance, absence confirmations, and attendance analytics. Handles attendance recording, status changes, and attendance reporting.

### Dismissal Management Service
**Service Type:** Business  
**Description:** Manages student dismissal tracking and dismissal status. Handles dismissal recording, status updates, and dismissal reporting.

### Class Operations Service
**Service Type:** Business  
**Description:** Manages classroom operations including class attendance, class attention tracking, class excuses, and scheduled class sessions. Handles real-time class operations and class activity tracking.

### Timetable Management Service
**Service Type:** Business  
**Description:** Manages school timetables, period scheduling, timetable assignments, and timetable rules. Handles timetable creation, teacher assignments, and timetable optimization.

### Exam Management Service
**Service Type:** Business  
**Description:** Manages exam periods, exam committees, exam scheduling, exam attendance, and exam observers. Handles exam organization, committee formation, and exam-related reporting.

### Subject & Grade Management Service
**Service Type:** Business  
**Description:** Manages subjects, grade distributions, student grades, and grade activities. Handles subject assignments, grade recording, and grade analytics.

### Leave Management Service
**Service Type:** Business  
**Description:** Manages leave requests, leave approvals, and leave tracking for employees and students. Handles leave workflows, leave status management, and leave reporting.

### Excuse Management Service
**Service Type:** Business  
**Description:** Manages absence excuse requests, excuse approvals, and excuse tracking. Handles excuse workflows, excuse status management, and excuse reporting.

### Calls Management Service
**Service Type:** Business  
**Description:** Manages student call-out system for guardians. Handles call requests, call processing, live call tracking, and call history.

### Conduct & Discipline Service
**Service Type:** Business  
**Description:** Manages student conduct problems, absence procedures, conduct rules, and disciplinary actions. Handles conduct problem tracking, procedure application, and conduct reporting.

### Reports & Analytics Service
**Service Type:** Business  
**Description:** Provides comprehensive reporting and analytics across all domains. Generates reports for attendance, exams, classes, leaves, calls, and other business metrics with customizable filters and formats.

### Holiday Schedule Service
**Service Type:** Business  
**Description:** Manages holiday schedules, academic calendars, and schedule notifications. Handles holiday definitions, schedule types, and holiday-related notifications.

