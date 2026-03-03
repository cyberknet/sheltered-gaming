# Sheltered Gaming Website

A static website for Sheltered Gaming community game servers, built with 11ty and auto-deployed to Cloudflare Pages.

## Features

- 🎮 **Multiple Game Servers** - Rust, Icarus, Minecraft Java, and Minecraft Bedrock
- 📱 **Responsive Design** - Works great on desktop, tablet, and mobile
- 🌙 **Dark Gaming Theme** - Modern aesthetic with RGB accent colors
- ⚡ **Static Site** - Fast, secure, and no backend needed
- 🚀 **Auto-Deploy** - Push markdown → auto-build and deploy to Cloudflare Pages
- 🔗 **Discord Integration** - Easy Discord server invites and community links

## Quick Start

### Local Development

```bash
# Install dependencies
npm install

# Start development server with live reload
npm start

# Build for production
npm run build
```

The development server will run at `http://localhost:8080` and auto-reload when you change files.

### Project Structure

```
src/
├── _includes/
│   ├── layouts/
│   │   ├── base.html          # Main page template
│   │   └── game-page.html     # Game page template
│   └── components/            # Reusable components
├── css/
│   └── style.css              # All styling
├── games/
│   ├── rust.md                # Rust server page
│   ├── icarus.md              # Icarus server page
│   ├── minecraft-java.md      # Minecraft Java server page
│   └── minecraft-bedrock.md   # Minecraft Bedrock server page
└── index.md                    # Homepage

_site/                          # Generated static HTML (don't edit)
.eleventy.js                    # 11ty configuration
package.json                    # Dependencies and scripts
wrangler.toml                   # Cloudflare Pages config
```

## Updating Server Information

Edit the markdown files in `src/games/` to update server information:

```yaml
---
layout: game-page.html
title: Rust Server
serverIp: "YOUR_ACTUAL_SERVER_IP"
serverPort: "28015"
playerCount: "Currently Online"
discordInvite: "https://discord.gg/YOUR_INVITE"
---
```

Replace these placeholders with actual values:
- `PLACEHOLDER_SERVER_IP` → Your actual server IP address
- `serverPort` → Your server's port number
- `playerCount` → Current player count or "Currently Online"
- `discordInvite` → Your Discord server invite link

## Deploying to Cloudflare Pages

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed instructions on:
1. Setting up your GitHub repository
2. Connecting to Cloudflare Pages
3. Configuring auto-deployment
4. Managing your domain

### What Happens Automatically

1. You commit markdown changes to GitHub
2. Push to the `main` branch
3. Cloudflare Pages automatically:
   - Triggers a build
   - Runs `npm run build`
   - Generates static HTML in `_site/`
   - Deploys to your site
4. Your site is live (usually within 1-2 minutes)

## Editing Content

### Homepage

Edit `src/index.md` to customize the homepage. This file uses the `base.html` layout.

### Game Pages

Each game has its own markdown file in `src/games/`:
- `rust.md` - Rust server page
- `icarus.md` - Icarus server page
- `minecraft-java.md` - Minecraft Java server page
- `minecraft-bedrock.md` - Minecraft Bedrock server page

All game pages use the `game-page.html` layout, which automatically displays:
- Server IP and port
- Player count
- Discord invite button

### Styling

Edit `src/css/style.css` to customize colors, fonts, and layout. The site uses CSS custom properties (variables) for easy theming:

```css
--primary-dark: #0a0e27;      /* Main background */
--secondary-dark: #1a1f3a;    /* Card backgrounds */
--accent-rgb: #ff006e;        /* Pink accent */
--accent-green: #00d9ff;      /* Cyan accent */
--accent-purple: #b537f2;     /* Purple accent */
```

## GitHub Actions (CI)

This project includes GitHub Actions that:
- Validates builds on pull requests and pushes
- Checks for placeholder values that need replacement
- Lists all generated pages

See `.github/workflows/build.yml` for configuration.

## Troubleshooting

### Build fails locally
```bash
# Clear cache and rebuild
npm run clean
npm install
npm run build
```

### Changes not appearing
- Make sure you edited files in the `src/` folder, not `_site/`
- The `_site/` folder is generated and will be overwritten
- Cloudflare Pages deployments can take 1-2 minutes

### Discord invite not working
- Check that the invite link is correct and not expired
- Test the link in your browser before adding to the site
- Use a permanent invite link if possible

## Tech Stack

- **11ty (Eleventy)** - Static site generator
- **Markdown** - Content format
- **Liquid** - Template language
- **CSS3** - Styling with custom properties
- **Cloudflare Pages** - Hosting and auto-deployment

## License

MIT - Feel free to use this project as a template for other gaming communities!

## Support

Questions or issues? Check out our Discord server or open an issue on GitHub.
