# Hwalik (حوليك) - Saudi Home Services Platform

## Overview

Hwalik is a Saudi Arabian service marketplace platform that connects clients with professional technicians for home services. The platform supports Arabic (RTL) and follows Material Design principles with marketplace-specific patterns inspired by Airbnb, TaskRabbit, and Noon.com. Services include plumbing, electrical work, cleaning, AC maintenance, painting, and carpentry.

The application enables two user types:
- **Clients**: Browse technicians, request services, and manage service requests
- **Technicians**: Create profiles, receive service requests, and manage their work

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- React 18 with TypeScript
- Vite as build tool and development server
- Wouter for client-side routing (lightweight React Router alternative)
- TanStack Query (React Query) for server state management
- Shadcn/ui component library with Radix UI primitives
- Tailwind CSS for styling with custom design system

**Design System:**
- RTL-first approach with Arabic typography (Cairo font via Google Fonts)
- Custom color palette based on Material Design principles
- Light/dark mode support via CSS custom properties
- Responsive design with mobile-first breakpoints
- Custom hover/active elevation states for interactive elements

**State Management:**
- AuthContext for authentication state (user sessions stored in localStorage)
- TanStack Query for server data caching and synchronization
- No global state library required - leveraging React Query's built-in caching

**Component Organization:**
- Page components in `client/src/pages/`
- Reusable UI components in `client/src/components/`
- Shadcn/ui primitives in `client/src/components/ui/`
- Path aliases configured: `@/` for client source, `@shared/` for shared types

### Backend Architecture

**Technology Stack:**
- Node.js with Express.js
- TypeScript with ES modules
- In-memory storage (MemStorage class) - designed to be replaced with database
- Drizzle ORM configured for PostgreSQL (schema defined but database not yet connected)

**API Design:**
- RESTful endpoints under `/api` prefix
- JSON request/response format
- Zod schema validation for all inputs
- Error handling middleware with standardized error responses

**Current Storage Implementation:**
- MemStorage class implements IStorage interface
- Seeded with demo data for development
- All CRUD operations defined in storage interface
- Ready for database migration (Drizzle schema already defined)

**Planned Database Schema (Drizzle/PostgreSQL):**
- `users` table: Supports both clients and technicians (role-based)
- `technicians` table: Extended profile information for technician users
- `service_requests` table: Tracks service requests between clients and technicians
- UUID primary keys via `gen_random_uuid()`

### Authentication System

**Current Implementation:**
- Phone number + password authentication
- Simple session management via localStorage on client
- User registration supports dual roles (client/technician)
- AuthContext provides login/logout/register functions
- No JWT or session tokens implemented yet

**Security Considerations:**
- Passwords stored in plain text (should implement bcrypt hashing)
- No session expiration mechanism
- No CSRF protection
- Ready for enhancement with proper authentication middleware

### Routing Structure

**Client Routes:**
- `/` - Home page with hero, categories, how-it-works
- `/technicians` - Browse and filter technicians
- `/register` - User registration (client or technician)
- `/login` - User authentication
- `/request-service` - Create service request (requires technicianId param)
- `/client-dashboard` - Client's service request management
- `/technician-dashboard` - Technician's request management
- `/not-found` - 404 page

**API Routes:**
- `POST /api/users` - User registration (creates user and optionally technician profile)
- `POST /api/login` - User authentication
- `GET /api/technicians` - List all technicians (filterable by serviceType)
- `GET /api/technicians/:id` - Get technician details
- `POST /api/requests` - Create service request
- `GET /api/requests/client/:clientId` - Get client's requests
- `GET /api/requests/technician/:technicianId` - Get technician's requests
- `PATCH /api/requests/:id/status` - Update request status

### Development vs Production

**Development Mode:**
- Vite dev server with HMR (Hot Module Replacement)
- Middleware mode - Express serves Vite middleware
- Replit-specific plugins (cartographer, dev banner, error overlay)
- Source maps enabled

**Production Build:**
- Client: Vite builds to `dist/public`
- Server: esbuild bundles to `dist/index.js`
- Static file serving from build directory
- Environment detection via `NODE_ENV`

## External Dependencies

### UI Component Libraries
- **Radix UI**: Headless component primitives (dialogs, dropdowns, popovers, etc.)
- **Shadcn/ui**: Pre-built accessible components built on Radix
- **Lucide React**: Icon library
- **cmdk**: Command palette component
- **Embla Carousel**: Carousel component

### Styling & Design
- **Tailwind CSS**: Utility-first CSS framework
- **class-variance-authority**: Component variant management
- **clsx & tailwind-merge**: Conditional class name utilities
- **Google Fonts**: Cairo font family for Arabic typography

### Form Management
- **React Hook Form**: Form state and validation
- **@hookform/resolvers**: Validation resolver integration
- **Zod**: Schema validation library
- **drizzle-zod**: Drizzle ORM + Zod integration

### Data Fetching
- **TanStack Query (React Query)**: Server state management, caching, and synchronization

### Database (Configured but Not Connected)
- **Drizzle ORM**: TypeScript ORM for PostgreSQL
- **@neondatabase/serverless**: Serverless PostgreSQL driver
- **Drizzle Kit**: Database migrations and schema management
- PostgreSQL database connection ready via `DATABASE_URL` environment variable

### Routing
- **Wouter**: Lightweight React routing library (alternative to React Router)

### Session Management (Server)
- **connect-pg-simple**: PostgreSQL session store for Express (installed but not used yet)

### Development Tools
- **Vite**: Build tool and dev server
- **esbuild**: Fast JavaScript bundler for server build
- **tsx**: TypeScript execution for development
- **TypeScript**: Type safety across frontend and backend

### Date Handling
- **date-fns**: Date utility library

### Replit Integration
- **@replit/vite-plugin-runtime-error-modal**: Development error overlay
- **@replit/vite-plugin-cartographer**: Code mapping plugin
- **@replit/vite-plugin-dev-banner**: Development banner

### Build & Development
- Scripts defined: `dev`, `build`, `start`, `check`, `db:push`
- Shared TypeScript configuration across client and server
- Path aliases for clean imports