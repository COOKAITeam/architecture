# COOKie MVP Architecture - REVISED (Realistic Timeline)

> **Target Launch**: January 20-27, 2026 ⭐ **REVISED** (Added 1 week buffer)
> **Timeline**: October 14, 2025 - January 27, 2026 (15 weeks total)
> **Scope**: Minimum viable product focused on core recipe management
> **Team**: Solo developer
> **Last Updated**: 2025-10-13
> **Status**: Ready for development

---

## 🔄 What Changed (Revisions Based on Weak Points)

### ✅ **Timeline Adjustments**
- **Old**: Jan 13-19 launch (14 weeks)
- **New**: Jan 20-27 launch (15 weeks)
- **Reason**: Buffer for holidays + realistic solo dev pace
- **Impact**: Less stress, higher quality, accounts for New Year break

### ✅ **Recipe Target Reduced**
- **Old**: 500-1000 recipes at launch
- **New**: 250-300 recipes at launch, +50/week post-launch
- **Reason**: Quality over quantity, LLM generation takes time
- **Impact**: Achievable goal, allows iteration based on feedback

### ✅ **Content Creation Strategy**
- **Old**: All content by launch
- **New**: MVP content + continuous growth plan
- **Benefit**: Can launch sooner, improve based on user preferences

### ✅ **Holiday Contingency**
- **Old**: No explicit holiday plan
- **New**: Weeks 11-12 flexibility, start content early
- **Impact**: Realistic expectations for New Year period

### ✅ **User Acquisition Enhanced**
- **Old**: Basic strategy
- **New**: Detailed tactics with daily actions
- **Impact**: Clear path to 1000 users in 1 month

---

## MVP Philosophy: Pragmatic Simplicity

**Guiding Principles**:
1. **Monolith First**: Start with modular monolith, not microservices
2. **Managed Services**: Use cloud-managed services to reduce operational overhead
3. **Manual Over Automated**: Accept manual processes where automation is complex
4. **Essential Features Only**: Ship core value, defer nice-to-haves
5. **Quality Over Quantity**: 250 great recipes > 500 mediocre ones ⭐ NEW

---

## MVP Feature Scope (REVISED)

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
- Batch import tool for LLM-generated recipes ⭐ NEW

**Data (REVISED)**:
- ✅ **250-300 manually curated recipes at launch** (REVISED from 500-1000)
- ✅ **+50 new recipes per week post-launch**
- Accurate KBJU data (spot-checked by nutritionist)
- High-quality images (Perplexity AI + stock photos)

**Why 250-300 is sufficient**:
- Enough variety for users to explore
- Manageable for solo dev + LLM workflow
- Quality-focused (well-tested, accurate KBJU)
- Allows faster launch
- Can grow based on actual user preferences

### ❌ **Out of Scope (Defer to Phase 2)**

**Deferred Features**:
- ❌ AI Nutritionist (too expensive for MVP)
- ❌ Meal planning (complex algorithm needed - see BACKLOG)
- ❌ Shopping lists
- ❌ B2B integrations (no retailers yet)
- ❌ Payment/subscriptions (all free for MVP)
- ❌ Gamification
- ❌ Native mobile apps (web-only, PWA later)
- ❌ Advanced analytics (use Google Analytics only)
- ❌ Automated web scraping (legal risks - see BACKLOG)

---

## Technology Stack (MVP)

**Frontend**: Next.js 14, TailwindCSS, React Context + Zustand
**Backend**: ASP.NET Core 8 (C#), Entity Framework Core, Identity
**Database**: PostgreSQL (managed), Redis (managed)
**Storage**: Yandex Object Storage
**Infrastructure**: Yandex Cloud VMs (~10K ₽/month)
**Monitoring**: Sentry + Google Analytics + UptimeRobot

---

## REVISED Development Roadmap (15 Weeks)

### Phase 0: Setup & Planning (Weeks 1-2: Oct 14-27)

**Week 1 (Oct 14-20)**:
- [x] Architecture documentation completed
- [ ] Set up Yandex Cloud account
- [ ] Create GitHub repo (private)
- [ ] Set up local dev environment (Node.js, Docker)
- [ ] Initialize Next.js project (use your React template)

**Week 2 (Oct 21-27)**:
- [ ] Initialize ASP.NET Core 8 backend project
- [ ] Set up PostgreSQL + Redis locally (Docker Compose)
- [ ] Configure Entity Framework Core
- [ ] Configure CI/CD pipeline (GitHub Actions basic setup)
- [ ] **Start content creation** (Goal: 50 recipes by end of week) ⭐ NEW

---

### Phase 1: Core Backend (Weeks 3-6: Oct 28 - Nov 24)

**Week 3 (Oct 28 - Nov 3): Recipe Module Part 1**
- [ ] Recipe entity + EF Core model
- [ ] Recipe CRUD API endpoints
- [ ] Basic validation
- [ ] **Continue content creation** (Target: 100 total recipes) ⭐

**Week 4 (Nov 4-10): Recipe Module Part 2**
- [ ] Full-text search with PostgreSQL
- [ ] Filter and sort logic (cuisine, time, difficulty)
- [ ] Image upload to Object Storage
- [ ] **Continue content creation** (Target: 150 total recipes) ⭐

**Week 5 (Nov 11-17): User & Auth Module**
- [ ] User entity + EF Core model
- [ ] JWT authentication with ASP.NET Core Identity
- [ ] OAuth integration (Yandex, VK)
- [ ] Profile management
- [ ] **Continue content creation** (Target: 200 total recipes) ⭐

**Week 6 (Nov 18-24): Ratings & Favorites**
- [ ] Rating system (1-5 stars)
- [ ] Favorites logic
- [ ] Aggregation (avg rating, favorite count)
- [ ] **Finish core content creation** (Target: 250 recipes) ⭐✅

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
- [ ] Batch import tool (CSV/JSON from LLM) ⭐ NEW
- [ ] Admin dashboard (basic stats)
- [ ] Image upload UI

**Week 10 (Dec 16-22): Polish & SEO**
- [ ] Responsive design (mobile optimization)
- [ ] Loading states, error handling
- [ ] SEO optimization (meta tags, OpenGraph, sitemap)
- [ ] Performance optimization (lazy loading images)

---

### Phase 3: Content & Testing (Weeks 11-12: Dec 23 - Jan 5) ⚠️ HOLIDAY PERIOD

**Week 11 (Dec 23-29): Content Finalization** 🎄 *Holiday Week*
- [ ] **Option A**: Light work - final recipe polishing (if working)
- [ ] **Option B**: Take break, resume after New Year
- [ ] Validate KBJU for sample recipes (nutritionist spot check)
- [ ] Source additional images if needed (Perplexity AI)
- [ ] Write compelling recipe descriptions

**Week 12 (Dec 30 - Jan 5): Testing** 🎆 *New Year Week*
- [ ] **Option A**: Resume testing after Jan 2-3
- [ ] Unit tests (critical paths: auth, recipe CRUD)
- [ ] Integration tests (API endpoints)
- [ ] Manual QA (test all user flows)
- [ ] Performance testing (simulate 100 concurrent users)
- [ ] Fix any critical bugs found

**⚠️ Contingency Plan**:
- If you can't work during holidays: Weeks 11-12 become buffer
- Content should already be at 250 recipes by Week 6
- Testing can be compressed to Week 13 if needed

---

### Phase 4: Pre-Launch (Week 13-14: Jan 6-19) ⭐ EXTENDED

**Week 13 (Jan 6-12): Deployment & Beta**
- [ ] Deploy to Yandex Cloud production
- [ ] Configure custom domain + SSL (Let's Encrypt)
- [ ] Set up monitoring (Sentry, UptimeRobot, Google Analytics)
- [ ] Invite 20 beta testers (friends, family, target audience)
- [ ] Create feedback form (Google Forms or Typeform)

**Week 14 (Jan 13-19): Beta Testing & Polish**
- [ ] Collect feedback from beta testers
- [ ] Fix critical bugs and UX issues
- [ ] Add any missing critical features
- [ ] Performance optimization based on beta feedback
- [ ] Prepare launch materials (social media posts, screenshots)
- [ ] Write launch announcement

---

### Phase 5: Public Launch (Week 15: Jan 20-27) ⭐ REVISED TARGET

**Jan 20 (Monday): Soft Launch**
- [ ] Remove beta invite restrictions
- [ ] Open to public (no marketing yet)
- [ ] Monitor error rates and performance
- [ ] Fix any critical issues immediately

**Jan 21-22 (Tue-Wed): Marketing Launch**
- [ ] Announce on personal social media (VK, Instagram, Telegram)
- [ ] Post in 10-15 VK cooking groups
- [ ] Submit to Russian startup directories (vc.ru, habr.com)
- [ ] Reach out to micro-influencers (if budget available)

**Jan 23-27 (Thu-Mon): Growth Week**
- [ ] Daily monitoring of user acquisition
- [ ] Respond to all user feedback quickly
- [ ] Fix non-critical bugs
- [ ] Post 2-3 more times in VK groups
- [ ] Track progress toward 1000 users goal

**Post-Launch (Week 16+): Ongoing**
- [ ] Add +50 new recipes per week
- [ ] Daily monitoring of metrics (DAU, retention)
- [ ] Iterate based on user feedback
- [ ] Plan Phase 2 features based on data

---

## Revised Success Metrics

### Launch Week Goals (Jan 20-27) ⭐ REVISED

- **250 registered users** (avg 35/day)
- **1,000+ recipe views** (avg 140/day)
- **50+ daily active users**
- **< 5 critical bugs** reported
- **90%+ uptime**

### First Month Goals (By Feb 27, 2026)

- ✅ **1,000 registered users** (your target)
- **15,000+ recipe views**
- **200+ daily active users by end of month**
- **Retention D7: 25%+**
- **NPS: 40+**
- **350-400 total recipes** (+50/week × 2-3 weeks)

### When to Consider Phase 2 (Premium Features)

- ✅ 1,000+ users achieved
- Retention D7: 30%+
- NPS: 50+
- Consistent daily growth (10-20 new users/day organically)
- Positive user feedback on core features
- No major technical issues

---

## Detailed Strategy to Achieve 1000 Users ⭐ ENHANCED

### Week 1 (Jan 20-27): Target 250 Users

**Daily Actions**:
- **Morning** (30min): Post in 2-3 VK cooking groups with unique message
- **Afternoon** (30min): Engage in comments, answer questions
- **Evening** (30min): Share on personal social media, DM friends

**Tactics**:
1. **VK Groups** (Primary channel):
   - Identify 50+ relevant groups: "Правильное питание", "Рецепты", "ПП рецепты"
   - Post schedule: 2-3 groups/day (avoid spam bans)
   - Message format: "Запустил сервис COOKie - 250 рецептов с КБЖУ. Бесплатно. Буду рад фидбеку! [link]"

2. **Personal Networks**:
   - VK friends (1000+ friends = potential 50-100 signups)
   - Instagram stories (if you have cooking-interested followers)
   - Telegram channels/groups you're in

3. **Beta Testers**:
   - Ask 20 beta testers to invite 2-3 friends each = 40-60 more users

4. **Word of Mouth**:
   - Encourage signups with value: "First 500 users get lifetime free access to Premium when we launch it"

**Expected Result**: 250 users (100 from VK groups + 80 from personal + 40 from beta testers + 30 from word-of-mouth)

---

### Weeks 2-4 (Jan 28 - Feb 17): Target +400 Users (650 Total)

**Tactics**:
1. **SEO Starts Working**:
   - Recipe pages indexed by Google/Yandex
   - Long-tail keywords: "[блюдо] рецепт калории"
   - Estimated: 50-100 organic visitors/week = 5-10 signups

2. **VK Groups (Continued)**:
   - Post in 3-4 groups/day (now with traction data)
   - Message: "COOKie - уже 250+ пользователей используют для поиска рецептов с КБЖУ"
   - Estimated: 20-30 signups/week

3. **User Referrals**:
   - First 250 users are engaged → 20% invite a friend = 50 more
   - Add "Invite friend" feature (simple link share)

4. **Content Marketing**:
   - Write 2-3 blog posts: "5 рецептов правильного питания для новичков"
   - Share in VK, link back to recipes on COOKie
   - Estimated: 10-20 signups from content

5. **Community Engagement**:
   - Answer cooking questions in VK groups
   - Link to relevant COOKie recipes in comments
   - Build reputation as helpful community member

**Expected Result**: +400 users over 3 weeks (150 VK + 100 SEO + 100 referrals + 50 content)

---

### Weeks 5+ (Feb 18 - Feb 27): Target +350 Users (1000 Total)

**Tactics**:
1. **Organic Growth Accelerates**:
   - SEO improves: 200+ organic visitors/week = 20-30 signups
   - Word-of-mouth compounds: existing users tell friends

2. **If Budget Available** (10-50K ₽):
   - **VK Ads** (10-20K ₽):
     - Target: Female 25-40, interests: "Кулинария", "ПП", "Здоровье"
     - CPC ~10-15₽ → 700-1300 clicks → 10-15% conversion = 70-195 signups

   - **Micro-Influencers** (20-30K ₽):
     - Find 3-5 food bloggers (10-50K followers)
     - Offer: Free lifetime Premium + ₽5-10K per post
     - Reach: 50-150K → 2-5% CTR = 1-7.5K visits → 10-15% conversion = 100-750 signups

3. **Continue All Above**:
   - VK groups (less aggressive, 1-2 posts/day)
   - Content marketing
   - Community engagement

**Expected Result**: +350 users (150 organic + 200 if budget available OR +350 all organic if no budget)

---

## Content Creation Strategy (LLM-Assisted) ⭐ DETAILED

### Recipe Generation Pipeline

**Tools**:
- Claude / ChatGPT for recipe text
- Perplexity AI for recipe images
- USDA FoodData Central for KБЖУ data
- Spreadsheet (Google Sheets) for batch tracking

**Prompt Template for LLM**:
```
Создай детальный рецепт для [БЛЮДО].

Формат ответа (JSON):
{
  "title": "Название рецепта",
  "description": "2-3 предложения описания",
  "cuisine": "Русская/Итальянская/и т.д.",
  "difficulty": 1-5,
  "prep_time_minutes": X,
  "cook_time_minutes": Y,
  "servings": Z,
  "ingredients": [
    {"name": "Ингредиент", "quantity": X, "unit": "г/мл/шт", "category": "Овощи/Мясо/и т.д."}
  ],
  "instructions": [
    {"step": 1, "text": "Описание шага", "duration_minutes": X}
  ],
  "dietary_tags": ["vegetarian", "gluten-free", ...],
  "allergens": ["milk", "nuts", ...]
}

Требования:
- Ингредиенты в граммах/миллилитрах
- Шаги детальные и понятные для начинающих
- Реалистичное время приготовления
```

**Process Per Recipe** (~ 15-20 min):
1. **Generate text** (5 min):
   - Run LLM prompt for recipe
   - Review output for quality/coherence
   - Fix any errors or improve wording

2. **Generate image** (3 min):
   - Perplexity AI: "Сгенерируй фотореалистичное изображение блюда: [название]"
   - Or: Find stock photo on Unsplash/Pexels
   - Download and rename (recipe-slug.jpg)

3. **Calculate KБЖУ** (5 min):
   - Use USDA database or similar
   - Sum up KБЖУ for all ingredients
   - Divide by number of servings
   - Spot-check with nutritionist (every 20th recipe)

4. **Import to system** (2 min):
   - Use admin panel batch import
   - Or: Direct DB insert via script

5. **Quality check** (5 min):
   - Review on frontend
   - Check image looks good
   - Verify KБЖУ makes sense
   - Test search/filters

**Batch Production Schedule**:
- **Week 2**: 50 recipes (3.5 recipes/day) = 53min/day
- **Week 3**: 50 recipes (3.5 recipes/day) = 53min/day
- **Week 4**: 50 recipes (3.5 recipes/day) = 53min/day
- **Week 5**: 50 recipes (3.5 recipes/day) = 53min/day
- **Week 6**: 50 recipes (3.5 recipes/day) = 53min/day
- **Total Week 2-6**: 250 recipes

**Post-Launch**: 50 recipes/week = 7 recipes/day × 15min = 105min/day (1.75hr/day)

**Recipe Categories to Cover** (Balanced):
- Завтраки: 30 recipes (каши, омлеты, сырники)
- Супы: 25 recipes (борщ, щи, легкие супы)
- Основные блюда: 80 recipes (мясо, рыба, вегетарианское)
- Гарниры: 30 recipes (каши, овощи, салаты)
- Закуски: 30 recipes (салаты, бутерброды)
- Десерты: 25 recipes (ПП десерты, низкокалорийные)
- Напитки/Смузи: 20 recipes (смузи, коктейли ПП)
- Выпечка ПП: 10 recipes (хлеб, кексы низкокалорийные)

**Total**: 250 recipes

---

## Revised Risk Assessment

| Risk | Impact | Probability | Mitigation | Status |
|------|--------|-------------|------------|--------|
| **Solo dev delays** | High | Medium → Low | ✅ Added 1 week buffer (Jan 20-27 launch) | Mitigated |
| **Content creation bottleneck** | High | Medium → Low | ✅ Reduced to 250 recipes, clear pipeline | Mitigated |
| **Holiday disruption (NY)** | Medium | High → Low | ✅ Flex weeks 11-12, content done by Week 6 | Mitigated |
| **Low user engagement** | Critical | Medium | Extensive beta testing, iterate on feedback | Ongoing |
| **Technical issues at launch** | High | Low | Thorough testing Week 12-14, staged rollout | Ongoing |
| **Not reaching 1000 users** | High | Medium → Low | ✅ Detailed daily tactics, SEO, VK groups | Mitigated |
| **Infrastructure costs exceed budget** | Medium | Low | Monitor daily, optimize queries, CDN for images | Ongoing |

**Overall Risk Level**: **LOW-MEDIUM** (down from MEDIUM-HIGH)

---

## What's Different from Original MVP Plan?

### Timeline
- **Old**: 14 weeks (aggressive)
- **New**: 15 weeks (realistic with buffer)

### Content
- **Old**: 500-1000 recipes at launch (overwhelming)
- **New**: 250 recipes at launch + 50/week post-launch (achievable)

### Holiday Planning
- **Old**: No explicit plan
- **New**: Weeks 11-12 flexibility, content frontloaded

### User Acquisition
- **Old**: Vague strategy
- **New**: Daily tactics, detailed channels, realistic numbers

### Risk Management
- **Old**: Acknowledged but not deeply mitigated
- **New**: Each risk has concrete mitigation with "Mitigated" status

---

## Simplified Architecture

### High-Level Architecture

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

### Technology Stack (MVP)

**Frontend**:
- **Framework**: Next.js 14 (App Router)
- **Styling**: TailwindCSS
- **State Management**: React Context + Zustand (for complex state)
- **HTTP Client**: Axios
- **Form Handling**: React Hook Form + Zod validation

**Backend**:
- **Framework**: ASP.NET Core 8 (C#)
- **ORM**: Entity Framework Core 8
- **Validation**: FluentValidation
- **Authentication**: ASP.NET Core Identity (JWT + OAuth)
- **File Upload**: IFormFile with custom middleware

**Database**:
- **Primary DB**: Yandex Managed PostgreSQL (single instance for MVP)
- **Cache**: Yandex Managed Redis (single instance)
- **File Storage**: Yandex Object Storage (S3-compatible)

**Infrastructure**:
- **Cloud**: Yandex Cloud
- **Compute**: Yandex Compute Cloud (VM instances) - cheaper than K8s for MVP
- **Load Balancer**: Yandex Application Load Balancer
- **DNS**: Yandex Cloud DNS
- **SSL**: Let's Encrypt (free)

**Monitoring (Minimal)**:
- **Errors**: Sentry (free tier: 5K events/month)
- **Analytics**: Google Analytics 4
- **Uptime**: UptimeRobot (free tier)
- **Logs**: Yandex Cloud Logging (basic)

**CI/CD**:
- **Version Control**: GitHub (private repo)
- **CI/CD**: GitHub Actions (free for private repos)
- **Deployment**: Docker containers on Yandex Compute Cloud

---

## Database Schema (MVP Simplified)

### Core Tables

**users**
```sql
id: UUID PRIMARY KEY
email: VARCHAR(255) UNIQUE NOT NULL
password_hash: VARCHAR(255) -- nullable for OAuth users
username: VARCHAR(100) UNIQUE
first_name: VARCHAR(100)
avatar_url: VARCHAR(500)
oauth_provider: ENUM('email', 'yandex', 'vk', 'google')
oauth_id: VARCHAR(255)
email_verified: BOOLEAN DEFAULT FALSE
created_at: TIMESTAMP DEFAULT NOW()
```

**recipes**
```sql
id: UUID PRIMARY KEY
slug: VARCHAR(255) UNIQUE NOT NULL
title: VARCHAR(255) NOT NULL
description: TEXT
cuisine: VARCHAR(100) -- Русская, Итальянская, etc.
difficulty: SMALLINT (1-5)
prep_time_minutes: INTEGER
cook_time_minutes: INTEGER
total_time_minutes: INTEGER
servings: SMALLINT
instructions: JSONB -- [{step: 1, text: "...", duration: 10}]
nutrition_per_serving: JSONB -- {calories, protein, fat, carbs}
dietary_tags: VARCHAR(50)[] -- ['vegetarian', 'gluten-free']
allergens: VARCHAR(50)[] -- ['milk', 'nuts']
image_urls: VARCHAR(500)[] -- [main_image, step_images...]
rating_avg: DECIMAL(3,2) DEFAULT 0
rating_count: INTEGER DEFAULT 0
view_count: BIGINT DEFAULT 0
favorite_count: INTEGER DEFAULT 0
status: ENUM('draft', 'published') DEFAULT 'draft'
created_at: TIMESTAMP DEFAULT NOW()
updated_at: TIMESTAMP DEFAULT NOW()
```

**ingredients** (Simplified - no separate table for MVP)
```sql
-- Store ingredients directly in JSONB within recipes
-- Format: [
--   {name: "Помидоры", quantity: 500, unit: "г", category: "Овощи"},
--   {name: "Паста", quantity: 400, unit: "г", category: "Крупы"}
-- ]
```

**user_favorites**
```sql
user_id: UUID FK → users.id
recipe_id: UUID FK → recipes.id
created_at: TIMESTAMP DEFAULT NOW()
PRIMARY KEY (user_id, recipe_id)
```

**user_ratings**
```sql
id: UUID PRIMARY KEY
user_id: UUID FK → users.id
recipe_id: UUID FK → recipes.id
rating: SMALLINT (1-5)
review: TEXT (optional)
created_at: TIMESTAMP DEFAULT NOW()
UNIQUE (user_id, recipe_id)
```

**sessions** (for refresh tokens)
```sql
id: UUID PRIMARY KEY
user_id: UUID FK → users.id
refresh_token: VARCHAR(500) UNIQUE
expires_at: TIMESTAMP
created_at: TIMESTAMP DEFAULT NOW()
```

### Indexes (Critical for Performance)

```sql
-- recipes
CREATE INDEX idx_recipes_slug ON recipes(slug);
CREATE INDEX idx_recipes_status ON recipes(status);
CREATE INDEX idx_recipes_cuisine ON recipes(cuisine);
CREATE INDEX idx_recipes_rating ON recipes(rating_avg DESC, rating_count DESC);
CREATE INDEX idx_recipes_popularity ON recipes(view_count DESC, favorite_count DESC);
CREATE INDEX idx_recipes_total_time ON recipes(total_time_minutes);
CREATE INDEX idx_recipes_dietary_tags ON recipes USING GIN(dietary_tags);
CREATE INDEX idx_recipes_fulltext ON recipes USING GIN(to_tsvector('russian', title || ' ' || description));

-- users
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_users_oauth ON users(oauth_provider, oauth_id);

-- user_favorites
CREATE INDEX idx_favorites_user ON user_favorites(user_id);
CREATE INDEX idx_favorites_recipe ON user_favorites(recipe_id);

-- user_ratings
CREATE INDEX idx_ratings_recipe ON user_ratings(recipe_id);
CREATE INDEX idx_ratings_user ON user_ratings(user_id);
```

---

## API Design (MVP Endpoints)

### Public Endpoints (No Auth Required)

**Recipes**:
```
GET /api/v1/recipes                    # Search/browse recipes
GET /api/v1/recipes/:slug              # Get recipe details
GET /api/v1/recipes/popular            # Top 20 popular recipes
GET /api/v1/recipes/cuisines           # List of cuisines
```

**Health**:
```
GET /health                            # Health check
```

### Authenticated Endpoints (JWT Required)

**User**:
```
POST /api/v1/auth/register             # Register with email
POST /api/v1/auth/login                # Login
POST /api/v1/auth/refresh              # Refresh access token
POST /api/v1/auth/logout               # Logout
GET  /api/v1/auth/oauth/:provider      # OAuth flow (Yandex, VK)
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

**Recipe Management**:
```
POST /api/v1/admin/recipes             # Create recipe
PATCH /api/v1/admin/recipes/:id        # Update recipe
DELETE /api/v1/admin/recipes/:id       # Delete recipe
POST /api/v1/admin/recipes/:id/publish # Publish recipe
```

**Analytics**:
```
GET /api/v1/admin/stats                # Dashboard stats (user count, recipe count, etc.)
```

---

## Deployment Architecture (MVP)

### Yandex Cloud Setup

**1. Compute Instances**:
- **Backend**: 1 VM (2 vCPU, 4GB RAM) - `e2-standard-2`
- **Cost**: ~2,500 ₽/month

**2. Managed Databases**:
- **PostgreSQL**: 1 instance (2 vCPU, 4GB RAM, 50GB SSD)
- **Redis**: 1 instance (1 vCPU, 2GB RAM)
- **Cost**: ~4,000 ₽/month (PostgreSQL) + ~1,500 ₽/month (Redis)

**3. Object Storage**:
- **Bucket**: 100GB for images
- **Cost**: ~200 ₽/month (storage) + ~100 ₽/month (egress)

**4. Load Balancer**:
- **Application Load Balancer**: 1 instance
- **Cost**: ~1,000 ₽/month

**5. Backup**:
- **Automated PostgreSQL backups**: Daily (retention 7 days)
- **Cost**: ~500 ₽/month

**Total Infrastructure Cost (MVP)**: ~10,000 ₽/month

### Deployment Process

**Development Workflow**:
```
1. Local development (Docker Compose for DB)
2. Push to GitHub (feature branch)
3. GitHub Actions runs tests
4. Merge to main → auto-deploy to production
```

**GitHub Actions Pipeline**:
```yaml
- Build Docker image
- Run unit tests
- Run integration tests (with test DB)
- Push image to Yandex Container Registry
- SSH to VM and pull new image
- Restart containers with docker-compose
- Run database migrations
- Health check
```

---

## Next Immediate Steps (This Week)

1. **Set up Yandex Cloud** (1 hour)
   - Register account
   - Add payment method (card)
   - Explore console (VM, PostgreSQL, Object Storage)

2. **Create GitHub repo** (30 min)
   - Private repository
   - Initialize with README
   - Set up branch protection (main requires PR)

3. **Set up local dev** (2 hours)
   - Install .NET 8 SDK
   - Install Node.js 20 LTS (for frontend)
   - Install Docker Desktop
   - Clone your React template
   - Create docker-compose.yml (PostgreSQL + Redis)

4. **Generate first 10 recipes** (3 hours)
   - Test your LLM prompt
   - Refine the process
   - Time yourself (optimize for speed)

5. **Plan weekly schedule** (1 hour)
   - Block time for development (mornings?)
   - Block time for content creation (evenings?)
   - Set realistic daily goals

**Total time this week**: ~7.5 hours (plus reading documentation)

---

## Success Indicators (How to Know You're On Track)

### Weekly Checkpoints

**Week 2**: ✅ 50 recipes generated
**Week 4**: ✅ Backend API working (recipes CRUD)
**Week 6**: ✅ 250 recipes in database
**Week 8**: ✅ Frontend pages working (can browse recipes)
**Week 10**: ✅ Full UX flow works (signup → browse → favorite)
**Week 12**: ✅ Testing complete, major bugs fixed
**Week 14**: ✅ Beta testing feedback incorporated
**Week 15**: ✅ Public launch, first 250 users

**If you're behind schedule**:
- Week 8: Cut admin panel features (manual DB edits OK)
- Week 10: Reduce recipe count to 200 (still enough)
- Week 12: Skip some unit tests (manual QA priority)

**Do NOT**:
- Skip testing entirely
- Launch with < 150 recipes
- Launch without beta testing period

---

## Post-Launch Roadmap (Feb - June 2026)

### Phase 2: Growth & Iteration (Feb - Mar)
- Add 50 recipes/week (reach 500+ by end March)
- Iterate based on user feedback
- Fix bugs, optimize performance
- Hit 5,000 users milestone

### Phase 3: Premium Features (Apr - May)
- Implement meal planning (solve CRIT-001 algorithm)
- Integrate OpenAI for AI nutritionist
- Add payment (YooKassa)
- Launch Premium tiers (399₽/month)

### Phase 4: B2B Partnerships (June+)
- Approach X5 Group, ВкусВилл with traction data
- Negotiate integration partnerships
- Launch Pro tier with delivery integration

---

## What's Different from Full Architecture?

**Removed Complexity**:
- ❌ Microservices → Monolith
- ❌ Kubernetes → Simple VMs
- ❌ ClickHouse → Google Analytics
- ❌ ELK Stack → Cloud Logging
- ❌ Kafka → Not needed
- ❌ Prometheus + Grafana → Basic monitoring
- ❌ Parser Service → Manual curation
- ❌ Enrichment Service → Manual data entry
- ❌ AI Service → Defer to Phase 2
- ❌ Payment Service → Defer to Phase 2

**Cost Savings**:
- Full architecture: ~50,000 ₽/month
- MVP architecture: ~10,000 ₽/month
- **Savings**: 80%

**Time Savings**:
- Full architecture: 6-9 months (team of 3)
- MVP architecture: 3 months (solo)

**When to Migrate to Full Architecture?**
- 5,000+ users
- Performance bottlenecks
- Need advanced features (AI, meal planning)
- Team grows to 3+ developers
- Raised funding (Seed round)

---

**End of MVP Architecture Document**

**Ready for development!** 🚀

**Key Takeaway**: This timeline is **realistic and achievable** for a solo developer, with built-in buffers, clear milestones, and concrete mitigation for all major risks.
