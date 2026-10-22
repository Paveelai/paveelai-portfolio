# Workspace Rules (`paveelai-portfolio`)

## Multi-Machine Git Sync Rule (Run at Session Start)
The user works across two machines on this repository (`https://github.com/Paveelai/paveelai-portfolio.git`).
Before making any file edits at the start of a new session:
1. Check the local Git state (`git status -sb`, `git branch`, and recent commits on `dev` and `main`).
2. Remind the user (or provide the terminal command) to pull the latest changes from GitHub across both `main` and `dev` before starting edits if they haven't synced on the current machine yet:
   ```bash
   git checkout main && git pull origin main && git checkout dev && git pull origin dev && git merge main --no-edit
   ```

## Publishing / Live Deployment Workflow
- Working branch: `dev`
- Live production branch: `main`
- When the user asks for the terminal commands to push/publish changes live, always provide this exact sequence (using straight ASCII double quotes `"` for the commit message):
  ```bash
  git add index.html
  git commit -m "<commit message>"
  git push origin dev
  git checkout main && git merge dev --no-edit && git push origin main && git checkout dev
  ```
  *(If new media files in `img/` or `video/` were added, include them in `git add`.)*

