# Laravel Developer Test Tasks

## 1. Multi-Role Login System
Create a login page that authenticates users with three different roles (Admin, Manager, User). After successful authentication, redirect users to role-specific dashboards with appropriate access controls. Implement proper session management and role-based middleware to protect routes.

## 2. Spatie Roles and Permissions CRUD with AJAX
Implement a complete CRUD system using Spatie Laravel Permission package. Create API endpoints for managing roles and permissions, and build a frontend interface using AJAX and jQuery for seamless user interactions without page refreshes. Include proper validation and error handling.

## 3. Events and Listeners Implementation
Design and implement a custom event system with corresponding listeners. Create an event that triggers when a specific user action occurs (like user registration or order placement) and implement multiple listeners that handle different aspects of the event (send email, log activity, update statistics).

## 4. Jobs and Queue Processing
Create background job processing system using Laravel queues. Implement jobs that handle time-consuming tasks (like sending bulk emails or processing large datasets) and configure proper queue workers. Include job failure handling and retry mechanisms.

## 5. Laravel Artisan Commands and Cron Jobs
Develop custom Artisan commands that perform scheduled tasks such as database cleanup, report generation, or data synchronization. Configure these commands to run automatically using Laravel's task scheduler (cron jobs) and implement proper logging and error reporting for scheduled tasks.
