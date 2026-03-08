# Mystora Workspace

Welcome to the Mystora workspace.

## Important Git Commands

Here is a quick reference for common Git operations:

### `git add`
Use `git add` to stage changes for the next commit.
- Stage specific file: `git add <file>`
- Stage all files in the current directory: `git add .`
- Stage all files in the repository: `git add -A`

### `git commit`
Use `git commit` to save your staged changes to the local repository.
- Commit with a message: `git commit -m "Your descriptive commit message"`
- Add and commit all tracked modified files at once: `git commit -am "Your commit message"`

### `git reset`
Use `git reset` to undo changes or unstage files.
- Unstage a file (keep the modifications): `git reset <file>`
- Undo the last commit (keep the modifications un-staged): `git reset HEAD~1`
- Undo the last commit and discard all modifications (Caution: Destructive): `git reset --hard HEAD~1`
- Undo local un-staged modifications to a specific file: `git checkout -- <file>` or `git restore <file>`
