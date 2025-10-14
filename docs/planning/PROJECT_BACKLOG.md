# COOKie Project - Development Backlog

> **Purpose**: Track development tasks organized by implementation phase (Frontend → Backend → Integration)
> **Last Updated**: 2025-10-15
> **Status**: Active - Frontend-First Development Strategy

---

## 📋 Overview

This backlog is organized by **development phase** to support a frontend-first approach:
1. **Frontend MVP Tasks** (Weeks 7-10) - Prioritized for immediate work
2. **Backend MVP Tasks** (Weeks 3-6) - Core API development
3. **Integration & Polish** (Weeks 10-12) - Connect frontend/backend, testing
4. **Post-MVP** - Phase 2+ features

---

## 🎨 Frontend MVP Tasks (Weeks 7-10)

### FRONT-001: Core Pages & Navigation (Week 7)
**Status**: Ready to Start
**Priority**: CRITICAL
**Phase**: MVP Week 7 (25 Nov - 1 Dec)
**Estimated Effort**: 5 days

**Description**:
Build core application pages and navigation structure using Next.js 14 App Router.

**Acceptance Criteria**:
- [ ] **Home Page** (`app/(main)/page.tsx`)
  - Hero section with search bar
  - Featured recipes grid (6-8 recipes)
  - Popular categories section
  - Responsive layout (mobile + desktop)
- [ ] **Recipes Search/Browse Page** (`app/(main)/recipes/page.tsx`)
  - Recipe grid with pagination
  - Filter sidebar (cuisine, difficulty, time, dietary tags)
  - Search bar with debouncing
  - Loading states & empty states
- [ ] **Recipe Detail Page** (`app/(main)/recipes/[slug]/page.tsx`)
  - Recipe header (title, image, rating, time, difficulty)
  - Ingredients list
  - Cooking steps (numbered)
  - Nutrition info panel (KBJU)
  - Favorite button (requires auth)
- [ ] **Global Navigation**
  - Header component (logo, nav links, auth buttons)
  - Footer component (links, social, copyright)
  - Mobile hamburger menu

**Components to Build**:
```typescript
components/
├── layout/
│   ├── Header.tsx
│   ├── Footer.tsx
│   └── MobileMenu.tsx
├── recipes/
│   ├── RecipeCard.tsx
│   ├── RecipeGrid.tsx
│   ├── RecipeFilters.tsx
│   ├── RecipeDetail.tsx
│   ├── NutritionInfo.tsx
│   ├── IngredientsList.tsx
│   └── CookingSteps.tsx
└── ui/
    ├── Button.tsx
    ├── Input.tsx
    ├── Card.tsx
    ├── Badge.tsx
    └── Spinner.tsx
```

**Tech Stack Used**:
- Next.js 14 App Router
- TailwindCSS for styling
- Lucide React for icons
- Mock data initially (JSON files)

**Dependencies**: None (can start immediately)

---

### FRONT-002: User Authentication Flow (Week 8)
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: MVP Week 8 (2-8 Dec)
**Estimated Effort**: 4 days

**Description**:
Implement authentication using NextAuth.js with email/password and OAuth providers.

**Acceptance Criteria**:
- [ ] **NextAuth.js Setup**
  - Configure `app/api/auth/[...nextauth]/route.ts`
  - Credentials provider (email + password)
  - OAuth providers: Yandex, VK
  - Session management with JWT
  - Refresh token handling
- [ ] **Login Page** (`app/(auth)/login/page.tsx`)
  - Email/password form (React Hook Form + Zod)
  - OAuth buttons (Yandex, VK)
  - "Forgot password" link
  - Redirect to previous page after login
- [ ] **Register Page** (`app/(auth)/register/page.tsx`)
  - Email, password, confirm password fields
  - Validation (Zod schema)
  - Terms & conditions checkbox
  - Redirect to onboarding or home
- [ ] **Auth Context/Store**
  - Zustand store or React Context for auth state
  - `useAuth` hook for accessing user data
  - Protected route HOC or middleware
- [ ] **Session Persistence**
  - Store JWT in httpOnly cookies
  - Axios interceptor for auth token
  - Auto-refresh on 401 errors

**Components to Build**:
```typescript
components/
├── forms/
│   ├── LoginForm.tsx
│   └── RegisterForm.tsx
└── ui/
    ├── Input.tsx (with error states)
    └── Modal.tsx (for auth modals)

stores/
└── useAuthStore.ts

lib/
└── api/
    ├── axiosClient.ts (with interceptors)
    └── auth.ts (login/register/logout methods)
```

**Tech Stack Used**:
- NextAuth.js v5
- React Hook Form + Zod
- Axios with interceptors
- Zustand for client-side auth state

**Dependencies**:
- Backend auth endpoints ready (BACK-003)
- Can use mock API initially

---

### FRONT-003: User Profile & Favorites (Week 8)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Week 8 (2-8 Dec)
**Estimated Effort**: 3 days

**Description**:
Build user profile management and favorites functionality.

**Acceptance Criteria**:
- [ ] **Profile Page** (`app/(main)/profile/page.tsx`)
  - Display user info (name, email, avatar)
  - Edit profile form (name, avatar upload)
  - Password change form
  - Account settings (email notifications)
- [ ] **Favorites Page** (`app/(main)/profile/favorites/page.tsx`)
  - Grid of favorited recipes
  - Filter/sort options
  - Remove from favorites
  - Empty state when no favorites
- [ ] **Favorite Button Component**
  - Heart icon (filled when favorited)
  - Optimistic UI updates
  - Auth required (redirect to login)
  - Toast notification on add/remove

**API Hooks**:
```typescript
hooks/api/
├── useUser.ts          // GET /api/v1/users/me
├── useUpdateUser.ts    // PATCH /api/v1/users/me
├── useFavorites.ts     // GET /api/v1/users/me/favorites
└── useFavorite.ts      // POST/DELETE /api/v1/recipes/:id/favorite
```

**Tech Stack Used**:
- TanStack Query for data fetching
- React Hook Form for profile editing
- Optimistic updates for favorites

**Dependencies**:
- Backend user/favorites endpoints (BACK-004, BACK-005)
- Authentication working (FRONT-002)

---

### FRONT-004: Recipe Rating System (Week 8)
**Status**: Not Started
**Priority**: MEDIUM
**Phase**: MVP Week 8 (2-8 Dec)
**Estimated Effort**: 2 days

**Description**:
Implement 5-star rating system for recipes.

**Acceptance Criteria**:
- [ ] **Rating Stars Component**
  - Display average rating (read-only)
  - Interactive stars for user rating
  - Show user's existing rating
  - Hover effects
- [ ] **Rating Submission**
  - Submit rating (1-5 stars)
  - Optional review text (Phase 2)
  - Update optimistically
  - Show success toast
- [ ] **Rating Display**
  - Average rating on recipe cards
  - Rating count ("4.5 (123 ratings)")
  - User's rating highlighted on detail page

**Components to Build**:
```typescript
components/recipes/
├── RatingStars.tsx      // Display + interactive
└── RatingDisplay.tsx    // Read-only with count
```

**API Hooks**:
```typescript
hooks/api/
├── useRating.ts         // GET user's rating for recipe
└── useSubmitRating.ts   // POST /api/v1/recipes/:id/rating
```

**Tech Stack Used**:
- TanStack Query with optimistic updates
- Lucide React for star icons

**Dependencies**:
- Backend rating endpoints (BACK-006)
- Authentication (FRONT-002)

---

### FRONT-005: Admin Panel - Recipe Management (Week 9)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Week 9 (9-15 Dec)
**Estimated Effort**: 5 days

**Description**:
Build admin panel for recipe CRUD operations and batch import.

**Acceptance Criteria**:
- [ ] **Admin Dashboard** (`app/admin/dashboard/page.tsx`)
  - Total recipes count
  - Published vs draft count
  - Recent activity
  - Quick actions
- [ ] **Recipe List** (`app/admin/recipes/page.tsx`)
  - Paginated table of all recipes
  - Filter by status (draft/published)
  - Search by title
  - Edit/delete actions
- [ ] **Recipe Create/Edit Form** (`app/admin/recipes/new/page.tsx`, `app/admin/recipes/[id]/edit/page.tsx`)
  - Title, slug, description
  - Cuisine, difficulty, times, servings
  - Ingredients (dynamic list)
  - Instructions (dynamic steps)
  - Nutrition values (KBJU)
  - Dietary tags, allergens
  - Image upload (Yandex Object Storage)
  - Status (draft/published)
  - Form validation with Zod
- [ ] **Batch Import Tool** (`app/admin/recipes/import/page.tsx`)
  - Upload CSV/JSON file
  - Preview imported recipes
  - Validate data
  - Import in batches
  - Show progress/errors

**Components to Build**:
```typescript
components/
├── admin/
│   ├── RecipeTable.tsx
│   ├── RecipeForm.tsx
│   ├── IngredientInput.tsx (dynamic list)
│   ├── InstructionInput.tsx (dynamic steps)
│   ├── ImageUpload.tsx
│   └── BatchImport.tsx
└── ui/
    ├── Table.tsx
    ├── Select.tsx
    ├── Textarea.tsx
    └── FileUpload.tsx
```

**API Hooks**:
```typescript
hooks/api/admin/
├── useRecipes.ts         // GET /api/v1/admin/recipes
├── useRecipe.ts          // GET /api/v1/admin/recipes/:id
├── useCreateRecipe.ts    // POST /api/v1/admin/recipes
├── useUpdateRecipe.ts    // PATCH /api/v1/admin/recipes/:id
├── useDeleteRecipe.ts    // DELETE /api/v1/admin/recipes/:id
├── usePublishRecipe.ts   // POST /api/v1/admin/recipes/:id/publish
└── useBatchImport.ts     // POST /api/v1/admin/recipes/batch
```

**Tech Stack Used**:
- React Hook Form (large forms)
- Zod schemas for validation
- TanStack Query mutations
- File upload to Yandex Object Storage

**Dependencies**:
- Backend admin endpoints (BACK-007)
- Admin role middleware
- Object Storage configured

---

### FRONT-006: Polish, SEO & Performance (Week 10)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Week 10 (16-22 Dec)
**Estimated Effort**: 5 days

**Description**:
Polish UI/UX, optimize SEO, and improve performance.

**Acceptance Criteria**:
- [ ] **Responsive Design**
  - Test all pages on mobile (320px - 768px)
  - Test on tablet (768px - 1024px)
  - Fix layout issues
  - Touch-friendly interactions
- [ ] **Loading & Error States**
  - Skeleton loaders for recipe cards
  - Spinner for page transitions
  - Error boundaries
  - Retry mechanisms
  - User-friendly error messages
- [ ] **SEO Optimization**
  - Dynamic meta tags (title, description, OG, Twitter)
  - Structured data (schema.org Recipe markup)
  - Sitemap.xml generation
  - robots.txt
  - Google Search Console setup
- [ ] **Performance**
  - Image optimization (next/image, lazy loading)
  - Code splitting (dynamic imports for heavy components)
  - Font optimization (next/font)
  - Minimize bundle size
  - Lighthouse score 90+ (Performance, SEO, Accessibility)
- [ ] **Accessibility**
  - Keyboard navigation
  - ARIA labels
  - Focus management
  - Screen reader testing

**Tasks**:
```typescript
// SEO
app/layout.tsx              // Root metadata
app/(main)/recipes/[slug]/page.tsx  // Dynamic recipe metadata

// Performance
- Implement lazy loading for recipe images
- Dynamic import for admin panel (not needed on main site)
- Optimize fonts (Inter variable font)

// Components
components/common/
├── LoadingState.tsx
├── ErrorMessage.tsx
├── ErrorBoundary.tsx
└── SkeletonLoader.tsx
```

**Tech Stack Used**:
- next/image for optimization
- next/font for font loading
- Next.js metadata API
- Lighthouse CI for testing

**Dependencies**:
- All core features completed
- Backend API stable

---

## 🔧 Backend MVP Tasks (Weeks 3-6)

### BACK-001: Project Setup & Infrastructure (Week 3)
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: MVP Week 3 (28 Oct - 3 Nov)
**Estimated Effort**: 3 days

**Description**:
Initialize ASP.NET Core 8 backend project with PostgreSQL and Redis.

**Acceptance Criteria**:
- [ ] ASP.NET Core 8 project created
- [ ] Entity Framework Core 8 configured
- [ ] PostgreSQL connection setup (local Docker)
- [ ] Redis connection setup (local Docker)
- [ ] FluentValidation integrated
- [ ] Serilog for logging
- [ ] docker-compose.yml for local dev (PostgreSQL + Redis)
- [ ] Seed data for development
- [ ] Swagger/OpenAPI documentation

**Dependencies**: None

---

### BACK-002: Recipe Entity & Database (Week 3)
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: MVP Week 3 (28 Oct - 3 Nov)
**Estimated Effort**: 2 days

**Description**:
Create Recipe entity model and database schema.

**Acceptance Criteria**:
- [ ] Recipe entity with all fields (title, slug, description, cuisine, difficulty, times, servings, instructions, nutrition, tags, allergens, images, ratings, counts, status, timestamps)
- [ ] EF Core migration created
- [ ] Database indexes (slug, status, cuisine, rating, popularity, dietary_tags, full-text search)
- [ ] Seed 10 test recipes

**Database Schema**:
```sql
recipes (
  id, slug, title, description, cuisine, difficulty,
  prep_time_minutes, cook_time_minutes, total_time_minutes, servings,
  instructions (JSONB), nutrition_per_serving (JSONB),
  dietary_tags, allergens, image_urls,
  rating_avg, rating_count, view_count, favorite_count,
  status, created_at, updated_at
)
```

**Dependencies**: BACK-001

---

### BACK-003: Authentication & User Management (Week 5)
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: MVP Week 5 (11-17 Nov)
**Estimated Effort**: 5 days

**Description**:
Implement authentication with ASP.NET Core Identity, JWT tokens, and OAuth.

**Acceptance Criteria**:
- [ ] User entity (id, email, password_hash, username, first_name, avatar_url, oauth_provider, oauth_id, email_verified, created_at)
- [ ] ASP.NET Core Identity integration
- [ ] JWT token generation/validation
- [ ] Refresh token mechanism
- [ ] OAuth integration (Yandex, VK providers)
- [ ] Password reset flow
- [ ] Email verification (optional for MVP)

**API Endpoints**:
```
POST /api/v1/auth/register
POST /api/v1/auth/login
POST /api/v1/auth/refresh
POST /api/v1/auth/logout
GET  /api/v1/auth/oauth/:provider
```

**Dependencies**: BACK-001, BACK-002

---

### BACK-004: Recipe CRUD API (Week 3-4)
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: MVP Weeks 3-4 (28 Oct - 10 Nov)
**Estimated Effort**: 4 days

**Description**:
Build public-facing recipe API endpoints.

**Acceptance Criteria**:
- [ ] GET /api/v1/recipes (search, filters, pagination, sorting)
  - Full-text search (PostgreSQL tsvector)
  - Filter by: cuisine, difficulty, max_time, dietary_tags
  - Sort by: rating, popularity, created_at
  - Pagination (page, per_page)
- [ ] GET /api/v1/recipes/:slug (single recipe details)
- [ ] GET /api/v1/recipes/popular (top 20)
- [ ] GET /api/v1/recipes/cuisines (list of cuisines)
- [ ] Response caching (Redis, 5 min TTL)
- [ ] Request validation (FluentValidation)
- [ ] Error handling middleware

**Tech Stack**:
- Entity Framework Core queries
- Redis caching layer
- FluentValidation for request DTOs

**Dependencies**: BACK-002

---

### BACK-005: Favorites & User Profile (Week 5-6)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Weeks 5-6 (11-24 Nov)
**Estimated Effort**: 3 days

**Description**:
Implement user favorites and profile management.

**Acceptance Criteria**:
- [ ] user_favorites table (user_id, recipe_id, created_at, PK composite)
- [ ] GET /api/v1/users/me (current user profile)
- [ ] PATCH /api/v1/users/me (update profile)
- [ ] GET /api/v1/users/me/favorites (user's favorite recipes)
- [ ] POST /api/v1/recipes/:id/favorite (add to favorites)
- [ ] DELETE /api/v1/recipes/:id/favorite (remove from favorites)
- [ ] Update favorite_count on recipes
- [ ] JWT middleware for protected routes

**Dependencies**: BACK-003, BACK-004

---

### BACK-006: Rating System (Week 6)
**Status**: Not Started
**Priority**: MEDIUM
**Phase**: MVP Week 6 (18-24 Nov)
**Estimated Effort**: 2 days

**Description**:
Implement recipe rating system (1-5 stars).

**Acceptance Criteria**:
- [ ] user_ratings table (id, user_id, recipe_id, rating 1-5, review text, created_at, UNIQUE user_id+recipe_id)
- [ ] POST /api/v1/recipes/:id/rating (submit rating)
- [ ] PATCH /api/v1/recipes/:id/rating (update rating)
- [ ] DELETE /api/v1/recipes/:id/rating (delete rating)
- [ ] Aggregate rating calculation (average, count)
- [ ] Update recipe.rating_avg and recipe.rating_count
- [ ] Background job for rating aggregation (optional)

**Dependencies**: BACK-003, BACK-004

---

### BACK-007: Admin API Endpoints (Week 6)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Week 6 (18-24 Nov)
**Estimated Effort**: 3 days

**Description**:
Build admin-only endpoints for recipe management.

**Acceptance Criteria**:
- [ ] Admin role in ASP.NET Core Identity
- [ ] Role-based authorization middleware
- [ ] POST /api/v1/admin/recipes (create recipe)
- [ ] PATCH /api/v1/admin/recipes/:id (update recipe)
- [ ] DELETE /api/v1/admin/recipes/:id (delete recipe)
- [ ] POST /api/v1/admin/recipes/:id/publish (publish draft)
- [ ] POST /api/v1/admin/recipes/batch (batch import from JSON/CSV)
- [ ] GET /api/v1/admin/stats (dashboard statistics)
- [ ] Image upload to Yandex Object Storage
- [ ] Validation for all fields

**Dependencies**: BACK-003, BACK-004

---

### BACK-008: Image Upload & Object Storage (Week 6)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Week 6 (18-24 Nov)
**Estimated Effort**: 2 days

**Description**:
Implement image upload to Yandex Object Storage.

**Acceptance Criteria**:
- [ ] Configure Yandex Object Storage SDK
- [ ] Image upload endpoint (POST /api/v1/upload/image)
- [ ] File validation (type, size limits)
- [ ] Generate unique filenames
- [ ] Return CDN URL
- [ ] Handle errors gracefully
- [ ] Set proper CORS headers

**Dependencies**: BACK-001

---

## 🔗 Integration & Testing (Weeks 10-12)

### INT-001: Frontend-Backend Integration (Week 10)
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: MVP Week 10 (16-22 Dec)
**Estimated Effort**: 3 days

**Description**:
Connect frontend to live backend API.

**Acceptance Criteria**:
- [ ] Update axios baseURL to backend URL
- [ ] Configure CORS on backend
- [ ] Test all API endpoints with frontend
- [ ] Fix authentication flow (JWT tokens)
- [ ] Test OAuth flows (Yandex, VK)
- [ ] Handle API errors gracefully
- [ ] Test pagination, search, filters
- [ ] Test image uploads
- [ ] Environment variables configured

**Dependencies**: All FRONT-* and BACK-* tasks completed

---

### INT-002: End-to-End Testing (Week 11-12)
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP Weeks 11-12 (23 Dec - 5 Jan)
**Estimated Effort**: 5 days

**Description**:
Comprehensive testing of entire application.

**Acceptance Criteria**:
- [ ] **Manual QA**: Test all user flows
  - Registration → Login → Browse recipes → View detail → Favorite → Rate → Logout
  - Admin: Login → Create recipe → Edit → Publish
- [ ] **Unit Tests**: Backend (80%+ coverage)
  - Service layer tests
  - Repository tests
- [ ] **Integration Tests**: API endpoints
  - Auth flow tests
  - Recipe CRUD tests
  - Favorites/ratings tests
- [ ] **Component Tests**: Frontend (key components)
  - RecipeCard, RecipeFilters, LoginForm
- [ ] **Performance Testing**:
  - Load test API (100 concurrent users)
  - Test DB query performance
  - Check N+1 query issues
- [ ] **Security Testing**:
  - SQL injection attempts
  - XSS prevention
  - CSRF tokens
  - Auth bypass attempts

**Dependencies**: INT-001

---

## 🔴 Critical Blockers (Phase 2+)

### CRIT-001: Define Formal Meal Planning Algorithm
**Status**: Not Started
**Priority**: HIGH
**Phase**: Phase 2 (Post-MVP)
**Estimated Effort**: 2-3 weeks

**Description**:
Formal specification of meal planning optimization algorithm (Phase 2 feature).

**Acceptance Criteria**:
- [ ] Define hard constraints (allergies, dietary restrictions, KBJU limits)
- [ ] Define soft constraints (variety, cost, preferences)
- [ ] Choose algorithm (Branch & Bound, Genetic, Constraint Programming, Greedy)
- [ ] Document complexity and performance characteristics
- [ ] Create pseudocode/flowchart
- [ ] Validate with test data

**Notes**: Start with simple greedy algorithm, optimize later.

---

### CRIT-002: Error Handling Documentation
**Status**: Not Started
**Priority**: MEDIUM
**Phase**: Before Production Deploy
**Estimated Effort**: 1 week

**Description**:
Comprehensive error handling strategy for all services.

**Acceptance Criteria**:
- [ ] Document error scenarios (timeouts, DB failures, external API failures)
- [ ] Define error codes/messages (RFC 7807 Problem Details)
- [ ] Create error handling diagrams
- [ ] Define retry policies (exponential backoff)
- [ ] Define circuit breaker thresholds
- [ ] Document fallback strategies
- [ ] Create error monitoring/alerting rules

---

### CRIT-003: Legal Review of Web Scraping
**Status**: Not Started
**Priority**: CRITICAL
**Phase**: Before Using Parser Service
**Estimated Effort**: 1-2 weeks
**Budget**: 30,000-50,000 ₽

**Description**:
Legal consultation for web scraping strategy.

**Acceptance Criteria**:
- [ ] Consult IT/IP lawyer
- [ ] Review robots.txt compliance
- [ ] Assess copyright risks
- [ ] Define legally safe practices
- [ ] Draft attribution policy
- [ ] Consider partnership agreements

**Blocker**: Cannot deploy Parser Service without legal clearance.

**Alternative**: Manual curation for MVP (recommended).

---

### CRIT-004: OpenAI API Cost Management
**Status**: Not Started
**Priority**: HIGH
**Phase**: Phase 2 (AI Features)
**Estimated Effort**: 1 week

**Description**:
Prevent unsustainable OpenAI API costs for AI nutritionist feature.

**Acceptance Criteria**:
- [ ] Calculate projected costs for scenarios
- [ ] Implement request caching (Redis)
- [ ] Define rate limits (e.g., 100 queries/day per Premium user)
- [ ] Implement cost tracking per user
- [ ] Set up budget alerts
- [ ] Research alternatives (Llama 3, YandexGPT)

**Notes**: Target AI costs < 20% of Premium revenue.

---

## 🟡 Post-MVP Features (Phase 2+)

### HIGH-001: Progressive Web App (PWA)
**Priority**: MEDIUM-HIGH
**Phase**: Q1 2026
**Effort**: 1 week (research)

**Description**: Explore PWA as interim solution before native apps.

---

### HIGH-002: KBJU Data Validation Process
**Priority**: HIGH
**Phase**: MVP Content Creation
**Effort**: 2 weeks
**Budget**: 50,000-70,000 ₽

**Description**: Hire nutritionist for KBJU validation to ensure accuracy.

---

### HIGH-003: Recipe Partnership Strategy
**Priority**: HIGH
**Phase**: MVP
**Effort**: 3-4 weeks

**Description**: Partner with food bloggers instead of scraping.

---

### MED-001: A/B Testing Framework
**Priority**: MEDIUM
**Phase**: Q1 2026
**Effort**: 1 week

**Description**: Feature flags and A/B testing for data-driven decisions.

---

### MED-002: SEO Optimization Strategy
**Priority**: MEDIUM
**Phase**: MVP Week 10
**Effort**: 1 week

**Description**: Optimize recipe pages for organic search traffic.

---

### MED-003: Referral Program
**Priority**: MEDIUM
**Phase**: Q1 2026
**Effort**: 1 week

**Description**: Referral system to reduce CAC.

---

## 🔵 Future Features (Year 2-3)

### LOW-001: Multi-language Support
**Priority**: LOW
**Phase**: Year 2-3
**Effort**: 2-3 weeks

**Description**: Add English for international expansion.

---

### LOW-002: Video Recipe Parsing
**Priority**: LOW
**Phase**: Year 2
**Effort**: 4-6 weeks
**Budget**: 100,000-200,000 ₽

**Description**: Extract recipes from TikTok/YouTube using ASR + NLP.

**Note**: Manual curation likely cheaper and more accurate for MVP.

---

### LOW-003: White-label B2B Solution
**Priority**: LOW
**Phase**: Year 3
**Effort**: 8-12 weeks

**Description**: Offer COOKie as white-label for retailers.

**Note**: Only pursue if B2C is stable.

---

## 📋 Completed Tasks

### ✅ DONE-001: Enhanced Project Documentation
**Completed**: 2025-10-13

**Outcome**:
- COOKie-description.md updated
- COOKie-requirements-v1.md created (100+ requirements)
- 7 PlantUML architecture diagrams

---

### ✅ DONE-002: C4 Architecture Diagrams
**Completed**: 2025-10-13

**Outcome**:
- System Context, Container, Component diagrams
- Sequence diagrams (2)
- Deployment diagram
- Enhanced database schema

---

### ✅ DONE-003: Frontend Technology Stack Definition
**Completed**: 2025-10-15

**Outcome**:
- FRONTEND_STACK.md created (1000+ lines)
- FRONTEND_FOLDER_STRUCTURE.md created (600+ lines)
- Tech stack finalized: Next.js 14, TypeScript, Zustand, TanStack Query, TailwindCSS, custom components
- All dependencies documented with justifications

---

### ✅ DONE-004: Repository Cleanup
**Completed**: 2025-10-15

**Outcome**:
- Russian documentation archived
- Cross-references updated
- GitHub Actions workflow updated

---

## 🗑️ Rejected / Won't Do

### ❌ REJECTED-001: Multiple Payment Gateways (MVP)
**Reason**: Over-engineering - YooKassa sufficient
**Date**: 2025-10-13

### ❌ REJECTED-002: Full ELK Stack (MVP)
**Reason**: Too heavy - use Yandex Cloud Logging + Sentry
**Date**: 2025-10-13

### ❌ REJECTED-003: ClickHouse Sharding (MVP)
**Reason**: Premature optimization - defer to Year 2
**Date**: 2025-10-13

---

## 📊 Backlog Metrics

**Frontend Tasks**: 6 (FRONT-001 to FRONT-006)
**Backend Tasks**: 8 (BACK-001 to BACK-008)
**Integration Tasks**: 2 (INT-001, INT-002)
**Critical Blockers**: 4 (Phase 2+)
**Post-MVP Features**: 6 (HIGH/MED/LOW priority)
**Completed**: 4
**Rejected**: 3

**Estimated MVP Effort**:
- Frontend: ~24 days
- Backend: ~20 days
- Integration/Testing: ~8 days
- **Total**: ~52 days (~10-11 weeks)

**Budget Implications**:
- Legal consultation: 30-50K ₽
- Nutritionist: 50-70K ₽
- OpenAI costs: Monitor in Phase 2
- **Total**: 80-120K ₽ (MVP)

---

## 📝 Backlog Management Guidelines

### When to Add Tasks
- Critical bugs during development
- Features descoped from sprint
- Technical debt identified
- User feedback feature requests

### When to Remove Tasks
- ✅ Completed → move to "Completed Tasks"
- ❌ No longer relevant → move to "Rejected"
- Merged with another task

### Priority Definitions
- **CRITICAL**: Blocks production or poses legal/financial risk
- **HIGH**: Important for product success, needed soon
- **MEDIUM**: Nice to have, improves but not essential
- **LOW**: Future enhancements, wait until mature

### Task Naming Convention
- `FRONT-XXX`: Frontend tasks
- `BACK-XXX`: Backend tasks
- `INT-XXX`: Integration tasks
- `CRIT-XXX`: Critical blockers
- `HIGH/MED/LOW-XXX`: Post-MVP features

---

## 🔗 Related Documentation

- [MVP Architecture](../architecture/MVP_ARCHITECTURE.md) - Complete MVP specification
- [Frontend Stack](../technical/FRONTEND_STACK.md) - Technology decisions
- [Frontend Folder Structure](../technical/FRONTEND_FOLDER_STRUCTURE.md) - Project organization
- [Requirements](../requirements/COOKie-requirements-v1.md) - Detailed requirements

---

**Last Updated**: 2025-10-15
**Next Review**: Weekly during MVP development

**End of Backlog**
