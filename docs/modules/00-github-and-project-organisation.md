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
