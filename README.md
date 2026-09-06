# CareCamp Backend

Backend API for **CareCamp**, a medical camp management platform that provides authentication, camp management, participant registrations, payments, analytics, notifications, and feedback.

## Features

* User authentication and authorization
* JWT-based authentication
* Firebase Admin integration
* User management
* Medical camp management
* Camp registration
* Registration management
* Stripe payment integration
* Stripe webhook handling
* Feedback and ratings
* Analytics
* Notifications
* Request validation with Zod
* API rate limiting
* Security headers with Helmet
* CORS configuration
* HTTP request logging
* Centralized error handling
* MongoDB data persistence

## Core Modules

The backend is organized into feature-based modules:

```text
Authentication
Users
Camps
Registrations
Payments
Feedback
Notifications
Analytics
Public
```

Each feature is separated into dedicated routes, controllers, services, and validation logic where applicable.

## Tech Stack

### Backend

* Node.js
* Express.js
* JavaScript
* MongoDB
* Mongoose

### Authentication & Security

* JSON Web Tokens (JWT)
* Firebase Admin SDK
* bcryptjs
* Helmet
* express-rate-limit
* CORS

### Payments

* Stripe
* Stripe Webhooks

### Validation & Logging

* Zod
* Morgan
* Winston

### Development

* ESLint
* Prettier
* Husky
* lint-staged

## Architecture

The backend follows a modular structure that separates application concerns by domain.

```text
Request
   ↓
Route
   ↓
Middleware
   ↓
Controller
   ↓
Service
   ↓
Model
   ↓
MongoDB
```

Common middleware handles:

* Authentication
* Request validation
* Security
* Rate limiting
* Logging
* Error handling

## API Modules

### Authentication

Handles:

* User registration
* User login
* Authentication
* Authorization

### Users

Provides user-related management functionality.

### Camps

Handles:

* Creating camps
* Updating camps
* Deleting camps
* Retrieving camps
* Camp information
* Camp management

### Registrations

Handles participant registrations and registration management.

### Payments

Handles:

* Stripe payment processing
* Payment-related operations
* Stripe webhook events

### Feedback

Handles participant feedback and ratings.

### Notifications

Provides notification-related functionality for application users.

### Analytics

Provides data and statistics required by the application dashboards.

## Security

The API includes several security measures:

* JWT authentication
* Firebase Admin verification
* Password hashing with bcryptjs
* Helmet security headers
* Configurable CORS
* Request rate limiting
* Environment-based secrets
* Centralized error handling
* Request validation with Zod

The API rate limiter currently allows up to **100 requests per 15-minute window**.

## Stripe Webhooks

Stripe webhook requests are handled through a dedicated endpoint:

```text
POST /stripe-webhook
```

The endpoint uses a raw request body before the normal JSON body parser so Stripe webhook signatures can be processed correctly.

## API Prefixes

The backend supports API routes with both direct and `/api` prefixes for its domain modules.

Examples:

```text
/auth
/api/auth

/users
/api/users

/notifications
/api/notifications

/analytics
/api/analytics
```

The same pattern is also applied to camp, registration, payment, feedback, and public routes.

## Environment Variables

Create a `.env` file based on `.env.example`.

Required configuration includes:

```env
PORT=5000
NODE_ENV=development
CLIENT_URL=http://localhost:5173

MONGODB_URI=your_mongodb_connection_string
DB_USER=your_database_user
DB_PASSWORD=your_database_password

JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d

STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret

FB_SERVICE_KEY=your_firebase_admin_service_key
```

The repository provides an `.env.example` containing the server, MongoDB, JWT, Stripe, and Firebase Admin configuration fields.

**Never commit real credentials, API keys, database passwords, or Firebase service-account information to the repository.**

## Getting Started

### Prerequisites

Make sure you have installed:

* Node.js
* npm
* MongoDB
* Git

### Clone the Repository

```bash
git clone https://github.com/mrshanshuvo/carecamp-backend.git
cd carecamp-backend
```

### Install Dependencies

```bash
npm install
```

### Configure Environment Variables

Create a `.env` file:

```bash
cp .env.example .env
```

On Windows PowerShell, you can create the file manually and copy the required variables from `.env.example`.

Configure your MongoDB, JWT, Stripe, Firebase Admin, and client URL settings.

### Run the Development Server

```bash
npm run dev
```

The default server port is:

```text
http://localhost:5000
```

## Available Scripts

```bash
npm run dev
```

Starts the backend server.

```bash
npm run seed
```

Seeds application data.

```bash
npm run db:seed
```

Runs the database seed script.

```bash
npm run seed:users
```

Seeds user data.

```bash
npm run seed:data
```

Seeds application data.

```bash
npm run lint
```

Checks the project with ESLint.

```bash
npm run lint:fix
```

Automatically fixes applicable ESLint issues.

```bash
npm run format
```

Formats the project with Prettier.

```bash
npm run format:check
```

Checks Prettier formatting.

## Project Structure

```text
carecamp-backend/
├── api/
│   └── index.js
├── src/
│   ├── config/
│   │   ├── db.js
│   │   ├── env.js
│   │   ├── firebase.js
│   │   └── logger.js
│   ├── middlewares/
│   │   ├── auth.middleware.js
│   │   ├── errorHandler.js
│   │   ├── morgan.middleware.js
│   │   └── validate.middleware.js
│   ├── modules/
│   │   ├── analytics/
│   │   ├── auth/
│   │   ├── camps/
│   │   ├── feedback/
│   │   ├── notifications/
│   │   ├── payments/
│   │   ├── public/
│   │   ├── registrations/
│   │   └── users/
│   ├── app.js
│   └── server.js
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

## Frontend Integration

The backend serves as the API layer for the CareCamp frontend.

```text
┌─────────────────────────┐
│       CareCamp          │
│     React Frontend      │
└────────────┬────────────┘
             │
             │ REST API
             ↓
┌─────────────────────────┐
│   CareCamp Backend      │
│   Node.js + Express     │
└────────────┬────────────┘
             │
       ┌─────┴─────┐
       ↓           ↓
   MongoDB       Stripe
```

Authentication also integrates with Firebase Admin for server-side verification.

## Error Handling

The application includes centralized error handling and a dedicated not-found handler to provide consistent API error responses.

## Logging

The backend uses Morgan for HTTP request logging and Winston for application-level logging.

## Code Quality

The project uses:

* ESLint
* Prettier
* Husky
* lint-staged

These tools help maintain consistent formatting and code quality across the backend.

## Project Status

Active backend for the CareCamp medical camp management platform.

## License

This project is licensed under the MIT License.

## Author

**Shahid Hasan Shuvo**

Full Stack Developer
