# Module 00 – GitHub and Project Organisation

Notes for the steps completed in Module 00. Each step records the goal, the theory,
the GUI method, the PowerShell method and the verification results.

---

## Step 00.1 – Repository, commit, branch and Pull Request basics

**Completed:** 2026-11-26

### Goal

Understand how changes reach a Git repository and approve the first change.

### Theory

| Term | Meaning |
|------|---------|
| Repository (repo) | A project folder together with its full change history. |
| Commit | One saved change (a snapshot of files) with a description (commit message). |
| Branch | A separate line of work. `main` is the official version. |
| Pull Request (PR) | A request to merge changes from one branch into another (usually `main`), reviewed before the merge. |
| Merge | Applying the changes from a PR to the target branch. |

### Real-world application

Administrators keep scripts, configuration and documentation in Git. Changes go
through Pull Requests so another person can review them before they reach production.
The history shows who changed what and when, and a bad change can be reverted.

### GUI method (GitHub web interface)

1. Open the Pull Request.
2. Review the **Commits** and **Files changed** tabs.
3. Click **Merge pull request** → **Confirm merge**.
4. Check the files on the `main` branch.

### Verification

- PR #1 merged into `main` (initial project documentation).
- `main` contains `README.md`, `PROJECT_INSTRUCTIONS.md`, `LEARNING_ROADMAP.md`,
  `PROGRESS.md` and `.gitignore`.

### PowerShell method

Not applicable for this step (covered in later steps with the `git` CLI).

---

## Step 00.2 – Cloning the repository locally

**Completed:** 2026-11-27

### Goal

Create a local copy of the repository on the Windows workstation, using GitHub Desktop
(GUI) and the `git` command line (PowerShell).

### Theory

| Term | Meaning |
|------|---------|
| Clone | Download a full copy of a repository, including its history, to a local folder. |
| Remote (`origin`) | The address of the repository the clone came from. |
| Fetch | Check the remote for new changes without applying them. |
| Pull | Download new changes from the remote and apply them to the local branch. |
| Push | Upload local commits to the remote. |
| `.git` folder | Hidden folder that stores the history and settings of the local repository. Never delete or edit it manually. |

### Real-world application

Administrators work on scripts and documentation locally and push finished changes
to a central server (GitHub, GitLab, Azure DevOps). The command-line method is used
on servers without a GUI, over remote sessions, and in automation scripts.

### GUI method (GitHub Desktop)

1. Install GitHub Desktop and sign in to GitHub.com (browser sign-in).
2. **File** → **Clone repository…** → **GitHub.com** tab → select
   `windows-server-active-directory-lab`.
3. Set **Local path** to `D:\Repos\windows-server-active-directory-lab` → **Clone**.

#### GUI verification

- GitHub Desktop shows **Current repository: windows-server-active-directory-lab**
  and **Current branch: main**.
- **Fetch origin** shows no new changes to pull.
- The local folder contains the four `.md` files and `.gitignore`.
- The local `PROGRESS.md` shows step 00.1 as the last completed task.

### PowerShell method (`git` CLI)

A separate test folder (`D:\Repos\Test`) is used so the working copy is not affected.

```powershell
# Check that Git is installed and available in PowerShell
git --version

# If Git is missing (GitHub Desktop uses its own bundled copy), install it:
# winget install --id Git.Git -e

# Create a test folder and move into it
New-Item -Path D:\Repos\Test -ItemType Directory
Set-Location D:\Repos\Test

# Clone the repository
git clone https://github.com/mailmen84/windows-server-active-directory-lab.git
```

| Command | Purpose |
|---------|---------|
| `git --version` | Shows the installed Git version; confirms Git is on the `PATH`. |
| `winget install --id Git.Git -e` | Installs Git for Windows; `-e` requires an exact package match. |
| `New-Item -ItemType Directory` | Creates a folder. |
| `Set-Location` | Changes the current directory (alias `cd`). |
| `git clone <url>` | Downloads the repository into a new subfolder named after it. |

#### PowerShell verification

```powershell
Set-Location .\windows-server-active-directory-lab
git status
git remote -v
git log --oneline -5
```

Results:

- `git --version` → `git version 2.56.1.windows.1`
- `git status` → `On branch main`, `Your branch is up to date with 'origin/main'`,
  `nothing to commit, working tree clean`
- `git remote -v` → `origin https://github.com/mailmen84/windows-server-active-directory-lab.git`
  for both `(fetch)` and `(push)`
- `git log --oneline -5` → latest commit is `Merge pull request #2`

### References

- [GitHub Docs – Cloning a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
- [GitHub Desktop documentation](https://docs.github.com/en/desktop)
- [Git documentation – git clone](https://git-scm.com/docs/git-clone)
- [Microsoft Learn – winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/)

---

## Step 00.3 - Editing, committing and pushing a change

**Completed:** 2026-11-27

### Goal

Complete the full change cycle on my own: branch -> edit -> commit -> push ->
Pull Request -> merge -> clean up.

### Theory

| Term | Meaning |
|------|---------|
| Working directory | The files on disk that are being edited. |
| Staging area | Changes selected for the next commit (`git add`; checkboxes in GitHub Desktop). |
| Commit | A snapshot of the staged changes saved in the local history. |
| Push | Upload local commits to GitHub. Until then, the change exists only locally. |
| Feature branch | A short-lived branch for one change; `main` stays untouched until the merge. |

Good commit messages are short, in English, in imperative mood and describe
**what and why** (`Replace en dashes in progress log`), not only which file changed
(`Update PROGRESS.md`).

### Real-world application

This is how administrators change scripts and documentation in a team: a branch per
change, a descriptive commit, a Pull Request for review, and deleting the branch after
the merge so the repository does not fill up with old branches.

### GUI method (GitHub Desktop + VS Code)

Change: replace en dashes (`–`) with hyphens (`-`) in `PROGRESS.md`.

1. **Current branch** -> **New branch** -> `fix-progress-dashes`.
2. Edit the file in VS Code (**Ctrl+H**, **Replace All**, **Ctrl+S**).
3. Review the diff in the **Changes** tab.
4. Enter a commit summary -> **Commit to fix-progress-dashes**.
5. **Publish branch** -> **Create Pull Request** -> merge on GitHub (PR #4).
6. Switch back to `main`, **Fetch origin** -> **Pull origin**, delete the branch.

#### GUI verification

- PR #4 merged into `main`; only dash characters changed in `PROGRESS.md`.
- No en dashes left in `PROGRESS.md`; branch deleted.

### PowerShell method (`git` CLI)

Change: add `.vscode/` to `.gitignore` (VS Code workspace settings are local
editor settings, not project documentation).

```powershell
Set-Location D:\Repos\windows-server-active-directory-lab
git switch main
git pull

# One-time identity setup (use the GitHub "noreply" address, never a private email)
git config --global user.name "mailmen84"
git config --global user.email "<id>+mailmen84@users.noreply.github.com"

git switch -c add-vscode-gitignore
Add-Content -Path .gitignore -Value "`n# Editor settings`n.vscode/"
git status
git diff
git add .gitignore
git commit -m "Ignore VS Code workspace settings"
git push -u origin add-vscode-gitignore

# After the Pull Request is merged on GitHub (PR #5):
git switch main
git pull
git branch -d add-vscode-gitignore
git push origin --delete add-vscode-gitignore
git fetch --prune
git branch -a
```

| Command | Purpose |
|---------|---------|
| `git switch <branch>` | Switch to an existing branch. |
| `git switch -c <branch>` | Create a new branch and switch to it. |
| `git pull` | Download and apply new commits from GitHub. |
| `git config --global user.name/user.email` | Set the author identity written into every commit. |
| `Add-Content` | Append text to the end of a file. `` `n `` is a new line in PowerShell. |
| `git status` / `git diff` | Show changed files / the exact changes. |
| `git add <file>` | Stage a change for the next commit. |
| `git commit -m "<message>"` | Save the staged changes as a commit. |
| `git push -u origin <branch>` | Upload the branch; `-u` remembers the upstream branch. |
| `git branch -d <branch>` | Delete a local branch (refuses if it is not merged). |
| `git push origin --delete <branch>` | Delete a branch on GitHub. |
| `git fetch --prune` | Remove local references to branches deleted on GitHub. |
| `git branch -a` | List local and remote branches. |

#### PowerShell verification

- PR #5 merged; `.gitignore` on `main` ends with `# Editor settings` and `.vscode/`.
- Commit `Ignore VS Code workspace settings` uses the GitHub noreply address.
- `git branch -a` shows only `main` and the remote working branches.

### Troubleshooting

| Problem | Cause | Resolution |
|---------|-------|------------|
| Prompt shows a deleted folder; `Test-Path` returns `False` | The PowerShell window was still located in the test folder deleted in step 00.2. | `Set-Location` to the real repository and check with `Get-Location` before running commands. |
| `fatal: refs/remotes/origin/HEAD cannot be resolved to branch` | Typo: `origin` typed twice in `git push`. | Run `git push -u origin <branch>`. |
| `remote: error: GH007: Your push would publish a private email address` | The commit was created before `user.email` was set to the noreply address. GitHub email privacy blocked the push. | Set the noreply address, then `git commit --amend --reset-author --no-edit` (only for commits that were **not** pushed yet) and push again. |
| Commit author shows a wrong name | Typo in `user.name`. | Fix with `git config --global user.name`. Pushed commits are not rewritten. |

### Lessons learned

- Always check the prompt (`Get-Location`) before running commands.
- Configure Git identity (noreply email) **before** the first commit on a new computer.
- Never rewrite history that is already on GitHub; `--amend` only for local commits.
- Delete branches after they are merged.

### References

- [GitHub Docs - Setting your commit email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address)
- [GitHub Docs - Blocking command line pushes that expose your personal email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/blocking-command-line-pushes-that-expose-your-personal-email-address)
- [Git documentation - git switch](https://git-scm.com/docs/git-switch)
- [Git documentation - git commit](https://git-scm.com/docs/git-commit)
- [Git documentation - git push](https://git-scm.com/docs/git-push)
