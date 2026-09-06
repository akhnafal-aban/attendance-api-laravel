# Attendance API (Laravel)

REST API for an attendance system: users check in and out of meetings, and admins monitor attendance in real time. Built with Laravel 11+ and Sanctum token auth.

The `develop` branch is the active one; `main` contains the earlier meetings/users CRUD.

## Features

- **Token auth** — Laravel Sanctum; login, registration, password reset, email verification endpoints
- **Check-in / check-out** — a user checks into an ongoing meeting and checks out when it ends
- **Attendance history** — per-user history endpoint
- **Meeting management** (admin) — CRUD plus filtered views: ongoing, completed, upcoming
- **Admin monitoring** — live attendance roster per meeting
- **Locations** (admin) — CRUD for meeting locations
- **Role gate** — `adminAccess` middleware separates admin routes from user routes

## Endpoints (develop branch)

| Method | Route | Auth | Description |
|---|---|---|---|
| POST | `/api/register` | – | Create account |
| POST | `/api/login` | – | Get token |
| GET | `/api/user` | user | Current user |
| GET | `/api/user/has-ongoing-meeting` | user | Is a meeting running now |
| POST | `/api/user/check-in` | user | Check into the ongoing meeting |
| POST | `/api/user/check-out` | user | Check out |
| GET | `/api/user/check-user-in-meeting` | user | Current check-in status |
| GET | `/api/user/attendances-history` | user | Own attendance history |
| GET/POST | `/api/meetings` | admin | List / create meetings |
| GET/PUT/DELETE | `/api/meetings/{id}` | admin | Read / update / delete a meeting |
| GET | `/api/meetings/ongoing` | admin | Ongoing meetings |
| GET | `/api/meetings/completed` | admin | Completed meetings |
| GET | `/api/meetings/upcoming` | admin | Upcoming meetings |
| GET | `/api/meetings/{id}/attendance` | admin | Live attendance for a meeting |
| GET/POST | `/api/users` | admin | List / create users |
| GET/PUT/DELETE | `/api/users/{id}` | admin | Read / update / delete a user |
| GET/POST | `/api/locations` | admin | List / create locations |

Full request/response examples: [Postman collection](https://documenter.getpostman.com/view/31499252/2sAXjM3BXm).

## Setup

```bash
cp .env.example .env          # then edit DB credentials
composer install
php artisan key:generate
php artisan migrate
php artisan db:seed
php artisan serve             # http://localhost:8000
```

Seeders populate roles, departments, divisions, locations, and two test accounts:

| Role | Email | Password |
|---|---|---|
| User | `test@test` | `123123123` |
| Admin | `admin@admin` | `123123123` |

A Next.js frontend is not included; the [Breeze Next.js starter](https://github.com/laravel/breeze-next) pairs with this API out of the box (`FRONTEND_URL=http://localhost:3000` is preconfigured in `.env.example`).

## Tech

Laravel, PHP, Sanctum, MySQL.
