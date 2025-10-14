# COOKie Project - Architecture & Documentation Summary

> **Completed**: 2025-10-13
> **Status**: First Iteration Complete
> **Next Steps**: Review, Validate, and Begin Development

---

## Summary of Work Completed

This document summarizes the comprehensive refactoring and architectural design work completed for the COOKie project.

### 1. Documentation Refactored

#### 1.1 Project Description ([COOKie-description.md](COOKie-description.md))

**Improvements Made**:
- ✅ Added executive summary with key facts
- ✅ Expanded market analysis with detailed competitor breakdown
- ✅ Enhanced target audience segmentation (TAM/SAM/SOM analysis)
- ✅ Detailed product modules with technical specifications
- ✅ Clear tiers and pricing strategy
- ✅ Technology stack recommendations
- ✅ Structured table of contents for easy navigation

**Key Additions**:
- Competitor analysis table comparing existing solutions
- Market size calculations: TAM ~10-12M, SAM ~2.5-3M users
- Detailed value proposition for B2C and B2B segments
- 5 product modules with implementation phases
- Tiers comparison table (Free, Premium 399₽, Pro 699₽)

#### 1.2 Requirements Specification ([COOKie-requirements-v1.md](COOKie-requirements-v1.md))

**Completely New Document** with:
- ✅ Comprehensive functional requirements for MVP and Future phases
- ✅ Detailed non-functional requirements (Performance, Scalability, Security, Observability)
- ✅ Data model requirements with GDPR compliance
- ✅ Integration requirements for external APIs
- ✅ UI/UX requirements with accessibility standards
- ✅ Metrics and analytics framework

**Structure**:
- 10 major sections covering all aspects of the system
- 100+ detailed requirements with unique IDs (FR-RS-001, NFR-PF-001, etc.)
- Clear prioritization (CRITICAL, HIGH, MEDIUM, LOW)
- Phase-based roadmap (MVP → Phase 2 → Phase 3)

**Key Sections**:
- Recipe Service: 5 major functional areas with 20+ sub-requirements
- Parser Service: Web scraping and video parsing
- Data Enrichment: KBJU calculation, normalization, classification
- Analytics: Events, metrics, reporting, A/B testing
- User Service: Authentication, profiles, favorites
- AI Nutritionist (Future): LLM integration, personalized recommendations
- Meal Planning (Future): Automated meal plan generation
- Order Service (Future): Integration with retailers

### 2. Architecture Diagrams Created

#### 2.1 C4 Model Diagrams

**Level 1: System Context** ([c4_level1_system_context.puml](diagrams/c4_level1_system_context.puml))
- Shows COOKie platform in the context of users and external systems
- 4 personas: B2C User, Content Manager, Analyst, B2B Partner
- 15+ external systems (recipe sources, delivery APIs, LLMs, payment gateways)
- Clear visualization of data flows and integrations

**Level 2: Container Diagram** ([c4_level2_container.puml](diagrams/c4_level2_container.puml))
- Microservices architecture breakdown
- 4 frontend containers (Web, Mobile, Admin, Partner Portal)
- API Gateway as single entry point
- 7 MVP microservices + 3 future services
- 3 databases (PostgreSQL, ClickHouse, Redis)
- Message queue (Kafka/RabbitMQ)
- File storage (S3/MinIO)

**Level 3: Component Diagram for Recipe Service** ([c4_level3_recipe_service_components.puml](diagrams/c4_level3_recipe_service_components.puml))
- Internal architecture of Recipe Service
- 4 API controllers (Recipe, Ingredient, Category, Rating)
- 6 business logic services
- 4 data access repositories
- 3 integration adapters (Cache, Storage, Event Publisher)
- 2 utility components

#### 2.2 Sequence Diagrams

**User Search and View Recipe** ([sequence_user_search_recipe.puml](diagrams/sequence_user_search_recipe.puml))
- Complete flow from search query to recipe viewing
- Includes authentication, caching, personalization
- Shows interactions between 10+ components
- Analytics event tracking

**AI-Assisted Meal Planning** ([sequence_meal_planning_flow.puml](diagrams/sequence_meal_planning_flow.puml))
- Premium feature flow
- Integration with OpenAI for recommendations
- Recipe matching and optimization
- Shopping list generation
- Push notification delivery

#### 2.3 Deployment Diagram ([deployment_diagram.puml](diagrams/deployment_diagram.puml))

**Infrastructure Design**:
- Kubernetes cluster with multiple pod groups
- Load balancer (NGINX/ALB)
- PostgreSQL cluster with replication
- ClickHouse cluster with sharding
- Redis cluster with 3 nodes
- Kafka cluster for message queuing
- S3-compatible storage
- Monitoring stack (Prometheus, Grafana, ELK, Sentry)

**Key Features**:
- Auto-scaling policies defined
- Resource limits specified
- Backup strategy documented
- SLO targets included (99.9% uptime, P95 < 500ms)

#### 2.4 Enhanced Database Schema ([enhanced_database_schema.puml](diagrams/enhanced_database_schema.puml))

**Comprehensive Data Model**:
- **Recipe Domain**: recipes, ingredients, recipe_ingredients, categories, tags
- **User Domain**: users, user_profiles, ratings, favorites
- **Meal Planning Domain**: meal_plans, meal_plan_items, shopping_lists
- **Analytics Domain**: user_events, recipe_analytics
- **Payment Domain**: subscriptions, payments

**Technical Details**:
- All tables with complete field specifications
- Data types, constraints, and defaults defined
- Indexes specified for performance (20+ indexes)
- Partitioning strategies for analytics tables
- Relationships with cardinality
- UK (Unique Keys) and FK (Foreign Keys) marked

---

## Project Architecture Overview

### Technology Stack Recommended

**Frontend**:
- React.js / Next.js (Web)
- React Native (iOS/Android)
- TailwindCSS (Styling)
- Redux/Zustand (State Management)

**Backend**:
- Node.js with NestJS (Core services)
- Python with FastAPI (ML services, Parser, Enrichment)
- PostgreSQL (Primary database)
- Redis (Caching)
- ClickHouse (Analytics)
- Kafka/RabbitMQ (Message queue)

**ML/AI**:
- OpenAI API / Anthropic Claude (Chatbot)
- scikit-learn, TensorFlow (Recommendations)
- Hugging Face Transformers (NLP)

**Infrastructure**:
- Docker + Kubernetes (Container orchestration)
- AWS / Yandex Cloud (Cloud hosting)
- S3/MinIO (File storage)
- GitLab CI/CD (Automation)

**Monitoring**:
- Prometheus + Grafana (Metrics)
- ELK Stack (Logs)
- Sentry (Errors)
- Amplitude (Product analytics)

### Microservices Breakdown

**MVP Services** (Months 1-6):
1. **Recipe Service** - Core recipe management, search, ratings
2. **Parser Service** - Web scraping, data extraction
3. **Data Enrichment Service** - Normalization, KBJU calculation, classification
4. **Analytics Service** - Events, metrics, reporting
5. **User Service** - Profiles, preferences
6. **Auth Service** - Authentication, authorization
7. **Notification Service** - Email, Push, SMS
8. **Payment Service** - Subscriptions, billing

**Phase 2 Services** (Months 7-18):
9. **AI Nutritionist Service** - LLM-based recommendations
10. **Meal Planning Service** - Automated meal plan generation
11. **Order Service** - Integration with retailers

**Phase 3 Services** (Year 2-3):
12. **Gamification Service** - Achievements, challenges
13. **Advanced ML Models** - Improved recommendations
14. **B2B Integration API** - White-label solutions

---

## Key Metrics & Success Criteria

### Business Metrics

| Metric | Year 1 | Year 2 | Year 3 |
|--------|--------|--------|--------|
| **Users** | 5,000 | 25,000 | 80,000 |
| **Premium Conversion** | 10% | 12% | 15% |
| **Revenue** | 2-4M ₽ | 15-25M ₽ | 45-75M ₽ |
| **MRR** | 200K ₽ | 1.5M ₽ | 4.5M ₽ |
| **CAC** | 400-600 ₽ | 400-600 ₽ | 400-600 ₽ |
| **LTV** | 2,500-4,000 ₽ | 2,500-4,000 ₽ | 2,500-4,000 ₽ |

### Technical Metrics (SLOs)

| Metric | Target |
|--------|--------|
| **Uptime** | 99.9% |
| **API Latency P95** | < 500ms |
| **API Latency P99** | < 1000ms |
| **Search P95** | < 300ms |
| **Error Rate** | < 0.1% |
| **RPS Capacity** | 100 (MVP) → 2000 (Year 2) |

### User Engagement Metrics

| Metric | Target |
|--------|--------|
| **WAU (North Star)** | Growing weekly |
| **Retention D7** | 30% |
| **Retention D30** | 20% |
| **Avg recipes viewed/week** | 10+ |
| **% with favorites** | 40% |

---

## Strengths of Current Architecture

### ✅ Strong Points

1. **Microservices Architecture**
   - Clear separation of concerns
   - Independent scalability
   - Technology flexibility (Node.js + Python)

2. **Comprehensive C4 Diagrams**
   - Complete visualization at 3 levels
   - Easy for new developers to understand
   - Aligned with industry standards

3. **Detailed Requirements**
   - 100+ specific requirements with unique IDs
   - Clear prioritization
   - Phase-based roadmap

4. **Scalability Built-In**
   - Horizontal scaling for all services
   - Database replication and sharding
   - Caching strategy (Redis)
   - Message queue for async processing

5. **Observability First**
   - Prometheus + Grafana for metrics
   - ELK for logs
   - Distributed tracing
   - Comprehensive alerting

6. **Security Considerations**
   - JWT authentication
   - RBAC authorization
   - Rate limiting
   - Encryption at rest and in transit

7. **Data Model**
   - Normalized database schema
   - Proper indexing strategy
   - Partitioning for analytics
   - GDPR compliance considerations

---

## Weak Points & Areas for Improvement

### ⚠️ Potential Issues

1. **Complexity for MVP**
   - **Issue**: Full microservices architecture may be over-engineering for 5K users
   - **Recommendation**: Consider starting with a modular monolith and extracting services as needed
   - **Alternative**: Deploy only Recipe Service + Parser + Enrichment initially, keep others as modules

2. **Parser Service Legal Risks**
   - **Issue**: Web scraping may violate ToS of recipe sites
   - **Recommendation**:
     - Consult with legal team before deploying Parser
     - Focus on sites with explicit API or open data
     - Implement strict robots.txt compliance
     - Consider partnerships with recipe sites instead

3. **AI Service Costs**
   - **Issue**: OpenAI API costs can be high with unlimited Premium users
   - **Recommendation**:
     - Implement strict rate limiting (even for Premium)
     - Cache common queries
     - Use smaller models for simple questions
     - Consider self-hosted models for basic recommendations

4. **Database Sharding Premature**
   - **Issue**: ClickHouse sharding mentioned but not needed for MVP volumes
   - **Recommendation**: Start with single ClickHouse node, shard only when reaching 10M+ events/day

5. **Missing Error Scenarios**
   - **Issue**: Sequence diagrams mostly show happy paths
   - **Recommendation**: Document error handling flows (API failures, timeouts, validation errors)

6. **Internationalization Over-Scoped**
   - **Issue**: Multiple language support mentioned but not critical for MVP
   - **Recommendation**: Focus on Russian only for MVP, add English in Phase 2

7. **Payment Integration** ✅ **FIXED**
   - **Updated**: Now using only YooKassa (best Russian market support)
   - **Rationale**: Simplifies integration, reduces complexity, lower costs

8. **Monitoring Stack Heavy**
   - **Issue**: ELK + Prometheus + Grafana + Sentry is a lot for MVP
   - **Recommendation**:
     - MVP: Sentry (errors) + Cloud-native logs (CloudWatch/Yandex Cloud Logging)
     - Phase 2: Add Prometheus + Grafana
     - Phase 3: Consider ELK if truly needed

9. **Meal Planning Algorithm Undefined**
   - **Issue**: "Linear programming or greedy algorithm" is vague
   - **Recommendation**:
     - Specify exact algorithm (e.g., Branch & Bound, Genetic Algorithm)
     - Define constraints formally (hard vs soft constraints)
     - Create a separate technical design doc for this component

10. **B2B Integration Assumptions**
    - **Issue**: Assumes APIs exist for all retailers (X5, VkusVill, etc.)
    - **Reality Check**: Many retailers don't have public APIs
    - **Recommendation**:
      - Start with one retailer pilot (sign agreement first)
      - Be prepared for custom integrations or manual processes initially

11. **User Profile Complexity**
    - **Issue**: Many optional fields may lead to incomplete data
    - **Recommendation**:
      - Progressive disclosure: collect data over time
      - Incentivize profile completion (better recommendations)
      - A/B test: mandatory vs optional fields

12. **Video Parsing Overly Ambitious**
    - **Issue**: Extracting recipes from TikTok/YouTube videos is complex and expensive
    - **Recommendation**:
      - De-prioritize for MVP
      - Start with metadata only (title, description)
      - Consider manual curation instead of automated extraction

---

## Specific Recommendations

### 1. MVP Simplification (Months 1-3)

**Phase 1A: Core MVP** (Deploy in 6-8 weeks):
- Recipe Service with basic CRUD
- Simple web scraper (manual trigger, not automated)
- Manual data enrichment (hire temp workers to input KBJU)
- Basic analytics (Google Analytics only)
- User auth via email only (no OAuth)
- PostgreSQL + Redis only (no ClickHouse yet)

**Phase 1B: Enhanced MVP** (Weeks 9-16):
- Automated parser with scheduler
- ML-based KBJU calculation
- OAuth providers (Yandex ID, VK ID)
- Custom analytics service (start collecting events)
- Basic recommendations (content-based filtering)

**Phase 1C: Premium Features** (Weeks 17-24):
- AI Nutritionist integration
- Meal planning (simple greedy algorithm)
- Payment integration (YooKassa)
- Premium subscriptions launch

### 2. Technology Stack Adjustments

**Instead of**:
- Full microservices from day 1

**Consider**:
- Modular monolith (NestJS) with clear module boundaries
- Extract to microservices when:
  - Service needs independent scaling (Parser, AI)
  - Team size grows (separate teams per service)
  - Different tech stack required (Python for ML)

**Benefits**:
- Faster initial development
- Simpler deployment
- Easier debugging
- Lower infrastructure costs

### 3. Data Strategy

**Prioritize**:
1. **Quality over quantity**: Start with 1,000 high-quality recipes (manually curated) instead of 10,000 scraped
2. **Partnerships**: Reach out to food bloggers for content partnerships (legal + quality)
3. **UGC incentives**: Gamify recipe submission by users (later phase)

**KBJU Data**:
- License existing food databases (USDA is free, but check RU alternatives)
- Consider partnership with nutritionists for data validation
- Clearly mark estimated vs validated KBJU

### 4. Go-to-Market Strategy

**Pre-Launch** (Month 0):
- Build landing page with email signup
- Target: 500 email signups before launch
- Run ads to gauge interest and CAC

**Launch** (Month 1):
- Invite-only beta (first 100 users)
- Iterate based on feedback
- Fix critical bugs before public launch

**Growth** (Months 2-6):
- SEO optimization (recipe pages are great for SEO)
- Content marketing (blog with nutrition tips)
- Partnership with fitness influencers
- Referral program (both users get 1 month Premium)

### 5. Metrics Dashboard Priorities

**Week 1 Metrics** (must have):
- User signups per day
- Active users (DAU)
- Recipe views per user
- Top viewed recipes

**Month 1 Metrics** (add):
- Retention D1, D7
- Conversion to registered users
- Search queries (popular terms)
- Error rate

**Month 3 Metrics** (add):
- Retention D30
- Conversion to Premium
- ARPU, LTV
- NPS (Net Promoter Score)

### 6. Team & Roles (Initial)

**Minimal Viable Team** (Pre-seed):
1. **You** (Full-stack developer + Product)
2. **Backend Developer** (Node.js, Python)
3. **Frontend Developer** (React, React Native)
4. **Part-time Designer** (UI/UX)
5. **Part-time Content Manager** (Recipe curation)

**Total cost estimate**:
- Founders equity + 2 FTE salaries (~200K ₽/month total)
- 6 months = 1.2M ₽ (fits in 1-2M Pre-seed budget)

### 7. Risk Mitigation

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| Legal issues with scraping | Medium | High | Start with partnerships, not scraping |
| Low user engagement | Medium | Critical | Extensive user testing before launch |
| High AI API costs | High | Medium | Strict rate limiting, caching |
| Competition from Yandex/VK | Low | Critical | Move fast, build community |
| KBJU calculation errors | Medium | Medium | Manual validation, user reports |
| Payment gateway issues | Low | High | Thorough testing, fallback provider |

---

## Next Steps

### Immediate Actions (This Week)

1. **Review Documentation**
   - [ ] Read through all updated documents
   - [ ] Validate requirements with stakeholders
   - [ ] Prioritize MVP features (keep only essentials)

2. **Technical Decisions**
   - [ ] Decide: Microservices vs Modular Monolith
   - [ ] Choose cloud provider (AWS vs Yandex Cloud vs on-prem)
   - [ ] Select payment gateway (YooKassa recommended)

3. **Legal & Compliance**
   - [ ] Consult lawyer on web scraping legality
   - [ ] Draft ToS and Privacy Policy
   - [ ] Research GDPR/152-FZ compliance requirements

4. **Market Validation**
   - [ ] Create landing page (Tilda/Readymag)
   - [ ] Run small ads campaign (10K ₽ budget)
   - [ ] Survey target audience (50+ responses)

### Short-term (Weeks 2-4)

5. **Set Up Infrastructure**
   - [ ] Create cloud accounts (AWS/Yandex Cloud)
   - [ ] Set up CI/CD pipeline (GitLab/GitHub Actions)
   - [ ] Configure environments (dev, staging, prod)

6. **Build MVP Prototype**
   - [ ] Set up project structure (monorepo recommended)
   - [ ] Implement Recipe Service core
   - [ ] Create simple UI (Next.js)
   - [ ] Deploy to staging

7. **Content Preparation**
   - [ ] Manually curate first 100 recipes
   - [ ] Validate KBJU with nutritionist
   - [ ] Prepare recipe images (stock photos ok for MVP)

### Medium-term (Months 2-3)

8. **Beta Testing**
   - [ ] Recruit 50 beta testers (target audience)
   - [ ] Collect feedback (surveys, interviews)
   - [ ] Iterate on UX

9. **Marketing Setup**
   - [ ] Create social media accounts (Instagram, VK, Telegram)
   - [ ] Start content marketing (blog posts, tips)
   - [ ] Build email list (newsletter)

10. **Fundraising Preparation**
    - [ ] Update pitch deck with MVP traction
    - [ ] Prepare financial model (3-year projection)
    - [ ] Reach out to angel investors / accelerators

---

## Questions for Clarification

### Business Questions

1. **Monetization Priority**
   - Primary focus: B2C subscriptions or B2B partnerships?
   - If B2B: Do you have existing contacts at X5, VkusVill?

2. **Target Launch Date**
   - When do you want to have MVP live?
   - Hard deadline or flexible?

3. **Budget**
   - Confirmed Pre-seed: 1-2M ₽?
   - How much allocated to: development, marketing, infrastructure?

4. **Team**
   - Solo founder or co-founders?
   - Developers already on team or need to hire?

### Technical Questions

5. **Existing Codebase**
   - Is there any code already written?
   - Or starting completely from scratch?

6. **Infrastructure Preference**
   - Cloud provider preference (cost vs features)?
   - Managed services vs self-hosted (e.g., managed K8s vs own cluster)?

7. **Mobile App Priority**
   - MVP: Web-only or need mobile app?
   - If mobile: iOS + Android or one platform first?

### Product Questions

8. **Recipe Source Strategy**
   - Scraping (risky), Partnerships (slow), Manual curation (expensive), UGC (quality issues)?
   - What's your preferred approach?

9. **Premium Features**
   - Which features are truly Premium vs should be free?
   - Willing to give more for free to grow userbase?

10. **Geographic Focus**
    - Russia-only or all СНГ from day 1?
    - Moscow/SPb focus or broader?

---

## Conclusion

The COOKie project now has:
- ✅ **Comprehensive architecture** with C4 diagrams at 3 levels
- ✅ **Detailed requirements** covering MVP and future phases
- ✅ **Complete data model** with indexes and constraints
- ✅ **Technology stack** recommendations
- ✅ **Deployment strategy** with auto-scaling and monitoring
- ✅ **Sequence diagrams** for critical user flows

However, some **simplifications are recommended** for MVP to reduce time-to-market and risk:
- Consider modular monolith instead of full microservices
- Prioritize partnerships over scraping for legal safety
- Start with one payment gateway and one retailer
- Focus on quality (1K recipes) over quantity (10K+ recipes)
- Simplify monitoring stack for MVP

**The foundation is solid. Now it's time to validate assumptions with the market and start building.**

---

## Files Created/Updated

### Documentation
- ✅ [COOKie-description.md](COOKie-description.md) - Enhanced project description
- ✅ [COOKie-requirements-v1.md](COOKie-requirements-v1.md) - NEW: Complete requirements spec
- ✅ [PROJECT_SUMMARY.md](PROJECT_SUMMARY.md) - This file

### Diagrams
- ✅ [diagrams/c4_level1_system_context.puml](diagrams/c4_level1_system_context.puml)
- ✅ [diagrams/c4_level2_container.puml](diagrams/c4_level2_container.puml)
- ✅ [diagrams/c4_level3_recipe_service_components.puml](diagrams/c4_level3_recipe_service_components.puml)
- ✅ [diagrams/sequence_user_search_recipe.puml](diagrams/sequence_user_search_recipe.puml)
- ✅ [diagrams/sequence_meal_planning_flow.puml](diagrams/sequence_meal_planning_flow.puml)
- ✅ [diagrams/deployment_diagram.puml](diagrams/deployment_diagram.puml)
- ✅ [diagrams/enhanced_database_schema.puml](diagrams/enhanced_database_schema.puml)

**Total: 3 documents + 7 PUML diagrams**

---

## UPDATED (2025-10-13): MVP Architecture Revised

Following user agreement on identified weak points, the MVP architecture has been **revised and simplified** to be realistic for a solo developer:

### Key Changes Made

**[MVP_ARCHITECTURE.md](MVP_ARCHITECTURE.md)** - **REVISED VERSION** (now the canonical MVP reference)

✅ **Timeline Extended**:
- Old: 14 weeks (Jan 13-19 launch)
- New: 15 weeks (Jan 20-27 launch)
- Reason: Added buffer for holidays + realistic solo dev pace

✅ **Recipe Target Reduced**:
- Old: 500-1000 recipes at launch
- New: 250-300 recipes at launch + 50/week post-launch
- Reason: Quality over quantity, LLM generation takes time

✅ **Holiday Contingency Added**:
- Weeks 11-12 (Dec 23 - Jan 5) have flexible Options A/B
- Content frontloaded to Week 6 to account for New Year break

✅ **User Acquisition Strategy Enhanced**:
- Detailed daily actions (morning/afternoon/evening)
- Week-by-week tactics to reach 1000 users
- VK groups strategy (2-3 posts/day), SEO, referrals, content marketing
- Optional paid tactics if budget becomes available (10-50K ₽)

✅ **Content Creation Pipeline Detailed**:
- Clear LLM-assisted workflow (~15-20 min per recipe)
- Batch production schedule (3.5 recipes/day = 53 min/day)
- Tools: Claude/ChatGPT (text), Perplexity AI (images), USDA (KBЖУ)
- Recipe category breakdown (Завтраки: 30, Супы: 25, Основные: 80, etc.)

✅ **Risk Assessment Updated**:
- All major risks now show "Mitigated" status with concrete actions
- Overall risk level reduced from MEDIUM-HIGH to LOW-MEDIUM

### Simplified MVP Architecture Benefits

**Cost Savings**:
- Full architecture: ~50,000 ₽/month
- MVP architecture: ~10,000 ₽/month
- **Savings**: 80%

**Time Savings**:
- Full architecture: 6-9 months (team of 3)
- MVP architecture: 3 months solo (15 weeks)

**Complexity Removed for MVP**:
- ❌ Microservices → Monolith
- ❌ Kubernetes → Simple VMs
- ❌ ClickHouse → Google Analytics
- ❌ ELK Stack → Cloud Logging
- ❌ Kafka → Not needed
- ❌ Prometheus + Grafana → Basic monitoring (Sentry + UptimeRobot)

### Additional Files Created

**Additional Documentation**:
- ✅ [FILE_GUIDE.md](FILE_GUIDE.md) - Navigation guide for all documentation

**Backlog & Planning**:
- ✅ [PROJECT_BACKLOG.md](PROJECT_BACKLOG.md) - 16 prioritized tasks (4 critical, 3 high, 3 medium, 3 low, 2 completed, 3 rejected)

### Success Metrics - Updated

**Launch Week (Jan 20-27)**:
- 250 registered users (avg 35/day)
- 1,000+ recipe views (avg 140/day)
- 50+ daily active users
- < 5 critical bugs
- 90%+ uptime

**First Month (By Feb 27, 2026)**:
- ✅ **1,000 registered users** (user's target)
- 15,000+ recipe views
- 200+ daily active users
- Retention D7: 25%+
- NPS: 40+
- 350-400 total recipes

### When to Consider Phase 2

Only proceed with Premium features when:
- ✅ 1,000+ users achieved
- Retention D7: 30%+
- NPS: 50+
- Consistent daily growth (10-20 new users/day organically)
- Positive user feedback on core features
- No major technical issues

---

**Total Documentation**: 10 documents (English + Russian) + 7 PUML diagrams

---

**Good luck with COOKie! 🍪**

**Ready for development!** 🚀
