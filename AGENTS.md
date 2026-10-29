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

## Presentation Deck Mode Guidelines & Architecture
- **Typography Scale (+10%)**: Presentation Deck Mode typography is calibrated at **+10%** relative to Webpage baseline (not +20%) with tightened vertical margins and padding. This ensures zero text cutoff on compact laptop screens (e.g. 1024×640) while maintaining clean visual weight on 1080p and 4K displays.
- **Slide 1 Layout (50/50 Grid)**:
  - **Left column (`.pres-hero-info`)**: Project title, metadata, and details (Objective, Strategy, Execution, Achievements).
  - **Right column (`.pres-hero-media`)**: Looping hero video (no play icon overlay, non-clickable to enlarge), followed directly beneath by **"Skills & Capabilities"** (`.project-skills`), followed directly beneath by **"Sources"** (`.project-sources`).
- **Case Study Slides**:
  - The left column (`.pres-casestudy-text-col`) contains the top title bar, "Case Study" pill, and the 4 case study narrative blocks. Sources are not repeated here since they live on Slide 1.
- **Deep-Linking via `#deck`**:
  - Direct URL deep-linking into Presentation Mode is handled via `window.location.hash === '#deck'`. State transitions update browser history via `history.replaceState`.
- **Spotlight Video Modals**:
  - Master film modals use the unified lightbox modal with standard 16:9 ratio and high-res video posters.

