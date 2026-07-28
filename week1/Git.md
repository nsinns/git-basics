# Git Branching Strategy & Command Reference

This is the single workflow students use from Day 1 (Week 1's portfolio repo) all the way through the capstone. Keeping one consistent model for 6 months — rather than switching strategies mid-program — is what makes it muscle memory by the time they walk into interviews.

## The Model: GitHub Flow (Weeks 1–16)

Simple, trunk-based, and exactly what most companies actually use day to day (full Git Flow with `develop`/`release` branches is overkill for a portfolio repo and rarely what students will meet in their first job anyway).

```
main  ●───────●───────●───────●───────●   (always working, always deployable)
       \     ↑ \     ↑ \     ↑ \     ↑
        \   PR  \   PR  \   PR  \   PR
         ●───●    ●───●    ●───●    ●───●
      feature/   feature/  feature/  feature/
      week01-cli week02-sql week03-eda ...
```

**Rules:**
1. `main` is always stable — nothing gets pushed to it directly.
2. Every lab/task gets its own short-lived branch off `main`.
3. Work is merged back via a **Pull Request**, reviewed (by a peer or mentor) before merging.
4. Branches are deleted after merge — no accumulating stale branches.

**Naming convention:**
- `feature/week03-eda-pandas`
- `fix/api-auth-bug`
- `docs/readme-update`
- `chore/add-linting`

## Extended Model for Capstone (Weeks 17–24)

Capstone projects are bigger and often longer-lived than a single lab, so add two things on top of GitHub Flow:

1. **Tag a release at every sprint demo** (Weeks 17–24 map 1:1 to sprints) — e.g., `v0.1-sprint1`, `v0.2-sprint2` — so there's a clean, demoable snapshot of progress at each checkpoint, exactly like a real team would tag a release before a stakeholder demo.
2. **Squash-merge feature branches into `main`** to keep the capstone's commit history readable for anyone reviewing the repo later (recruiters will look at this).

If students are working in pairs/small teams for the capstone, add one more layer: a shared `main` still stays protected, but each teammate branches off it independently and PRs back in — no shared `develop` branch needed at this scale.

## Commit Message Convention

Use [Conventional Commits](https://www.conventionalcommits.org/) — it's a small habit that reads as "this person has worked on a real team" in a portfolio review.

| Prefix | Use for |
|---|---|
| `feat:` | a new feature or capability |
| `fix:` | a bug fix |
| `docs:` | documentation only |
| `refactor:` | code change that doesn't add a feature or fix a bug |
| `test:` | adding or fixing tests |
| `chore:` | tooling, config, dependency bumps |

Example: `feat: add retry logic to ETL extract step`

---

## Full Command Reference

### 1. One-time setup
```bash
git clone https://github.com/<username>/<portfolio-repo>.git
cd <portfolio-repo>
git config user.name "Your Name"
git config user.email "you@example.com"
```

### 2. Starting new work (every lab starts here)
```bash
git checkout main
git pull origin main                      # make sure main is current
git checkout -b feature/week05-etl-pipeline
```

### 3. Daily work loop
```bash
git status                                 # see what changed
git add .                                  # stage changes
git commit -m "feat: add extract step for ETL pipeline"
git push -u origin feature/week05-etl-pipeline   # first push on this branch
git push                                   # subsequent pushes
```

### 4. Opening a Pull Request
Via GitHub CLI (recommended — feels like real dev tooling):
```bash
gh pr create --base main --head feature/week05-etl-pipeline \
  --title "Week 5: ETL pipeline" \
  --body "Extract from API + CSV, transform with pandas, load to Postgres."
```
Or open it from the GitHub web UI after pushing.

### 5. Reviewing someone else's PR locally
```bash
git fetch origin
git checkout feature/their-branch-name
# run it, test it, read the diff
```

### 6. Keeping your branch up to date with main
If `main` has moved on while you were working (common once the cohort starts merging in parallel):
```bash
git checkout feature/week05-etl-pipeline
git fetch origin
git merge origin/main
# resolve any conflicts, then:
git add .
git commit -m "merge: resolve conflicts with main"
git push
```
(Rebasing — `git rebase origin/main` — is the cleaner-history alternative; introduce it once students are comfortable with merge, usually around Month 2.)

### 7. Merging the PR
- Prefer **"Squash and merge"** on GitHub for lab branches — keeps `main`'s history one clean commit per feature.
- Delete the branch immediately after merge (GitHub offers a button; or):
```bash
git branch -d feature/week05-etl-pipeline
git push origin --delete feature/week05-etl-pipeline
```

### 8. Tagging a release (Sprint Demos & Capstone)
```bash
git checkout main
git pull origin main
git tag -a v0.2-sprint2 -m "Sprint 2 demo: data layer complete"
git push origin v0.2-sprint2
```

---

## Recommended Branch Protection Settings (GitHub repo settings)

- Require a pull request before merging into `main`
- Require at least 1 approving review
- Require status checks to pass before merging (once CI is introduced in Week 13)
- Do not allow direct pushes to `main`
- Automatically delete head branches after merge

Setting this up in Week 1 — even before students strictly need it — normalizes "you literally cannot push straight to main" as the default state of a real project.

---

## Common Mistakes & Recovery Commands

| Situation | Command |
|---|---|
| Committed to the wrong branch | `git stash` → checkout correct branch → `git stash pop` |
| Need to undo the last commit but keep changes | `git reset --soft HEAD~1` |
| Need to discard local changes entirely | `git checkout -- <file>` or `git restore <file>` |
| Committed with a typo in the message | `git commit --amend -m "corrected message"` |
| Need to undo a commit that's already pushed/merged | `git revert <commit-hash>` (never force-rewrite shared history) |
| Accidentally deleted a branch | `git reflog` → find the commit → `git checkout -b <branch-name> <commit-hash>` |
| Merge conflict panic | `git status` (shows conflicted files) → open, resolve manually, `git add .` → `git commit` |

**One hard rule worth teaching early:** never `git push --force` to `main`, and generally avoid it on shared branches at all — it's the single most common way a junior engineer causes real damage on a team repo. `--force-with-lease` on your *own* feature branch is fine; force-pushing to anything shared is not.

---

## Worked Example: Week 5 Lab, Start to Finish

```bash
git checkout main
git pull origin main
git checkout -b feature/week05-etl-pipeline

# ...write the extract/transform/load script...

git add .
git commit -m "feat: add extract step pulling from public API"

# ...continue working...

git add .
git commit -m "feat: add transform step with pandas cleaning"
git add .
git commit -m "feat: add Postgres load with upsert logic"

git push -u origin feature/week05-etl-pipeline

gh pr create --base main --head feature/week05-etl-pipeline \
  --title "Week 5: ETL pipeline" \
  --body "Extract → transform → load with retry/error handling."

# peer reviews it, requests one small change
git add .
git commit -m "fix: handle empty API response gracefully"
git push

# peer approves, PR gets squash-merged on GitHub
git checkout main
git pull origin main
git branch -d feature/week05-etl-pipeline
```

This exact loop repeats every week for 24 weeks — by the capstone, it's not something students think about anymore, it's just how they work.