---
name: Create Pull Request
description: Helps the user or agent stage, commit, and push changes to GitHub, then generates a PR link. Use this when the user is ready to submit their changes for review or deployment.
---

# Create Pull Request Skill

## Workflow Integration

This skill is designed to be used in conjunction with the `create-pr` workflow. It provides the logic for formatting commits and generating GitHub URLs without requiring the `gh` CLI.

## Commit Message Guidelines

Strive for clear, concise commit messages.

- **Format**: `Action: Brief description`
- **Examples**:
  - `Feat: add "Click" book review post`
  - `Fix: update broken link in resume`
  - `Docs: update Jekyll configuration for local preview`

## Branching Strategy

- If the user is on `main`, suggest creating a new branch before committing: `git checkout -b feature/your-feature-name`.
- If already on a feature branch, proceed with staging and committing.

## PR Link Generation

Since we cannot create the PR via CLI, we generate a URL that opens the PR creation page on GitHub with the correct branches pre-selected.

- **Base URL**: `https://github.com/taylor-consulting/taylor-consulting.github.page/compare/main...[BRANCH_NAME]`
- **Replace `[BRANCH_NAME]`** with the local branch name that was pushed to origin.

## PR Description Template

When providing the link to the user, also suggest a brief PR description:

```markdown
### Summary
[Brief description of changes]

### Checklist
- [x] Tested locally
- [x] Front matter follows site standards
- [x] Links verified
```

## Step-by-Step Execution logic

1. **Verify State**: Run `git status` to see what's being committed.
2. **Stage**: `git add .` (or specific files).
3. **Commit**: `git commit -m "Your message"`
4. **Push**: `git push origin [BRANCH_NAME]`
5. **Link**: Provide the URL to the user.
