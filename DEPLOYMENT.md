# Deploying to Cloudflare Pages

This guide walks you through setting up auto-deployment of your Sheltered Gaming website to Cloudflare Pages.

## Prerequisites

1. ✅ A GitHub account with this repository
2. ✅ A Cloudflare account (free tier is fine)
3. ✅ Your custom domain (optional, but recommended)

## Step 1: Push to GitHub

First, ensure your code is on GitHub:

```bash
# Initialize git if not already done
git init

# Add all files
git add .

# Make initial commit
git commit -m "Initial commit: Sheltered Gaming website"

# Add remote (replace with your repo URL)
git remote add origin https://github.com/YOUR_USERNAME/sheltered-gaming.git

# Push to main branch
git branch -M main
git push -u origin main
```

## Step 2: Set Up Cloudflare Pages

### Option A: Auto-setup from Cloudflare Dashboard

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. Click **Pages** in the left sidebar
3. Click **Create a project**
4. Select **Connect to Git**
5. **Authorize Cloudflare** to access your GitHub account
6. Select your GitHub organization and repository (`sheltered-gaming`)
7. Click **Begin setup**

### Project Configuration

On the "Set up builds and deployments" screen:

- **Project name**: `sheltered-gaming` (or your preferred name)
- **Production branch**: `main`
- **Framework preset**: Select `11ty` (it will auto-detect)
- **Build command**: `npm run build`
- **Build output directory**: `_site`
- **Root directory**: `/` (leave default)
- **Environment variables**: (leave empty for now)

Click **Save and Deploy**

## Step 3: Verify Deployment

1. Cloudflare will trigger a build automatically
2. You'll see a build log - wait for it to complete (usually 1-2 minutes)
3. Once complete, you'll get a URL like `sheltered-gaming.pages.dev`
4. Click the link to verify your site deployed correctly

## Step 4: Connect Your Custom Domain (Optional)

### If you own ShelteredGaming.com:

1. In Cloudflare Pages project settings
2. Go to **Custom domains**
3. Click **Set up a custom domain**
4. Enter your domain: `sheltered-gaming.com`
5. Follow the instructions to verify DNS:
   - Go to your domain registrar
   - Add the CNAME record that Cloudflare provides
   - Wait for DNS propagation (can take up to 24 hours)

### If you want to use Cloudflare DNS:

1. Add your domain to Cloudflare (also free)
2. Set nameservers with your registrar
3. Then follow the custom domain steps above

You can also use a subdomain like `gaming.shelteredgaming.com` if you prefer.

## Step 5: Auto-Deployment is Now Active!

From now on, whenever you:

1. **Edit markdown files** in the `src/games/` folder
2. **Commit and push** to GitHub
3. **Cloudflare automatically**:
   - Detects the change
   - Builds the site (`npm run build`)
   - Deploys to your live site

No manual steps needed after this!

### Push Updates Example

```bash
# Edit your Rust server info
nano src/games/rust.md
# (Update serverIp, serverPort, etc.)

# Commit and push
git add src/games/rust.md
git commit -m "Update Rust server info"
git push

# Done! Cloudflare handles the rest automatically
```

## Step 6: Monitor Deployments (Optional)

To see deployment history and logs:

1. Go to Cloudflare Pages project
2. Click **Deployments** tab
3. View recent builds and their logs
4. If a build fails, click to see error details

## Troubleshooting

### Build Fails on Cloudflare

Check the build logs in the Cloudflare dashboard:

1. Go to Pages → Your project
2. Click **Deployments**
3. Click the failed deployment
4. View the **Build log**
5. Common issues:
   - Missing npm dependencies (run `npm install` locally to test)
   - Placeholder values not replaced (check `src/games/` files)
   - Typos in frontmatter (must be valid YAML)

### Changes not appearing after push

- **Wait 2-3 minutes** for the build to complete
- Check the **Deployments** tab to verify build succeeded
- Clear your browser cache (Ctrl+Shift+Delete)
- Check that files are in `src/` not `_site/`

### Domain not working

- Verify CNAME record was added correctly
- Wait up to 24 hours for DNS propagation
- Use DNS lookup tools to check: `nslookup sheltered-gaming.com`
- Go to Cloudflare Pages → Settings → Custom domains to verify setup

### Still having issues?

1. Try building locally: `npm run build`
2. Check the README.md for local dev instructions
3. Look at the GitHub Actions logs for clues
4. Verify all placeholder values are updated in markdown files

## To Update Server Information

Once deployed, updating server info is simple:

1. **Find** the game page you want to update (e.g., `src/games/rust.md`)
2. **Edit** the front matter at the top:
   ```yaml
   serverIp: "play.shelteredgaming.com"
   serverPort: "28015"
   playerCount: "45/100 players"
   discordInvite: "https://discord.gg/your-invite"
   ```
3. **Save** and **commit**:
   ```bash
   git add src/games/rust.md
   git commit -m "Update Rust server IP"
   git push
   ```
4. **Done!** Cloudflare automatically deploys within 1-2 minutes

## Team Collaboration

Multiple people can work on the site:

1. **Each person** clones the repo: `git clone <repo-url>`
2. **Create branches** for features: `git checkout -b update/rust-server-info`
3. **Make changes** and commit
4. **Push and create** a Pull Request on GitHub
5. **Another person reviews** and merges to `main`
6. **Cloudflare auto-deploys** after merge

## Advanced: Manual Deployments

If you need to manually trigger a deployment without pushing code:

1. Go to Cloudflare Pages → Your project
2. Click **Deployments** → **Retry build** on any previous deployment

This will rebuild and redeploy using the current GitHub code.

## Questions?

See the main README.md for more info about the project structure and editing content!
