> Here's a comprehensive list of Git commands organized from beginner to expert level, with examples and descriptions, designed for you to practice daily and gradually enhance your skills.
>  This list also touches on concepts related to using Git as a CI/CD tool.

# Git Command Cheat Sheet

## Beginner

| **Command**               | **Description**                                                                                       | **Example**                                      |
|---------------------------|-------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| `git init`                | Initializes a new Git repository.                                                                     | `git init`                                       |
| `git clone <url>`         | Clones a repository from a remote source (e.g., GitHub).                                               | `git clone https://github.com/user/repo.git`     |
| `git status`              | Shows the working directory status and staged changes.                                                 | `git status`                                     |
| `git add <file>`          | Adds file(s) to the staging area for commit.                                                           | `git add file.txt`                               |
| `git commit -m "message"` | Commits staged changes with a descriptive message.                                                     | `git commit -m "Initial commit"`                 |
| `git push`                | Pushes changes to a remote repository.                                                                 | `git push origin main`                           |
| `git pull`                | Fetches and merges changes from the remote repository.                                                 | `git pull origin main`                           |
| `git log`                 | Shows the commit history.                                                                              | `git log`                                        |
| `git diff`                | Shows the differences between working directory, staged, or committed files.                           | `git diff HEAD`                                  |
| `git checkout <branch>`   | Switches to the specified branch.                                                                      | `git checkout main`                              |
| `git branch`              | Lists branches or creates a new branch.                                                                | `git branch`, `git branch new-feature`           |

## Intermediate

| **Command**                     | **Description**                                                                                  | **Example**                                        |
|----------------------------------|--------------------------------------------------------------------------------------------------|----------------------------------------------------|
| `git fetch`                      | Retrieves changes from the remote repository but does not merge them.                            | `git fetch origin`                                 |
| `git merge <branch>`             | Merges another branch into the current branch.                                                   | `git merge feature-branch`                         |
| `git reset <file>`               | Unstages a file from the staging area without deleting it.                                        | `git reset file.txt`                               |
| `git reset --hard`               | Resets the working directory and staging area to the last commit, discarding changes.             | `git reset --hard`                                 |
| `git rebase <branch>`            | Reapplies commits from the current branch on top of another base branch.                          | `git rebase main`                                  |
| `git stash`                      | Temporarily saves changes not ready to commit and resets the working directory.                   | `git stash`                                        |
| `git stash pop`                  | Restores stashed changes back to the working directory.                                           | `git stash pop`                                    |
| `git cherry-pick <commit>`       | Applies changes from a specific commit onto the current branch.                                   | `git cherry-pick a1b2c3d`                          |
| `git remote add <name> <url>`    | Adds a new remote repository.                                                                    | `git remote add origin https://github.com/repo.git` |
| `git remote -v`                  | Shows remote repository URLs.                                                                    | `git remote -v`                                    |
| `git tag <tagname>`              | Creates a tag for a specific commit (often for releases).                                         | `git tag v1.0.0`                                   |
| `git log --oneline --graph`      | Shows a compact log with a visual graph of commits.                                               | `git log --oneline --graph`                        |
| `git commit --amend`             | Modifies the previous commit with new changes or a new message.                                   | `git commit --amend -m "Updated commit message"`   |
| `git diff --staged`              | Shows differences between staged files and the last commit.                                       | `git diff --staged`                                |
| `git clean -f`                   | Removes untracked files from the working directory.                                               | `git clean -f`                                     |
| `git reflog`                     | Shows the history of changes made to references (HEAD, branches).                                 | `git reflog`                                       |

## Advanced

| **Command**                           | **Description**                                                                               | **Example**                                         |
|---------------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------|
| `git blame <file>`                    | Shows who last modified each line of a file.                                                  | `git blame file.txt`                                |
| `git bisect start`                    | Starts a binary search to find a commit that introduced a bug.                                | `git bisect start`                                  |
| `git bisect good <commit>`            | Marks a known good commit during a binary search.                                             | `git bisect good a1b2c3d`                           |
| `git bisect bad <commit>`             | Marks a bad commit to identify when a bug was introduced.                                     | `git bisect bad a1b2c3d`                            |
| `git submodule add <url>`             | Adds a submodule to your repository.                                                          | `git submodule add https://github.com/user/submodule.git` |
| `git rebase --interactive <branch>`   | Rebases the current branch interactively, allowing you to reorder, squash, or edit commits.    | `git rebase --interactive main`                     |
| `git stash save "description"`        | Stashes changes with a description.                                                           | `git stash save "WIP"`                              |
| `git stash list`                      | Shows all stashes.                                                                           | `git stash list`                                    |
| `git stash apply <stash>`             | Applies a specific stash without removing it from the stash list.                             | `git stash apply stash@{0}`                         |
| `git reset --soft HEAD~1`             | Resets the last commit, keeping changes in the staging area.                                  | `git reset --soft HEAD~1`                           |
| `git branch -d <branch>`              | Deletes a branch.                                                                            | `git branch -d feature-branch`                      |
| `git branch -m <old> <new>`           | Renames a branch.                                                                            | `git branch -m old-branch new-branch`               |
| `git push origin :<branch>`           | Deletes a branch on a remote repository.                                                     | `git push origin :old-branch`                       |
| `git filter-branch --force`           | Rewrites branches (used to remove large files, sensitive data).                               | `git filter-branch --force --index-filter 'rm -rf largefile.txt'` |
| `git worktree add`                    | Adds a new working tree linked to the same repository.                                        | `git worktree add ../path-to-another-dir new-branch` |
| `git config --global`                 | Configures global settings like username, email, editor, etc.                                 | `git config --global user.name "Your Name"`         |

## Expert

| **Command**                           | **Description**                                                                               | **Example**                                         |
|---------------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------|
| `git commit --squash <commit>`        | Combines multiple commits into one during an interactive rebase.                              | `git rebase --interactive main && git commit --squash a1b2c3d` |
| `git subtree add --prefix <dir> <url>`| Adds a repository as a subtree in the specified directory.                                     | `git subtree add --prefix subfolder https://github.com/repo.git` |
| `git push --tags`                     | Pushes all tags to the remote repository.                                                     | `git push --tags`                                    |
| `git push --force`                    | Forces a push, potentially overwriting remote changes (be cautious).                          | `git push --force origin feature-branch`             |
| `git cherry <branch>`                 | Shows commits that are in the current branch but not in the specified branch.                  | `git cherry main`                                    |
| `git bundle create`                   | Creates a bundle of a repository that can be shared or used offline.                          | `git bundle create repo.bundle HEAD main`            |
| `git fsck`                            | Verifies the integrity of the repository.                                                     | `git fsck`                                           |
| `git gc`                              | Cleans up unnecessary files and optimizes the local repository.                               | `git gc`                                             |
| `git archive`                         | Creates an archive of files from a particular commit or branch.                               | `git archive --format=zip HEAD > archive.zip`        |
| `git daemon`                          | Starts a simple Git server to share your repository over the network.                         | `git daemon --base-path=/path/to/repo/`              |
| `git worktree prune`                  | Removes working trees that are no longer used.                                                | `git worktree prune`                                 |

## Git for CI/CD Integration

| **Command**                           | **Description**                                                                               | **Example**                                         |
|---------------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------|
| `git commit --allow-empty`            | Creates a commit with no changes (useful for triggering builds in CI).                        | `git commit --allow-empty -m "Trigger build"`       |
| `git rev-parse --abbrev-ref HEAD`     | Prints the current branch name (used in CI scripts for branch-specific actions).              | `git rev-parse --abbrev-ref HEAD`                   |
| `git rev-list --count HEAD`           | Counts the number of commits (useful for generating version numbers in CI/CD).

---


> Daily Practice Tips
To practice daily, try combining various commands. For example:


**Day 1**: Set up a repository (git init), make some changes, commit them (git add, git commit), and push to a remote (git push).

**Day 2**: Clone a repo (git clone), switch branches (git branch, git checkout), and create a pull request workflow.

**Day 3**: Practice resolving conflicts (git merge, git rebase) and resetting changes (git reset).

**Day 4**: Work with stashes (git stash, git stash pop), and manage submodules (git submodule).

**Day 5**: Dive into advanced branching, rebasing (git rebase), and interacting with remotes (git remote, git fetch).

**Day 6**: Explore CI/CD commands and scripts for continuous integration tasks.
