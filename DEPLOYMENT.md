# Deployment Guide

Complete guide for deploying the **Moe Kyaw Aung Portfolio** to GitHub Pages.

---

## Quick Deploy (2 minutes)

### Step 1 — Create the Repository

1. Go to [github.com/new](https://github.com/new)
2. Sign in as **Dev-moe-kyawaung**
3. Set repository name: `moe-kyaw-aung-portfolio`
4. Set visibility: **Public** ← required for free GitHub Pages
5. Do NOT initialize with README (you already have files)
6. Click **Create repository**

### Step 2 — Push Files

```bash
# Clone or initialize local repo
git init
git add .
git commit -m "🚀 feat: initial portfolio release v2.0.0"
git branch -M main
git remote add origin https://github.com/Dev-moe-kyawaung/moe-kyaw-aung-portfolio.git
git push -u origin main
```

### Step 3 — Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Under **Build and deployment**, set Source to: **GitHub Actions**
3. The workflow (`.github/workflows/deploy.yml`) will trigger automatically
4. Wait ~60 seconds, then visit:

```
https://dev-moe-kyawaung.github.io/moe-kyaw-aung-portfolio/
```

---

## GitHub Actions Workflow

The included workflow (`.github/workflows/deploy.yml`) runs automatically on every push to `main`:

```
Push to main
    │
    ▼
[Job 1] Validate
    • Confirms index.html exists
    • Reports file sizes
    │
    ▼
[Job 2] Build
    • Configures GitHub Pages
    • Injects build timestamp
    • Uploads artifact
    │
    ▼
[Job 3] Deploy
    • Deploys to github-pages environment
    • Outputs live URL
```

Check workflow status at:  
`https://github.com/Dev-moe-kyawaung/moe-kyaw-aung-portfolio/actions`

---

## Manual Deploy (Alternative)

If you prefer branch-based deployment:

1. **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main`, Folder: `/ (root)`
4. Save

> ⚠️ Manual deploy doesn't use the GitHub Actions workflow. The Actions method is recommended.

---

## Custom Domain (Optional)

To use a custom domain (e.g. `moekyawaung.dev`):

1. Add a `CNAME` file in the root:
   ```
   moekyawaung.dev
   ```
2. In **Settings → Pages → Custom domain**, enter your domain
3. Update your DNS provider:
   - Add 4 A records pointing to GitHub's IPs:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - Add a CNAME: `www` → `dev-moe-kyawaung.github.io`
4. Enable **Enforce HTTPS** ✅

---

## Updating the Portfolio

```bash
# Make your changes to index.html or index-v2.html
git add .
git commit -m "✨ feat: update projects section"
git push origin main
# GitHub Actions auto-deploys in ~60 seconds
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| 404 on the homepage | Check Pages source is set to GitHub Actions |
| Workflow failing | Check Actions tab for error logs |
| Changes not showing | Hard refresh `Ctrl+Shift+R` — CDN cache |
| Fonts not loading | Check internet connection (uses Google Fonts CDN) |
| Badge images broken | shields.io may be rate-limited — retry in 5 min |
