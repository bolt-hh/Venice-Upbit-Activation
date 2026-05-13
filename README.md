# Venice × Korea — Community Activation

Community activation tool for the Venice Korea launch. Users submit proof of $VVV purchase on Upbit and Venice.ai sign-up to enter the prize pool.

## Deploy to Vercel

### Option 1 — Drag & drop (~30 seconds)
1. Zip this folder
2. Go to https://vercel.com/new
3. Drag the zip onto the page
4. Click **Deploy**

### Option 2 — GitHub + Vercel (recommended)
```bash
git init
git add .
git commit -m "venice korea activation"
git remote add origin <your-repo-url>
git push -u origin main
```
Then on https://vercel.com/new → Import Git Repository → select repo → Deploy.
Any future `git push` auto-deploys.

### Option 3 — Vercel CLI
```bash
npm i -g vercel
vercel
vercel --prod
```

## Custom domain
Vercel dashboard → Project → Settings → Domains → add your domain.

## File structure
```
deploy/
├── index.html          ← full activation page (single-file app)
├── tweaks-panel.jsx    ← React tweaks panel component
├── assets/
│   ├── venice-keys-red.svg   ← Venice keys logo
│   └── hh-logo.jpg           ← Holo Hive logo
└── vercel.json         ← routing + caching headers
```

## Before going live — checklist
- [ ] Update `SUPABASE_URL` and keys in `index.html` (search `BACKEND CREDENTIALS`)
- [ ] Update `R2_UPLOAD_ENDPOINT` and `R2_PUBLIC_BASE_URL` with your Venice R2 worker
- [ ] Update `ADMIN_PASSWORD_HASH` — generate via: `echo -n "yourpassword" | sha256sum`
- [ ] Set deadline in Supabase `app_settings` table: `key = deadline`, `value = ISO timestamp`
- [ ] Set `accepting_entries = true` in `app_settings`
- [ ] Add KOL handles via the Admin Panel at `yoursite.com/#admin`
- [ ] Confirm hashtag / campaign copy in hero section
- [ ] Add `og:image` and favicon (optional)

## Supabase schema note
The app currently maps:
- `upbit_proof_url` → `screenshot_url` column
- `venice_proof_url` → `frame_used` column

To use proper column names, add `upbit_proof_url` and `venice_proof_url` columns to your `entries` table and update the JSON body in `submitEntry()` in `index.html`.

## Admin panel
Access at `yoursite.com/#admin` — password-protected.

Features:
- **Dashboard** — live entry count, KOL breakdown, 7-day chart, deadline editor
- **Entries** — full table, CSV export, screenshot ZIP download, bulk delete
- **KOL list** — add / remove KOL handles
- **Link clicks** — ecosystem link analytics
- **Winners** — random selection (100 × $10 stable + 5 × $100 $VVV), CSV export

## Tweaks panel
Click the **Tweaks** button in the toolbar to toggle the design panel.
Controls: particle density, size, speed, color, glow, bg grid, radial glow.

---
Powered by **Venice** × **Holo Hive**
