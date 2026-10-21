# Git and GitHub Practical Commands – Complete Viva/Exam Notes

These commands cover the same types of practical questions shown in your notebook: repository creation, adding files, commits, history, differences, branches, pushing, cloning, README, pulling, merging, and collaboration.

Important: Run commands in Git Bash or the VS Code terminal / PowerShell. Commands marked as GitHub website steps must be performed on GitHub.com.

## Q1. Create a local repository and commit an HTML file

Question: Create a local repository named myproject, create index.html, add content, and commit it.

```bash
# 1. Create a project folder manually and open its terminal
git init

# 2. Check repository status
git status

# 3. Create index.html manually using an editor
# Write HTML content and save the file

# 4. Stage the file
git add index.html

# 5. Commit the file
git commit -m "Add index.html"

# 6. View commit history
git log
```

If you want Git to use `main` as the initial branch, run:

```bash
git branch -M main
```

## Q2. Add a file and make another commit

```bash
git status
git add index.html
git commit -m "Update index.html"
git log --oneline
```

If the file is not yet tracked, `git add` stages it for the first time. If it has been modified, the same command stages the new changes.

## Q3. Check Git history

```bash
git log
git log --oneline
git log --oneline --all --graph
git show
git show <commit-id>
```

- `git log` — detailed commit history.
- `git log --oneline` — compact history.
- `git log --oneline --all --graph` — visual branch history.
- `git show` — details and changes from a commit.

## Q4. Modify index.html and view the difference from the last commit

```bash
git status
git diff
git diff --staged
git add index.html
git diff --staged
git commit -m "Modify index.html"
```

- `git diff` — changes not staged yet.
- `git diff --staged` — changes already staged for commit.
- Save your file before running `git diff`.

## Q5. Create a branch named development, add about.html, and commit it

```bash
# Check existing branches
git branch

# Create and switch to development
git switch -c development

# Create about.html manually and write your profile information

# Stage and commit
git add about.html
git commit -m "Add about page"

# Check status and branch
git status
git branch
git log --oneline
```

To switch back to the `main` branch:

```bash
git switch main
```

Older equivalent commands:

```bash
git checkout -b development
git checkout main
```

## Q6. Push code to GitHub and create README.md

Question: Upload your local project to GitHub and add a README file describing the project.

First, create a new, empty repository on GitHub.com. Copy its repository URL, then run:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main

# Connect local repository to GitHub
git remote add origin <GitHub-repository-URL>

# Upload code
git push -u origin main
```

Next, create `README.md` manually in your project folder and write the project description.

```bash
git add README.md
git commit -m "Add project README"
git push
```

If `origin` already exists, use:

```bash
git remote set-url origin <GitHub-repository-URL>
```

On GitHub.com, you can also create `README.md` through Add file → Create new file, enter the description, and commit the changes.

## Q7. Clone an existing repository and check its status

```bash
# Download the repository to your computer
git clone <GitHub-repository-URL>

# Enter the cloned project directory
cd <repository-folder>

# Check the working tree
git status

# Check remote repository
git remote -v

# View branches and commit history
git branch
git log --oneline
```

`git clone` downloads the repository and automatically configures its remote, usually named `origin`.

## Q8. Edit a file on GitHub, then pull the changes to your computer

Question: Change a file on GitHub.com and download the latest changes into your local repository.

1. Open the repository on GitHub.com.
2. Open the file, click the edit icon, modify it, and commit the change.
3. In your local terminal, run:

```bash
git status
git pull origin main
git log --oneline
```

If you are working on a different branch, replace `main` with that branch name.

If you have uncommitted local changes, commit or safely stash them before pulling if they could conflict.

## Q9. Merge the development branch into main

```bash
# Switch to main
git switch main

# Get the latest main branch
git pull origin main

# Merge development into main
git merge development

# Upload merged code
git push origin main
```

If you get merge conflicts:

```bash
git status
```

Open the conflicting files, resolve the conflict markers manually, then:

```bash
git add .
git commit -m "Resolve merge conflicts"
git push origin main
```

## Q10. Complete Git workflow: Initialize, Add, Commit, Branch, Merge, Push and Pull

### Practical workflow

```bash
# Initialize repository
git init

# Add and commit files
git add .
git commit -m "Initial commit"

# Create a branch and work
git switch -c development

# Merge into main
git switch main
git merge development

# Share and synchronize with GitHub
git push -u origin main
git pull origin main
```

Note: Before pushing, configure `origin` with:

```bash
git remote add origin <GitHub-repository-URL>
```

A successful push also requires the GitHub repository to exist and your account to have permission.

## Other important Git and GitHub practical questions

### Q11. Check the status of files

```bash
git status
git status --short
```

Shows modified, staged, untracked files, and the current branch.

### Q12. Add all files and commit them

```bash
git add .
git status
git commit -m "Add project files"
```

`git add .` stages new and modified files in the current directory and its subdirectories. It does not stage deleted files outside the applicable path scope.

### Q13. Create, list, rename and delete branches

```bash
# List local branches
git branch

# Create a branch
git branch development

# Switch branch
git switch development

# Create and switch in one command
git switch -c feature

# Rename current branch
git branch -m new-name

# Delete a merged local branch
git branch -d feature

# Delete a remote branch
git push origin --delete feature
```

### Q14. Connect to GitHub and manage remotes

```bash
# View remote URLs
git remote -v

# Add a remote
git remote add origin <GitHub-repository-URL>

# Change remote URL
git remote set-url origin <GitHub-repository-URL>

# Download remote branch information
git fetch origin

# Upload current branch
git push -u origin main

# Download and merge latest changes
git pull origin main
```

### Q15. Create and use a .gitignore file

Create `.gitignore` manually and list files or folders that Git should ignore.

Example contents:

```gitignore
node_modules/
.env
dist/
*.log
```

Then run:

```bash
git status
git add .gitignore
git commit -m "Add gitignore"
```

Use case: Prevent dependency folders, environment secrets, generated builds, and log files from being committed.

### Q16. Undo changes and recover files

| Task | Command |
|---|---|
| Unstage a file | `git restore --staged index.html` |
| Discard unstaged changes to a file | `git restore index.html` |
| Restore a file from a commit | `git restore --source=<commit-id> index.html` |
| Safely undo a commit using a new commit | `git revert <commit-id>` |
| Temporarily save changes | `git stash` |
| Restore stashed changes | `git stash pop` |
| List stashes | `git stash list` |

Be careful: `git restore index.html` discards the file's unstaged changes. Avoid `git reset --hard` unless you intentionally want to discard tracked changes.

### Q17. Compare branches and commits

```bash
# Compare current working files
git diff

# Compare two branches
git diff main development

# Show recent commits
git log --oneline -5

# Show files changed in the latest commit
git show --stat HEAD

# Show current branch name
git branch --show-current
```

### Q18. Fix common Git errors

| Error | Common solution |
|---|---|
| `remote origin already exists` | `git remote set-url origin <URL>` |
| `src refspec main does not match any` | Make an initial commit, then `git branch -M main` |
| `fatal: not a git repository` | Navigate to the correct folder containing `.git` |
| `Your branch is behind origin/main` | `git pull origin main` |
| `Untracked files` | `git add <filename>` |
| `Merge conflict` | Resolve files, run `git add .`, then commit |
| `Permission denied` | Check GitHub authentication and repository access |
| `Push rejected` | Fetch/pull remote changes and resolve conflicts before pushing |

If Git asks for your name and email before committing, configure them:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

### Q19. Important Git configuration commands

```bash
# View configuration
git config --list

# View current username
git config user.name

# View current email
git config user.email

# Set default initial branch
git config --global init.defaultBranch main

# Show current repository root
git rev-parse --show-toplevel
```

### Q20. Difference between Git and GitHub

| Git | GitHub |
|---|---|
| Version control system | Online platform for Git repositories |
| Works locally on your computer | Hosts repositories online |
| Uses commands like add, commit, branch | Provides pull requests, issues, reviews and collaboration |
| Can work without internet for local operations | Internet is normally needed to access the hosted service |

## Quick revision: Commands to memorize

| Command | Purpose |
|---|---|
| `git init` | Initialize repository |
| `git clone <URL>` | Download repository |
| `git status` | Check current status |
| `git add .` | Stage changes |
| `git commit -m "message"` | Save a commit |
| `git log --oneline` | View history |
| `git diff` | View unstaged differences |
| `git branch` | List branches |
| `git switch -c feature` | Create and switch branch |
| `git merge feature` | Merge branch |
| `git remote -v` | View remote URLs |
| `git push` | Upload commits |
| `git pull` | Download and merge changes |
| `git fetch` | Download remote updates without merging |
| `git stash` | Temporarily save changes |
| `git revert <commit-id>` | Undo a commit safely |

Practical exam tip: For every question, follow this sequence: check status → perform the operation → add → commit → push (if required) → verify using status or log. Use `git add .` only when you intend to stage all applicable changes, not just one specified file.

---

This repository contains practical Git and GitHub viva notes for study and revision.

# Docker Commands and Viva Notes

## 1. Build and manage Docker images

| Command | Purpose |
|---|---|
| `docker images` | List all local images |
| `docker pull mysql:latest` | Download an image from Docker Hub |
| `docker build -t my-app .` | Build an image using the Dockerfile in the current directory |
| `docker build -t my-app -f Dockerfile2 .` | Build using a specific Dockerfile |
| `docker image inspect my-app` | View image details |
| `docker image rm my-app` | Remove an image |

## 2. Create and manage containers

| Command | Purpose |
|---|---|
| `docker run my-app` | Create and run a container |
| `docker run --name my-container my-app` | Run with a custom container name |
| `docker run -d --name my-container my-app` | Run in the background |
| `docker run -it my-app bash` | Run interactively with a Bash shell, if available |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers, including stopped ones |
| `docker start my-container` | Start a stopped container |
| `docker stop my-container` | Stop a running container |
| `docker restart my-container` | Restart a container |
| `docker rm my-container` | Remove a stopped container |
| `docker logs my-container` | View container logs |
| `docker exec -it my-container bash` | Open a shell inside a running container, if available |

## 3. Port mapping — very important

Syntax:

```bash
docker run -d --name my-container -p HOST_PORT:CONTAINER_PORT my-app
```

Example from the Tomcat practical:

```bash
docker run -d --name my-tc-container -p 8080:8080 my-tomcat-app
```

- Host port: `8080` — the port on your computer.
- Container port: `8080` — the port inside the container.

Check the container:

```bash
docker ps
```

Open the application in your browser:

```text
http://localhost:8080/webapp/
```

If port `8080` is already occupied on your computer, map another host port, such as `8085:8080`.

## 4. Dockerfile commands

These are instructions written inside a file named Dockerfile, not commands typed directly into PowerShell.

| Instruction | Purpose |
|---|---|
| `FROM` | Select the base image |
| `WORKDIR` | Set the working directory |
| `COPY` | Copy files from host to image |
| `ADD` | Copy files or extract archives; supports remote sources |
| `RUN` | Execute commands while building the image |
| `CMD` | Set the default command when the container starts |
| `ENTRYPOINT` | Define the main executable |
| `EXPOSE` | Document the intended container port |
| `ENV` | Set environment variables |
| `VOLUME` | Declare a mount point for persistent data |

Example Dockerfile for the Java application shown in your PDF:

```dockerfile
FROM openjdk:11
WORKDIR /app
COPY HelloWorld.java .
RUN javac HelloWorld.java
CMD ["java", "HelloWorld"]
```

Build and run it:

```bash
docker build -t java-app .
docker run --name java-container java-app
```

## 5. Docker Hub login and credentials

| Command | Purpose |
|---|---|
| `docker login` | Log in to Docker Hub |
| `docker login -u username` | Log in with a username |
| `docker logout` | Log out |
| `docker pull username/my-app:latest` | Download an image |
| `docker push username/my-app:latest` | Upload an image |

To upload your own image:

```bash
docker login
docker build -t username/my-app:latest .
docker push username/my-app:latest
```

Replace `username` with your Docker Hub username. If password authentication is unavailable, use a Docker Hub access token when prompted for a password.

## 6. MySQL container commands

The PDF demonstrates running MySQL with port mapping and a root password.

```bash
docker pull mysql:8.3.0
```

Run MySQL:

```bash
docker run -d --name mysql-db -p 3316:3306 -e MYSQL_ROOT_PASSWORD=mysql mysql:8.3.0
```

Check the running container:

```bash
docker ps
```

Here, host port `3316` maps to MySQL's container port `3306`. Connect using `localhost:3316` and the configured credentials.

## Git credential helper reset example

```bash
@"protocol=https
host=github.com
"@ | git credential reject
```

This command tells Git to reject the stored credential entry for `github.com` in the credential helper.

## Publish a web app image to Docker Hub

1. Build the Docker image

```bash
Run these commands from the folder containing your Dockerfile.
docker build -t my-web-app .
```

2. Login to Docker Hub

```bash
docker login
```

3. Tag the image

```bash
docker tag my-web-app diya1306/my-web-app:latest
```

4. Push the image to Docker Hub

```bash
docker push diya1306/my-web-app:latest
```

5. Pull the image from Docker Hub

```bash
docker pull diya1306/my-web-app:latest
```

6. Create and run a container

```bash
docker run -d --name hub-container -p 8080:80 diya1306/my-web-app:latest
```

7. Verify the result

```bash
docker images
docker ps
```

Open `http://localhost:8080` to test your application.

Docker Hub repository: `hub.docker.com/r/diya1306/my-web-app`

Note: The repository will be accessible after you push the image successfully.

---

This file includes Git/GitHub practical notes and Docker practical commands for exam preparation and revision.
