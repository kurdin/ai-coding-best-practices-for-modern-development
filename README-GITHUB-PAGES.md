# GitHub Pages Deployment

This repository is configured to automatically deploy the AI Coding Best Practices presentation to GitHub Pages.

## ⚠️ IMPORTANT: Initial Setup Required

**You MUST manually enable GitHub Pages first:**

1. **Go to your repository on GitHub**
2. **Navigate to Settings → Pages** (in the left sidebar)
3. **Under "Source", select "GitHub Actions"**
4. **Click Save**
5. **Then push your code or re-run the workflow**

## Why Manual Setup?

GitHub requires repository owners to explicitly enable Pages for security reasons. The workflow cannot automatically enable it due to permission restrictions.

## After Initial Setup

Once Pages is enabled, the workflow will automatically:
- Copy `ai-coding-best-practices.html` to `index.html`
- Deploy all files including the cheatsheets
- Make the presentation available at: `https://[username].github.io/[repository-name]/`

## Files Deployed

- `index.html` (main presentation)
- `Claude Code CLI Cheatsheet.md`
- `OpenAI Codex CLI Cheatsheet.md`
- `README.md`

## Deployment Triggers

The GitHub Pages deployment runs on:
- Push to `main` branch
- Pull requests to `main` branch
- Manual trigger via GitHub Actions tab

## Access Your Deployed Site

Once deployed, your presentation will be available at:
```
https://[your-github-username].github.io/aI-coding-best-practices-for-modern-development/
```

The cheatsheets will be accessible as styled HTML pages at:
- Claude Code Cheatsheet: `https://[username].github.io/[repo]/claude-code-cheatsheet.html`
- OpenAI Codex Cheatsheet: `https://[username].github.io/[repo]/openai-codex-cheatsheet.html`

Original markdown files are also available:
- `https://[username].github.io/[repo]/Claude%20Code%20CLI%20Cheatsheet.md`
- `https://[username].github.io/[repo]/OpenAI%20Codex%20CLI%20Cheatsheet.md`

## Manual Deployment

To manually trigger a deployment:
1. Go to Actions tab
2. Select "Deploy to GitHub Pages" workflow
3. Click "Run workflow"
4. Select the branch and click "Run workflow"