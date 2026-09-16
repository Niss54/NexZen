


<p align="center"> <img src="./public/part4.png" alt="NexZen Hackathon" width="560"> </p>

<p align="center"><strong>The Hackathon & Event Discovery Platform for Student Builders</strong></p>

<p align="center"><em>Discover. Apply. Build. Win.</em></p>

React (image) TypeScript (image) Vite (image) Tailwind CSS (image) Supabase (image) Framer Motion (image) Express (image) Vercel (image)

NexZen is a full-stack, monorepo web platform that connects student developers with hackathons and tech events — featuring discovery, filtering, team formation, multi-step applications, and a personal dashboard — all wrapped in a polished dark-glassmorphism design system.

🚀 Live Demo · 📖 Documentation · 🐛 Report a Bug · ✨ Request a Feature

🖼️ NexZen Visuals
<p align="center"> <img src="./public/nexzen-logo.png" alt="NexZen Logo" width="220"> </p>

<p align="center"> <img src="./public/part5.png" alt="NexZen Hackathon Logo" width="420"> </p>

<p align="center"> <img src="./public/nexzen-banner.png" alt="NexZen Banner" width="720"> </p>

Asset note: All README images are referenced from the existing public/ directory, so the README stays portable for GitHub and local clones.

📌 Table of Contents
About the Project

Key Features

Tech Stack

Project Architecture

Folder Structure

Getting Started

Prerequisites

Installation

Environment Variables

Running Locally

Available Scripts

Pages & Routes

UI Component Library

Data Models

Supabase Schema

API Endpoints

Design System

Deployment

Contributing

License

🎯 About the Project
NexZen solves a real problem for Indian student builders: hackathon discovery is fragmented. Students spend hours searching across LinkedIn, DevPost, and college WhatsApp groups trying to find events relevant to their skill level and domain.

NexZen brings everything into one place:

Browse hundreds of hackathons and tech events with rich detail pages

Filter by domain, mode (online/offline/hybrid), difficulty, prize pool, and status

Form or join a team with role-based matching

Complete a guided multi-step application with resume upload, project links, and domain selection

Track all activity from a personal dashboard — applications, teams, and saved events

The platform is built as a Supabase-ready monorepo with a mock data layer, making it immediately runnable without a backend while being production-deployable with a real Supabase project.

✨ Key Features
🔍 Discovery
Advanced hackathon search with multi-criteria filtering (domain, mode, difficulty, prize, status)

Event discovery across 7 categories: conferences, workshops, webinars, competitions, meetups, hackathons, challenges

Featured & trending section on the landing page with animated counters

👤 Auth & Profiles
Email/password signup and login with form validation (Zod + React Hook Form)

Google OAuth support (mock; pluggable via Supabase Auth)

Full user profiles: education, skills, domains, GitHub/LinkedIn/portfolio links, live projects

🏆 Hackathon Detail
Complete hackathon pages: prize breakdown, timeline, problem statements, judging criteria, rules, FAQs

Tiered sponsor showcase (Title / Gold / Silver / Technology / Education / Community / Media)

Registration status badge (Open / Closed / Upcoming)

📝 Multi-Step Applications
5-step guided application wizard:

Personal Info

Academic Details

Domains & Skills

Social Links & Projects

Resume Upload

Real-time step progress with Stepper component

👥 Team Management
Create teams with custom roles, domain matching, and size limits

Join teams via team listing page

View all your teams in a dedicated dashboard tab

🔔 Notifications
In-app notification system (application updates, team invites, hackathon reminders)

Notification context with read/unread state

📊 Dashboard
Personal stats: hackathons participated, wins

Recent applications with status tracking (Applied → Under Review → Shortlisted → Selected)

Saved hackathons and upcoming events at a glance

🎨 UI & UX
Dark glassmorphism design system with custom nexzen-* Tailwind tokens

Smooth page transitions and micro-animations via Framer Motion

Cursor follower effect on desktop

Skeleton loading states on all data-heavy pages

Fully responsive — desktop, tablet, and mobile

🛠 Tech Stack
Frontend
LayerTechnologyPurpose	

Framework	React 19	UI rendering
Language	TypeScript 6	Type safety across the entire codebase
Build Tool	Vite 8	Fast HMR dev server and optimized production builds
Routing	React Router v7	Client-side routing with lazy-loaded pages
State / Data	TanStack Query v5	Server state management and caching
Forms	React Hook Form + Zod	Schema-validated multi-step forms
Styling	Tailwind CSS v3	Utility-first CSS with custom design tokens
Animations	Framer Motion 13	Declarative animations and transitions
Icons	Lucide React	Consistent icon set
Date Handling	date-fns	Lightweight date formatting
Class Utilities	clsx + tailwind-merge	Conditional and conflict-free class merging
Backend Client	@supabase/supabase-js	Supabase auth and database access
Backend
LayerTechnologyPurpose	

Runtime	Node.js	JavaScript server environment
Framework	Express 5	HTTP server and middleware
Language	TypeScript	Type-safe server code
Database / Auth	Supabase (PostgreSQL)	Managed database, auth, and storage
Validation	Zod	Runtime schema validation
Security	Helmet	Secure HTTP headers
Rate Limiting	express-rate-limit	200 req / 15 min per IP
Dev Runner	tsx watch	TypeScript execution without compile step
Tooling & Infrastructure
ToolPurpose	
npm Workspaces	Monorepo management (client + server)
oxlint	Fast Rust-based linter (replaces ESLint)
Vitest	Unit and integration testing
concurrently	Run frontend + backend dev servers together
Vercel	Zero-config SPA deployment
🏗 Project Architecture
                    ┌─────────────────────────────────┐
                    │           Browser (SPA)         │
                    │    React 19 + Vite + TW CSS      │
                    └──────────────┬──────────────────┘
                                   │
              ┌────────────────────┼────────────────────┐
              │                   │                    │
    ┌─────────▼────────┐  ┌───────▼──────────┐  ┌─────▼───────────┐
    │  React Context   │  │  Service Layer   │  │  TanStack Query  │
    │  Auth · Notifs   │  │  auth.ts         │  │  Caching / Data  │
    └─────────┬────────┘  │  hackathons.ts   │  └─────────────────┘
              │            │  events.ts       │
              │            │  teams.ts        │
              │            │  applications.ts │
              │            └───────┬──────────┘
              │                    │
    ┌──────── ▼────────────────────▼ ─────────┐
    │           Express.js API Server         │
    │   Helmet · CORS · Rate Limit · Zod      │
    └──────────────────┬──────────────────────┘
                       │
    ┌──────────────────▼──────────────────────┐
    │                Supabase                 │
    │  Auth · PostgreSQL · Storage · Realtime │
    └─────────────────────────────────────────┘

📁 Folder Structure
NexZen/
├── src/                            # Main frontend application
│   ├── components/
│   │   ├── events/
│   │   │   └── EventCard.tsx       # Event listing card
│   │   ├── hackathons/
│   │   │   └── HackathonCard.tsx   # Hackathon listing card
│   │   ├── landing/
│   │   │   └── AnimatedCounter.tsx # Stats counter on hero section
│   │   ├── layout/
│   │   │   ├── Layout.tsx          # Root layout wrapper (Outlet)
│   │   │   ├── Navbar.tsx          # Top navigation bar
│   │   │   └── Footer.tsx          # Global footer
│   │   ├── sponsors/
│   │   │   └── SponsorCard.tsx     # Sponsor tier card
│   │   ├── teams/
│   │   │   └── TeamCard.tsx        # Team listing card
│   │   └── ui/                     # Reusable primitive components
│   │       ├── Accordion.tsx
│   │       ├── Badge.tsx
│   │       ├── Button.tsx
│   │       ├── CursorFollower.tsx
│   │       ├── EmptyState.tsx
│   │       ├── FileUpload.tsx
│   │       ├── Input.tsx
│   │       ├── Modal.tsx
│   │       ├── MultiSelect.tsx
│   │       ├── Skeleton.tsx
│   │       ├── Stepper.tsx
│   │       ├── Tabs.tsx
│   │       └── Toast.tsx
│   │
│   ├── context/
│   │   ├── AuthContext.tsx          # Global auth state (login/signup/logout)
│   │   └── NotificationsContext.tsx # In-app notification state
│   │
│   ├── data/                        # Mock / seed data (TypeScript)
│   │   ├── hackathons.ts            # Sample hackathon records
│   │   ├── events.ts                # Sample event records
│   │   ├── sponsors.ts              # Sample sponsor records
│   │   └── users.ts                 # Mock user accounts
│   │
│   ├── lib/
│   │   └── supabase.ts              # Supabase client initialisation
│   │
│   ├── pages/                       # Route-level page components (lazy-loaded)
│   │   ├── LandingPage.tsx
│   │   ├── HackathonsPage.tsx
│   │   ├── HackathonDetailPage.tsx
│   │   ├── ApplyPage.tsx            # Multi-step application wizard
│   │   ├── EventsPage.tsx
│   │   ├── EventDetailPage.tsx
│   │   ├── SponsorsPage.tsx
│   │   ├── DashboardPage.tsx
│   │   ├── ProfilePage.tsx
│   │   ├── EditProfilePage.tsx
│   │   ├── MyApplicationsPage.tsx
│   │   ├── MyTeamsPage.tsx
│   │   ├── SavedHackathonsPage.tsx
│   │   ├── CreateTeamPage.tsx
│   │   ├── JoinTeamPage.tsx
│   │   ├── LoginPage.tsx
│   │   ├── SignUpPage.tsx
│   │   ├── ForgotPasswordPage.tsx
│   │   ├── AboutPage.tsx
│   │   ├── ContactPage.tsx
│   │   ├── FAQPage.tsx
│   │   ├── TermsPage.tsx
│   │   ├── PrivacyPage.tsx
│   │   └── NotFoundPage.tsx
│   │
│   ├── services/                    # API / data-access layer
│   │   ├── auth.ts                  # Auth service (mock → swap with real API)
│   │   ├── hackathons.ts            # Hackathon CRUD
│   │   ├── events.ts                # Event CRUD
│   │   ├── teams.ts                 # Team management
│   │   ├── applications.ts          # Application submission & tracking
│   │   └── supabaseData.ts          # Supabase direct queries
│   │
│   ├── types/
│   │   └── index.ts                 # All shared TypeScript interfaces & enums
│   │
│   ├── utils/
│   │   └── index.ts                 # Date formatting, slug generation, helpers
│   │
│   ├── App.tsx                      # Root component with router + providers
│   ├── main.tsx                     # ReactDOM entry point
│   └── index.css                    # Global CSS + Tailwind directives
│
├── server/                          # Express.js API server
│   └── src/
│       └── index.ts                 # Server entry (middleware, health check)
│
├── client/                          # Alternate client workspace (npm workspaces)
│   └── src/
│       └── App.tsx
│
├── public/                          # Static assets
│   ├── favicon.svg
│   ├── icons.svg
│   ├── nexzen-logo.png
│   ├── nexzen-banner.png
│   ├── part1.png
│   ├── part2.png
│   ├── part3.png
│   ├── part4.png
│   └── part5.png
│
├── .env.example                     # Environment variable template
├── .gitignore
├── .oxlintrc.json                   # oxlint configuration
├── tailwind.config.js               # Tailwind + NexZen design tokens
├── vite.config.ts                   # Vite bundler configuration
├── tsconfig.json                    # TypeScript root config
├── tsconfig.app.json                # App-specific TS config
├── vercel.json                      # Vercel SPA rewrite rules
└── package.json                     # Monorepo root (npm workspaces)

🚀 Getting Started
Prerequisites
Make sure the following are installed on your machine:

Node.js >= 20.x — Download

npm >= 10.x — bundled with Node.js

Git — Download

A Supabase project is optional for local development. The app runs fully on mock data without it.

Installation
# 1. Clone the repository
git clone https://github.com/your-username/nexzen.git

# 2. Navigate into the project directory
cd nexzen

# 3. Install all dependencies (monorepo — installs root + client + server)
npm install

Environment Variables
Copy the example environment file and fill in your Supabase credentials:

cp .env.example .env

Open .env and set the following:

# ─── Supabase (required for live data; app works with mock data without these) ───
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-supabase-anon-key

# ─── Server ───────────────────────────────────────────────────────────────────
PORT=4000

Note: If VITE_SUPABASE_URL and VITE_SUPABASE_ANON_KEY are not provided, the app will automatically fall back to the built-in mock data. No errors, no crashes — it just works locally.

Running Locally
# Start both the Vite frontend (port 5173) and Express backend (port 4000)
npm run dev

The app will be available at http://localhost:5173

Demo Login Credentials (no Supabase required):

Email:    demo@nexzen.in
Password: password123

📜 Available Scripts
Run these from the monorepo root:

ScriptCommandDescription	

Dev (full stack)	npm run dev	Start frontend + backend concurrently
Build	npm run build	Production build via Vite
Type Check	npm run typecheck	Run tsc -b across the monorepo
Lint	npm run lint	Run oxlint on src/
Test	npm run test	Run Vitest test suite
Env Check	npm run setup:env	Verify all .env.example files exist
Run from server/ workspace:

ScriptCommandDescription	

Server Dev	npm run dev --workspace server	Start Express with tsx watch
Server Build	npm run build --workspace server	Compile TS to dist/
Server Start	npm run start --workspace server	Run compiled server
🗺 Pages & Routes
Public Routes (no login required)
RoutePageDescription	

/	Landing Page	Hero, stats, featured hackathons, CTA
/hackathons	Hackathons	Browse & filter all hackathons
/hackathons/:slug	Hackathon Detail	Full info: prizes, timeline, problem statements
/events	Events	Browse conferences, workshops, webinars
/events/:slug	Event Detail	Speaker lineup, agenda, registration
/sponsors	Sponsors	Tiered sponsor directory
/about	About	Team and mission
/contact	Contact	Contact form
/faq	FAQ	Accordion FAQ
/terms	Terms	Terms of service
/privacy	Privacy	Privacy policy
Auth Routes (redirect to dashboard if logged in)
RoutePageDescription	

/login	Login	Email/password + Google OAuth
/signup	Sign Up	Registration with validation
/forgot-password	Forgot Password	Password reset flow
Protected Routes (login required)
RoutePageDescription	

/hackathons/:slug/apply	Apply	5-step application wizard
/dashboard	Dashboard	Personal stats, recent activity
/profile/:id	Profile	Public user profile
/profile/edit	Edit Profile	Update personal, academic & social info
/my/applications	My Applications	Track all submitted applications
/my/teams	My Teams	View and manage your teams
/my/saved	Saved Hackathons	Bookmarked hackathons
/teams/create	Create Team	Form a new team for a hackathon
/teams/join	Join Team	Browse and join open teams
🧩 UI Component Library
All reusable components live in src/components/ui/. These are project-specific but designed to be composable:

ComponentDescription	
<Button />	Primary, secondary, ghost, danger variants with loading state
<Input />	Text input with label, error, and icon support
<Badge />	Status and category badges with color variants
<Modal />	Accessible modal dialog with overlay
<Tabs />	Horizontal tab switcher with active indicator
<Accordion />	Collapsible FAQ / content sections
<Toast />	Non-blocking notification toasts (success, error, info, warning)
<Skeleton />	Shimmer loading placeholder for all page layouts
<Stepper />	Step progress indicator for multi-step forms
<MultiSelect />	Searchable multi-option select for domains and skills
<FileUpload />	Drag-and-drop file upload with preview (resume / avatar)
<EmptyState />	Illustrated empty state for empty lists
<CursorFollower />	Glowing cursor follower effect (desktop only)
📐 Data Models
All TypeScript types are defined in src/types/index.ts.

Core Enums
type Mode              = 'online' | 'offline' | 'hybrid';
type Difficulty        = 'beginner' | 'intermediate' | 'advanced' | 'open';
type ApplicationStatus = 'applied' | 'under_review' | 'shortlisted' | 'selected' | 'rejected' | 'completed';
type TeamStatus        = 'open' | 'closed' | 'full';
type SponsorCategory   = 'title' | 'gold' | 'silver' | 'technology' | 'education' | 'community' | 'media';
type EventCategory     = 'conference' | 'workshop' | 'webinar' | 'competition' | 'meetup' | 'hackathon' | 'challenge';

Supported Domains (16 total)
Web Development · App Development · AI/ML · Data Science · Cybersecurity · IoT · Blockchain · Cloud Computing · UI/UX · Game Development · Robotics · Embedded Systems · AR/VR · DevOps · Software Development · Other

Key Interfaces
User

interface User {
  id: string;
  email: string;
  fullName: string;
  avatar?: string;
  mobile?: string;
  bio?: string;
  // Education
  college?: string;
  course?: string;  // B.Tech, BCA, MCA, etc.
  branch?: string;
  currentYear?: number;
  graduationYear?: number;
  city?: string; state?: string;
  // Skills
  domains: Domain[];
  skills: string[];
  // Social
  github?: string; linkedin?: string;
  instagram?: string; youtube?: string;
  portfolio?: string;
  liveProjects?: Project[];
  // Stats
  hackathonsParticipated?: number;
  hackathonsWon?: number;
  resumeUrl?: string;
}

Hackathon

interface Hackathon {
  id: string;
  name: string; slug: string;
  organizer: string;
  mode: Mode;
  location?: string;
  registrationDeadline: string;
  startDate: string; endDate: string;
  prizePool: string;
  prizeBreakdown: Prize[];
  minTeamSize: number; maxTeamSize: number;
  allowIndividual: boolean;
  domains: Domain[];
  difficulty: Difficulty;
  registrationStatus: 'open' | 'closed' | 'upcoming';
  problemStatements: ProblemStatement[];
  timeline: TimelineItem[];
  judgingCriteria: { criterion: string; weight: number }[];
  sponsors: Sponsor[];
  faqs: FAQItem[];
  isFeatured?: boolean;
}

Application

interface Application {
  id: string;
  hackathonId: string;
  userId: string;
  type: 'individual' | 'team';
  teamId?: string;
  status: ApplicationStatus;  // applied → under_review → shortlisted → selected
  appliedAt: string;
  submissionDeadline: string;
}

🗄 Supabase Schema
When connecting a real Supabase project, create the following tables. Enable Row Level Security (RLS) on all tables.

-- Users / Profiles
create table profiles (
  id           uuid references auth.users on delete cascade primary key,
  full_name    text,
  avatar_url   text,
  mobile       text,
  bio          text,
  college      text,
  course       text,
  branch       text,
  current_year int,
  domains      text[],
  skills       text[],
  github       text,
  linkedin     text,
  portfolio    text,
  resume_url   text,
  created_at   timestamptz default now()
);

-- Hackathons
create table hackathons (
  id                    uuid default gen_random_uuid() primary key,
  name                  text not null,
  slug                  text unique not null,
  organizer             text,
  mode                  text,         -- online | offline | hybrid
  registration_deadline timestamptz,
  start_date            timestamptz,
  end_date              timestamptz,
  prize_pool            text,
  registration_status   text,         -- open | closed | upcoming
  difficulty            text,
  domains               text[],
  is_featured           boolean default false,
  created_at            timestamptz default now()
);

-- Events
create table events (
  id                    uuid default gen_random_uuid() primary key,
  name                  text not null,
  slug                  text unique not null,
  organizer             text,
  category              text,
  mode                  text,
  date                  timestamptz,
  is_free               boolean default true,
  registration_status   text,
  domains               text[],
  is_featured           boolean default false,
  created_at            timestamptz default now()
);

-- Teams
create table teams (
  id              uuid default gen_random_uuid() primary key,
  name            text not null,
  hackathon_id    uuid references hackathons(id),
  leader_id       uuid references profiles(id),
  max_size        int default 4,
  status          text default 'open',  -- open | closed | full
  domains         text[],
  created_at      timestamptz default now()
);

-- Applications
create table applications (
  id                   uuid default gen_random_uuid() primary key,
  hackathon_id         uuid references hackathons(id),
  user_id              uuid references profiles(id),
  type                 text default 'individual',
  team_id              uuid references teams(id),
  status               text default 'applied',
  submission_deadline  timestamptz,
  applied_at           timestamptz default now(),
  updated_at           timestamptz default now()
);

🔌 API Endpoints
The Express server (server/src/index.ts) provides a foundation for backend routes. Current endpoints:

MethodEndpointDescription	

GET	/health	Health check — returns { status: 'ok', service: 'nexzen-server' }
GET	/	Root — returns { message: 'NEXZEN API is running.' }
Planned endpoints (add as you expand the backend):

MethodEndpointDescription	

POST	/api/auth/login	Authenticate user
POST	/api/auth/signup	Register new user
POST	/api/auth/forgot-password	Send reset email
GET	/api/hackathons	List hackathons with filters
GET	/api/hackathons/:slug	Get single hackathon
GET	/api/events	List events with filters
POST	/api/applications	Submit an application
GET	/api/users/:id/applications	Get user's applications
🎨 Design System
NexZen uses a custom dark design system defined in tailwind.config.js under the nexzen color namespace.

Color Tokens
TokenHexUsage	

nexzen-bg	#080B14	Page background
nexzen-surface	#0D1117	Elevated surface
nexzen-card	#111827	Card background
nexzen-accent	#6366F1	Primary actions, highlights
nexzen-violet	#8B5CF6	Secondary accent
nexzen-cyan	#06B6D4	Tertiary accent, tags
nexzen-pink	#EC4899	Warning, prizes
nexzen-green	#10B981	Success, open status
nexzen-yellow	#F59E0B	Warning, pending
nexzen-red	#EF4444	Error, closed status
nexzen-text	#F8FAFC	Primary text
nexzen-muted	#94A3B8	Secondary text
nexzen-subtle	#475569	Disabled / placeholder
Typography
Font (sans):   Inter, system-ui, -apple-system
Font (mono):   JetBrains Mono, Fira Code

Custom Animations
ClassEffect	
animate-fade-in	Opacity 0 → 1
animate-fade-up	Fade in from below
animate-pulse-glow	Pulsing glow ring
animate-float	Gentle up-down float
animate-shimmer	Skeleton loading shimmer
animate-border-glow	Animated glowing border
Background Utilities
bg-nexzen-gradient      /* Indigo → Violet → Cyan diagonal gradient */
bg-nexzen-gradient-dark /* Subtle dark overlay variant */
bg-glass                /* Glassmorphism base */
bg-grid-pattern         /* Subtle dot-grid pattern */

🖼️ Asset Paths
The README uses relative paths such as ./public/nexzen-logo.png and ./public/part4.png. Keep the image files inside the repository's public/ directory so GitHub and local clones resolve them correctly.

🚢 Deployment
Vercel (Recommended)
NexZen is pre-configured for Vercel. The vercel.json includes SPA rewrite rules so direct URL access works correctly.

# Install Vercel CLI
npm i -g vercel

# Deploy from project root
vercel

Set the following environment variables in your Vercel project dashboard:

VITE_SUPABASE_URL
VITE_SUPABASE_ANON_KEY

Manual Build
# Generate production build
npm run build

# Output is in /dist — serve with any static host
# (Netlify, Cloudflare Pages, GitHub Pages, S3, etc.)

🤝 Contributing
Contributions are welcome! Here's how to get started:

# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/your-username/nexzen.git

# 3. Create a feature branch
git checkout -b feature/your-feature-name

# 4. Make your changes and run checks
npm run typecheck
npm run lint
npm run test

# 5. Commit using conventional commits
git commit -m "feat: add filter by prize pool on hackathons page"

# 6. Push and open a Pull Request
git push origin feature/your-feature-name

Commit Convention: This project follows Conventional Commits.

feat:     New feature
fix:      Bug fix
docs:     Documentation only
style:    Formatting, no logic change
refactor: Code refactor
test:     Adding or updating tests
chore:    Build process or tooling

📄 License
This project is licensed under the MIT License. See the LICENSE file for details.

Made with ❤️ for student builders across India

⬆ Back to Top
