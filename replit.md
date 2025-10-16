# Ocean Pollution Escape Room - Educational Game

## Overview

This is an educational escape room game focused on ocean pollution awareness. The application features six interactive mini-games that teach players about marine environmental issues including plastic pollution, microplastics, oil spills, coral reef restoration, sea turtle rescue, and sustainable alternatives to single-use plastics. Built as a full-stack web application, it combines an Express.js backend with a vanilla JavaScript frontend game experience, while also including React/Vite infrastructure for potential future enhancements.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Dual Frontend Approach:**
- **Primary Game Interface**: Vanilla JavaScript-based game (`/client/public/game.html`) with custom CSS and modular game components
- **React Shell**: React application that serves primarily as a redirect layer to the vanilla JS game, with infrastructure in place for future React-based features

**Rationale**: The vanilla JavaScript approach was chosen for the main game to provide direct DOM manipulation and simpler game logic without framework overhead. The React infrastructure remains available for future admin panels, user dashboards, or progressive enhancement.

**Game Architecture**:
- Component-based mini-game system with six independent game modules (plastic sorting, straw quiz, turtle rescue, microplastic measurement, oil spill cleanup, coral reef restoration)
- Centralized game controller managing state, progress tracking, and screen transitions
- Modular utility systems for audio management, local storage, timer/scoring, and leaderboard functionality

### Backend Architecture

**Express.js Server with Vite Integration:**
- Development mode: Vite middleware serves frontend with HMR (Hot Module Reload)
- Production mode: Static file serving from compiled assets
- Server-side structure prepared for API routes but currently minimal implementation

**Storage Strategy:**
- **In-Memory Storage**: Current implementation uses `MemStorage` class for user data
- **Database Schema**: Drizzle ORM configured with PostgreSQL schema defined but not actively used
- **Client Storage**: Browser LocalStorage for game progress, scores, and leaderboard data

**Rationale**: The in-memory storage provides rapid development without database dependencies. The PostgreSQL/Drizzle infrastructure is pre-configured for easy migration when persistent storage becomes necessary.

### Data Management

**Database Design (Prepared, Not Active):**
- Drizzle ORM with PostgreSQL dialect configured
- Schema location: `shared/schema.ts`
- Migration directory: `./migrations`
- Current schema includes basic user table with username/password fields

**Client-Side State:**
- Game progress stored in localStorage with versioning (`GameStorage` utility)
- Leaderboard data persisted locally per game type
- Audio preferences and UI state managed in-memory

**Rationale**: LocalStorage provides immediate persistence without server dependency, suitable for a single-player educational game. Database infrastructure ready for multiplayer or cloud-sync features.

### Build and Development Pipeline

**Bundling Strategy:**
- Vite for frontend asset bundling and development server
- esbuild for server-side code compilation
- PostCSS with Tailwind CSS for styling (configured but primarily used in React components)

**Development Workflow:**
- `npm run dev`: Runs development server with Vite HMR
- `npm run build`: Compiles both frontend (Vite) and backend (esbuild) for production
- `npm run start`: Serves production build

**Rationale**: Vite provides fast HMR and optimized production builds. esbuild handles server compilation efficiently. The dual-build process ensures both client and server are production-ready.

### UI Component System

**Shadcn/ui Component Library:**
- Radix UI primitives wrapped with Tailwind styling
- Comprehensive component collection (40+ components) available but minimally used in current vanilla JS game
- Design system based on CSS custom properties for theming

**Rationale**: The component library is infrastructure for future React-based features (admin panels, user profiles). The vanilla game uses custom CSS for performance and simplicity.

### Styling Architecture

**CSS Strategy:**
- Custom CSS for vanilla game (`/client/public/css/game.css`) with ocean-themed animations and effects
- Tailwind CSS configured for React components with custom theme extensions
- CSS custom properties for consistent theming across both approaches

**Rationale**: Separation allows the game to maintain lightweight styling while providing a robust design system for future features.

## External Dependencies

### Database and Storage
- **@neondatabase/serverless**: PostgreSQL serverless driver (configured for Neon Database)
- **Drizzle ORM**: Type-safe database toolkit with PostgreSQL dialect
- **connect-pg-simple**: Session store for PostgreSQL (installed but not implemented)

### Frontend Framework and Libraries
- **React 18**: UI library (minimal usage, primarily for redirect)
- **Vite**: Build tool and development server
- **@react-three/fiber & @react-three/drei**: 3D rendering libraries (installed, potentially for future 3D ocean visualizations)
- **@tanstack/react-query**: Server state management (configured but not actively used)

### UI Component Dependencies
- **Radix UI**: Headless UI component primitives (extensive collection)
- **Tailwind CSS**: Utility-first CSS framework
- **class-variance-authority & clsx**: Component variant and className utilities

### Development and Build Tools
- **TypeScript**: Type safety across the stack
- **tsx**: TypeScript execution for development
- **esbuild**: JavaScript/TypeScript bundler for server code
- **vite-plugin-glsl**: GLSL shader support (for potential 3D features)

### Utility Libraries
- **zod**: Schema validation (used with Drizzle)
- **date-fns**: Date manipulation utilities
- **nanoid**: Unique ID generation

### Audio and Media
- Asset support configured for GLTF/GLB models and various audio formats (MP3, OGG, WAV)
- No external audio library; uses native Web Audio API through custom `AudioManager` class

**Note**: Several dependencies appear to be prepared for future features (3D rendering, session management, advanced state management) but are not actively used in the current vanilla JavaScript game implementation.