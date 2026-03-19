# Step 02: Plan

**Task:** Fork Handy repo, get all modifications from Melvynx/Parler fork, create PR in original repo
**Started:** 2026-03-19T06:29:44Z

---

## Planning Progress

## Implementation Plan

### Overview
Fork cjpais/Handy to user's GitHub account, clone locally, fetch all changes from Melvynx/Parler fork (42 commits ahead), merge them into a feature branch, resolve conflicts, and create a PR to the original repo.

### Prerequisites
- [ ] GitHub CLI (`gh`) authenticated
- [ ] Git available locally

---

### Step-by-Step Execution

#### Step 1: Fork cjpais/Handy
- `gh repo fork cjpais/Handy --clone=false`
- This creates a fork under user's GitHub account

#### Step 2: Clone the fork locally
- `gh repo clone {user}/Handy /Users/franck/Github/handy`
- Working directory already exists but has no git repo

#### Step 3: Add Melvynx/Parler as remote
- `git remote add melvynx https://github.com/Melvynx/Parler.git`
- `git fetch melvynx`

#### Step 4: Create feature branch
- `git checkout -b feat/melvynx-parler-changes main`

#### Step 5: Merge Melvynx changes
- `git merge melvynx/main --no-edit`
- Handle merge conflicts if any (expected: 57 commits divergence)
- Key conflict areas: Cargo.lock, bun.lock, package.json, icons, actions.rs

#### Step 6: Resolve conflicts
- For each conflicted file, analyze and resolve
- Keep both upstream and Melvynx changes where possible
- For binary files (icons), keep Melvynx versions

#### Step 7: Push and create PR
- `git push -u origin feat/melvynx-parler-changes`
- `gh pr create` targeting cjpais/Handy with summary of all Melvynx changes

---

### Acceptance Criteria Mapping
- [ ] AC1: Fork created on user's GitHub → Step 1
- [ ] AC2: Cloned locally with remotes → Steps 2-3
- [ ] AC3: Melvynx changes in branch → Steps 4-6
- [ ] AC4: PR created on cjpais/Handy → Step 7
- [ ] AC5: PR contains all Melvynx feature additions → Steps 5-6

### Risks & Considerations
- **Merge conflicts**: 57 commits behind means significant divergence. Conflicts likely in Cargo.lock, bun.lock, and possibly source files.
- **Rebranding**: Melvynx renamed the app to "Parler" — this is included as user requested "toutes ces modifications".
- **Binary files**: Icon replacements are binary — conflicts need manual resolution.
