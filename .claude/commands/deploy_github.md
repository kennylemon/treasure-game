Deploy the current project to GitHub by following these steps:

1. Check if git is initialized (`git status`). If not, run `git init`.
2. Check if a remote named `origin` exists (`git remote -v`). If not, use `gh repo create` to create a new GitHub repository and add it as the remote.
3. Check for a `.gitignore` — if `node_modules` is not ignored, add it.
4. Stage all files: `git add -A`
5. Commit: `git commit -m "Initial commit"` (skip if nothing to commit)
6. Push to GitHub: `git push -u origin main` (or `master` if that's the default branch)
7. Report the GitHub repository URL when done.

Ask the user for the desired repo name and whether it should be public or private before creating the repo.
