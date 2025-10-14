# COOKie MVP Architecture

> **Target Launch**: January 20-27, 2026
> **Timeline**: October 14, 2025 - January 27, 2026 (15 weeks)
> **Scope**: Minimum viable product focused on core recipe management
> **Team**: Solo developer

---

## MVP Philosophy: Pragmatic Simplicity

**Guiding Principles**:
1. **Monolith First**: Start with modular monolith, not microservices
2. **Managed Services**: Use cloud-managed services to reduce operational overhead
3. **Manual Over Automated**: Accept manual processes where automation is complex
4. **Essential Features Only**: Ship core value, defer nice-to-haves
5. **Quality Over Quantity**: 250 great recipes > 500 mediocre ones

---

## MVP Feature Scope

### ✅ **In Scope (Must Have)**

**Core Features**:
- Recipe browsing and search (full-text + filters)
- Recipe detail page with KBJU
- User registration and authentication (email/password + OAuth)
- User favorites (bookmark recipes)
- Basic rating system (1-5 stars)
- Responsive web interface (mobile + desktop)

**Admin Features**:
- Admin panel for recipe management
- Recipe CRUD operations
- Moderation workflow (draft → published)
- Batch import tool for LLM-generated recipes

**Content**:
- **250-300 recipes at launch**
- **+50 new recipes per week post-launch**
- Accurate KBJU data (spot-checked by nutritionist)
- High-quality images (Perplexity AI + stock photos)

### ❌ **Out of Scope (Defer to Phase 2)**

- AI Nutritionist (too expensive for MVP)
- Meal planning (complex algorithm needed)
- Shopping lists
- B2B integrations
- Payment/subscriptions (all free for MVP)
- Gamification
- Native mobile apps (web-only, PWA later)
- Advanced analytics (use Google Analytics only)
- Automated web scraping (legal risks)

---

## Technology Stack

**Frontend**: Next.js 14, TailwindCSS, React Context + Zustand
**Backend**: ASP.NET Core 8 (C#), Entity Framework Core, Identity
**Database**: PostgreSQL (managed), Redis (managed)
**Storage**: Yandex Object Storage
**Infrastructure**: Yandex Cloud VMs (~10K ₽/month)
**Monitoring**: Sentry + Google Analytics + UptimeRobot

---

## Development Roadmap (15 Weeks)

### Phase 0: Setup & Planning (Weeks 1-2: Oct 14-27)

**Week 1 (Oct 14-20)**:
- [ ] Set up Yandex Cloud account
- [ ] Create GitHub repos (private)
- [ ] Set up local dev environment (.NET 8 SDK, Node.js, Docker)
- [ ] Initialize Next.js project

**Week 2 (Oct 21-27)**:
- [ ] Initialize ASP.NET Core 8 backend project
- [ ] Set up PostgreSQL + Redis locally (Docker Compose)
- [ ] Configure Entity Framework Core
- [ ] Configure CI/CD pipeline (GitHub Actions basic setup)
- [ ] Start content creation (Goal: 50 recipes by end of week)

---

### Phase 1: Core Backend (Weeks 3-6: Oct 28 - Nov 24)

**Week 3 (Oct 28 - Nov 3): Recipe Module Part 1**
- [ ] Recipe entity + EF Core model
- [ ] Recipe CRUD API endpoints
- [ ] Basic validation
- [ ] Continue content creation (Target: 100 total recipes)

**Week 4 (Nov 4-10): Recipe Module Part 2**
- [ ] Full-text search with PostgreSQL
- [ ] Filter and sort logic (cuisine, time, difficulty)
- [ ] Image upload to Object Storage
- [ ] Continue content creation (Target: 150 total recipes)

**Week 5 (Nov 11-17): User & Auth Module**
- [ ] User entity + EF Core model
- [ ] JWT authentication with ASP.NET Core Identity
- [ ] OAuth integration (Yandex, VK)
- [ ] Profile management
- [ ] Continue content creation (Target: 200 total recipes)

**Week 6 (Nov 18-24): Ratings & Favorites**
- [ ] Rating system (1-5 stars)
- [ ] Favorites logic
- [ ] Aggregation (avg rating, favorite count)
- [ ] Finish core content creation (Target: 250 recipes)

---

### Phase 2: Frontend (Weeks 7-10: Nov 25 - Dec 22)

**Week 7 (Nov 25 - Dec 1): Core Pages**
- [ ] Homepage (hero + popular recipes grid)
- [ ] Recipe search/browse page with filters
- [ ] Recipe detail page (ingredients, steps, KBJU, ratings)

**Week 8 (Dec 2-8): User Features**
- [ ] Registration/login flow
- [ ] OAuth buttons (Yandex, VK)
- [ ] User profile page
- [ ] Favorites page with filtering

**Week 9 (Dec 9-15): Admin Panel**
- [ ] Recipe CMS (create, edit, publish)
- [ ] Batch import tool (CSV/JSON from LLM)
- [ ] Admin dashboard (basic stats)
- [ ] Image upload UI

**Week 10 (Dec 16-22): Polish & SEO**
- [ ] Responsive design (mobile optimization)
- [ ] Loading states, error handling
- [ ] SEO optimization (meta tags, OpenGraph, sitemap)
- [ ] Performance optimization (lazy loading images)

---

### Phase 3: Content & Testing (Weeks 11-12: Dec 23 - Jan 5)

⚠️ **Holiday Period** - Flexible schedule, adjust as needed

**Week 11 (Dec 23-29)**: Content finalization, KBJU validation, image sourcing
**Week 12 (Dec 30 - Jan 5)**: Unit tests, integration tests, manual QA, performance testing

**Contingency**: If unavailable during holidays, content is already complete (Week 6), testing can be compressed to Week 13

---

### Phase 4: Pre-Launch (Weeks 13-14: Jan 6-19)

**Week 13 (Jan 6-12): Deployment & Beta**
- [ ] Deploy to Yandex Cloud production
- [ ] Configure custom domain + SSL
- [ ] Set up monitoring (Sentry, UptimeRobot, Google Analytics)
- [ ] Invite 20 beta testers
- [ ] Create feedback form

**Week 14 (Jan 13-19): Beta Testing & Polish**
- [ ] Collect feedback from beta testers
- [ ] Fix critical bugs and UX issues
- [ ] Performance optimization based on feedback
- [ ] Prepare launch materials
- [ ] Write launch announcement

---

### Phase 5: Public Launch (Week 15: Jan 20-27)

**Jan 20 (Monday)**: Soft Launch
- [ ] Remove beta invite restrictions
- [ ] Open to public
- [ ] Monitor error rates and performance

**Jan 21-22 (Tue-Wed)**: Marketing Launch
- [ ] Announce on social media (VK, Instagram, Telegram)
- [ ] Post in 10-15 VK cooking groups
- [ ] Submit to startup directories (vc.ru, habr.com)

**Jan 23-27 (Thu-Mon)**: Growth Week
- [ ] Daily monitoring of user acquisition
- [ ] Respond to user feedback
- [ ] Fix non-critical bugs
- [ ] Track progress toward 1000 users goal

**Post-Launch (Week 16+)**: Add +50 new recipes per week, iterate based on feedback

---

## Success Metrics

### Launch Week Goals (Jan 20-27)

- **250 registered users** (avg 35/day)
- **1,000+ recipe views** (avg 140/day)
- **50+ daily active users**
- **< 5 critical bugs** reported
- **90%+ uptime**

### First Month Goals (By Feb 27, 2026)

- **1,000 registered users**
- **15,000+ recipe views**
- **200+ daily active users by end of month**
- **Retention D7: 25%+**
- **NPS: 40+**
- **350-400 total recipes** (+50/week)

### When to Consider Phase 2

- ✅ 1,000+ users achieved
- Retention D7: 30%+
- NPS: 50+
- Consistent daily growth (10-20 new users/day organically)
- Positive user feedback on core features
- No major technical issues

---

## User Acquisition Strategy

### Week 1 (Jan 20-27): Target 250 Users

**Daily Actions**:
- **Morning** (30min): Post in 2-3 VK cooking groups
- **Afternoon** (30min): Engage in comments, answer questions
- **Evening** (30min): Share on personal social media

**Tactics**:
1. **VK Groups** (Primary channel): Identify 50+ relevant groups, post 2-3/day
2. **Personal Networks**: VK friends, Instagram stories, Telegram
3. **Beta Testers**: Ask to invite 2-3 friends each
4. **Incentive**: "First 500 users get lifetime free Premium access"

**Expected**: 100 VK + 80 personal + 40 beta testers + 30 word-of-mouth = 250 users

### Weeks 2-4 (Jan 28 - Feb 17): Target +400 Users (650 Total)

1. **SEO**: Recipe pages indexed, long-tail keywords (5-10 signups/week)
2. **VK Groups**: Continue posting with traction data (20-30 signups/week)
3. **User Referrals**: 20% invite a friend = 50 more
4. **Content Marketing**: 2-3 blog posts (10-20 signups)
5. **Community Engagement**: Answer questions in VK groups, link recipes

**Expected**: 150 VK + 100 SEO + 100 referrals + 50 content = +400 users

### Weeks 5+ (Feb 18 - Feb 27): Target +350 Users (1000 Total)

1. **Organic Growth**: SEO improves (20-30 signups/week), word-of-mouth compounds
2. **Optional Ads** (10-50K ₽): VK Ads or micro-influencers if budget available
3. **Continue All Above**: VK groups, content marketing, community engagement

**Expected**: 150 organic + 200 paid (if budget) OR +350 all organic = 1000 users

---

## Content Creation Strategy

### Recipe Generation Pipeline

**Tools**:
- Claude / ChatGPT for recipe text
- Perplexity AI for recipe images
- USDA FoodData Central for KБЖУ data
- Google Sheets for batch tracking

**Process Per Recipe** (~ 15-20 min):
1. **Generate text** (5 min): LLM prompt, review output
2. **Generate image** (3 min): AI generation or stock photo
3. **Calculate KБЖУ** (5 min): USDA database, spot-check with nutritionist
4. **Import to system** (2 min): Batch import tool
5. **Quality check** (5 min): Review on frontend

**Schedule**:
- **Weeks 2-6**: 50 recipes/week (3.5 recipes/day = 53min/day)
- **Post-Launch**: 50 recipes/week (7 recipes/day × 15min = 105min/day)

**Categories** (Total: 250 recipes):
- Завтраки: 30 | Супы: 25 | Основные блюда: 80
- Гарниры: 30 | Закуски: 30 | Десерты: 25
- Напитки/Смузи: 20 | Выпечка ПП: 10

---

## Architecture

### High-Level Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    Users (Web Browser)                   │
└─────────────────────┬───────────────────────────────────┘
                      │ HTTPS
                      ▼
┌─────────────────────────────────────────────────────────┐
│              Yandex Cloud Load Balancer                  │
└─────────────────────┬───────────────────────────────────┘
                      │
        ┌─────────────┴─────────────┐
        ▼                           ▼
┌────────────────┐          ┌────────────────┐
│   Web App      │          │   Admin Panel  │
│  (Next.js SSR) │          │   (React SPA)  │
└───────┬────────┘          └───────┬────────┘
        │                           │
        └─────────────┬─────────────┘
                      │ REST API
                      ▼
┌─────────────────────────────────────────────────────────┐
│      Backend Monolith (ASP.NET Core 8 C#)                │
│  ┌──────────────────────────────────────────────────┐   │
│  │ Modules:                                         │   │
│  │  - Recipe Module (CRUD, Search, Ratings)        │   │
│  │  - User Module (Auth, Profiles, Favorites)      │   │
│  │  - Admin Module (Moderation, CMS)               │   │
│  │  - Analytics Module (Basic events to GA)        │   │
│  └──────────────────────────────────────────────────┘   │
└───────────────────┬──────────────┬──────────────────────┘
                    │              │
        ┌───────────┴──────┐   ┌──┴─────────────┐
        ▼                  │   │                 ▼
┌────────────────┐         │   │      ┌────────────────┐
│   PostgreSQL   │         │   │      │  Redis Cache   │
│   (Managed)    │         │   │      │   (Managed)    │
└────────────────┘         │   │      └────────────────┘
                           │   │
                           ▼   ▼
                    ┌──────────────────┐
                    │  Object Storage  │
                    │ (Images, Assets) │
                    └──────────────────┘
```

### Technology Details

**Frontend**:
- Framework: Next.js 14 (App Router)
- Styling: TailwindCSS
- State Management: React Context + Zustand
- HTTP Client: Axios
- Form Handling: React Hook Form + Zod validation

**Backend**:
- Framework: ASP.NET Core 8 (C#)
- ORM: Entity Framework Core 8
- Validation: FluentValidation
- Authentication: ASP.NET Core Identity (JWT + OAuth)
- File Upload: IFormFile with custom middleware

**Database**:
- Primary DB: Yandex Managed PostgreSQL (2 vCPU, 4GB RAM, 50GB SSD)
- Cache: Yandex Managed Redis (1 vCPU, 2GB RAM)
- File Storage: Yandex Object Storage (S3-compatible, 100GB)

**Infrastructure**:
- Cloud: Yandex Cloud
- Compute: VM instances (2 vCPU, 4GB RAM)
- Load Balancer: Yandex Application Load Balancer
- DNS: Yandex Cloud DNS
- SSL: Let's Encrypt (free)

**Monitoring**:
- Errors: Sentry (free tier: 5K events/month)
- Analytics: Google Analytics 4
- Uptime: UptimeRobot (free tier)
- Logs: Yandex Cloud Logging (basic)

**CI/CD**:
- Version Control: GitHub (private repos)
- CI/CD: GitHub Actions
- Deployment: Docker containers on Yandex Compute Cloud

---

## Database Schema

### Core Tables

**users**
```sql
id, email, password_hash, username, first_name, avatar_url,
oauth_provider, oauth_id, email_verified, created_at
```

**recipes**
```sql
id, slug, title, description, cuisine, difficulty,
prep_time_minutes, cook_time_minutes, total_time_minutes, servings,
instructions (JSONB), nutrition_per_serving (JSONB),
dietary_tags, allergens, image_urls,
rating_avg, rating_count, view_count, favorite_count,
status, created_at, updated_at
```

**user_favorites**
```sql
user_id (FK), recipe_id (FK), created_at
PRIMARY KEY (user_id, recipe_id)
```

**user_ratings**
```sql
id, user_id (FK), recipe_id (FK), rating (1-5), review, created_at
UNIQUE (user_id, recipe_id)
```

**sessions**
```sql
id, user_id (FK), refresh_token, expires_at, created_at
```

### Indexes (Critical for Performance)

```sql
-- Recipes
CREATE INDEX idx_recipes_slug ON recipes(slug);
CREATE INDEX idx_recipes_status ON recipes(status);
CREATE INDEX idx_recipes_cuisine ON recipes(cuisine);
CREATE INDEX idx_recipes_rating ON recipes(rating_avg DESC, rating_count DESC);
CREATE INDEX idx_recipes_popularity ON recipes(view_count DESC, favorite_count DESC);
CREATE INDEX idx_recipes_total_time ON recipes(total_time_minutes);
CREATE INDEX idx_recipes_dietary_tags ON recipes USING GIN(dietary_tags);
CREATE INDEX idx_recipes_fulltext ON recipes USING GIN(to_tsvector('russian', title || ' ' || description));

-- Users
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_users_oauth ON users(oauth_provider, oauth_id);

-- Favorites
CREATE INDEX idx_favorites_user ON user_favorites(user_id);
CREATE INDEX idx_favorites_recipe ON user_favorites(recipe_id);

-- Ratings
CREATE INDEX idx_ratings_recipe ON user_ratings(recipe_id);
CREATE INDEX idx_ratings_user ON user_ratings(user_id);
```

---

## API Design

### Public Endpoints (No Auth)

```
GET /api/v1/recipes                    # Search/browse recipes
GET /api/v1/recipes/:slug              # Get recipe details
GET /api/v1/recipes/popular            # Top 20 popular recipes
GET /api/v1/recipes/cuisines           # List of cuisines
GET /health                            # Health check
```

### Authenticated Endpoints (JWT Required)

**Auth**:
```
POST /api/v1/auth/register             # Register with email
POST /api/v1/auth/login                # Login
POST /api/v1/auth/refresh              # Refresh access token
POST /api/v1/auth/logout               # Logout
GET  /api/v1/auth/oauth/:provider      # OAuth flow (Yandex, VK)
```

**User**:
```
GET  /api/v1/users/me                  # Get current user profile
PATCH /api/v1/users/me                 # Update profile
```

**Favorites**:
```
GET /api/v1/users/me/favorites         # Get user's favorites
POST /api/v1/recipes/:id/favorite      # Add to favorites
DELETE /api/v1/recipes/:id/favorite    # Remove from favorites
```

**Ratings**:
```
POST /api/v1/recipes/:id/rating        # Rate recipe
PATCH /api/v1/recipes/:id/rating       # Update rating
DELETE /api/v1/recipes/:id/rating      # Delete rating
```

### Admin Endpoints (Admin Role Required)

```
POST /api/v1/admin/recipes             # Create recipe
PATCH /api/v1/admin/recipes/:id        # Update recipe
DELETE /api/v1/admin/recipes/:id       # Delete recipe
POST /api/v1/admin/recipes/:id/publish # Publish recipe
GET /api/v1/admin/stats                # Dashboard stats
```

---

## Deployment

### Infrastructure Cost (MVP): ~10,000 ₽/month

- Compute: ~2,500 ₽/month (1 VM)
- PostgreSQL: ~4,000 ₽/month (managed)
- Redis: ~1,500 ₽/month (managed)
- Object Storage: ~300 ₽/month (100GB)
- Load Balancer: ~1,000 ₽/month
- Backup: ~500 ₽/month (daily, 7-day retention)

### Deployment Process

1. Local development (Docker Compose for DB)
2. Push to GitHub (feature branch)
3. GitHub Actions runs tests
4. Merge to main → auto-deploy to production
5. Docker image built and pushed to Yandex Container Registry
6. SSH to VM, pull new image, restart containers
7. Run database migrations
8. Health check

---

## Risk Assessment

| Risk | Impact | Mitigation | Status |
|------|--------|------------|--------|
| Solo dev delays | High | 15-week timeline with 1-week buffer | Mitigated |
| Content creation bottleneck | High | 250 recipes (not 500), clear pipeline, 15-20 min/recipe | Mitigated |
| Holiday disruption | Medium | Weeks 11-12 flexible, content done by Week 6 | Mitigated |
| Low user engagement | Critical | Beta testing, iterate on feedback, 1000 user strategy | Ongoing |
| Technical issues at launch | High | Thorough testing Weeks 12-14, staged rollout | Ongoing |
| Not reaching 1000 users | High | Detailed daily tactics, VK groups, SEO, referrals | Mitigated |
| Infrastructure costs exceed budget | Medium | Monitor daily, optimize queries, CDN for images | Ongoing |

**Overall Risk Level**: **LOW-MEDIUM**

---

## Next Immediate Steps

1. **Set up Yandex Cloud** (1 hour): Register, add payment method, explore console
2. **Create GitHub repos** (30 min): Private repos, branch protection
3. **Set up local dev** (2 hours): .NET 8 SDK, Node.js, Docker, docker-compose.yml
4. **Generate first 10 recipes** (3 hours): Test LLM prompt, refine process
5. **Plan weekly schedule** (1 hour): Block time for development and content creation

**Total time this week**: ~7.5 hours

---

## Weekly Checkpoints

**Week 2**: ✅ 50 recipes generated
**Week 4**: ✅ Backend API working (recipes CRUD)
**Week 6**: ✅ 250 recipes in database
**Week 8**: ✅ Frontend pages working
**Week 10**: ✅ Full UX flow works
**Week 12**: ✅ Testing complete
**Week 14**: ✅ Beta testing complete
**Week 15**: ✅ Public launch

---

## Post-Launch Roadmap

### Phase 2: Growth & Iteration (Feb - Mar)
- Add 50 recipes/week (reach 500+ by end March)
- Iterate based on user feedback
- Hit 5,000 users milestone

### Phase 3: Premium Features (Apr - May)
- Implement meal planning algorithm
- Integrate OpenAI for AI nutritionist
- Add payment (YooKassa)
- Launch Premium tiers (399₽/month)

### Phase 4: B2B Partnerships (June+)
- Approach X5 Group, ВкусВилл with traction data
- Negotiate integration partnerships
- Launch Pro tier with delivery integration

---

**Ready for development!**
