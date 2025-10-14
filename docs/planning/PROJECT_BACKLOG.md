# COOKie Project - Development Backlog

> **Purpose**: Track critical modifications, future tasks, and items that cannot be completed immediately
> **Last Updated**: 2025-10-13
> **Status**: Active

---

## 🔴 Critical Tasks (Blockers / High Priority)

### CRIT-001: Define Formal Meal Planning Algorithm
**Status**: Not Started
**Priority**: HIGH
**Assigned to**: To be determined
**Description**:
Current state: Vague mention of "linear programming or greedy algorithm"
Required: Formal specification of meal planning optimization algorithm

**Acceptance Criteria**:
- [ ] Define hard constraints (allergies, dietary restrictions, KBJU limits)
- [ ] Define soft constraints (variety, cost, user preferences)
- [ ] Choose specific algorithm (Branch & Bound, Genetic Algorithm, Constraint Programming, or Greedy)
- [ ] Document algorithm complexity and performance characteristics
- [ ] Create pseudocode or flowchart
- [ ] Validate with sample data (10 test cases)

**Estimated Effort**: 2-3 weeks (research + implementation + testing)

**Dependencies**: Recipe Service with KBJU data, User Profile Service

**Notes**:
- Consider using Python libraries: PuLP (linear programming), DEAP (genetic algorithms), or OR-Tools (Google's constraint solver)
- Start with simple greedy algorithm for MVP, optimize later

---

### CRIT-002: Error Handling Documentation for All Services
**Status**: Not Started
**Priority**: HIGH
**Assigned to**: To be determined
**Description**:
Current state: Sequence diagrams show only happy paths
Required: Comprehensive error handling strategy for all microservices

**Acceptance Criteria**:
- [ ] Document error scenarios for each service (Recipe, Parser, Enrichment, etc.)
- [ ] Define error codes and messages (standardized format)
- [ ] Create error handling sequence diagrams (API timeout, DB failure, external API failure)
- [ ] Define retry policies (exponential backoff parameters)
- [ ] Define circuit breaker thresholds
- [ ] Document fallback strategies
- [ ] Create error monitoring and alerting rules

**Estimated Effort**: 1 week (documentation)

**Dependencies**: All services

**Notes**:
- Use RFC 7807 Problem Details for HTTP APIs
- Implement at API Gateway level for consistency

---

### CRIT-003: Legal Review of Web Scraping Strategy
**Status**: Not Started
**Priority**: CRITICAL
**Assigned to**: Legal consultant (to be hired)
**Description**:
Current state: Parser Service designed to scrape recipe sites
Risk: Potential ToS violations, copyright infringement

**Acceptance Criteria**:
- [ ] Consult with lawyer specializing in IT/IP law
- [ ] Review robots.txt compliance for target sites (1000.menu, tableofgods.com)
- [ ] Assess copyright risks for recipe content
- [ ] Define legally safe scraping practices
- [ ] Draft attribution policy for scraped content
- [ ] Consider alternative: partnership agreements with recipe sites

**Estimated Effort**: 1-2 weeks (legal consultation)

**Budget**: 30,000-50,000 ₽ (legal fees)

**Blocker**: Cannot deploy Parser Service to production without legal clearance

**Notes**:
- Recipes themselves are not copyrightable (facts), but specific expression/text is
- Images are definitely copyrighted - need explicit permission or use own photos
- Consider manual curation for MVP to avoid legal risks entirely

---

### CRIT-004: OpenAI API Cost Management Strategy
**Status**: Not Started
**Priority**: HIGH
**Assigned to**: Backend developer
**Description**:
Risk: Unlimited AI queries for Premium users could result in unsustainable API costs

**Acceptance Criteria**:
- [ ] Calculate projected OpenAI costs for different user scenarios
- [ ] Implement request caching for common queries (Redis with TTL)
- [ ] Define rate limits even for Premium users (e.g., 100 queries/day)
- [ ] Implement query cost tracking per user
- [ ] Set up budget alerts in OpenAI dashboard
- [ ] Research alternatives: self-hosted models (Llama 3, Mistral), YandexGPT

**Estimated Effort**: 1 week (implementation + testing)

**Dependencies**: AI Nutritionist Service (Phase 2)

**Notes**:
- GPT-4: ~$0.03 per query (assuming 1K input + 500 output tokens)
- 1000 Premium users × 50 queries/month = 50K queries = $1,500/month
- Target: Keep AI costs under 20% of Premium revenue

---

## 🟡 High Priority Tasks (Important but not blocking)

### HIGH-001: Progressive Web App (PWA) Research
**Status**: Not Started
**Priority**: MEDIUM-HIGH
**Phase**: Post-MVP (February-March 2026)
**Description**:
Explore PWA as interim solution before native mobile apps

**Acceptance Criteria**:
- [ ] Research PWA capabilities (push notifications, offline mode, home screen install)
- [ ] Compare PWA vs React Native for COOKie use case
- [ ] Estimate development effort for PWA
- [ ] Create technical design doc for PWA implementation
- [ ] Test PWA on iOS and Android devices

**Estimated Effort**: 1 week (research)

**Notes**:
- PWA might be sufficient for Phase 1-2 (until gamification requires native features)
- iOS has limited PWA support (no background push, limited storage)

---

### HIGH-002: KBJU Data Validation Process
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP
**Description**:
Ensure nutritional data accuracy to avoid health risks and maintain trust

**Acceptance Criteria**:
- [ ] License or acquire authoritative nutrition database (USDA FoodData Central, Russian equivalent)
- [ ] Hire nutritionist for data validation (part-time, remote)
- [ ] Create validation checklist for each recipe
- [ ] Implement user reporting mechanism for incorrect KBJU
- [ ] Define confidence score for KBJU calculations (0-100%)
- [ ] Add disclaimer: "Nutritional information is estimated"

**Estimated Effort**: 2 weeks (setup + first batch validation)

**Budget**: 50,000-70,000 ₽ (nutritionist fees for 1000 recipes)

**Dependencies**: Recipe database

---

### HIGH-003: Recipe Partnership Strategy
**Status**: Not Started
**Priority**: HIGH
**Phase**: MVP
**Description**:
Establish partnerships with food bloggers/recipe creators instead of scraping

**Acceptance Criteria**:
- [ ] Identify 10-20 Russian food bloggers with quality content
- [ ] Draft partnership agreement template (content license)
- [ ] Define value proposition for bloggers (exposure, revenue share?)
- [ ] Reach out to 5 bloggers for pilot partnerships
- [ ] Implement attribution system (byline, link to original)
- [ ] Create blogger portal for content submission

**Estimated Effort**: 3-4 weeks (outreach + agreements)

**Notes**:
- Offer: Free Premium subscription + attribution + potential revenue share
- Target bloggers: 10K-100K followers (micro-influencers)

---

## 🟢 Medium Priority Tasks

### MED-001: A/B Testing Framework Setup
**Status**: Not Started
**Priority**: MEDIUM
**Phase**: Post-MVP (Q1 2026)
**Description**:
Implement proper A/B testing infrastructure for data-driven decisions

**Acceptance Criteria**:
- [ ] Choose A/B testing library (LaunchDarkly, Optimizely, or custom)
- [ ] Implement feature flags in backend
- [ ] Create user bucketing logic (consistent hashing by user_id)
- [ ] Define experiment framework (hypothesis, metrics, sample size)
- [ ] Set up statistical significance calculator
- [ ] Create dashboard for experiment results

**Estimated Effort**: 1 week (implementation)

**Dependencies**: Analytics Service

---

### MED-002: SEO Optimization Strategy
**Status**: Not Started
**Priority**: MEDIUM
**Phase**: MVP
**Description**:
Recipe pages are great for organic traffic - optimize for search engines

**Acceptance Criteria**:
- [ ] Implement proper meta tags (Open Graph, Twitter Cards)
- [ ] Add structured data (schema.org Recipe markup)
- [ ] Optimize page titles and descriptions
- [ ] Implement dynamic sitemap.xml
- [ ] Set up Google Search Console
- [ ] Create content strategy (blog posts linking to recipes)
- [ ] Target keywords: "[название блюда] рецепт калории кбжу"

**Estimated Effort**: 1 week (implementation)

**Notes**:
- Recipe pages can drive significant organic traffic (30-40% of users)
- Focus on long-tail keywords with low competition

---

### MED-003: Referral Program Design
**Status**: Not Started
**Priority**: MEDIUM
**Phase**: Q1 2026 (after achieving product-market fit)
**Description**:
Implement referral system to reduce CAC

**Acceptance Criteria**:
- [ ] Define referral incentive (both users get 1 month Premium free?)
- [ ] Implement referral link generation (unique code per user)
- [ ] Create referral tracking in database
- [ ] Build referral dashboard for users (how many friends invited)
- [ ] Set up email notifications for successful referrals
- [ ] Add anti-fraud measures (prevent self-referrals)

**Estimated Effort**: 1 week (implementation)

**Expected Impact**: 10-20% reduction in CAC

---

## 🔵 Low Priority / Future Tasks

### LOW-001: Multi-language Support
**Status**: Not Started
**Priority**: LOW
**Phase**: Year 2-3 (international expansion)
**Description**:
Add English (and potentially other languages) for international markets

**Acceptance Criteria**:
- [ ] Implement i18n framework (i18next for React)
- [ ] Translate UI strings (Russian → English)
- [ ] Handle recipe content localization (separate DB tables?)
- [ ] Support multiple cuisines with local ingredient names

**Estimated Effort**: 2-3 weeks

**Notes**: Defer until product-market fit in Russia

---

### LOW-002: Video Recipe Parsing
**Status**: Not Started
**Priority**: LOW
**Phase**: Year 2 (if budget allows)
**Description**:
Extract recipes from TikTok/YouTube videos using ASR + NLP

**Acceptance Criteria**:
- [ ] Research ASR providers (Yandex SpeechKit, Google Speech-to-Text)
- [ ] Implement transcript extraction
- [ ] Train NER model for ingredient extraction
- [ ] Extract key frames for recipe steps
- [ ] Calculate accuracy vs manual curation
- [ ] Assess cost-benefit (expensive!)

**Estimated Effort**: 4-6 weeks (R&D + implementation)

**Budget**: 100,000-200,000 ₽ (ASR API costs + ML development)

**Notes**: Likely not worth it for MVP - manual curation is cheaper and more accurate

---

### LOW-003: White-label B2B Solution
**Status**: Not Started
**Priority**: LOW
**Phase**: Year 3 (after B2C product is mature)
**Description**:
Offer COOKie as white-label solution for retailers/meal delivery companies

**Acceptance Criteria**:
- [ ] Create multi-tenant architecture
- [ ] Build customization interface (branding, colors)
- [ ] Define pricing model (setup fee + monthly?)
- [ ] Create sales materials and demo

**Estimated Effort**: 8-12 weeks

**Notes**: Only pursue if B2C business is stable and profitable

---

## 📋 Completed Tasks

### ✅ DONE-001: Enhanced Project Documentation
**Completed**: 2025-10-13
**Description**: Refactored project description and created comprehensive requirements spec
**Outcome**:
- COOKie-description.md updated
- COOKie-requirements-v1.md created (100+ requirements)
- 7 PUML architecture diagrams created

---

### ✅ DONE-002: C4 Architecture Diagrams
**Completed**: 2025-10-13
**Description**: Created comprehensive C4 model diagrams (Levels 1-3)
**Outcome**:
- System Context diagram
- Container diagram (microservices)
- Component diagram (Recipe Service)
- Sequence diagrams (2)
- Deployment diagram
- Enhanced database schema

---

## 🗑️ Rejected / Won't Do

### ❌ REJECTED-001: Multiple Payment Gateway Support (MVP)
**Reason**: Over-engineering for MVP - single gateway (YooKassa) is sufficient
**Decision Date**: 2025-10-13

### ❌ REJECTED-002: Full ELK Stack for MVP
**Reason**: Too heavy for initial deployment - use cloud-native logging instead
**Decision Date**: 2025-10-13
**Alternative**: Yandex Cloud Logging + Sentry for errors

### ❌ REJECTED-003: ClickHouse Sharding for MVP
**Reason**: Premature optimization - single node handles MVP scale
**Decision Date**: 2025-10-13
**Defer to**: Year 2 (when reaching 10M+ events/day)

---

## 📊 Backlog Metrics

**Total Tasks**: 16
- Critical: 4
- High Priority: 3
- Medium Priority: 3
- Low Priority: 3
- Completed: 2
- Rejected: 3

**Estimated Total Effort**: 25-35 weeks (across multiple phases)

**Budget Implications**: ~200,000-320,000 ₽ (legal, nutritionist, potential API costs)

---

## Notes on Backlog Management

**When to add tasks**:
- Critical bugs discovered during development
- Features that were descoped from current sprint
- Technical debt that needs addressing
- New feature ideas from user feedback

**When to remove tasks**:
- Task is completed → move to "Completed Tasks" section
- Task is no longer relevant → move to "Rejected / Won't Do" section
- Task is merged with another task

**Priority Definitions**:
- **CRITICAL**: Blocks production deployment or poses legal/financial risk
- **HIGH**: Important for product success, should be done soon
- **MEDIUM**: Nice to have, improves product but not essential
- **LOW**: Future enhancements, can wait until product is mature

---

**End of Backlog**
