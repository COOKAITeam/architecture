# Quick Reference Card

> **One-page guide for common Git operations in COOKie architecture repository**

## 🚀 Starting New Work

```bash
git checkout main && git pull origin main
git checkout -b docs/your-feature-name
```

## ✏️ Making Changes

```bash
# Edit files, then:
git add <files>
git commit -m "docs: brief description"
git push -u origin docs/your-feature-name
```

## 🔄 Creating Pull Request

**Via GitHub CLI**:
```bash
gh pr create --fill
```

**Via Web**: Go to https://github.com/COOKAITeam/architecture and click "Compare & pull request"

## 🔀 Keeping Branch Updated

```bash
git checkout main && git pull origin main
git checkout docs/your-branch
git rebase main
git push --force-with-lease
```

## ✅ After PR Merge

```bash
git checkout main && git pull origin main
git branch -d docs/your-branch
```

## 📝 Commit Message Format

```
<type>: <subject>

<body>

Closes #123
```

**Types**: `docs`, `diagrams`, `feat`, `fix`, `refactor`, `chore`

## 🏷️ Branch Naming

- `docs/update-mvp-architecture`
- `diagrams/add-auth-flow`
- `fix/broken-links`
- `refactor/reorganize-planning`

## 🎫 Issue Creation

https://github.com/COOKAITeam/architecture/issues/new/choose

## ⚙️ Local Testing

```bash
# Markdown linting
npm install -g markdownlint-cli
markdownlint '**/*.md' --config .markdownlint.json --fix

# Link checking
npm install -g markdown-link-check
markdown-link-check README.md
```

## 🆘 Common Problems

**Branch behind main?**
```bash
git rebase origin/main
```

**Undo last commit (keep changes)?**
```bash
git reset --soft HEAD~1
```

**Committed to main by mistake?**
```bash
git branch docs/your-feature  # Save work
git checkout main
git reset --hard origin/main  # Reset main
git checkout docs/your-feature  # Continue on branch
```

## 📚 Full Documentation

See [GIT_WORKFLOW.md](../docs/guides/GIT_WORKFLOW.md) for comprehensive guide.
