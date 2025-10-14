# Working with COOKie Architecture

> **Note**: This is a private repository for the COOKie development team.
>
> This guide is for current team members and future co-workers.

## Getting Started

1. **Read the documentation**:
   - [README.md](README.md) - Project overview
   - [FILE_GUIDE.md](docs/guides/FILE_GUIDE.md) - File organization
   - [MVP_ARCHITECTURE.md](docs/architecture/MVP_ARCHITECTURE.md) - Technical architecture

2. **Check existing issues**: Before creating a new issue, search existing ones to avoid duplicates

3. **Check backlog**: See [PROJECT_BACKLOG.md](docs/planning/PROJECT_BACKLOG.md) for current tasks

## How to Work with Documentation

### Reporting Issues

Use the appropriate issue template:
- **Architecture questions**: Use "Architecture Question" template
- **Documentation issues**: Use "Documentation Update" template
- **Diagram requests**: Use "Diagram Request" template

### Making Changes

1. **Create a branch**: Use descriptive names
   - `docs/update-mvp-timeline`
   - `diagrams/add-auth-flow`
   - `planning/update-backlog`

3. **Make your changes**:
   - Follow existing formatting and structure
   - Update both English and Russian versions (if applicable)
   - Ensure diagrams are in PlantUML format

4. **Commit your changes**:
   ```bash
   # Use semantic commit messages
   git commit -m "docs: update MVP launch date"
   git commit -m "diagrams: add user registration sequence"
   git commit -m "planning: mark task CRIT-002 as completed"
   ```

5. **Push your branch**:
   ```bash
   git push origin your-branch-name
   ```

6. **Create a Pull Request**:
   - Use the PR template
   - Reference related issues
   - Provide clear description of changes
   - Request review from lead developer

## Documentation Standards

### Markdown Files

- Use clear, concise language
- Include table of contents for long documents
- Use proper heading hierarchy (H1 → H2 → H3)
- Add examples where helpful
- Link to related documents

### Diagrams

- **Format**: PlantUML (`.puml` extension)
- **Location**: Appropriate subfolder in `diagrams/`
- **Naming**: Descriptive, lowercase with underscores
  - Good: `mvp_simplified_architecture.puml`
  - Bad: `diagram1.puml`
- **Comments**: Add comments to explain complex parts

### File Organization

Follow the structure in [FILE_GUIDE.md](docs/guides/FILE_GUIDE.md):
- `docs/architecture/` - Technical architecture
- `docs/requirements/` - Requirements specs
- `docs/business/` - Business documentation
- `docs/planning/` - Project management
- `diagrams/` - PlantUML diagrams (organized by type)

## Commit Message Format

We follow semantic commit messages:

```
<type>: <description>

[optional body]

[optional footer]
```

**Types**:
- `docs`: Documentation updates
- `diagrams`: Diagram changes
- `planning`: Backlog or planning updates
- `fix`: Fix errors in documentation
- `refactor`: Restructure without changing content

**Examples**:
```
docs: update MVP timeline to 15 weeks

Added 1-week buffer for holidays. Launch date now Jan 20-27 instead of Jan 13-19.

Closes #42
```

```
diagrams: add user authentication sequence

Created sequence diagram showing OAuth flow for Yandex and VK authentication.

Related to #35
```

## Review Process

1. **Automated checks**: (if configured)
   - Markdown linting
   - Broken link detection
   - PlantUML syntax validation

2. **Manual review**:
   - At least one reviewer required
   - Check for clarity and accuracy
   - Ensure consistency with existing docs

3. **Approval**: Reviewer approves PR

4. **Merge**: Maintainer merges to `main`

## Team Guidelines

- Keep documentation clear and professional
- Focus on accuracy and consistency
- Ask questions when something is unclear
- Keep discussions on-topic and productive

## Questions?

- Create an issue with the "Architecture Question" template
- Check [FILE_GUIDE.md](docs/guides/FILE_GUIDE.md) for navigation help
- Review [PROJECT_SUMMARY.md](docs/planning/PROJECT_SUMMARY.md) for context
- Contact lead developer directly for urgent matters

---

**Repository**: COOKie Architecture (Private)
**Team**: Development team only
