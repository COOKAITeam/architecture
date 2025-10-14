# Git Workflow Guide for COOKie Architecture

> **Comprehensive guide for managing documentation using Git, branches, PRs, issues, and GitHub Actions**

---

## 📋 Table of Contents

1. [Quick Reference](#quick-reference)
2. [Branch Strategy](#branch-strategy)
3. [Issue Management](#issue-management)
4. [Pull Request Workflow](#pull-request-workflow)
5. [Commit Message Guidelines](#commit-message-guidelines)
6. [GitHub Actions](#github-actions)
7. [Common Scenarios](#common-scenarios)
8. [Troubleshooting](#troubleshooting)

---

## 🚀 Quick Reference

### Common Commands

```bash
# Start new work
git checkout main
git pull origin main
git checkout -b docs/your-feature-name

# Make changes and commit
git add <files>
git commit -m "docs: your commit message"

# Push and create PR
git push -u origin docs/your-feature-name
# Then create PR via GitHub UI

# Update branch with latest main
git checkout main
git pull origin main
git checkout docs/your-feature-name
git rebase main

# Clean up after PR merge
git checkout main
git pull origin main
git branch -d docs/your-feature-name
```

---

## 🌲 Branch Strategy

### Branch Types

| Prefix | Purpose | Example | Lifespan |
|--------|---------|---------|----------|
| `docs/` | Documentation updates | `docs/update-mvp-timeline` | Short (1-3 days) |
| `diagrams/` | Diagram changes | `diagrams/add-auth-flow` | Short (1-2 days) |
| `refactor/` | Restructuring docs | `refactor/reorganize-planning` | Medium (3-7 days) |
| `feat/` | New documentation sections | `feat/add-testing-guide` | Medium (3-7 days) |
| `fix/` | Fix errors or broken links | `fix/broken-links-in-readme` | Short (1 day) |
| `chore/` | Maintenance tasks | `chore/update-github-actions` | Short (1 day) |

### Branch Naming Convention

**Format**: `<type>/<brief-description>`

**Examples**:
- ✅ `docs/update-mvp-architecture`
- ✅ `diagrams/add-deployment-diagram`
- ✅ `refactor/simplify-file-guide`
- ✅ `fix/typos-in-readme`
- ❌ `my-branch` (no type prefix)
- ❌ `docs/this-is-a-very-long-branch-name-that-describes-everything` (too long)

### Creating a New Branch

```bash
# Always start from up-to-date main
git checkout main
git pull origin main

# Create and switch to new branch
git checkout -b docs/your-feature-name

# Verify you're on the new branch
git branch
```

---

## 🎫 Issue Management

### Creating Issues

**Use GitHub Issue Templates**:

1. Go to: https://github.com/COOKAITeam/architecture/issues/new/choose
2. Select appropriate template:
   - **Architecture Question** - Ask about design decisions
   - **Documentation Update** - Suggest improvements
   - **Diagram Request** - Request new diagrams

**Or create custom issue**:

```markdown
**Title**: Brief description (50 chars max)

**Description**:
- What needs to be done?
- Why is it needed?
- Any relevant context?

**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2

**Related Issues**: #123, #456
```

### Issue Labels

| Label | Meaning | When to Use |
|-------|---------|-------------|
| `priority: critical` | Urgent, blocking work | MVP blocker, incorrect tech stack |
| `priority: high` | Important, affects MVP | Timeline issues, missing docs |
| `priority: medium` | Should be done soon | Phase 2 planning, improvements |
| `priority: low` | Nice to have | Minor typos, formatting |
| `type: documentation` | Documentation changes | Any markdown updates |
| `type: diagrams` | Diagram changes | PlantUML updates |
| `type: refactor` | Restructuring | Reorganizing folders/files |
| `architecture` | Architecture-related | MVP spec, tech stack decisions |
| `planning` | Planning docs | Backlog, roadmap updates |
| `business` | Business docs | Market analysis, pitch deck |
| `in progress` | Currently being worked on | Active development |
| `blocked` | Waiting on something | Needs decision, external dependency |

### Linking Issues to PRs

**In PR description**:
```markdown
Closes #123
Fixes #456
Relates to #789
```

**GitHub Keywords** (auto-close issues when PR merges):
- `Closes #123`
- `Fixes #123`
- `Resolves #123`

---

## 🔄 Pull Request Workflow

### Step-by-Step Process

#### 1. Create Feature Branch

```bash
git checkout main
git pull origin main
git checkout -b docs/update-mvp-timeline
```

#### 2. Make Changes

Edit files, add new documentation, update diagrams.

#### 3. Stage and Commit

```bash
# Stage specific files
git add docs/architecture/MVP_ARCHITECTURE.md
git add docs/planning/PROJECT_BACKLOG.md

# Or stage all changes
git add .

# Commit with semantic message
git commit -m "docs: extend MVP timeline to 15 weeks

- Add 1 week buffer for holidays
- Update launch date to Jan 20-27
- Adjust content creation schedule
- Update risk assessment

Closes #42"
```

#### 4. Push Branch

```bash
# First push
git push -u origin docs/update-mvp-timeline

# Subsequent pushes
git push
```

#### 5. Create Pull Request

**Via GitHub CLI**:
```bash
gh pr create --title "docs: extend MVP timeline to 15 weeks" \
  --body "## Summary
Updates MVP timeline with holiday buffer.

## Changes
- Extended timeline by 1 week
- Updated all date references
- Added contingency planning

## Checklist
- [x] Updated MVP_ARCHITECTURE.md
- [x] Updated Russian version
- [x] Updated PROJECT_SUMMARY.md

Closes #42"
```

**Or via GitHub Web UI**:
1. Go to: https://github.com/COOKAITeam/architecture
2. Click "Compare & pull request" button (appears after push)
3. Fill in PR template:
   - **Title**: Semantic title (e.g., `docs: extend MVP timeline`)
   - **Description**: What changed and why
   - **Checklist**: Mark completed items
   - **Related Issues**: Link issues
4. Click "Create pull request"

#### 6. Address Review Feedback

```bash
# Make requested changes
git add <changed-files>
git commit -m "docs: address review feedback - clarify holiday schedule"
git push

# Or amend last commit (if no one else is working on branch)
git add <changed-files>
git commit --amend --no-edit
git push --force-with-lease
```

#### 7. Merge PR

**Options**:
- **Squash and merge** (recommended for multiple commits)
- **Rebase and merge** (for clean commit history)
- **Merge commit** (preserves all commits)

**After merge**:
```bash
# Switch to main and update
git checkout main
git pull origin main

# Delete local branch
git branch -d docs/update-mvp-timeline

# Delete remote branch (if not auto-deleted)
git push origin --delete docs/update-mvp-timeline
```

---

## 📝 Commit Message Guidelines

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

| Type | When to Use | Example |
|------|-------------|---------|
| `docs` | Documentation changes | `docs: update MVP architecture` |
| `diagrams` | Diagram updates | `diagrams: add deployment diagram` |
| `feat` | New documentation sections | `feat: add testing guide` |
| `fix` | Fix errors, typos, links | `fix: correct broken links in README` |
| `refactor` | Restructure without changing content | `refactor: reorganize planning docs` |
| `chore` | Maintenance tasks | `chore: update GitHub Actions` |
| `style` | Formatting only | `style: fix markdown formatting` |

### Scopes (Optional)

- `architecture` - Architecture docs
- `planning` - Planning docs
- `business` - Business docs
- `requirements` - Requirements docs
- `guides` - Guide docs
- `diagrams` - Diagram files
- `github` - GitHub config

### Subject

- Use imperative mood: "add" not "added" or "adds"
- No capitalization of first letter
- No period at the end
- Max 72 characters

### Body (Optional)

- Explain what changed and why
- Use bullet points for multiple changes
- Wrap at 72 characters

### Footer (Optional)

- Reference issues: `Closes #123`
- Breaking changes: `BREAKING CHANGE: description`

### Examples

**Good**:
```
docs: extend MVP timeline to 15 weeks

- Add 1 week buffer for holidays
- Update launch date to Jan 20-27
- Adjust content creation schedule
- Update risk assessment

Closes #42
```

**Bad**:
```
updated docs
```

---

## ⚙️ GitHub Actions

### Automated Workflows

#### 1. Documentation Validation

**Triggers**: PR to main, Push to main (docs changes)

**What it does**:
- ✅ Validates Markdown syntax
- ✅ Checks for broken links
- ✅ Verifies required files exist
- ✅ Validates directory structure
- ✅ Checks PlantUML syntax

**How to view**:
1. Go to PR page
2. Scroll to "Checks" section
3. Click on "Documentation Validation"

**If checks fail**:
```bash
# Run markdownlint locally
npm install -g markdownlint-cli
markdownlint '**/*.md' --ignore node_modules --config .markdownlint.json

# Fix issues and commit
git add .
git commit -m "fix: resolve markdown linting issues"
git push
```

#### 2. Auto-Label

**Triggers**: PR opened/edited, Issue opened/edited

**What it does**:
- 🏷️ Automatically adds labels based on:
  - Changed file paths
  - PR/issue title
  - Template type
  - Priority keywords

**Example labels added**:
- PR changing `docs/architecture/` → `architecture` + `documentation`
- PR title with "MVP" → `priority: high`
- PR title starting with "docs:" → `type: documentation`

#### 3. Stale Issue/PR Management

**Triggers**: Daily at 00:00 UTC

**What it does**:
- ⏰ Marks issues stale after 30 days of inactivity
- ⏰ Marks PRs stale after 14 days of inactivity
- 🗑️ Closes stale issues/PRs after 7 days
- 💡 Exempts `priority: critical` and `in progress` labels

**Preventing stale**:
- Add a comment to the issue/PR
- Add label `in progress` or `priority: critical`

---

## 🎯 Common Scenarios

### Scenario 1: Update MVP Architecture

```bash
# 1. Create issue (optional but recommended)
# Via GitHub UI or CLI:
gh issue create --title "Update MVP timeline with holiday buffer" \
  --body "Add 1 week buffer to accommodate New Year holidays"

# 2. Create branch
git checkout main
git pull origin main
git checkout -b docs/extend-mvp-timeline

# 3. Make changes
# Edit docs/architecture/MVP_ARCHITECTURE.md
# Update any references in PROJECT_SUMMARY.md

# 4. Commit changes
git add docs/architecture/MVP_ARCHITECTURE.md
git add docs/planning/PROJECT_SUMMARY.md
git commit -m "docs: extend MVP timeline to 15 weeks

- Add 1 week buffer for holidays
- Update launch date to Jan 20-27
- Adjust content creation schedule
- Update risk assessment

Closes #42"

# 5. Push and create PR
git push -u origin docs/extend-mvp-timeline
gh pr create --fill

# 6. Wait for review and CI checks
# 7. Merge PR (via GitHub UI)
# 8. Clean up
git checkout main
git pull origin main
git branch -d docs/extend-mvp-timeline
```

### Scenario 2: Add New Diagram

```bash
# 1. Create branch
git checkout main
git pull origin main
git checkout -b diagrams/add-auth-flow

# 2. Create diagram
# Create diagrams/sequence/sequence_authentication_flow.puml

# 3. Test diagram (optional but recommended)
# Open in VS Code with PlantUML extension
# Or generate PNG: plantuml diagrams/sequence/sequence_authentication_flow.puml

# 4. Update references
# Add link to FILE_GUIDE.md
# Mention in relevant architecture docs

# 5. Commit
git add diagrams/sequence/sequence_authentication_flow.puml
git add docs/guides/FILE_GUIDE.md
git commit -m "diagrams: add authentication flow sequence diagram

Add detailed sequence diagram showing:
- User login flow (email/password)
- OAuth authentication flow (Yandex, VK)
- JWT token generation and refresh
- Session management"

# 6. Push and create PR
git push -u origin diagrams/add-auth-flow
gh pr create --fill
```

### Scenario 3: Fix Typos Across Multiple Files

```bash
# 1. Create branch
git checkout main
git pull origin main
git checkout -b fix/typos-in-documentation

# 2. Fix typos in multiple files
# Edit multiple .md files

# 3. Stage all changes
git add .

# 4. Commit
git commit -m "fix: correct typos across documentation

- Fix spelling of 'authentication' in multiple files
- Correct grammar in MVP_ARCHITECTURE.md
- Fix date format inconsistencies"

# 5. Push and create PR
git push -u origin fix/typos-in-documentation
gh pr create --title "fix: correct typos across documentation" \
  --body "Minor typo and grammar fixes across multiple documentation files."
```

### Scenario 4: Refactor Documentation Structure

```bash
# 1. Create issue first (recommended for large changes)
gh issue create --title "Refactor planning documentation structure" \
  --body "Reorganize planning docs to separate backlog by priority"

# 2. Create branch
git checkout main
git pull origin main
git checkout -b refactor/reorganize-planning-docs

# 3. Make structural changes
# Move/rename files
# Update internal links

# 4. Commit logical chunks
git add docs/planning/backlog/
git commit -m "refactor: create backlog subdirectory structure

Create separate files for different priority backlogs:
- backlog/critical.md
- backlog/high-priority.md
- backlog/deferred.md"

git add docs/planning/PROJECT_BACKLOG.md
git commit -m "refactor: update main backlog to reference new structure"

git add docs/guides/FILE_GUIDE.md
git commit -m "docs: update FILE_GUIDE with new backlog structure"

# 5. Push and create PR
git push -u origin refactor/reorganize-planning-docs
gh pr create --title "refactor: reorganize planning documentation" \
  --body "## Summary
Split PROJECT_BACKLOG.md into priority-based files.

## Changes
- Create backlog/ subdirectory
- Split into critical/high/deferred files
- Update all internal references
- Update FILE_GUIDE.md

## Migration Notes
- Old PROJECT_BACKLOG.md archived
- All links updated
- No content changes

Closes #45"
```

### Scenario 5: Update After Backend Tech Stack Change

```bash
# 1. Create issue
gh issue create --title "Update all docs for C# backend migration" \
  --label "priority: critical,architecture"

# 2. Create branch
git checkout main
git pull origin main
git checkout -b docs/update-csharp-tech-stack

# 3. Update all references systematically
# Search and replace NestJS → ASP.NET Core
# Update code examples, commands, etc.

# 4. Commit by file type
git add docs/architecture/
git commit -m "docs(architecture): update tech stack to ASP.NET Core

- Replace NestJS references with ASP.NET Core 8
- Update ORM from Prisma to Entity Framework Core
- Update authentication to use ASP.NET Core Identity"

git add docs/planning/
git commit -m "docs(planning): update roadmap for C# tech stack

- Adjust Week 2 setup tasks
- Update prerequisites (add .NET 8 SDK)
- Revise development timeline estimates"

git add README.md ORGANIZATION.md
git commit -m "docs: update repository docs with C# tech stack

- Update README tech stack section
- Update ORGANIZATION.md backend description
- Update related repositories table"

git add docs/guides/FILE_GUIDE.md
git commit -m "docs(guides): update FILE_GUIDE backend references"

# 5. Push and create PR
git push -u origin docs/update-csharp-tech-stack
gh pr create --title "docs: migrate documentation to C# backend stack" \
  --body "## Summary
Update all documentation to reflect C# backend decision.

## Changes
- ✅ Architecture docs (MVP_ARCHITECTURE.md)
- ✅ Planning docs (roadmap, backlog)
- ✅ Repository structure docs (README, ORGANIZATION)
- ✅ Guides (FILE_GUIDE)

## Tech Stack Changes
| Component | Old | New |
|-----------|-----|-----|
| Framework | NestJS | ASP.NET Core 8 |
| ORM | Prisma | Entity Framework Core |
| Auth | Passport.js | ASP.NET Core Identity |

## Testing
- [x] All links verified
- [x] No broken references
- [x] Russian docs updated
- [x] Diagrams reviewed (no code-specific changes needed)

Closes #47"
```

---

## 🔧 Troubleshooting

### Problem: Branch is Behind Main

**Symptoms**:
```
Your branch is behind 'origin/main' by 5 commits
```

**Solution**:
```bash
# Option 1: Rebase (recommended - cleaner history)
git checkout docs/your-branch
git fetch origin
git rebase origin/main

# If conflicts occur:
# 1. Fix conflicts in editor
# 2. Stage resolved files
git add <resolved-files>
# 3. Continue rebase
git rebase --continue

# Push with force (only if you're the only one on this branch)
git push --force-with-lease

# Option 2: Merge (preserves full history)
git checkout docs/your-branch
git merge origin/main
git push
```

### Problem: Accidentally Committed to Main

**Symptoms**:
```
You're on main branch and made commits locally
```

**Solution**:
```bash
# If not pushed yet:
# 1. Create branch from current state
git branch docs/your-feature

# 2. Reset main to remote state
git checkout main
git reset --hard origin/main

# 3. Switch to your feature branch
git checkout docs/your-feature

# 4. Push feature branch
git push -u origin docs/your-feature
```

### Problem: Need to Undo Last Commit

**Solution**:
```bash
# Undo commit but keep changes (most common)
git reset --soft HEAD~1

# Undo commit and unstage changes
git reset HEAD~1

# Undo commit and discard changes (careful!)
git reset --hard HEAD~1
```

### Problem: CI Checks Failing

**Markdown Linting Errors**:
```bash
# Install markdownlint locally
npm install -g markdownlint-cli

# Run linter
markdownlint '**/*.md' --config .markdownlint.json

# Fix automatically where possible
markdownlint '**/*.md' --config .markdownlint.json --fix

# Commit fixes
git add .
git commit -m "fix: resolve markdown linting issues"
git push
```

**Broken Links**:
```bash
# Install link checker
npm install -g markdown-link-check

# Check specific file
markdown-link-check docs/architecture/MVP_ARCHITECTURE.md

# Fix broken links in editor
# Commit fixes
git add <fixed-files>
git commit -m "fix: repair broken links in documentation"
git push
```

**PlantUML Syntax Errors**:
```bash
# Install PlantUML
# Download from: https://plantuml.com/download

# Check syntax
java -jar plantuml.jar -syntax diagrams/your-diagram.puml

# Fix syntax errors in editor
# Test by generating diagram
java -jar plantuml.jar diagrams/your-diagram.puml

# Commit fixes
git add diagrams/your-diagram.puml
git commit -m "fix: correct PlantUML syntax errors"
git push
```

### Problem: Need to Update PR After Review

**Solution**:
```bash
# Make requested changes
# Edit files based on feedback

# Add and commit
git add <changed-files>
git commit -m "docs: address review feedback

- Clarify holiday schedule wording
- Add missing Russian translation
- Fix table formatting"

# Push (automatically updates PR)
git push
```

### Problem: Want to Split PR into Smaller PRs

**Solution**:
```bash
# 1. Create new branches for each logical change
git checkout -b docs/update-timeline
git cherry-pick <commit-hash-for-timeline>
git push -u origin docs/update-timeline

git checkout -b docs/update-backlog
git cherry-pick <commit-hash-for-backlog>
git push -u origin docs/update-backlog

# 2. Close original PR
# 3. Create new PRs from smaller branches
```

---

## 📚 Additional Resources

### GitHub CLI Cheatsheet

```bash
# Install GitHub CLI
# Windows: winget install --id GitHub.cli
# Mac: brew install gh

# Authenticate
gh auth login

# Create issue
gh issue create

# List issues
gh issue list

# Create PR
gh pr create --fill

# List PRs
gh pr list

# View PR in browser
gh pr view --web

# Checkout PR locally
gh pr checkout 123

# Review PR
gh pr review --approve
gh pr review --comment -b "Looks good!"
gh pr review --request-changes -b "Please fix X"

# Merge PR
gh pr merge 123 --squash
```

### Git Aliases (Add to ~/.gitconfig)

```ini
[alias]
  # Shortcuts
  co = checkout
  br = branch
  ci = commit
  st = status

  # Useful commands
  up = pull --rebase origin main
  logo = log --oneline --graph --decorate
  last = log -1 HEAD
  unstage = reset HEAD --

  # Branch cleanup
  bclean = "!git branch --merged | grep -v '\\*\\|main' | xargs -n 1 git branch -d"
```

---

## 🎓 Best Practices

### DO ✅

- **Create issues before starting work** on significant changes
- **Use semantic commit messages** consistently
- **Keep PRs focused** on a single logical change
- **Update both English and Russian** documentation when applicable
- **Reference issues** in commits and PRs
- **Respond to review feedback** promptly
- **Test locally** before pushing (markdownlint, link checks)
- **Keep branches short-lived** (merge within 1-3 days)
- **Delete merged branches** to keep repository clean
- **Use draft PRs** for work in progress

### DON'T ❌

- **Don't commit to main directly** (use branches and PRs)
- **Don't leave stale branches** (clean up after merge)
- **Don't create large PRs** (split into smaller logical chunks)
- **Don't ignore CI failures** (fix before merging)
- **Don't force push to shared branches** (only to your own branches)
- **Don't forget to pull** before creating new branches
- **Don't use vague commit messages** ("updated docs")
- **Don't mix unrelated changes** in one commit/PR

---

## 📞 Getting Help

**Questions about workflow?**
- Create an issue with `question` label
- Ask in team chat/communication channel

**Found a bug in CI?**
- Create an issue with `ci/cd` label
- Include error messages and workflow run URL

**Need workflow improvement?**
- Create an issue with `enhancement` label
- Propose your idea and rationale

---

**Last Updated**: 2025-10-14
**Version**: 1.0
**Maintainer**: COOKie Architecture Team
