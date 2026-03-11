# MDC Git & GitHub Workshop

Welcome! This workshop will introduce you to the basics of Git and GitHub through a hands-on group activity. By the end, you'll have cloned a repo, made changes on a branch, opened a pull request, and dealt with merge conflicts — all core skills for collaborating on code.

---

## What is Git? What is GitHub?

**Git** is a *version control system* — a tool that tracks changes to your files over time. It lets you save snapshots of your work (called **commits**), travel back in time to earlier versions, and work on different features simultaneously using **branches**.

**GitHub** is a website that hosts Git repositories in the cloud. It adds collaboration features on top of Git: pull requests, code reviews, issue tracking, and more.

---

## Key Concepts

| Term | What it means |
|------|--------------|
| **Repository (repo)** | A folder tracked by Git, containing your project and its full history |
| **Clone** | Download a copy of a remote repo to your local machine |
| **Branch** | An independent line of development; lets multiple people work without stepping on each other |
| **Commit** | A saved snapshot of your changes, with a message describing what you did |
| **Push** | Upload your local commits to GitHub |
| **Pull Request (PR)** | A request to merge your branch's changes into another branch (usually `main`) |
| **Merge conflict** | When two branches have changed the same part of the same file — Git needs your help to decide which version to keep |

---

## Workshop Activity Overview

1. **Clone** the shared repo to your computer
2. **Create a new branch** for your group
3. **Edit** the Python file — each group member edits a different print statement
4. **Commit** your change individually (so your branch has multiple commits)
5. **Push** your branch to GitHub
6. **Open a Pull Request** and request a review
7. **Address review feedback**, then merge
8. **Resolve merge conflicts** (for groups 2+)

---

## Step-by-Step Instructions

### Step 1 — Clone the Repository

Clone the repo to get a local copy on your machine.

```bash
git clone https://github.com/mdcUM/git-workshop.git
cd git-workshop
```

> **What this does:** Downloads the entire repository — all files and history — to a new folder on your computer.

---

### Step 2 — Create a New Branch

Each group should work on their own branch. Pick a short, descriptive name (e.g., `group-1`).

**One person** creates the branch and pushes it to GitHub straight away (before making any edits), so it exists remotely for the rest of the group to pull down:

```bash
git checkout -b your-branch-name
git push --set-upstream origin your-branch-name
```

**Everyone else** then fetches the remote branch and switches to it — note there is **no `-b` flag** here, since the branch already exists:

```bash
git fetch origin
git checkout your-branch-name
```

> **Why `git fetch` and not `git pull`?** `git pull` is actually two commands in one: it fetches changes *and* immediately merges them into your **current** branch. Since at this point you're still on `main` and the new branch doesn't exist locally yet, a `git pull` would also update `main`, which isn't necessary when we just want to grab the new branch. `git fetch` downloads all the latest information from GitHub (including any new branches) without touching your working files.

> **Why not just run `git checkout -b` on every device?** The `-b` flag creates a brand new local branch from scratch. If two people each run `git checkout -b group-1`, they'll have two independent local branches that happen to share a name — they won't be in sync, and pushing will cause confusion. Fetching and checking out an existing remote branch is the correct approach for everyone after the first person.

To **verify** you're all on the right branch:

```bash
git branch
```

The branch with a `*` next to it is your current branch.

---

### Step 3 — Edit the Python File

Open `workshop.py` in your editor. You'll see 4 print statements like:

```python
print("Name: Idea")
print("Name: Idea")
print("Name: Idea")
print("Name: Idea")
```

**Each group member edits exactly one distinct print statement** — replacing the placeholder with your name and a workshop idea for the future.

> **Important:** Each person should edit a *different* line. This ensures each person makes their own commit, and it's also what creates merge conflicts for later groups!

---

### Step 4 — Stage, Commit, and Push (each member individually)

After editing your line, each group member runs the following commands **one at a time**:

**Check what you've changed:**
```bash
git status
git diff
```

**Stage your change:**
```bash
git add workshop.py
```

**Commit with a meaningful message:**
```bash
git commit -m "Add [Your Name]'s workshop idea"
```

>  **What this does:** `git add` stages your file (marks it as ready to commit). `git commit` saves a permanent snapshot with your message. Each person's commit will appear separately in the branch history.

**Pull before you push:** Before pushing, run `git pull` to grab any commits your teammates have already pushed. This keeps your branch in sync and avoids rejected pushes.

```bash
git pull origin your-branch-name
```

**Then push your commit:**
```bash
git push origin your-branch-name
```

> If it's your first push for this branch, Git might tell you to set the upstream. Just run the command it suggests, or use:
> ```bash
> git push --set-upstream origin your-branch-name
> ```

Repeat this process for each group member — by the end, your shared branch on GitHub should have one commit per person.

---

### Step 5 — Open a Pull Request

Go to the repository on GitHub. You should see a banner prompting you to open a pull request for your recently pushed branch. Click it, or navigate to **Pull Requests → New Pull Request**.

- Set the **base branch** to `main`
- Set the **compare branch** to your group's branch
- Write a short description of what your group added

[How to create a pull request (GitHub Docs)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

---

### Step 6 — Request a Review

On the PR page, find the **Reviewers** section on the right sidebar and request a review from your workshop leader.

[How to request a pull request review (GitHub Docs)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/requesting-a-pull-request-review)

---

### Step 7 — Address Review Feedback

Your reviewer will leave a comment on the PR.

[How to leave a review comment (GitHub Docs)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request)

Make the requested change in your local file, then commit and push again:

```bash
git add workshop.py
git commit -m "Address review feedback"
git push origin your-branch-name
```

Then, on GitHub, **resolve the conversation** to let the reviewer know it's been addressed.

[How to resolve a review comment (GitHub Docs)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/commenting-on-a-pull-request#resolving-conversations)

Once the reviewer approves, you can **merge the PR** into `main`.

---

## Step 8 — Resolving Merge Conflicts (Groups 2 and beyond)

Because Group 1 already merged changes to `workshop.py` into `main`, your branch may now be **out of date** with `main`. When the same lines were edited differently, Git can't auto-merge — you'll have a **merge conflict**.

### Option A — Resolve in the GitHub Web Interface

GitHub will show a "Resolve conflicts" button directly on the PR page if the conflict is simple enough. Click it, edit the file in the browser to keep the changes you want, then mark it as resolved and commit.

[Resolving merge conflicts on GitHub (GitHub Docs)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github)

---

### Option B — Resolve Locally (via merge commit in VSCode or terminal)

**1. Make sure your local `main` is up to date:**

```bash
git checkout main
git pull origin main
```

**2. Switch back to your branch and merge `main` into it:**

```bash
git checkout your-branch-name
git merge main
```

Git will tell you there's a conflict and mark the affected file(s). Open `workshop.py` and you'll see conflict markers like this:

```
<<<<<<< HEAD
print("Your group's version of this line")
=======
print("The version that's already in main")
>>>>>>> main
```

**3. Resolve the conflict:**

Edit the file to keep the correct content (usually, you want to keep *both* groups' lines — just delete the conflict markers `<<<<<<<`, `=======`, `>>>>>>>`).

**In VSCode**, you'll see a visual diff with clickable options: *Accept Current Change*, *Accept Incoming Change*, or *Accept Both Changes*. Choose what makes sense.

**4. Stage the resolved file and commit:**

```bash
git add workshop.py
git commit -m "Merge main into branch and resolve conflicts"
```

**5. Push your updated branch:**

```bash
git push origin your-branch-name
```

Your PR on GitHub will automatically update, and if there are no more conflicts, you'll be able to merge!

[Resolving merge conflicts using the command line (GitHub Docs)](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)

---

## Quick Reference — Git Commands

```bash
# Clone a repo
git clone <url>

# See your current branch and status
git status
git branch

# Create and switch to a new branch
git checkout -b <branch-name>

# Switch to an existing branch
git checkout <branch-name>

# Stage changes
git add <filename>        # stage a specific file
git add .                 # stage all changes

# Commit
git commit -m "Your message here"

# Push to GitHub
git push origin <branch-name>

# Pull latest changes from GitHub
git pull origin <branch-name>

# Update your branch with changes from main
git checkout main
git pull origin main
git checkout <your-branch>
git merge main
```