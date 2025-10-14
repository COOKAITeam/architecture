# COOKie Multi-Repository Workflow

> **Version**: 1.0
> **Last Updated**: 2025-10-15
> **Purpose**: Guide for working across multiple COOKie repositories

---

## Overview

COOKie uses a **mono-documentation, multi-code** repository structure:

| Repository | Purpose | Tech Stack | Access |
|------------|---------|-----------|--------|
| **architecture** | Documentation hub, architecture specs, planning | Markdown, PlantUML | Public (eventually) |
| **cookie-frontend** | Web application | Next.js 14, TypeScript | Private |
| **cookie-backend** | API server | ASP.NET Core 8 (C#) | Private |
| **cookie-infrastructure** | DevOps & deployment | Terraform, Docker | Private |
| **recipes-data** | Recipe datasets & migrations | JSON, CSV, SQL | Private |

---

## Repository Structure

```
@COOKAITeam/
├── architecture/                 📚 YOU ARE HERE
│   ├── docs/
│   │   ├── architecture/         MVP_ARCHITECTURE.md
│   │   ├── technical/            FRONTEND_STACK.md, FRONTEND_FOLDER_STRUCTURE.md
│   │   ├── planning/             PROJECT_BACKLOG.md
│   │   └── guides/               This file
│   └── diagrams/
│
├── cookie-frontend/              ⚛️ Next.js Application
│   ├── src/
│   │   ├── app/                  Next.js 14 App Router
│   │   ├── components/
│   │   ├── hooks/
│   │   └── lib/
│   ├── public/
│   └── package.json
│
├── cookie-backend/               🔧 ASP.NET Core API
│   ├── COOKie.API/
│   ├── COOKie.Core/
│   ├── COOKie.Infrastructure/
│   └── COOKie.sln
│
├── cookie-infrastructure/        🏗️ DevOps
│   ├── terraform/
│   ├── docker/
│   └── .github/workflows/
│
└── recipes-data/                 📊 Data & Migrations
    ├── seeds/
    ├── migrations/
    └── scripts/
```

---

## Workflow Patterns

### Pattern 1: Architecture → Code

**Use Case**: Implementing a feature defined in architecture docs

**Steps**:
1. **Read** architecture docs in `architecture` repo
2. **Create issue** in code repo (frontend/backend)
3. **Link** back to architecture docs
4. **Implement** in code repo
5. **Update** architecture repo if design changes

**Example**:
```bash
# 1. You're in architecture repo, reading FRONT-001
# Located in: docs/planning/PROJECT_BACKLOG.md

# 2. Create issue in frontend repo
cd ../cookie-frontend
gh issue create \
  --title "FRONT-001: Implement core pages & navigation (Week 7)" \
  --body "Implements FRONT-001 from architecture backlog.

**Architecture Reference**:
https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#front-001

**Acceptance Criteria** (from backlog):
- [ ] Home Page with hero section
- [ ] Recipes Browse Page with filters
- [ ] Recipe Detail Page
- [ ] Header/Footer components

**Components to Build**:
- RecipeCard, RecipeGrid, RecipeFilters
- Header, Footer, MobileMenu

**Tech Stack**:
- Next.js 14 App Router
- TailwindCSS
- Lucide React icons

**Estimated Effort**: 5 days
" \
  --label "enhancement" \
  --milestone "Week 7"

# 3. Implement feature
# ... write code in cookie-frontend ...

# 4. Commit with issue reference
git commit -m "feat: implement core pages & navigation

- Add Home page with hero section
- Add Recipes browse page with filters
- Add Recipe detail page
- Create RecipeCard, RecipeGrid components

Closes #42
Implements COOKAITeam/architecture#FRONT-001"

# 5. Update architecture if design changed
cd ../architecture
# Update docs if needed
```

---

### Pattern 2: Code → Architecture

**Use Case**: Documenting changes made during implementation

**Steps**:
1. **Implement** feature in code repo
2. **Document** technical decisions
3. **Update** architecture docs
4. **Link** PR to architecture PR

**Example**:
```bash
# 1. Feature implemented in cookie-frontend
cd cookie-frontend
git commit -m "feat: add custom toast notification system

- Created Toast component with Headless UI
- Added useToast hook for global notifications
- Styled with TailwindCSS animations"

# 2. Document in architecture
cd ../architecture
git checkout -b docs/add-toast-component

# Edit FRONTEND_STACK.md or FRONTEND_FOLDER_STRUCTURE.md
# Add Toast component documentation

git commit -m "docs: document Toast component implementation

Updates FRONTEND_STACK.md with Toast component details.

Related: COOKAITeam/cookie-frontend#45"

gh pr create --title "docs: add Toast component to stack" \
  --body "Documents Toast implementation from cookie-frontend#45"
```

---

### Pattern 3: Cross-Repo Feature Development

**Use Case**: Feature requires changes in multiple repos (e.g., new API endpoint + frontend)

**Steps**:
1. **Create epic issue** in architecture repo
2. **Create sub-issues** in respective repos
3. **Link all issues** together
4. **Coordinate PRs** (backend first, then frontend)

**Example**:
```bash
# 1. Create epic in architecture
cd architecture
gh issue create \
  --title "Epic: Recipe Rating System" \
  --body "Implement 5-star rating system across frontend and backend.

## Backend Tasks
- [ ] Create user_ratings table
- [ ] Implement POST /api/v1/recipes/:id/rating
- [ ] Add rating aggregation logic

## Frontend Tasks
- [ ] Create RatingStars component
- [ ] Add rating submission form
- [ ] Implement optimistic updates

## Architecture Tasks
- [ ] Update API documentation
- [ ] Add rating to database schema diagram

**Related**:
- cookie-backend#XX (to be created)
- cookie-frontend#YY (to be created)" \
  --label "epic"

# 2. Create backend issue
cd ../cookie-backend
gh issue create \
  --title "BACK-006: Implement rating system API" \
  --body "Part of epic: COOKAITeam/architecture#10

Implements rating submission and aggregation endpoints.

**API Endpoints**:
- POST /api/v1/recipes/:id/rating
- PATCH /api/v1/recipes/:id/rating
- DELETE /api/v1/recipes/:id/rating

**Database**:
- user_ratings table
- Aggregate rating_avg, rating_count on recipes

**Architecture Ref**:
https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#back-006" \
  --label "backend,api"

# 3. Create frontend issue
cd ../cookie-frontend
gh issue create \
  --title "FRONT-004: Implement recipe rating UI" \
  --body "Part of epic: COOKAITeam/architecture#10

Implements 5-star rating component and submission.

**Components**:
- RatingStars.tsx (interactive)
- RatingDisplay.tsx (read-only)

**API Integration**:
- useRating hook (TanStack Query)
- Optimistic updates

**Depends On**: cookie-backend#XX

**Architecture Ref**:
https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#front-004" \
  --label "frontend,enhancement"

# 4. Implement backend first
cd ../cookie-backend
# ... implement ...
gh pr create --title "feat: add rating system API" \
  --body "Closes #XX
Part of COOKAITeam/architecture#10"

# 5. After backend merged, implement frontend
cd ../cookie-frontend
# ... implement ...
gh pr create --title "feat: add recipe rating UI" \
  --body "Closes #YY
Depends on cookie-backend#XX
Part of COOKAITeam/architecture#10"
```

---

## Issue Linking Syntax

### GitHub Issue References

```markdown
# Same repo
Closes #42
Fixes #42
Resolves #42

# Cross-repo (full notation)
Closes COOKAITeam/cookie-frontend#42
Implements COOKAITeam/architecture#FRONT-001

# Multiple issues
Closes #41, #42, #43
Related: cookie-backend#10, cookie-frontend#20
```

### Commit Message Examples

```bash
# Feature implementation
feat: implement user authentication flow

- Add login/register pages
- Integrate NextAuth.js
- Add JWT token handling

Implements COOKAITeam/architecture#FRONT-002
Closes #15

# Bug fix
fix: resolve rating submission error

- Handle null user_id in rating submission
- Add error toast for failed requests

Fixes #23
Related: COOKAITeam/architecture#10

# Documentation update
docs: update API endpoints documentation

- Add rating endpoints to spec
- Update database schema diagram

Related: COOKAITeam/cookie-backend#12

# Refactoring
refactor: extract RecipeCard to shared component

- Move RecipeCard to components/ui/
- Add variant prop for different layouts

Related: #18
```

---

## Milestones & Labels

### Shared Milestones Across Repos

Use consistent milestone names for sprint planning:

```
Week 7 (Nov 25 - Dec 1)
Week 8 (Dec 2-8)
Week 9 (Dec 9-15)
Week 10 (Dec 16-22)
Week 11-12 (Dec 23 - Jan 5)
Phase 2
Phase 3
```

### Shared Labels

| Label | Color | Use |
|-------|-------|-----|
| `epic` | Purple | Multi-repo features |
| `frontend` | Blue | Frontend-specific |
| `backend` | Green | Backend-specific |
| `infrastructure` | Orange | DevOps/deployment |
| `documentation` | Gray | Docs updates |
| `bug` | Red | Bug fixes |
| `enhancement` | Light blue | New features |
| `technical-debt` | Brown | Refactoring needed |
| `blocked` | Red | Waiting on dependency |
| `needs-design` | Yellow | UI/UX design required |
| `architecture-review` | Purple | Needs architecture approval |

---

## Development Workflow

### Sprint Planning (Weekly)

```bash
# 1. Review backlog in architecture repo
cd architecture
open docs/planning/PROJECT_BACKLOG.md

# 2. Create issues for sprint tasks
# Frontend tasks → cookie-frontend
# Backend tasks → cookie-backend

# 3. Assign to milestone (e.g., "Week 7")

# 4. Link issues to architecture backlog items

# 5. Start development
```

### Daily Development

```bash
# Morning: Check architecture docs
cd architecture
git pull
# Read relevant docs (FRONTEND_STACK.md, etc.)

# Work in code repo
cd ../cookie-frontend
git checkout -b feature/recipe-cards
# ... code ...

# Reference architecture in commits
git commit -m "feat: implement recipe card component

Follows design from FRONTEND_FOLDER_STRUCTURE.md

Implements COOKAITeam/architecture#FRONT-001"

# Create PR
gh pr create --title "feat: implement recipe card component" \
  --body "Implements recipe card with rating display.

**Architecture Ref**:
https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#front-001

**Preview**:
![Screenshot](./screenshot.png)

Closes #42"
```

### Code Review

```bash
# Reviewer: Check architecture compliance
# 1. Read architecture reference in PR description
# 2. Verify implementation matches spec
# 3. Check for deviations (good or bad)
# 4. Suggest architecture updates if needed

# Example review comment:
"This looks great! However, I notice you're using Zustand here
instead of TanStack Query for server state (per FRONTEND_STACK.md).
Is there a reason for this deviation? If this is intentional,
we should update the architecture docs."
```

---

## Context for AI Assistant (Claude Code)

When working with Claude Code across repositories, provide context:

### Starting a New Session

```markdown
Current repository: cookie-frontend
Related repos:
- architecture: https://github.com/COOKAITeam/architecture
- cookie-backend: https://github.com/COOKAITeam/cookie-backend

Current task: Implementing FRONT-001 (Core Pages)

Architecture reference:
{paste relevant section from PROJECT_BACKLOG.md}

Tech stack:
{paste relevant section from FRONTEND_STACK.md}
```

### Cross-Repo Commands

```bash
# Clone all repos
git clone git@github.com:COOKAITeam/architecture.git
git clone git@github.com:COOKAITeam/cookie-frontend.git
git clone git@github.com:COOKAITeam/cookie-backend.git
git clone git@github.com:COOKAITeam/cookie-infrastructure.git

# Open multiple repos in VS Code
code architecture cookie-frontend cookie-backend

# Search across all repos (from parent directory)
rg "RecipeCard" architecture/ cookie-frontend/

# Keep architecture docs open while coding
# Tab 1: architecture/docs/planning/PROJECT_BACKLOG.md
# Tab 2: cookie-frontend/src/components/recipes/RecipeCard.tsx
```

---

## Issue Templates

### Architecture Repo Issue Templates

**Epic Template** (`.github/ISSUE_TEMPLATE/epic.md`):
```markdown
---
name: Epic
about: Multi-repo feature requiring coordination
title: 'Epic: [Feature Name]'
labels: epic
---

## Overview
Brief description of the epic.

## Scope

### Backend Tasks
- [ ] Task 1 (cookie-backend#XX)
- [ ] Task 2 (cookie-backend#YY)

### Frontend Tasks
- [ ] Task 1 (cookie-frontend#ZZ)
- [ ] Task 2 (cookie-frontend#AA)

### Architecture Tasks
- [ ] Update documentation
- [ ] Update diagrams

## Architecture References
- [PROJECT_BACKLOG.md](link)
- [MVP_ARCHITECTURE.md](link)

## Timeline
Target: Week X

## Dependencies
- [ ] Backend API ready
- [ ] Design approved
```

**Architecture Decision Template** (`.github/ISSUE_TEMPLATE/architecture-decision.md`):
```markdown
---
name: Architecture Decision
about: Propose a technical architecture decision
title: 'ADR: [Decision Title]'
labels: architecture-review
---

## Context
What is the issue we're addressing?

## Options Considered

### Option 1: [Name]
**Pros**:
-
**Cons**:
-

### Option 2: [Name]
**Pros**:
-
**Cons**:
-

## Decision
Chosen option: [X]

**Rationale**:
-

## Consequences
What becomes easier/harder?

## Action Items
- [ ] Update FRONTEND_STACK.md
- [ ] Update PROJECT_BACKLOG.md
- [ ] Communicate to team
```

### Frontend/Backend Issue Templates

**Feature Template** (`.github/ISSUE_TEMPLATE/feature.md`):
```markdown
---
name: Feature Request
about: Implement a new feature
title: '[FRONT/BACK-XXX]: [Feature Name]'
labels: enhancement
---

## Architecture Reference
Link to PROJECT_BACKLOG.md or architecture docs.

**Backlog Item**: FRONT-XXX or BACK-XXX

## Description
What should this feature do?

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Technical Details
**Components/Services**:
- Component1
- Component2

**API Endpoints** (if backend):
- POST /api/v1/...
- GET /api/v1/...

## Dependencies
- [ ] Depends on #XX
- [ ] Depends on COOKAITeam/cookie-backend#YY

## Estimated Effort
X days

## Related Issues
- COOKAITeam/architecture#XX (epic)
```

---

## CI/CD Integration

### GitHub Actions Triggers

**Architecture Repo** (`.github/workflows/sync-docs.yml`):
```yaml
name: Sync Documentation

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Notify other repos of doc updates
        run: |
          # Trigger workflow in cookie-frontend
          gh workflow run sync-architecture-docs.yml \
            --repo COOKAITeam/cookie-frontend
```

**Frontend Repo** (`.github/workflows/check-architecture-compliance.yml`):
```yaml
name: Check Architecture Compliance

on:
  pull_request:
    branches: [main]

jobs:
  check-compliance:
    runs-on: ubuntu-latest
    steps:
      - name: Check for architecture reference
        run: |
          # Ensure PR body contains architecture reference
          if ! gh pr view ${{ github.event.pull_request.number }} \
             --json body --jq .body | grep -q "COOKAITeam/architecture"; then
            echo "⚠️ PR should reference architecture docs"
            exit 1
          fi
```

---

## Best Practices

### 1. Always Link to Architecture

✅ **Do**:
```markdown
Implements FRONT-001 from architecture backlog.

**Reference**:
https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#front-001
```

❌ **Don't**:
```markdown
Added recipe cards.
```

### 2. Update Architecture When Design Changes

✅ **Do**: If you deviate from architecture during implementation, update the docs
❌ **Don't**: Let architecture docs drift from reality

### 3. Use Consistent Naming

✅ **Do**: Use task IDs (FRONT-001, BACK-003) in issues, commits, PRs
❌ **Don't**: Use vague references ("that feature we discussed")

### 4. Create Epics for Multi-Repo Features

✅ **Do**: Create epic in architecture, link sub-issues from other repos
❌ **Don't**: Create disconnected issues in each repo

### 5. Document Technical Decisions

✅ **Do**: If you make a significant tech choice, document it in architecture repo
❌ **Don't**: Keep important decisions only in code comments

---

## Troubleshooting

### Problem: Can't find architecture docs for my task

**Solution**:
```bash
cd architecture
# Search backlog
rg "authentication" docs/planning/PROJECT_BACKLOG.md

# Search all docs
rg "authentication" docs/

# Check FILE_GUIDE for navigation
open docs/guides/FILE_GUIDE.md
```

### Problem: Architecture docs outdated

**Solution**:
```bash
cd architecture
git checkout -b docs/update-auth-flow
# Update docs
git commit -m "docs: update authentication flow

- Add OAuth refresh token flow
- Update sequence diagram

Based on implementation in cookie-backend#42"
gh pr create
```

### Problem: Need to coordinate backend + frontend changes

**Solution**:
1. Create epic in architecture repo
2. Create backend issue (implement first)
3. Create frontend issue (depends on backend)
4. Link all three issues
5. Merge backend PR before starting frontend

### Problem: Issue tracker getting messy

**Solution**:
- Use milestones to organize by sprint
- Use labels consistently
- Close stale issues
- Convert old issues to discussions if needed

---

## Quick Reference

### Commands Cheat Sheet

```bash
# Create issue
gh issue create --title "FRONT-001: Core pages" --body "..." --label "enhancement"

# Create PR
gh pr create --title "feat: add feature" --body "Closes #42"

# Link to other repo issue
# In commit: "Implements COOKAITeam/architecture#FRONT-001"
# In PR body: "Related: COOKAITeam/cookie-backend#10"

# Check issue status
gh issue list --label "epic" --state open

# View specific issue
gh issue view 42

# Search issues across repos (from parent dir)
gh issue list --repo COOKAITeam/architecture --search "authentication"
```

### URL Patterns

```
# Architecture backlog item
https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#front-001

# Frontend issue
https://github.com/COOKAITeam/cookie-frontend/issues/42

# Backend PR
https://github.com/COOKAITeam/cookie-backend/pull/10

# Cross-link in markdown
Implements [FRONT-001](https://github.com/COOKAITeam/architecture/blob/main/docs/planning/PROJECT_BACKLOG.md#front-001)
```

---

## Summary

**Key Principles**:
1. 📚 **Architecture repo** = single source of truth for design
2. 🔗 **Always link** issues/PRs to architecture docs
3. 📝 **Update architecture** when implementation differs
4. 🎯 **Use task IDs** (FRONT-XXX, BACK-XXX) for consistency
5. 🚀 **Create epics** for multi-repo features

**Workflow**:
Architecture → Issue → Implementation → PR → Update Architecture (if needed)

**Tools**:
- GitHub Issues for task tracking
- GitHub Actions for automation
- Markdown links for cross-references
- Consistent labels & milestones

---

**Last Updated**: 2025-10-15
**Next Review**: After first sprint (Week 7)
