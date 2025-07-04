# GitHub Tutorial for Software Engineers

A comprehensive guide for using GitHub in professional software development environments.

## 1. Git Basics

### Initial Setup
```bash
# Configure global settings
git config --global user.name "Your Name"
git config --global user.email "your.email@company.com"

# Check configuration
git config --list
```

### Repository Operations
```bash
# Clone repository
git clone https://github.com/company/project.git

# Initialize new repository
git init
git remote add origin https://github.com/company/project.git
```

## 2. Daily Workflow

### Basic Commands
```bash
# Check status
git status

# Add files
git add .                    # Add all files
git add filename.py          # Add specific file

# Commit changes
git commit -m "Add user authentication feature"

# Push changes
git push origin main

# First time push (sets up tracking)
git push -u origin main        # -u sets upstream tracking
```

### Understanding -u Flag
The `-u` (or `--set-upstream`) flag establishes a tracking relationship:
```bash
# With -u: Sets up tracking between local and remote branch
git push -u origin main

# After tracking is set, you can use shorthand:
git push                       # Automatically pushes to tracked remote
git pull                       # Automatically pulls from tracked remote

# Check tracking relationships
git branch -vv
```

### Pulling Updates
```bash
# Fetch and merge latest changes
git pull origin main

# Fetch without merging
git fetch origin
```

## 3. Branching Strategy

### Create and Switch Branches
```bash
# Create new branch
git checkout -b feature/user-auth

# Switch to existing branch
git checkout main

# List all branches
git branch -a

# Delete branch
git branch -d feature/user-auth
```

### Common Branch Types
- `main/master` - Production code
- `develop` - Development integration
- `feature/feature-name` - New features
- `bugfix/bug-description` - Bug fixes
- `hotfix/critical-fix` - Critical production fixes

## 4. Collaboration Workflow

### Pull Requests (PRs)
```bash
# 1. Create feature branch
git checkout -b feature/new-api

# 2. Make changes and commit
git add .
git commit -m "Implement new API endpoints"

# 3. Push branch
git push origin feature/new-api

# 4. Create PR on GitHub web interface
```

### Code Review Process
1. **Create PR** with clear title and description
2. **Assign reviewers** from your team
3. **Address feedback** by pushing new commits
4. **Merge** after approval
5. **Delete branch** after merging

## 5. Advanced Git Operations

### Merge vs Rebase
```bash
# Merge (preserves commit history)
git merge feature/new-feature

# Rebase (cleaner history)
git rebase main
```

### Stashing Changes
```bash
# Save current work temporarily
git stash

# Apply stashed changes
git stash pop

# List stashes
git stash list
```

### Undoing Changes
```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert specific commit
git revert commit-hash
```

## 6. GitHub Features

### Issues and Project Management
```bash
# Reference issues in commits
git commit -m "Fix login bug - closes #123"

# Link PRs to issues
git commit -m "Add user validation - resolves #456"
```

### GitHub Actions (CI/CD)
Create `.github/workflows/ci.yml`:
```yaml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Python
        uses: actions/setup-python@v3
        with:
          python-version: '3.9'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: pytest
```

## 7. Organization Best Practices

### Commit Message Standards
```bash
# Format: type(scope): description
feat(auth): add JWT token validation
fix(api): resolve null pointer exception
docs(readme): update installation instructions
test(user): add unit tests for user service
```

### Branch Protection Rules
- Require PR reviews before merging
- Require status checks to pass
- Restrict force pushes to main
- Delete head branches after merge

### .gitignore Best Practices
```bash
# Python
__pycache__/
*.pyc
.env
venv/

# Node.js
node_modules/
npm-debug.log

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db
```

## 8. Security and Access Control

### SSH Key Setup
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@company.com"

# Add to SSH agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Add public key to GitHub account
cat ~/.ssh/id_ed25519.pub
```

### Personal Access Tokens
- Use for HTTPS authentication
- Set appropriate scopes
- Store securely (environment variables)
- Rotate regularly

## 9. Troubleshooting Common Issues

### Merge Conflicts
```bash
# When conflict occurs
git status                   # See conflicted files
# Edit files to resolve conflicts
git add resolved-file.py
git commit -m "Resolve merge conflict"
```

### Large File Handling
```bash
# Install Git LFS
git lfs install

# Track large files
git lfs track "*.zip"
git add .gitattributes
```

### Repository Cleanup
```bash
# Remove untracked files
git clean -fd

# Compress repository
git gc --aggressive
```

## 10. Team Workflows

### Git Flow
```bash
# Start new feature
git flow feature start new-feature

# Finish feature
git flow feature finish new-feature

# Create release
git flow release start 1.0.0
```

### Semantic Versioning
- `MAJOR.MINOR.PATCH` (e.g., 2.1.3)
- Major: Breaking changes
- Minor: New features (backward compatible)
- Patch: Bug fixes

### Release Management
```bash
# Create tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Push tags
git push origin --tags

# Create release on GitHub
# Use GitHub web interface or GitHub CLI
```

## 11. Monitoring and Analytics

### Useful GitHub Features
- **Insights**: Repository traffic and contributions
- **Security**: Vulnerability alerts and dependency scanning
- **Actions**: CI/CD pipeline monitoring
- **Projects**: Kanban boards for task management

### Git Aliases (Productivity)
```bash
# Add to ~/.gitconfig
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
```

## 12. Emergency Procedures

### Hotfix Workflow
```bash
# 1. Create hotfix branch from main
git checkout main
git checkout -b hotfix/critical-security-fix

# 2. Make fix and test
git add .
git commit -m "hotfix: patch security vulnerability"

# 3. Create emergency PR
git push origin hotfix/critical-security-fix

# 4. Merge to main and develop
# 5. Tag release
git tag -a v1.0.1 -m "Hotfix release 1.0.1"
```

### Rollback Procedures
```bash
# Revert to previous release
git checkout main
git revert commit-hash

# Force reset (use with caution)
git reset --hard previous-commit-hash
git push --force-with-lease origin main
```

This guide covers essential GitHub operations for professional software development. Always follow your organization's specific workflows and policies.