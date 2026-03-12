# Deploy QuotePro Dashboard to Cloudflare Pages

This repo is set up to deploy to **Cloudflare Pages** via GitHub Actions when you push to `main`.

## What’s included

| File | Purpose |
|------|--------|
| `wrangler.toml` | Cloudflare Pages project config (name, compatibility). |
| `.github/workflows/deploy-cloudflare-pages.yml` | GitHub Action that runs `wrangler pages deploy` on push to `main`. |
| `index.html` | Redirects site root to `QuotePro_Suite_Dashboard.html`. |
| `.gitignore` | Keeps logs, IDE, and secrets out of the repo. |

## One-time setup

### 1. Cloudflare API token

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com).
2. Go to **My Profile** → **API Tokens** → **Create Token**.
3. Use the **Edit Cloudflare Workers** template (or create a custom token with **Account** → **Cloudflare Pages** → **Edit**).
4. Create the token and copy it (you won’t see it again).

### 2. Cloudflare Account ID

1. In Cloudflare Dashboard, open any domain or go to **Workers & Pages**.
2. In the right-hand sidebar, copy your **Account ID**.

### 3. GitHub repository secrets

1. Open your GitHub repo → **Settings** → **Secrets and variables** → **Actions**.
2. Add:
   - **Name:** `CLOUDFLARE_API_TOKEN`  
     **Value:** the API token from step 1.
   - **Name:** `CLOUDFLARE_ACCOUNT_ID`  
     **Value:** the Account ID from step 2.

### 4. (Optional) Create the Pages project in Cloudflare

- You can let the first deployment create the project name `quotepro-dashboard`.
- Or create it yourself: **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → skip and create a **Direct Upload** project named `quotepro-dashboard`. After that, deployments from the workflow will go to this project.

## Deploying

- **Automatic:** Push (or merge) to the `main` branch. The workflow runs and deploys the current directory to Cloudflare Pages.
- **Manual:** Repo → **Actions** → **Deploy to Cloudflare Pages** → **Run workflow**.

## After deploy

- Your site will be at:  
  `https://quotepro-dashboard.pages.dev`  
  (or the custom domain you set in Cloudflare Pages).
- Visiting the root URL will redirect to `QuotePro_Suite_Dashboard.html`.

## Branch / production

- The workflow runs on pushes to `main`. To use another branch (e.g. `master`), edit `.github/workflows/deploy-cloudflare-pages.yml` and change `branches: [main]` to your branch.
