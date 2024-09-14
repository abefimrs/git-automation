# Git Hooks and Automation in DevOps

Git hooks are scripts that Git automatically executes before or after specific events, such as making a commit or pushing code to a remote repository. These hooks can be powerful tools to automate workflows, enforce policies, and ensure code quality. In a DevOps environment, Git hooks are an excellent way to integrate various automation tasks directly into the development workflow, reducing errors and ensuring consistency.

---

## Types of Git Hooks

Git hooks are divided into **client-side** and **server-side** hooks.

- **Client-Side Hooks**: Triggered on local operations such as committing or merging code.
  - Common examples: `pre-commit`, `commit-msg`, `pre-push`
- **Server-Side Hooks**: Triggered on events like receiving a push in a remote repository.
  - Common examples: `pre-receive`, `post-receive`, `update`

---

## Key Git Hooks for Automation

### 1. Pre-Commit Hook

- **Trigger**: Runs before the commit is created.
- **Usage**: Validate code quality, run tests, or check formatting to prevent bad commits.

**Example: Automating Code Formatting with Prettier**

Automatically format code before every commit to ensure consistency.

```bash
#!/bin/bash
# .git/hooks/pre-commit

echo "Running Prettier..."
prettier --write '**/*.js' # Automatically format JavaScript files

if [ $? -ne 0 ]; then
  echo "Prettier failed. Aborting commit."
  exit 1
fi

``````

**Automation Example**:Enforce code formatting standards across teams to avoid style inconsistencies. Developers can’t commit code unless it's properly formatted, reducing PR review times.




### 2. Commit-msg Hook
- **Trigger**: Runs after a commit message is typed but before the commit is finalized.
- **Usage** : Ensure commit messages follow a specific convention (e.g., conventional commits).

**Example: Enforcing Commit Message Format**

Ensure that commit messages follow a standard format like [Type]: Message to maintain consistency and help with automated changelog generation.

````
#!/bin/bash
# .git/hooks/commit-msg

COMMIT_MSG=$(cat "$1")
if ! grep -qE "^\[(feat|fix|chore)\]: " <<< "$COMMIT_MSG"; then
  echo "Invalid commit message format. Expected format: '[Type]: Message'"
  exit 1
fi
````

**Automation Example** : Ensures that all commits follow a specific format, enabling tools like semantic versioning and automatic changelog generation in CI/CD pipelines.

### 3. Pre-Push Hook

- **Trigger**: Runs before pushing commits to a remote repository.
- **Usage**: Run tests, lint code, or check for vulnerabilities to prevent faulty code from reaching the repository.
**Example: Running Unit Tests Before Push**

Prevent pushing code if unit tests fail.
````
#!/bin/bash
# .git/hooks/pre-push

echo "Running tests before push..."
npm test

if [ $? -ne 0 ]; then
  echo "Tests failed. Aborting push."
  exit 1
fi
````

**Automation Example: Prevents breaking code from reaching the repository, ensuring that all pushed code has passed a baseline quality check. This helps maintain the integrity of the main branch in CI/CD pipelines.**

### 4. Pre-Receive Hook (Server-Side)

- **Trigger**: Runs before the remote repository accepts a push.
- **Usage**: Enforce repository-wide policies, such as branch protection rules, code validation, or rejecting large files.
**Example: Blocking Large File Uploads**

Rejects any push that contains files larger than 10MB to avoid bloating the repository.

````
#!/bin/bash
# .git/hooks/pre-receive

MAX_SIZE=10485760 # 10 MB in bytes

while read oldrev newrev refname
do
  # Find all files added/modified in the push and check their size
  git diff-tree -r --name-only --diff-filter=AM $oldrev $newrev | while read filename
  do
    FILESIZE=$(git ls-tree -r $newrev -- $filename | awk '{print $4}')
    if [ "$FILESIZE" -gt "$MAX_SIZE" ]; then
      echo "File $filename exceeds the maximum allowed size of 10MB"
      exit 1
    fi
  done
done
````
**Automation Example**: Prevent large files from being added to the repository by mistake, maintaining the repository’s performance and size.

### 5. Post-Receive Hook (Server-Side)
- **Trigger**: Runs after the repository accepts a push.
- **Usage**: Trigger actions such as deployment, sending notifications, or updating issue trackers.
**Example: Automated Deployment on Push**

Automatically deploy code to a staging environment after a successful push to the staging branch.

````
#!/bin/bash
# .git/hooks/post-receive

while read oldrev newrev refname
do
  if [[ "$refname" == "refs/heads/staging" ]]; then
    echo "Deploying to staging..."
    # Run deployment script
    ./deploy-staging.sh
  fi
done
````

**Automation Example**: As soon as code is pushed to the staging branch, it automatically deploys to the staging environment, ensuring continuous deployment in a DevOps pipeline.

## Full DevOps Workflow with Git Hooks and Automation
- In a DevOps scenario, you can use Git hooks at various stages to automate tasks and enforce policies.

- Pre-Commit (Local): Run a pre-commit hook that automatically formats code using Prettier and ensures code is linted before committing.
- Commit-msg (Local): The commit-msg hook checks that commit messages follow the conventional commit format [feat/fix/chore]: Message, helping to generate changelogs and maintain project history consistency.
- Pre-Push (Local): Before a developer can push their code, the pre-push hook ensures that all unit tests and lint checks have passed. If the tests fail, the push is aborted.
- Pre-Receive (Server-Side): When the code is pushed to the repository, a server-side pre-receive hook verifies that no large files (above 10MB) are included and checks that the pushed code meets specific branch protection rules.
- Post-Receive (Server-Side): After the code is accepted by the repository, the post-receive hook automatically triggers a deployment script that deploys the new code to a staging environment.

## Benefits of Using Git Hooks for Automation in DevOps
- **Consistent Code Quality**: Git hooks ensure that developers can't push or commit code that doesn't meet your project’s quality standards, such as style guides, test coverage, or security checks.
- **Prevention of Errors**: Automation via hooks reduces human error by automatically checking and enforcing policies before code is committed or pushed.
- **Faster Feedback Loop**: Pre-push or pre-receive hooks provide immediate feedback, allowing developers to fix issues before they become bigger problems in the CI/CD pipeline.
- **Streamlined Workflow**: Automating routine tasks like formatting, testing, and deployment streamlines the development process, allowing DevOps teams to focus on writing and improving code.
- **Security**: Security checks can be enforced early, such as preventing secrets from being committed or running vulnerability scans on dependencies, shifting security left in the pipeline.
- **Branch Protection**: Hooks prevent unauthorized or accidental changes to protected branches like main or production, ensuring that code is reviewed and tested thoroughly before being merged.

## Conclusion
Git hooks are a powerful tool in the DevOps arsenal, enabling you to automate various tasks and enforce standards at every step of the development lifecycle. By leveraging hooks effectively, you can significantly improve both developer productivity and the robustness of your DevOps pipeline.


