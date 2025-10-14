# COOKie Architecture & Documentation

> **Central documentation repository for the COOKie project**
> A recipe discovery platform with AI-powered meal planning and nutritional analysis

**Status**: 🔒 Private Repository | 🟢 Active Development

---

## 📋 About This Repository

This repository serves as the **central hub** for all COOKie project documentation, architecture decisions, and planning materials. Code repositories are separate:

### COOKie GitHub Organization Structure

```
@COOKAITeam/
├── architecture (this repo)     📚 Documentation, diagrams, requirements
├── cookie-frontend              ⚛️ Next.js 14 web application
├── cookie-backend               🔧 ASP.NET Core C# API server
├── cookie-infrastructure        🏗️ Terraform, Docker, CI/CD configs
└── recipes-data                 📊 Recipe datasets and migrations
```

---

## 🚀 Quick Start

### For Developers

1. **Start here**: [MVP Architecture](docs/architecture/MVP_ARCHITECTURE.md) - Complete MVP specification
2. **Track progress**: [Project Backlog](docs/planning/PROJECT_BACKLOG.md) - Current tasks and priorities
3. **Understand scope**: [Requirements](docs/requirements/COOKie-requirements-v1.md) - Detailed feature specifications
4. **See structure**: [File Guide](docs/guides/FILE_GUIDE.md) - Navigation guide

### For Stakeholders/Investors

1. **Business overview**: [Project Description](docs/business/COOKie-description.md) - Market analysis and business model
2. **Investment pitch**: [Investor Pitch](docs/business/COOKie-investor-pitch.md) - Financial projections and strategy
3. **Technical summary**: [Project Summary](docs/planning/PROJECT_SUMMARY.md) - Architecture overview and status

### For Team Members

1. **Review architecture**: Browse [diagrams/](diagrams/) folder
2. **Check backlog**: See [PROJECT_BACKLOG.md](docs/planning/PROJECT_BACKLOG.md) for current tasks
3. **Organization structure**: See [ORGANIZATION.md](ORGANIZATION.md) for repository workflow

---

## 📁 Repository Structure

```
COOKie_architecture/
├── docs/
│   ├── architecture/        # Technical architecture documents
│   │   ├── MVP_ARCHITECTURE.md           ⭐ PRIMARY MVP SPEC
│   │   └── MVP_АРХИТЕКТУРА.md            (Russian version)
│   │
│   ├── requirements/        # Functional and non-functional requirements
│   │   └── COOKie-requirements-v1.md
│   │
│   ├── business/            # Business and market analysis
│   │   ├── COOKie-description.md
│   │   ├── COOKie-investor-pitch.md
│   │   └── cookie-economic-analysis-report.pdf
│   │
│   ├── planning/            # Project management and tracking
│   │   ├── PROJECT_BACKLOG.md            ⭐ TASK TRACKING
│   │   ├── BACKLOG_ПРОЕКТА.md            (Russian version)
│   │   ├── PROJECT_SUMMARY.md
│   │   └── ИТОГОВЫЙ_ОБЗОР.md             (Russian version)
│   │
│   └── guides/              # Documentation guides
│       └── FILE_GUIDE.md                 ⭐ NAVIGATION GUIDE
│
├── diagrams/                # PlantUML architecture diagrams
│   ├── mvp/                 # MVP architecture diagrams
│   │   └── mvp_simplified_architecture.puml  ⭐ USE FOR MVP
│   │
│   ├── c4/                  # C4 model diagrams (future reference)
│   │   ├── c4_level1_system_context.puml
│   │   ├── c4_level2_container.puml
│   │   └── c4_level3_recipe_service_components.puml
│   │
│   ├── sequence/            # Sequence diagrams for user flows
│   │   ├── sequence_user_search_recipe.puml
│   │   └── sequence_meal_planning_flow.puml
│   │
│   ├── deployment/          # Infrastructure diagrams
│   │   └── deployment_diagram.puml
│   │
│   └── database/            # Database schemas
│       └── enhanced_database_schema.puml
│
├── archive/                 # Outdated documents (reference only)
│   ├── docs/
│   └── diagrams/
│
├── .github/                 # GitHub templates and workflows
│   ├── ISSUE_TEMPLATE/
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│
└── README.md                # This file
```

---

## 🎯 Project Overview

### Vision

**COOKie** is a recipe discovery and meal planning platform that helps users:
- Find recipes by ingredients, cuisine, or dietary preferences
- Get accurate nutritional information (PFC) for every recipe
- Plan meals with AI-powered recommendations
- Order ingredients directly from partnered retailers

### Target Market

- **TAM (Total Addressable Market)**: 10-12M users in Russia
- **SAM (Serviceable Addressable Market)**: 2.5-3M active users
- **SOM (Serviceable Obtainable Market)**: 30K users in Year 1

### MVP Scope (January 2026 Launch)

**Core Features**:
- ✅ Recipe browsing and search (full-text + filters)
- ✅ User authentication (email/password + OAuth)
- ✅ Favorites and ratings (1-5 stars)
- ✅ 250-300 curated recipes with accurate PFC
- ✅ Admin panel for content management
- ✅ Responsive web interface

**Deferred to Phase 2**:
- ❌ AI Nutritionist (too expensive for MVP)
- ❌ Meal planning
- ❌ Shopping lists and retail integrations
- ❌ Premium subscriptions
- ❌ Native mobile apps

---

## 🏗️ Architecture Summary

### MVP Architecture (Simplified Monolith)

```
┌─────────────────┐
│   Web Users     │
└────────┬────────┘
         │ HTTPS
         ▼
┌─────────────────┐
│  Load Balancer  │ (Yandex Cloud)
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐ ┌────────┐
│ Next.js│ │ Admin  │
│  Web   │ │ Panel  │
└────┬───┘ └───┬────┘
     │         │
     └────┬────┘
          │ REST API
          ▼
    ┌──────────┐
    │ ASP.NET  │ (Monolith Backend)
    │Core C# API│
    └─────┬────┘
          │
    ┌─────┼─────┐
    ▼     ▼     ▼
┌─────┐ ┌───┐ ┌─────┐
│ PG  │ │Red│ │  S3 │
│ SQL │ │is │ │Store│
└─────┘ └───┘ └─────┘
```

**Technology Stack**:
- **Frontend**: Next.js 14, TailwindCSS, Zustand
- **Backend**: ASP.NET Core 8 (C#), Entity Framework Core
- **Database**: PostgreSQL (managed), Redis (cache)
- **Storage**: Yandex Object Storage
- **Hosting**: Yandex Cloud VMs (~10K ₽/month)
- **Monitoring**: Sentry + Google Analytics + UptimeRobot

### Why Monolith for MVP?

- **Cost**: 80% cheaper than microservices (~10K vs ~50K ₽/month)
- **Speed**: Faster development for solo developer
- **Simplicity**: Easier to debug and deploy
- **Scalable**: Can migrate to microservices at 5,000+ users

See [MVP_ARCHITECTURE.md](docs/architecture/MVP_ARCHITECTURE.md) for complete details.

---

## 📊 Key Metrics & Timeline

### MVP Timeline

**Start**: October 14, 2025
**Launch**: January 20-27, 2026
**Duration**: 15 weeks

**Phases**:
1. **Weeks 1-2**: Setup & Planning
2. **Weeks 3-6**: Core Backend (Recipe, User, Auth modules)
3. **Weeks 7-10**: Frontend (Pages, Admin panel, SEO)
4. **Weeks 11-12**: Content & Testing (250 recipes, QA)
5. **Weeks 13-14**: Pre-Launch (Beta testing, bug fixes)
6. **Week 15**: Public Launch 🚀

### Success Metrics

**Launch Week (Jan 20-27)**:
- 250 registered users
- 1,000+ recipe views
- < 5 critical bugs
- 90%+ uptime

**First Month (By Feb 27, 2026)**:
- ✅ **1,000 registered users** (primary goal)
- 15,000+ recipe views
- 200+ daily active users
- Retention D7: 25%+
- NPS: 40+

---

## 🔧 Development Setup

### Prerequisites

- .NET 8 SDK
- Node.js 20 LTS (for frontend)
- Docker Desktop
- PostgreSQL 15+
- Redis 7+

### Repository Clones

```bash
# Clone all repositories
git clone git@github.com:COOKAITeam/architecture.git
git clone git@github.com:COOKAITeam/cookie-frontend.git
git clone git@github.com:COOKAITeam/cookie-backend.git
git clone git@github.com:COOKAITeam/cookie-infrastructure.git
git clone git@github.com:COOKAITeam/recipes-data.git
```

### Viewing Diagrams

**Option 1: VS Code** (Recommended)
```bash
# Install PlantUML extension
code --install-extension jebbs.plantuml
```

**Option 2: Online Viewer**
- Visit: http://www.plantuml.com/plantuml/uml/
- Copy/paste `.puml` file contents

**Option 3: Local Rendering**
```bash
# Install PlantUML
brew install plantuml  # macOS
apt-get install plantuml  # Ubuntu

# Render diagram
plantuml diagrams/mvp/mvp_simplified_architecture.puml
```

---

## 📖 Documentation

### Essential Reading

1. **[MVP Architecture](docs/architecture/MVP_ARCHITECTURE.md)** - Complete MVP specification (START HERE)
2. **[Project Backlog](docs/planning/PROJECT_BACKLOG.md)** - Current tasks and priorities
3. **[Requirements Specification](docs/requirements/COOKie-requirements-v1.md)** - Detailed functional requirements
4. **[File Guide](docs/guides/FILE_GUIDE.md)** - Navigation guide for all files

### Business Documentation

- **[Project Description](docs/business/COOKie-description.md)** - Market analysis and business model
- **[Investor Pitch](docs/business/COOKie-investor-pitch.md)** - Financial projections and investment strategy
- **[Economic Analysis Report](docs/business/cookie-economic-analysis-report.pdf)** - Detailed economic analysis (Perplexity AI)

### Architecture Diagrams

- **[MVP Simplified Architecture](diagrams/mvp/mvp_simplified_architecture.puml)** - Use this for MVP development
- **[C4 Model Diagrams](diagrams/c4/)** - System context, containers, components (future reference)
- **[Sequence Diagrams](diagrams/sequence/)** - User flows and interactions
- **[Database Schema](diagrams/database/enhanced_database_schema.puml)** - Complete data model

---

## 🔧 Working with Documentation

### For Team Members

When updating documentation:

1. **Check backlog**: Review [PROJECT_BACKLOG.md](docs/planning/PROJECT_BACKLOG.md) for current tasks
2. **Create branch**: Create a feature branch from `main`
3. **Make changes**: Keep documentation clear and consistent
4. **Update diagrams**: Use PlantUML format for all architecture diagrams
5. **Commit**: Use semantic commit messages: `docs: update MVP timeline`
6. **Submit PR**: Include description of changes and link related issues

### Documentation Standards

- Architecture changes require updates to both diagrams and docs
- Maintain both English and Russian versions where applicable
- Follow existing formatting and structure
- Update [FILE_GUIDE.md](docs/guides/FILE_GUIDE.md) if adding new files

---

## 🗂️ Related Repositories

| Repository | Description | Tech Stack |
|------------|-------------|------------|
| [cookie-frontend](https://github.com/COOKAITeam/cookie-frontend) | Web application | Next.js 14, TailwindCSS, Zustand |
| [cookie-backend](https://github.com/COOKAITeam/cookie-backend) | API server | ASP.NET Core 8 (C#), EF Core, PostgreSQL |
| [cookie-infrastructure](https://github.com/COOKAITeam/cookie-infrastructure) | DevOps configs | Terraform, Docker, GitHub Actions |
| [recipes-data](https://github.com/COOKAITeam/recipes-data) | Recipe datasets | JSON, CSV, migration scripts |

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Team

**Lead Developer**: Voldemar

**Team**: Solo developer (open to future co-workers)

---

## 📞 Contact

- **Email**: voldemar22864@gmail.com
- **Telegram**: @John_Silver64

---

## 🎯 Roadmap

### Phase 1: MVP (Oct 2025 - Jan 2026) ✅ Current
- Recipe browsing and search
- User authentication
- 250-300 curated recipes
- Basic ratings and favorites

### Phase 2: Growth (Feb - Mar 2026)
- +50 recipes per week
- SEO optimization
- User acquisition campaigns
- Goal: 5,000 users

### Phase 3: Premium Features (Apr - May 2026)
- AI Nutritionist (OpenAI integration)
- Meal planning
- Premium subscriptions (399₽/month)
- Goal: 10,000 users

### Phase 4: B2B Partnerships (June 2026+)
- Retail integrations (X5 Group, ВкусВилл)
- Shopping list with delivery
- Pro tier (699₽/month)
- Goal: 50,000 users

---

## 📈 Project Status

**Current Phase**: MVP Development (Week 1 of 15)
**Launch Target**: January 20-27, 2026
**Status**: 🟢 On Track

See [PROJECT_SUMMARY.md](docs/planning/PROJECT_SUMMARY.md) for detailed status updates.

---

**Built with ❤️ for healthier eating in Russia**

🍪 **COOKie** - Вкусно. Полезно. Просто.
