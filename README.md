# Team Availability — Global Coverage View

An interactive, single-file web app for visualizing team availability across global time zones. Built for async-first teams that need to understand who's online when.

![Status](https://img.shields.io/badge/status-ready-brightgreen)
![Dependencies](https://img.shields.io/badge/dependencies-none-blue)
![License](https://img.shields.io/badge/license-MIT-yellow)

## What It Does

- **24-hour heatmap** showing each team member's availability (Available / Limited / Asleep)
- **Timezone shifting** — view the entire board in any timezone so everyone sees hours in their local time
- **Aggregate coverage bar** — instantly see how many people are online at each hour
- **Per-person editing** — click any name to customize their schedule hour-by-hour with click/drag painting
- **Add/remove members** and sort by name, timezone, or total availability
- **Hover tooltips** with person details, status, and their local time

## Quick Start

No build step, no dependencies, no server required. It's a single HTML file.

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/team-availability.git

# Open it
open index.html
# or just double-click index.html in your file manager
```

## Hosting Options

### GitHub Pages (recommended for sharing)

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Set source to **Deploy from a branch**, select `main`, root `/`
4. Your team can access it at `https://YOUR_USERNAME.github.io/team-availability/`

### Other options

- **Internal file share** — drop `index.html` on a shared drive; anyone can open it locally
- **Any static host** — Netlify, Vercel, Cloudflare Pages, S3, etc. Just deploy `index.html`
- **Email it** — it's one file, fully self-contained

## Customizing Your Team

Open `index.html` and find the `people` array near the top of the `<script>` block. Each person looks like this:

```javascript
{ name: 'Sarah Chen', tz: 8, hours: makeSchedule(9, 18, 1, 1) }
```

- **`name`** — display name
- **`tz`** — UTC offset (e.g., `-6` for Central, `5.5` for India, `0` for London)
- **`makeSchedule(workStart, workEnd, limitedBefore, limitedAfter)`** — helper that generates a 24-hour array:
  - `workStart` / `workEnd` — core working hours in their local time
  - `limitedBefore` / `limitedAfter` — hours of "limited" availability on either side

For more granular control, you can provide a raw 24-element array:

```javascript
{
  name: 'Kenji Watanabe',
  tz: 9,
  hours: ['s','s','s','s','s','s','s','s','l','a','a','a','s','s','a','a','a','a','l','s','s','s','s','s']
  //       0a  1a  2a  3a  4a  5a  6a  7a  8a  9a 10a 11a 12p  1p  2p  3p  4p  5p  6p  7p  8p  9p 10p 11p
}
```

Values: `'a'` = available, `'l'` = limited, `'s'` = asleep/off

Or just use the built-in editor — click any person's name in the UI to paint their schedule visually.

## Data Persistence

**Current behavior:** The app holds data in memory. Edits made in the browser are lost on refresh. This is intentional — it keeps the app zero-dependency and easy to share.

**If you need persistence**, a few options:
- Edit the `people` array in the source file directly and commit changes
- Fork and add `localStorage` support (a few lines of JS)
- Connect to a backend/database for multi-user editing

## Browser Support

Modern browsers (Chrome, Firefox, Safari, Edge). No IE support.

## License

MIT — use it however you want.
