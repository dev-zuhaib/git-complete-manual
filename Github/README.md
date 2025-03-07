# The Complete GitHub Guide

**Created by:** dev-zuhaib  
**Last updated:** 2025-03-07

## Table of Contents
- [Introduction](#introduction)
- [Account Setup and Management](#account-setup-and-management)
- [Repositories](#repositories)
- [GitHub Flow](#github-flow)
- [Pull Requests](#pull-requests)
- [Issues](#issues)
- [Project Management](#project-management)
- [GitHub Actions](#github-actions)
- [GitHub Pages](#github-pages)
- [Security Features](#security-features)
- [GitHub CLI](#github-cli)
- [GitHub API](#github-api)
- [Teams and Organizations](#teams-and-organizations)
- [GitHub Marketplace & Integrations](#github-marketplace--integrations)
- [Advanced Features](#advanced-features)
- [GitHub Enterprise](#github-enterprise)
- [Best Practices](#best-practices)

## Introduction

### What is GitHub?

GitHub is a web-based platform built on top of Git that provides hosting for software development version control and collaboration. It offers all of the distributed version control and source code management (SCM) functionality of Git plus its own features.

### Core Features

- **Version Control**: Track changes and maintain a history of your codebase
- **Collaboration**: Enable multiple people to work together on projects
- **Pull Requests**: Review code before merging it
- **Issues**: Track bugs, feature requests, and tasks
- **Project Management**: Organize work with project boards
- **Actions**: Automate workflows
- **Security**: Scan code for vulnerabilities
- **Web Hosting**: Host documentation and static websites

## Account Setup and Management

### Creating a GitHub Account

1. Visit [github.com](https://github.com)
2. Fill in username, email, and password
3. Verify your account

### Setting Up Your Profile

Your GitHub profile serves as your developer identity.

1. Add a profile picture
2. Write a bio
3. Add your location, company, and website
4. Pin important repositories

**Profile README:**
Create a special repository named exactly the same as your username to add a README to your profile page.

```
https://github.com/username/username
```

Example:
```markdown
# Hello, I'm Dev Zuhaib 👋

I'm a software developer passionate about open-source projects.

## My Skills
- JavaScript/TypeScript
- React & Node.js
- Cloud Infrastructure

## Connect with me
- [Website](https://example.com)
- [LinkedIn](https://linkedin.com/in/username)
```

### Authentication

**Setting up SSH Keys:**
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start ssh-agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (Mac)
pbcopy < ~/.ssh/id_ed25519.pub
# Windows (PowerShell)
# Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard
# Linux
# cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard
```

Then add the key to GitHub under Settings → SSH and GPG keys.

**Personal Access Tokens:**
1. Go to Settings → Developer settings → Personal access tokens
2. Click "Generate new token"
3. Select scopes based on needed permissions
4. Use the token for HTTPS authentication

### Profile Settings

- **Two-factor authentication**: Set up 2FA for enhanced security
- **Notification settings**: Configure email and web notifications
- **Email settings**: Manage verified emails and notification preferences
- **Appearance**: Toggle between light and dark mode
- **Account settings**: Change username, delete account, etc.

## Repositories

### Creating a Repository

**Through the Web Interface:**
1. Click the + icon in the top-right and select "New repository"
2. Fill in repository name, description, visibility, and initialization options
3. Click "Create repository"

**Through the CLI:**
```bash
# Initialize local directory
git init

# Connect to GitHub repo
git remote add origin https://github.com/username/repo-name.git

# Push initial commit
git add .
git commit -m "Initial commit"
git push -u origin main
```

### Repository Settings

- **General**: Change name, visibility, features, merge options
- **Collaborators**: Add users who can contribute to your repo
- **Branches**: Configure protection rules
- **Webhooks**: Set up notifications to external services
- **Pages**: Configure GitHub Pages
- **Actions**: Manage GitHub Actions permissions
- **Security**: Configure security policies and features

### README and Documentation

A good README typically includes:

1. Project name and description
2. Installation instructions
3. Usage examples
4. Contribution guidelines
5. License information

**Other documentation files:**
- `CONTRIBUTING.md`: Guidelines for contributors
- `CODE_OF_CONDUCT.md`: Community behavior expectations
- `LICENSE`: Legal terms for using your code
- `SECURITY.md`: Vulnerability reporting procedure

### GitHub Templates

Templates help standardize issues and PRs:

1. Create `.github` directory in your repository
2. Add template files:
   - `ISSUE_TEMPLATE/bug_report.md`
   - `ISSUE_TEMPLATE/feature_request.md`
   - `PULL_REQUEST_TEMPLATE.md`

Example bug report template:
```markdown
---
name: Bug Report
about: Create a report to help us improve
title: '[BUG] '
labels: 'bug'
assignees: ''
---

**Describe the bug**
A clear description of the issue.

**To Reproduce**
Steps to reproduce the behavior.

**Expected behavior**
What you expected to happen.

**Screenshots**
If applicable, add screenshots.

**Environment**
 - OS: [e.g. Windows 10]
 - Browser: [e.g. Chrome 92]
 - Version: [e.g. 2.1.0]
```

### Repository Insights

GitHub provides analytics about your repository:
- **Pulse**: Activity overview
- **Contributors**: Who contributed and how much
- **Community**: Health metrics and recommended practices
- **Traffic**: Views and clones
- **Commits**: Commit history and patterns
- **Code frequency**: Additions and deletions over time
- **Dependency graph**: Package dependencies

## GitHub Flow

GitHub Flow is a lightweight, branch-based workflow:

1. **Create a branch** from the repository
2. **Make changes** and add commits
3. **Open a pull request**
4. **Review and discuss** the code
5. **Deploy** for final testing (optional)
6. **Merge** the pull request

### Branching Strategies

**Common Branch Types:**
- `main` or `master`: Production-ready code
- `develop`: Integration branch for features
- `feature/*`: New features
- `hotfix/*`: Urgent fixes for production
- `release/*`: Preparing for a release

**Protection Rules:**
1. Go to repository settings → Branches
2. Click "Add rule" next to branch protection rules
3. Configure options like:
   - Require pull request reviews
   - Require status checks
   - Require signed commits
   - Include administrators
   - Restrict who can push

## Pull Requests

Pull Requests (PRs) are the heart of collaboration on GitHub.

### Creating a Pull Request

1. Push your branch to GitHub
2. Navigate to your repository
3. Click "Compare & pull request"
4. Fill in the PR title and description
5. Select reviewers, assignees, labels
6. Click "Create pull request"

**Through the CLI (with GitHub CLI):**
```bash
gh pr create --title "Add new feature" --body "This PR implements..." --reviewer username
```

### Anatomy of a Pull Request

- **Title**: Short, descriptive summary
- **Description**: Detailed explanation
- **Assignees**: People responsible for the PR
- **Reviewers**: People who should review the code
- **Labels**: Categories for the PR
- **Projects**: Project boards the PR belongs to
- **Milestone**: Release this PR is targeting
- **Linked issues**: Issues this PR addresses

### Code Reviews

**Review Process:**
1. Examine code changes in the "Files changed" tab
2. Add comments on specific lines
3. Suggest changes using the suggestion feature
4. Submit your review with:
   - Comment: General feedback
   - Approve: Ready to merge
   - Request changes: Needs modifications

**Best Practices:**
- Be respectful and constructive
- Review for correctness, style, and performance
- Consider edge cases
- Ask questions instead of making demands
- Use suggestions for minor fixes

### Merging Options

- **Merge commit**: Preserves all commits and creates a merge commit
- **Squash and merge**: Combines all commits into one
- **Rebase and merge**: Applies changes without a merge commit

**Auto-merge:**
Enable auto-merge to automatically merge a PR when all requirements are met.

### Managing Pull Requests

**Resolving conflicts:**
1. GitHub will indicate if there are conflicts
2. Click on "Resolve conflicts" button
3. Edit the file to fix the conflicts
4. Mark as resolved and commit

**Linking issues:**
Use keywords in PR description to automatically link issues:
- `closes #123`
- `fixes #456`
- `resolves #789`

## Issues

Issues are used to track ideas, feedback, tasks, bugs, and feature requests.

### Creating Issues

1. Go to the repository's "Issues" tab
2. Click "New issue"
3. Choose a template if available
4. Fill in title and description
5. Add labels, assignees, projects, and milestone

**Through the CLI:**
```bash
gh issue create --title "Bug in login form" --body "When submitting..."
```

### Issue Fields

- **Title**: Brief description
- **Description**: Detailed explanation with steps, screenshots
- **Assignees**: Who should work on this
- **Labels**: Categorize the issue (bug, enhancement, etc.)
- **Projects**: Assign to project boards
- **Milestone**: Group with related issues for a release
- **Linked pull requests**: PRs that address this issue

### Issue Templates

Create issue templates to standardize reporting:
1. Go to repository settings → Options
2. Scroll to "Features" and click "Set up templates"
3. Create templates for bug reports, feature requests, etc.

### Managing Issues

- **Filtering**: Use search queries to find issues
- **Sorting**: Arrange by newest, oldest, most commented, etc.
- **Pinning**: Pin important issues to the top
- **Closing**: Close resolved or invalid issues
- **Reopening**: Reopen if the issue resurfaces
- **Transfer**: Move to another repository

**Search Syntax:**
```
is:issue is:open label:bug assignee:username
```

## Project Management

GitHub offers project management tools to organize and prioritize work.

### Project Boards

**Types of Project Boards:**
- **Repository projects**: Linked to a single repository
- **Organization projects**: Span multiple repositories
- **User projects**: Personal project boards

**Creating a Project Board:**
1. Go to repository or organization
2. Click "Projects" tab
3. Click "New project"
4. Choose a template or start from scratch
5. Name your project and add a description

### Project Views

GitHub Projects (new version) offers multiple views:
- **Table**: Spreadsheet-like view
- **Board**: Kanban-style columns
- **Roadmap**: Timeline view
- **Custom fields**: Track priority, status, etc.

### Automation

**Default automation:**
- Newly added issues go to "To do"
- Newly opened PRs go to "In progress"
- Closed issues/PRs go to "Done"

**Custom automation rules:**
1. Click "..." on a column
2. Select "Manage automation"
3. Configure triggers and actions

### Milestones

Milestones group issues and PRs for a specific goal or timeframe:

1. Go to "Issues" or "Pull Requests" tab
2. Click "Milestones"
3. Click "New milestone"
4. Add title, due date, and description

### Labels

Labels categorize issues and PRs:

1. Go to "Issues" tab
2. Click "Labels"
3. Click "New label"
4. Choose name, description, and color

**Default labels include:**
- bug
- documentation
- duplicate
- enhancement
- good first issue
- help wanted
- invalid
- question
- wontfix

## GitHub Actions

GitHub Actions automate workflows directly in your repository.

### Workflow Basics

Workflows are defined in YAML files in `.github/workflows/`:

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '16'
        
    - name: Install dependencies
      run: npm ci
      
    - name: Run tests
      run: npm test
```

### Common Workflow Triggers

- **push**: Run when commits are pushed
- **pull_request**: Run when PRs are opened or updated
- **schedule**: Run on a schedule using cron syntax
- **workflow_dispatch**: Manual trigger
- **repository_dispatch**: Trigger via REST API
- **issues**: Trigger on issue events
- **release**: Trigger on release events

### Jobs and Steps

- **Jobs**: Independent units that run in parallel by default
- **Steps**: Sequential tasks within a job

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Step 1
        run: echo "Running step 1"
        
  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Deploy
        run: echo "Deploying..."
```

### Environment Variables and Secrets

**Environment Variables:**
```yaml
env:
  NODE_ENV: production
  
jobs:
  build:
    env:
      DATABASE_URL: mongodb://localhost:27017
    steps:
      - name: Step with specific env
        env:
          SPECIAL_TOKEN: value
        run: echo $SPECIAL_TOKEN
```

**Secrets:**
1. Go to repository settings → Secrets → Actions
2. Click "New repository secret"
3. Add name and value

```yaml
steps:
  - name: Use secret
    env:
      API_TOKEN: ${{ secrets.API_TOKEN }}
    run: ./script.sh
```

### Marketplace Actions

GitHub Marketplace offers pre-built actions for common tasks:

```yaml
steps:
  # Deploy to AWS
  - name: Configure AWS credentials
    uses: aws-actions/configure-aws-credentials@v1
    with:
      aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-region: us-east-1
```

### Workflow Artifacts

Share data between jobs with artifacts:

```yaml
jobs:
  build:
    steps:
      - name: Create artifact
        run: echo hello > output.txt
      - name: Upload artifact
        uses: actions/upload-artifact@v3
        with:
          name: my-artifact
          path: output.txt
          
  deploy:
    needs: build
    steps:
      - name: Download artifact
        uses: actions/download-artifact@v3
        with:
          name: my-artifact
```

### Matrix Builds

Run tests across multiple configurations:

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [14.x, 16.x, 18.x]
        os: [ubuntu-latest, windows-latest, macos-latest]
    
    steps:
      - uses: actions/checkout@v3
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm test
```

### Self-hosted Runners

Run workflows on your own infrastructure:

1. Go to repository settings → Actions → Runners
2. Click "New self-hosted runner"
3. Follow setup instructions

```yaml
jobs:
  build:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v3
      # more steps...
```

## GitHub Pages

GitHub Pages hosts static websites directly from your repositories.

### Setting Up GitHub Pages

**For user/organization sites:**
1. Create a repository named `username.github.io`
2. Push HTML/CSS/JS files to the main branch

**For project sites:**
1. Go to repository settings → Pages
2. Select branch and folder (usually main/root or main/docs)

### Jekyll Support

GitHub Pages supports Jekyll for static site generation:

1. Add a `_config.yml` file to your repository
2. Create Markdown files for content
3. GitHub automatically builds the site

**Simple _config.yml:**
```yaml
theme: jekyll-theme-minimal
title: My Project Documentation
description: Comprehensive guide to my project
```

### Custom Domains

Add a custom domain to your GitHub Pages site:

1. Go to repository settings → Pages
2. Under "Custom domain," enter your domain
3. Create a CNAME record with your DNS provider
4. Add a `CNAME` file to your repository with your domain

### GitHub Pages Limitations

- GitHub Pages sites are public (even from private repos)
- Size limit of 1GB
- Soft bandwidth limit of 100GB/month
- Build limit of 10 builds/hour

## Security Features

GitHub offers various security features to protect your code.

### Dependency Scanning

**Dependabot alerts:**
1. Go to repository settings → Security & analysis
2. Enable Dependabot alerts
3. Receive notifications about vulnerabilities

**Dependabot security updates:**
Automatically create PRs to update vulnerable dependencies.

**Dependency review:**
Review dependency changes in PRs.

### Code Scanning

**CodeQL Analysis:**
1. Go to repository settings → Security & analysis
2. Enable code scanning
3. Configure workflow
4. Review and fix alerts

Example workflow:
```yaml
name: "CodeQL"

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  schedule:
    - cron: '0 0 * * 0'

jobs:
  analyze:
    name: Analyze
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout repository
      uses: actions/checkout@v3
      
    - name: Initialize CodeQL
      uses: github/codeql-action/init@v2
      with:
        languages: javascript, python
        
    - name: Perform CodeQL Analysis
      uses: github/codeql-action/analyze@v2
```

### Secret Scanning

GitHub automatically scans repositories for known types of secrets:

1. Go to repository settings → Security & analysis
2. Enable secret scanning
3. GitHub will alert you if credentials are committed

### Security Policy

Create a `SECURITY.md` file with:
1. Supported versions
2. Reporting process
3. Disclosure policy
4. Expected response time

### Security Advisories

Create private forks to fix vulnerabilities:

1. Go to Security tab → Advisories
2. Click "New draft security advisory"
3. Fill in details
4. Request a CVE (Common Vulnerabilities and Exposures)
5. Create a temporary private fork to fix the issue

## GitHub CLI

GitHub CLI (`gh`) is a command-line tool for GitHub.

### Installation

**macOS:**
```bash
brew install gh
```

**Windows:**
```bash
winget install --id GitHub.cli
```

**Linux (Ubuntu):**
```bash
sudo apt install gh
```

### Authentication

```bash
gh auth login
```

### Common Commands

**Repository commands:**
```bash
# Clone repository
gh repo clone username/repo

# Create repository
gh repo create my-project --public

# Fork repository
gh repo fork username/repo
```

**PR commands:**
```bash
# Create PR
gh pr create --title "Fix bug" --body "Description"

# List PRs
gh pr list

# Check out a PR
gh pr checkout 123

# Review PR
gh pr review 123 --approve

# Merge PR
gh pr merge 123
```

**Issue commands:**
```bash
# Create issue
gh issue create --title "Bug report" --body "Details"

# List issues
gh issue list

# Close issue
gh issue close 123

# Reopen issue
gh issue reopen 123
```

**Workflow commands:**
```bash
# List workflows
gh workflow list

# Run workflow
gh workflow run workflow.yml

# View workflow runs
gh run list
```

## GitHub API

GitHub provides a REST and GraphQL API for programmatic access.

### REST API Basics

**Authentication:**
```bash
curl -H "Authorization: token YOUR_TOKEN" \
  https://api.github.com/user
```

**Get repository information:**
```bash
curl https://api.github.com/repos/username/repo
```

**Create an issue:**
```bash
curl -X POST \
  -H "Authorization: token YOUR_TOKEN" \
  -d '{"title":"API Test Issue","body":"Created via API"}' \
  https://api.github.com/repos/username/repo/issues
```

### GraphQL API

**Simple query:**
```graphql
query {
  repository(owner: "username", name: "repo") {
    issues(last: 5, states: OPEN) {
      edges {
        node {
          title
          url
          createdAt
        }
      }
    }
  }
}
```

**Using curl:**
```bash
curl -X POST \
  -H "Authorization: bearer YOUR_TOKEN" \
  -d '{"query": "query { viewer { login } }"}' \
  https://api.github.com/graphql
```

### Webhooks

Webhooks send HTTP POST payloads when events occur:

1. Go to repository settings → Webhooks
2. Click "Add webhook"
3. Set payload URL, content type, and secret
4. Select events to trigger the webhook
5. Click "Add webhook"

## Teams and Organizations

GitHub Organizations help manage team access and permissions.

### Creating an Organization

1. Click your profile photo → Settings → Organizations
2. Click "New organization"
3. Choose a plan
4. Fill in organization name and contact email

### Teams

Teams group members and set permissions:

1. Go to organization → Teams tab
2. Click "New team"
3. Set team name, description, and parent team
4. Add members
5. Grant repository access

**Team permission levels:**
- Read: View and clone 
- Triage: Manage issues and PRs
- Write: Push to non-protected branches
- Maintain: Push to protected branches
- Admin: Full access

### Organization Settings

- **Member privileges**: Default permissions, base repository access
- **Repository defaults**: Issue templates, workflow permissions
- **Security**: 2FA enforcement, IP allow list
- **OAuth Apps**: Manage third-party access
- **Audit log**: Track organization activities

### Enterprise Features

- **SAML single sign-on**: Enterprise authentication
- **SCIM provisioning**: Automatic user management
- **Audit log streaming**: Real-time security events
- **IP allow lists**: Restrict access by IP address
- **Enterprise policies**: Organization-wide settings

## GitHub Marketplace & Integrations

GitHub Marketplace offers tools and services to extend GitHub's functionality.

### Popular Integration Categories

- **CI/CD**: Travis CI, CircleCI, Jenkins
- **Code quality**: SonarCloud, CodeFactor, DeepScan
- **Project management**: ZenHub, Jira, Trello
- **Security**: Snyk, WhiteSource, Veracode
- **Monitoring**: Sentry, Datadog, New Relic
- **Deployment**: Heroku, Netlify, Vercel

### Installing GitHub Apps

1. Find the app on GitHub Marketplace
2. Click "Set up plan"
3. Choose plan and billing
4. Select repositories to install on
5. Authorize access

### OAuth Apps vs. GitHub Apps

**OAuth Apps:**
- Act on behalf of a user
- Access determined by user's permissions
- User-to-server tokens

**GitHub Apps:**
- Act as their own entity
- Fine-grained permissions
- Server-to-server tokens
- Can be installed on specific repositories

### Creating Custom GitHub Apps

1. Go to Settings → Developer settings → GitHub Apps
2. Click "New GitHub App"
3. Fill in app details and permissions
4. Set webhook URL
5. Generate private key

## Advanced Features

### GitHub Codespaces

Cloud-based development environments:

1. Click "Code" button on repository
2. Select "Open with Codespaces"
3. Choose a configuration or create new

```json
// .devcontainer/devcontainer.json
{
  "name": "Node.js",
  "image": "mcr.microsoft.com/devcontainers/javascript-node:0-18",
  "forwardPorts": [3000],
  "extensions": [
    "dbaeumer.vscode-eslint"
  ]
}
```

### GitHub Copilot

AI pair programmer:

1. Install GitHub Copilot extension in VS Code
2. Sign in with GitHub account
3. Enable for languages in settings
4. Start coding with AI suggestions

### GitHub Discussions

Community conversations:

1. Go to repository settings → Options
2. Enable Discussions feature
3. Create categories
4. Start discussions with:
   - Q&A format
   - Announcements
   - General discussions
   - Ideas

### GitHub Sponsors

Fund open source development:

1. Go to GitHub Sponsors page
2. Click "Join the waitlist" or "Set up GitHub Sponsors"
3. Complete profile and payment details
4. Set up tiers and goals

### GitHub Mobile

Access GitHub on the go:

1. Download GitHub Mobile from App Store or Google Play
2. Sign in with GitHub account
3. Review notifications, PRs, and issues
4. Merge PRs and respond to comments

## GitHub Enterprise

GitHub Enterprise offers advanced features for large organizations.

### GitHub Enterprise Cloud

- Hosted on GitHub's infrastructure
- SAML/SCIM integration
- 50,000 minutes of GitHub Actions
- 99.95% uptime SLA
- Advanced security features
- Priority support

### GitHub Enterprise Server

- Self-hosted on your infrastructure
- Compatible with GitHub Actions
- Cluster deployment options
- Data residency compliance
- LDAP/AD integration
- Audit logging

### Migration to GitHub Enterprise

1. Assess current systems and repositories
2. Set up organizations and teams
3. Configure SSO and user management
4. Import repositories
5. Set up CI/CD pipelines
6. Train users

## Best Practices

### Repository Structure

- Clear, descriptive name
- Well-documented README
- Consistent organization
- .gitignore for build artifacts
- Small, focused repositories over monoliths

### Branching Strategy

Choose a workflow that fits your team:
- GitHub Flow: Simple, trunk-based development
- Git Flow: Feature branches with dedicated releases
- Trunk-based: Frequent commits to main with feature flags

### Code Review Culture

- Small, focused PRs
- Timely reviews
- Constructive feedback
- Use code owners for critical paths
- Automated checks before review

### Documentation

- README: Project overview, setup, usage
- Wiki: Extended documentation
- Issues: Track bugs and features
- Discussions: Community support
- GitHub Pages: Public documentation

### Security Best Practices

- Enable all security features
- Keep dependencies updated
- Add SECURITY.md
- Use secret scanning
- Review code for vulnerabilities
- Enforce 2FA

---

## Resources

- [GitHub Docs](https://docs.github.com)
- [GitHub Skills](https://skills.github.com)
- [GitHub Blog](https://github.blog)
- [GitHub YouTube](https://www.youtube.com/github)
- [GitHub Community Forum](https://github.community)

---

*This guide was created by dev-zuhaib on 2025-03-07*
