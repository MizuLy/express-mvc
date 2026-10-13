# Express MVC Folder Structure

A clean starting point for building Express.js APIs with a layered MVC-inspired folder structure. This repository is intended to help organize routes, controllers, services, middleware, validation, configuration, and tests as an application grows.

It is a structure/template project rather than a completed feature application. Most folders currently contain `.gitkeep` files so the layout can be copied and extended for a new API.

## Folder Structure

```text
express-folder-structure/
├── docs/                  # API and project documentation
│   └── API.md
├── prisma/                # Prisma schema and future migrations
│   └── schema.prisma
├── src/
│   ├── config/            # Environment and external-service configuration
│   ├── controllers/       # HTTP request handlers
│   ├── middlewares/       # Authentication, errors, uploads, and other middleware
│   ├── routes/            # Express route definitions
│   ├── services/          # Business logic and data-access orchestration
│   ├── utils/             # Shared helper functions
│   ├── validators/        # Zod request schemas
│   ├── app.js             # Express application setup
│   └── server.js          # Server entry point
├── tests/
│   ├── integration/       # API and end-to-end tests
│   └── unit/              # Focused unit tests
├── .env.example           # Environment-variable template
├── prisma.config.ts       # Prisma configuration
└── package.json
```

## Tech Stack

- Node.js and Express 5
- Prisma ORM with PostgreSQL
- Zod for request validation
- JWT, bcrypt, and cookie-parser for authentication building blocks
- Multer and Cloudinary for file-upload building blocks
- CORS, rate limiting, Morgan, and dotenv for common API concerns

## Getting Started

### Install dependencies

```bash
npm install
```

### Configure the environment

Copy `.env.example` to `.env` and provide the values needed by your application. Keep secrets out of version control.

```bash
cp .env.example .env
```

### Prepare Prisma (optional)

After configuring `DATABASE_URL`, generate the Prisma client and create a local migration when the schema contains models:

```bash
npx prisma generate
npx prisma migrate dev
```

### Run the server

```bash
npm run dev   # Development with Nodemon
npm start     # Direct Node.js start
```

## Scripts

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start `src/server.js` with automatic reloads. |
| `npm start` | Start the server with Node.js. |
| `npm test` | Placeholder; configure a test runner before using it. |

## Layering Guidelines

Routes should map URLs to controllers. Controllers should handle HTTP concerns and delegate business logic to services. Services should own reusable business and data-access logic. Validators should reject invalid input before it reaches application logic, while middleware should contain cross-cutting request behavior. Keep tests in the folder matching the behavior they exercise.
