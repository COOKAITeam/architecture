# COOKie Architecture Repository - File Guide

> **Last Updated**: 2025-10-13
> **Repository**: `cookie-org/architecture` (Documentation hub)
> **Related Repos**: `cookie-frontend`, `cookie-backend`, `cookie-infrastructure`, `cookie-recipes-data`

---

## 🏗️ Repository Purpose

This is the **architecture and documentation repository** for COOKie. It contains:
- ✅ Technical architecture specifications
- ✅ Requirements and planning documents
- ✅ Business documentation
- ✅ PlantUML diagrams
- ❌ NO CODE (code is in separate repos)

---

## 📁 Folder Structure

```
architecture/
├── docs/
│   ├── architecture/           MVP_ARCHITECTURE.md ⭐, MVP_АРХИТЕКТУРА.md
│   ├── requirements/           COOKie-requirements-v1.md
│   ├── business/               COOKie-description.md, COOKie-investor-pitch.md
│   ├── planning/               PROJECT_BACKLOG.md ⭐, PROJECT_SUMMARY.md
│   └── guides/                 FILE_GUIDE.md (this file)
│
├── diagrams/
│   ├── mvp/                    mvp_simplified_architecture.puml ⭐
│   ├── c4/                     C4 model diagrams (future ref)
│   ├── sequence/               User flow diagrams
│   ├── deployment/             Infrastructure diagrams
│   └── database/               Database schemas
│
├── archive/                    Outdated docs and diagrams
│   ├── docs/
│   └── diagrams/
│
├── .github/                    Issue/PR templates, workflows
│   ├── ISSUE_TEMPLATE/
│   └── workflows/
│
└── README.md                   Repository overview ⭐
```

---

## ⭐ Start Here (Priority Files)

### For Developers

1. **[README.md](../../README.md)** - Repository overview
2. **[MVP_ARCHITECTURE.md](../architecture/MVP_ARCHITECTURE.md)** - Complete MVP spec (15-week roadmap, Jan 20-27 launch)
3. **[PROJECT_BACKLOG.md](../planning/PROJECT_BACKLOG.md)** - Task tracking (4 critical, 12 other tasks)
4. **[mvp_simplified_architecture.puml](../../diagrams/mvp/mvp_simplified_architecture.puml)** - Architecture diagram

### For Stakeholders/Investors

1. **[README.md](../../README.md)** - Quick overview
2. **[COOKie-description.md](../business/COOKie-description.md)** - Market analysis (745B ₽ market)
3. **[COOKie-investor-pitch.md](../business/COOKie-investor-pitch.md)** - Financial projections
4. **[PROJECT_SUMMARY.md](../planning/PROJECT_SUMMARY.md)** - Architecture status

---

## 📚 Documentation Files

### Architecture (docs/architecture/)

| File | Description | Priority |
|------|-------------|----------|
| [MVP_ARCHITECTURE.md](../architecture/MVP_ARCHITECTURE.md) | **PRIMARY MVP SPEC** - 15-week roadmap, tech stack, 250 recipes, 1000 users goal | ⭐⭐⭐ |
| [MVP_АРХИТЕКТУРА.md](../architecture/MVP_АРХИТЕКТУРА.md) | Russian version of MVP architecture | ⭐⭐⭐ |

**Key Updates** (Latest):
- ✅ Timeline: 15 weeks (Jan 20-27 launch, added 1-week buffer)
- ✅ Recipes: 250-300 at launch (reduced from 500-1000)
- ✅ User acquisition: Detailed daily tactics for 1000 users
- ✅ Content pipeline: LLM-assisted (15-20 min/recipe)
- ✅ Holiday contingency: Flexible weeks 11-12

### Requirements (docs/requirements/)

| File | Description | Priority |
|------|-------------|----------|
| [COOKie-requirements-v1.md](../requirements/COOKie-requirements-v1.md) | 100+ functional & non-functional requirements with IDs | ⭐⭐ |

**Contains**:
- FR-RS-001 to FR-RS-020 (Recipe Service)
- FR-US-001 to FR-US-015 (User Service)
- NFR-PF-001 to NFR-PF-010 (Performance)
- NFR-SE-001 to NFR-SE-015 (Security)

### Business (docs/business/)

| File | Description | Priority |
|------|-------------|----------|
| [COOKie-description.md](../business/COOKie-description.md) | Market analysis, TAM/SAM/SOM, competitors | ⭐ |
| [COOKie-investor-pitch.md](../business/COOKie-investor-pitch.md) | Financial projections, investment needs | ⭐ |
| [cookie-economic-analysis-report.pdf](../business/cookie-economic-analysis-report.pdf) | Detailed economic analysis (Perplexity AI) | ⭐ |

**Key Metrics**:
- TAM: 10-12M users in Russia
- SAM: 2.5-3M active users
- Market: 745B ₽ (17% annual growth)

### Planning (docs/planning/)

| File | Description | Priority |
|------|-------------|----------|
| [PROJECT_BACKLOG.md](../planning/PROJECT_BACKLOG.md) | **TASK TRACKING** - 16 prioritized tasks | ⭐⭐⭐ |
| [BACKLOG_ПРОЕКТА.md](../planning/BACKLOG_ПРОЕКТА.md) | Russian version of backlog | ⭐⭐⭐ |
| [PROJECT_SUMMARY.md](../planning/PROJECT_SUMMARY.md) | Complete work overview, weak points, recommendations | ⭐⭐ |
| [ИТОГОВЫЙ_ОБЗОР.md](../planning/ИТОГОВЫЙ_ОБЗОР.md) | Russian version of summary | ⭐⭐ |

**Critical Tasks** (CRIT-001 to CRIT-004):
- Meal planning algorithm (Phase 2)
- Error handling docs (MVP prerequisite)
- Legal review of scraping
- OpenAI cost management (Phase 2)

### Guides (docs/guides/)

| File | Description | Priority |
|------|-------------|----------|
| [FILE_GUIDE.md](FILE_GUIDE.md) | **THIS FILE** - Complete navigation guide | ⭐⭐⭐ |
| [GIT_WORKFLOW.md](GIT_WORKFLOW.md) | **Git workflow guide** - Branches, PRs, issues, GitHub Actions | ⭐⭐⭐ |

**GIT_WORKFLOW.md covers**:
- Branch strategy and naming conventions
- Issue management and labels
- Pull request workflow (step-by-step)
- Commit message guidelines
- GitHub Actions automation
- Common scenarios (updating docs, adding diagrams, refactoring)
- Troubleshooting guide

### Technical (docs/technical/)

| File | Description | Priority |
|------|-------------|----------|
| [FRONTEND_STACK.md](../technical/FRONTEND_STACK.md) | **FRONTEND TECH STACK** - Complete technology decisions for frontend MVP | ⭐⭐⭐ |
| [FRONTEND_FOLDER_STRUCTURE.md](../technical/FRONTEND_FOLDER_STRUCTURE.md) | **FOLDER STRUCTURE** - Project organization, naming conventions, code patterns | ⭐⭐⭐ |

**FRONTEND_STACK.md covers**:
- Next.js 14 + TypeScript configuration
- State management (Zustand + TanStack Query)
- UI approach (TailwindCSS + custom components)
- Authentication (NextAuth.js)
- Testing (Vitest + React Testing Library)
- Docker development setup
- All dependencies and justifications

**FRONTEND_FOLDER_STRUCTURE.md covers**:
- Complete project folder structure
- Naming conventions (components, hooks, types)
- Code organization patterns
- Route groups (Next.js 14 App Router)
- Testing structure
- Performance best practices

---

## 🗺️ Diagram Files

### MVP Diagrams (diagrams/mvp/)

| File | Description | Use For |
|------|-------------|---------|
| [mvp_simplified_architecture.puml](../../diagrams/mvp/mvp_simplified_architecture.puml) | **USE THIS FOR MVP** - Monolith architecture, ~10K ₽/month | ⭐⭐⭐ |

### C4 Model (diagrams/c4/) - Future Reference

| File | Description | Use For |
|------|-------------|---------|
| [c4_level1_system_context.puml](../../diagrams/c4/c4_level1_system_context.puml) | System context - 4 personas, 15+ external systems | Phase 2+ |
| [c4_level2_container.puml](../../diagrams/c4/c4_level2_container.puml) | Microservices architecture - 11 services | Migration from monolith |
| [c4_level3_recipe_service_components.puml](../../diagrams/c4/c4_level3_recipe_service_components.puml) | Recipe Service internals - 15+ components | Detailed design |

### Sequence Diagrams (diagrams/sequence/)

| File | Description | Use For |
|------|-------------|---------|
| [sequence_user_search_recipe.puml](../../diagrams/sequence/sequence_user_search_recipe.puml) | User searches and views recipe | Understanding user flow |
| [sequence_meal_planning_flow.puml](../../diagrams/sequence/sequence_meal_planning_flow.puml) | AI meal planning (Phase 2) | Future feature design |

### Other Diagrams

| Folder | Description | Use For |
|--------|-------------|---------|
| [deployment/](../../diagrams/deployment/) | Kubernetes deployment (future) | Year 2+ infrastructure |
| [database/](../../diagrams/database/) | Full database schema (15+ tables) | Phase 2+ data model |

---

## 🔧 How to View Diagrams

### Option 1: VS Code (Recommended)
```bash
code --install-extension jebbs.plantuml
```

### Option 2: Online Viewer
Visit: http://www.plantuml.com/plantuml/uml/ and paste `.puml` file contents

### Option 3: CLI Rendering
```bash
# Install PlantUML
brew install plantuml  # macOS
apt-get install plantuml  # Ubuntu

# Render diagram
plantuml diagrams/mvp/mvp_simplified_architecture.puml
```

---

## 🔄 Cross-Repository Workflow

### When Working on a Feature

1. **Check this repo** (`architecture`):
   - Review [PROJECT_BACKLOG.md](../planning/PROJECT_BACKLOG.md) for task
   - Read relevant section in [MVP_ARCHITECTURE.md](../architecture/MVP_ARCHITECTURE.md)
   - Check diagrams if needed

2. **Open issue in code repo**:
   - `cookie-frontend` for UI features
   - `cookie-backend` for API features
   - Reference architecture docs in issue

3. **Implement in code repo**:
   - Follow architecture guidelines
   - Keep code repo README updated

4. **Update this repo if needed**:
   - Update diagrams if architecture changes
   - Mark task complete in [PROJECT_BACKLOG.md](../planning/PROJECT_BACKLOG.md)
   - Update [MVP_ARCHITECTURE.md](../architecture/MVP_ARCHITECTURE.md) if scope changes

---

## 📝 Update Guidelines

### When to Update Files

| File | When | Frequency |
|------|------|-----------|
| MVP_ARCHITECTURE.md | Architecture changes | As needed |
| PROJECT_BACKLOG.md | Task complete/added | Daily/weekly |
| PROJECT_SUMMARY.md | Major milestones | After phases |
| Diagrams (*.puml) | Architecture changes | As needed |
| README.md | Major changes | Quarterly |

### Commit Message Format

```bash
# Documentation
docs: update MVP timeline to Jan 20-27
docs: add user acquisition strategy
docs: mark CRIT-002 as completed

# Diagrams
diagrams: simplify MVP architecture
diagrams: add user registration flow

# Planning
planning: add Phase 2 tasks to backlog
```

---

## 🏢 Related Repositories

| Repository | Description | Tech Stack |
|------------|-------------|------------|
| **architecture** (this) | Documentation hub | Markdown, PlantUML |
| [cookie-frontend](https://github.com/COOKAITeam/cookie-frontend) | Web application | Next.js 14, TailwindCSS |
| [cookie-backend](https://github.com/COOKAITeam/cookie-backend) | API server | ASP.NET Core 8 (C#), EF Core, PostgreSQL |
| [cookie-infrastructure](https://github.com/COOKAITeam/cookie-infrastructure) | DevOps configs | Terraform, Docker, GitHub Actions |
| [recipes-data](https://github.com/COOKAITeam/recipes-data) | Recipe datasets | JSON, CSV, migrations |

---

## ❓ FAQ

**Q: Where is the code?**
A: Code is in separate repositories (`cookie-frontend`, `cookie-backend`). This repo has **only documentation**.

**Q: Which architecture should I follow?**
A: Use [MVP_ARCHITECTURE.md](../architecture/MVP_ARCHITECTURE.md) and [mvp_simplified_architecture.puml](../../diagrams/mvp/mvp_simplified_architecture.puml). Ignore microservices diagrams (Phase 2+).

**Q: What tasks should I start with?**
A: Check [PROJECT_BACKLOG.md](../planning/PROJECT_BACKLOG.md) - start with HIGH priority tasks.

**Q: How do I view diagrams?**
A: Install PlantUML extension in VS Code, or use http://www.plantuml.com/plantuml/uml/

**Q: Do I need to read everything?**
A: No. Start with:
1. [README.md](../../README.md)
2. [MVP_ARCHITECTURE.md](../architecture/MVP_ARCHITECTURE.md)
3. [PROJECT_BACKLOG.md](../planning/PROJECT_BACKLOG.md)

---

## 📞 Getting Help

- **Technical questions**: Create issue in relevant code repository
- **Architecture questions**: Create issue in this repository (architecture)
- **Unclear documentation**: Create issue with label `documentation`

---

**Repository**: `cookie-org/architecture`
**Last Updated**: 2025-10-15
**Status**: 🟢 Ready for MVP development

---

**End of File Guide**
