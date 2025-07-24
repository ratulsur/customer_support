# Support Feedback System

## Overview

This is a full-stack web application built for collecting and managing customer support feedback. The system provides a public form for feedback submission and an executive dashboard for data analysis using natural language queries. The application uses modern web technologies with a React frontend, Express backend, and PostgreSQL database with Drizzle ORM.

## User Preferences

Preferred communication style: Simple, everyday language.
Executive dashboard password: 0765 (secured access)

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **UI Library**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with custom design tokens and Microsoft-inspired color scheme
- **State Management**: TanStack Query (React Query) for server state management
- **Form Handling**: React Hook Form with Zod validation
- **Routing**: Wouter for lightweight client-side routing

### Backend Architecture
- **Runtime**: Node.js with TypeScript
- **Framework**: Express.js for REST API
- **Database ORM**: Drizzle ORM with PostgreSQL dialect
- **Database Provider**: Neon serverless PostgreSQL
- **Session Management**: Connect-pg-simple for PostgreSQL-backed sessions
- **Build System**: ESBuild for production bundling

### Key Components

#### Authentication System
- **Executive Access Control**: Password-protected access to executive dashboard using password "0765"
- **AuthGuard Component**: React component that protects executive dashboard access
- **Session Management**: Client-side authentication state management

#### Database Schema
- **Support Tickets**: Core entity storing feedback submissions with fields for date, name, request, feedback, status, and Airtable integration
- **Executive Queries**: Stores natural language queries and their SQL translations with results
- **Users**: Legacy table maintained for compatibility

#### API Endpoints
- `POST /api/feedback`: Submit new support tickets
- `GET /api/stats`: Retrieve dashboard statistics
- `POST /api/executive-query`: Process natural language queries and return SQL results

#### External Integrations
- **Google Sheets Service**: Bidirectional sync with Google Sheets for external workflow integration (replaced Airtable)
- **Groq AI Service**: Natural language to SQL conversion using AI models (fully functional)
- **Scheduler Service**: Automated sync between Google Sheets and local database

## Data Flow

1. **Public Form Submission**: Users submit feedback through the public form, which validates data using Zod schemas and stores it both locally and in Airtable
2. **Executive Dashboard**: Executives can view statistics and submit natural language queries that get converted to SQL and executed against the database
3. **Data Synchronization**: A background scheduler continuously syncs data between Airtable and the local PostgreSQL database
4. **Real-time Updates**: The frontend uses React Query for automatic cache invalidation and real-time data updates

## External Dependencies

### Required Environment Variables
- `DATABASE_URL`: PostgreSQL connection string (Neon serverless) ✓ Configured
- `GOOGLE_SHEETS_API_KEY`: Google Sheets API authentication (optional for sync)
- `GOOGLE_SHEETS_SPREADSHEET_ID`: Google Sheets spreadsheet identifier (optional for sync)
- `GOOGLE_SHEETS_SHEET_NAME`: Google Sheets tab name (optional for sync, defaults to "Support Tickets")
- `GROQ_API_KEY`: Groq AI API key for natural language processing ✓ Configured

### Third-Party Services
- **Neon Database**: Serverless PostgreSQL hosting ✓ Active
- **Google Sheets**: External workflow and data management (optional)
- **Groq**: AI-powered natural language to SQL conversion ✓ Active

## Deployment Strategy

### Development
- Vite dev server with HMR for frontend development
- TSX for running TypeScript server files directly
- Integrated development setup with shared types between client and server

### Production Build
- Frontend: Vite builds optimized static assets to `dist/public`
- Backend: ESBuild compiles TypeScript server code to `dist/index.js`
- Database: Drizzle migrations stored in `./migrations` directory

### Key Architectural Decisions

1. **Monorepo Structure**: Single repository with shared types between client, server, and database schema for type safety and consistency
2. **Drizzle ORM**: Chosen for type-safe database operations and excellent TypeScript integration
3. **Neon Serverless**: Selected for PostgreSQL compatibility with serverless deployment capabilities
4. **Shadcn/ui**: Provides accessible, customizable components with consistent design system
5. **TanStack Query**: Manages server state, caching, and synchronization without complex state management
6. **Dual Storage Strategy**: Local database for performance with Airtable sync for external workflow integration
7. **AI Integration**: Groq service enables natural language querying for non-technical users

The architecture prioritizes type safety, developer experience, and maintainability while providing a robust foundation for customer support data management and analysis.