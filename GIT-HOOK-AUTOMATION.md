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

## Automation Example:
Enforce code formatting standards across teams to avoid style inconsistencies. Developers can’t commit code unless it's properly formatted, reducing PR review times.
