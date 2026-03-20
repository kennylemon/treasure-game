Deploy the project to GitHub Pages by following these steps:

## Prerequisites check
1. Run `git remote get-url origin` to get the remote URL. If it fails, tell the user to run `/deploy_github` first to push the repo to GitHub.
2. Parse the GitHub username and repo name from the remote URL.

## Configure Vite base path
3. Read `vite.config.ts`. Check if `base` is already set in `defineConfig`.
   - If not set (or set to `/`), add `base: '/<repo-name>/',` inside `defineConfig({` — this is required for GitHub Pages to serve assets correctly.
   - If already correctly set, skip this step.

## Install gh-pages
4. Check if `gh-pages` is in `package.json` devDependencies. If not, run `npm install --save-dev gh-pages`.

## Build
5. Run `npm run build` and wait for it to complete. If it fails, report the error and stop.

## Deploy to gh-pages branch
6. Run `npx gh-pages -d build` to push the `build/` directory to the `gh-pages` branch on origin.

## Enable GitHub Pages via API
7. Run:
   ```
   gh api repos/<username>/<repo>/pages \
     --method POST \
     -f build_type=legacy \
     -f source[branch]=gh-pages \
     -f source[path]=/ 2>&1
   ```
   If it returns "already enabled" or a 409 conflict, that's fine — Pages was already configured.

## Report the URL
8. The GitHub Pages URL will be: `https://<username>.github.io/<repo>/`
   Print this URL to the user and note that it may take 1–2 minutes to go live after the first deploy.

## Commit config changes
9. If `vite.config.ts` or `package.json` were modified, stage and commit them:
   ```
   git add vite.config.ts package.json package-lock.json
   git commit -m "Configure GitHub Pages deployment"
   git push
   ```
