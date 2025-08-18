# Cabineo - Professional GitHub Workflow Guide

## 🎯 **GitHub Learning Philosophy**
> **"GitHub is your professional portfolio and collaboration tool"**
> 
> This guide teaches you to use GitHub like a senior developer, building habits that will impress employers and make collaboration seamless.

---

## 🚀 **GitHub Workflow Overview**

### **Core Principles**
- **Linear History:** Clean, readable commit history
- **Issue-Driven Development:** Every feature starts with an issue
- **Milestone Planning:** Organized project phases
- **Professional Commits:** Conventional commit messages
- **Proper Branching:** Feature branches with clear purpose

### **Workflow Stages**
1. **Planning** → Create issues and milestones
2. **Development** → Branch, code, commit
3. **Review** → Pull request and code review
4. **Integration** → Merge and maintain history

---

## 📋 **Phase 1: GitHub Foundation Setup** (Week 1)

### **Day 1: Repository Setup & Initial Structure**

#### **GitHub Repository Configuration**
- [ ] **Enable branch protection** on `main` branch
  - Go to Settings → Branches → Add rule
  - Require pull request reviews before merging
  - Require status checks to pass before merging
  - Include administrators in restrictions

- [ ] **Set up repository settings**
  - Enable Issues
  - Enable Projects (for Kanban board)
  - Enable Wiki (for documentation)
  - Set up branch naming conventions

#### **Local Git Configuration**
```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set up credential helper (for macOS)
git config --global credential.helper osxkeychain
```

#### **Initial Commit & Push**
```bash
# Initialize repository
git init
git add .
git commit -m "feat: initial project setup with architecture"

# Add remote and push
git remote add origin https://github.com/yourusername/cabineo.git
git branch -M main
git push -u origin main
```

### **Day 2: Issue & Milestone Creation**

#### **Create Project Milestones**
1. **Go to Issues → Milestones**
2. **Create Phase 1 Milestone:**
   - Title: `Phase 1: Foundation & Setup`
   - Description: Complete project foundation and development environment
   - Due date: End of Week 1

#### **Create Initial Issues**
Create these issues and assign them to Phase 1 milestone:

**Issue #1: Project Structure Setup**
```
Title: Set up project folder structure and configuration
Labels: setup, foundation
Description: 
- Create folder structure from architecture document
- Set up Tailwind CSS configuration
- Configure Biome linting and formatting
- Set up Husky pre-commit hooks

Acceptance Criteria:
- [ ] All folders created according to architecture
- [ ] Tailwind CSS working and configured
- [ ] Biome formatting working correctly
- [ ] Husky pre-commit hooks functional
```

**Issue #2: TypeScript Foundation**
```
Title: Implement TypeScript types and validation
Labels: typescript, foundation
Description:
- Define core type interfaces for cabinet configuration
- Set up Zod validation schemas
- Configure strict TypeScript settings
- Create utility functions

Acceptance Criteria:
- [ ] All TypeScript interfaces defined
- [ ] Zod schemas implemented and working
- [ ] Strict TypeScript configuration active
- [ ] Utility functions created and tested
```

**Issue #3: State Management Setup**
```
Title: Implement Zustand stores architecture
Labels: state-management, foundation
Description:
- Set up Zustand store structure
- Implement cabinet configuration store
- Create material selection store
- Build UI state management

Acceptance Criteria:
- [ ] Store architecture implemented
- [ ] All stores functional and connected
- [ ] State updates working correctly
- [ ] No unnecessary re-renders
```

### **Day 3: Branching Strategy Implementation**

#### **Create Development Branch**
```bash
# Create and switch to develop branch
git checkout -b develop
git push -u origin develop

# Set develop as default branch for future features
git checkout main
git checkout -b feature/project-structure
```

#### **Branch Naming Convention**
```
main          - Production-ready code
develop       - Integration branch for features
feature/*     - New features (feature/project-structure)
fix/*         - Bug fixes (fix/typing-error)
docs/*        - Documentation updates (docs/readme-update)
chore/*       - Maintenance tasks (chore/dependency-update)
```

### **Day 4: First Feature Implementation**

#### **Work on Issue #1: Project Structure Setup**
```bash
# Ensure you're on feature branch
git checkout feature/project-structure

# Make your changes (create folders, configure tools)
# ... implement the project structure ...

# Stage and commit with conventional commit message
git add .
git commit -m "feat: set up project folder structure and configuration

- Create complete folder structure from architecture
- Configure Tailwind CSS with proper setup
- Set up Biome linting and formatting rules
- Implement Husky pre-commit hooks

Closes #1"
```

#### **Commit Message Format**
```
type(scope): description

[optional body]

[optional footer]

Examples:
feat(cabinet): add basic cabinet geometry generation
fix(ui): resolve slider component rendering issue
docs(architecture): update coordinate system documentation
chore(deps): update Three.js to latest version
```

### **Day 5: Pull Request & Code Review**

#### **Create Pull Request**
1. **Push your feature branch:**
   ```bash
   git push origin feature/project-structure
   ```

2. **Create Pull Request on GitHub:**
   - Base: `develop`
   - Compare: `feature/project-structure`
   - Title: `feat: set up project folder structure and configuration`
   - Description: Include issue reference and acceptance criteria

3. **Request Review:**
   - Assign yourself as assignee
   - Request review from team members (if any)
   - Add relevant labels

#### **Self-Review Checklist**
- [ ] Code follows project conventions
- [ ] All acceptance criteria met
- [ ] No console.log statements left
- [ ] Proper error handling implemented
- [ ] Documentation updated if needed

---

## 🔄 **GitHub Workflow for Each Phase**

### **Phase 2-3: 3D Fundamentals & Cabinet Geometry**

#### **Weekly Milestone Creation**
1. **Create milestone for each phase**
2. **Break down into daily issues**
3. **Use consistent labeling system**

#### **Daily Development Cycle**
```bash
# Morning: Start new feature
git checkout develop
git pull origin develop
git checkout -b feature/3d-scene-setup

# Work on your feature
# ... implement 3D scene ...

# Evening: Commit and push
git add .
git commit -m "feat(3d): implement basic Three.js scene with React Three Fiber

- Add Canvas component with proper sizing
- Implement basic lighting setup
- Add camera controls and orbit system
- Create responsive 3D container

Closes #15"

git push origin feature/3d-scene-setup
```

#### **Issue Management Best Practices**
- **Update issue progress** as you work
- **Add screenshots/videos** of 3D scenes
- **Link related issues** when dependencies exist
- **Use checkboxes** for acceptance criteria

### **Phase 4-5: Materials & User Interface**

#### **Complex Feature Management**
For complex features like materials system:
1. **Create parent issue** for the entire system
2. **Create sub-issues** for each component
3. **Use issue dependencies** to show relationships
4. **Link to architecture decisions** for context

#### **Pull Request Best Practices**
- **Keep PRs small** (max 300-500 lines)
- **Use descriptive titles** that explain the change
- **Include before/after screenshots** for UI changes
- **Add testing instructions** for reviewers

---

## 🎯 **Professional GitHub Habits**

### **Daily GitHub Routine**
1. **Morning (15 minutes):**
   - Check open issues and PRs
   - Update issue progress
   - Plan today's work

2. **Throughout the day:**
   - Commit frequently with clear messages
   - Update issues with progress
   - Add screenshots/videos of work

3. **Evening (15 minutes):**
   - Push feature branches
   - Create/update PRs
   - Plan tomorrow's tasks

### **Commit Frequency Guidelines**
- **Small commits:** Every logical change (2-3 per hour)
- **Medium commits:** Every feature component (1-2 per day)
- **Large commits:** Only for major refactoring

### **Branch Management**
```bash
# Keep branches short-lived (max 2-3 days)
# Delete merged branches
git branch -d feature/completed-feature

# Update develop regularly
git checkout develop
git pull origin develop
```

---

## 📊 **GitHub Project Management**

### **Project Board Setup**
1. **Go to Projects → New project**
2. **Choose Kanban board**
3. **Create columns:**
   - Backlog
   - In Progress
   - Review
   - Done

### **Automation Rules**
- **Auto-assign** issues to creator
- **Auto-label** based on issue templates
- **Auto-move** issues when PRs are created/merged

### **Issue Templates**
Create templates for different issue types:
- Bug Report
- Feature Request
- Documentation Update
- Learning Question

---

## 🚨 **Common GitHub Mistakes to Avoid**

### **❌ Don't Do This:**
- Commit directly to main/develop
- Use vague commit messages
- Leave branches open for weeks
- Ignore code review feedback
- Mix multiple features in one PR

### **✅ Do This Instead:**
- Always work in feature branches
- Write descriptive commit messages
- Keep branches focused and small
- Embrace code review feedback
- One feature per PR

---

## 🎉 **GitHub Success Metrics**

### **Weekly Goals**
- [ ] **5-7 meaningful commits** with clear messages
- [ ] **2-3 feature branches** completed and merged
- [ ] **All issues updated** with progress
- [ ] **Pull requests reviewed** and improved

### **Monthly Goals**
- [ ] **Clean commit history** with no merge commits
- [ ] **All milestones completed** on time
- [ ] **Documentation updated** with changes
- [ ] **Repository health score** improving

---

## 🔧 **GitHub Tools & Extensions**

### **Browser Extensions**
- **GitHub Pull Request Manager**
- **GitHub Code Folding**
- **GitHub Issue Link Status**

### **VS Code Extensions**
- **GitLens** - Enhanced Git capabilities
- **GitHub Pull Requests** - Manage PRs from editor
- **Conventional Commits** - Commit message helper

### **CLI Tools**
- **gh** - GitHub CLI for terminal operations
- **hub** - Alternative GitHub CLI

---

## 📚 **GitHub Learning Resources**

### **Official Documentation**
- [GitHub Guides](https://guides.github.com/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Conventional Commits](https://www.conventionalcommits.org/)

### **Advanced Topics**
- [GitHub Actions](https://docs.github.com/en/actions)
- [GitHub Pages](https://docs.github.com/en/pages)
- [GitHub Apps](https://docs.github.com/en/apps)

---

## 🚀 **Ready to Master GitHub?**

This workflow will transform you from a GitHub beginner to a professional developer who:

- **Maintains clean project history**
- **Collaborates effectively** with teams
- **Manages complex projects** systematically
- **Demonstrates senior-level skills** to employers

**Your GitHub journey starts with Phase 1. Ready to create your first professional issue and milestone?** 🎯

Remember: Every commit, every issue, every PR is building your professional reputation. Make them count! 💪

