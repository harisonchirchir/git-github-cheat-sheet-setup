# Git & GitHub First-Time Setup Cheat Sheet

A quick reference for configuring Git and GitHub for the first time.

## 1. Create a GitHub Account

1. Go to [github.com](https://github.com).
2. Click **Sign up**.
3. Enter your email, choose a username, and create a password.
4. Verify your email address (check your inbox for the verification email).
5. Optionally enable two-factor authentication (2FA) for added security.

---

## 2. Install Git

### macOS (Homebrew)
```sh
brew install git
```

### Ubuntu / Debian
```sh
sudo apt update && sudo apt install git -y
```

### Fedora / RHEL
```sh
sudo dnf install git -y
```

### Windows
Download the installer from [git-scm.com](https://git-scm.com/download/win) and run it.  
Or use [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/):

```powershell
winget install Git.Git
```

### Verify installation
```sh
git --version
```

---

## 3. Configure Git (Your Local Machine)

Set your username and email **globally** (applies to all repositories):

```sh
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

Optional but recommended settings:

```sh
git config --global core.autocrlf true          # avoids CRLF issues (Linux/macOS)
git config --global init.defaultBranch main     # set default branch to "main"
git config --global color.ui auto               # colored output
git config --global pull.rebase false           # merge by default on pull
```

Check your configuration:

```sh
git config --list
```

### Authenticate with GitHub (SSH, Recommended)

Generate an SSH key:

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```
> If your system doesn't support `ed25519`, use: `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

Start the SSH agent and add your key:

```sh
eval "$(ssh-agent -sh)"
ssh-add ~/.ssh/id_ed25519
```

Copy the SSH public key to your clipboard:

```sh
cat ~/.ssh/id_ed25519.pub
```

1. Go to **GitHub → Settings → SSH and GPG keys → New SSH key**.
2. Paste the key and save.

Test the connection:

```sh
ssh -T git@github.com
```
> You should see: `Hi <username>! You've successfully authenticated...`

---

## 4. Connect Git to GitHub & Create a New Repository

### Option A: Clone an existing GitHub repository

```sh
git clone git@github.com:<username>/<repository-name>.git
```

### Option B: Initialize a new local project and connect it to GitHub

1. Create the project folder and move into it:

   ```sh
   mkdir my-project && cd my-project
   ```

2. Initialize a Git repository:

   ```sh
   git init
   ```

3. Create a new repository on GitHub:
   - Go to [github.com/new](https://github.com/new).
   - Give it a name (no spaces, use kebab-case or snake_case).
   - Leave it **empty** (do NOT check "Add a README" if you already have local files).
   - Click **Create repository**.

4. Add the remote repository:

   ```sh
   git remote add origin git@github.com:<username>/<repository-name>.git
   ```

5. Verify the remote:

   ```sh
   git remote -v
   ```

---

## 5. Initialize Your Project with Git

```sh
git init
```

Stage all files:

```sh
git add .
```

Or stage specific files:

```sh
git add <filename>
```

Commit the changes:

```sh
git commit -m "Initial commit"
```

---

## 6. Pull from the Remote Repository

If the remote has changes (e.g., a `README` or `.gitignore` added on GitHub), pull first:

```sh
git pull origin main
```

> Resolve any merge conflicts before proceeding to push.

---

## 7. Push to GitHub

Push your local commits to the remote repository:

```sh
git push -u origin main
```

> The `-u` flag sets the upstream tracking branch so future pushes can be done with just `git push`.

---

## Quick Command Summary

```sh
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:<username>/<repository-name>.git
git pull origin main
git push -u origin main
```

---

## Useful Extras

Set default branch name globally:

```sh
git config --global init.defaultBranch main
```

Rename current branch to `main` (if initialized as `master`):

```sh
git branch -M main
```

Ignore files you don't want to commit:

```sh
echo "node_modules/" >> .gitignore
echo ".env" >> .gitignore
```

