# Git Commands for Integrating with CI/CD Pipelines

| **Command**                           | **Description**                                                                                     | **Example**                                          |
|---------------------------------------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------|
| `git commit --allow-empty`            | Creates a commit with no changes, useful for triggering builds in CI pipelines.                      | `git commit --allow-empty -m "Trigger build"`        |
| `git rev-parse --abbrev-ref HEAD`     | Prints the current branch name, often used in CI scripts to determine branch-specific tasks.         | `git rev-parse --abbrev-ref HEAD`                   |
| `git rev-list --count HEAD`           | Counts the number of commits, helpful for generating build numbers or versions in CI/CD pipelines.   | `git rev-list --count HEAD`                         |
| `git describe --tags`                 | Generates a description of the current commit based on the latest tag, used for versioning.          | `git describe --tags`                               |
| `git diff --name-only origin/main`    | Lists files that have changed compared to a remote branch, used in CI to selectively run tests.      | `git diff --name-only origin/main`                  |
| `git config credential.helper store`  | Stores Git credentials for use in CI environments to avoid interactive authentication prompts.       | `git config --global credential.helper store`        |
| `git clean -fd`                       | Forcefully removes untracked files and directories to ensure a clean workspace in CI pipelines.      | `git clean -fd`                                     |
| `git stash --include-untracked`       | Stashes all changes, including untracked files, ensuring a clean state for building in CI.           | `git stash --include-untracked`                     |
| `git show-ref --tags`                 | Displays all tags, useful for triggering CI/CD tasks based on version releases.                      | `git show-ref --tags`                               |
| `git log -1 --pretty=%B`              | Retrieves the latest commit message, often used in CI to parse information for deployments.          | `git log -1 --pretty=%B`                            |
| `git log --format="%H" -n 1`          | Retrieves the latest commit hash, useful in CI for tracking the commit version deployed.             | `git log --format="%H" -n 1`                        |
| `git checkout --force <branch>`       | Forces checkout of a specific branch in a CI pipeline, ignoring any local changes.                   | `git checkout --force main`                         |
| `git archive`                         | Creates an archive (e.g., zip) of the repository, often used to package code for deployment.         | `git archive --format=zip HEAD > repo.zip`          |
| `git submodule update --init --recursive` | Ensures submodules are initialized and updated, essential in CI environments for full project builds.| `git submodule update --init --recursive`           |
| `git fetch --tags`                    | Fetches all tags from the remote repository, useful for version-based CI tasks.                      | `git fetch --tags`                                  |

----

## Daily Practice Tips for Git CI/CD Integration

1. **Set up a basic CI Pipeline**: Create a GitHub Actions or GitLab CI pipeline triggered by `git push` or `git commit`.
2. **Automate builds**: Use `git commit --allow-empty` to trigger a CI build.
3. **Branch-specific builds**: Write a CI script that runs different jobs depending on the output of `git rev-parse --abbrev-ref HEAD`.
4. **Selective testing**: Implement a pipeline that runs tests only for files changed using `git diff --name-only`.
5. **Versioning**: Use `git describe --tags` or `git rev-list --count` to create dynamic version numbers in your pipeline.
6. **Clean builds**: Ensure a clean build environment by using `git clean -fd` or `git stash --include-untracked`.

By automating these Git tasks within CI/CD pipelines, you'll be able to create an efficient workflow that handles building, testing, and deployment with each commit or branch update.
