# Tides — deploy via git + Vercel

This folder is a ready-to-deploy static PWA. No build step, no framework —
Vercel just needs to serve these files as-is.

## 1. Push it to GitHub

```bash
cd tides-app
git init
git add .
git commit -m "Tides app"
git branch -M main
git remote add origin https://github.com/<your-username>/tides-app.git
git push -u origin main
```

(Create the empty repo on GitHub first, or use `gh repo create tides-app --public --source=. --push` if you have the GitHub CLI.)

## 2. Import into Vercel

- Go to vercel.com/new, pick the `tides-app` repo.
- Framework preset: **Other** (it's plain HTML/CSS/JS — no build command needed).
- Deploy.

You'll get a `tides-app.vercel.app` URL (or attach your own domain in the
Vercel dashboard afterward).

## 3. Install it as an app

Open the Vercel URL on her phone:
- **Android/Chrome**: menu → "Install app" (or a prompt appears automatically).
- **iOS/Safari**: Share button → "Add to Home Screen".

It'll open full-screen with its own icon, no browser bar — because of
`manifest.json` (`display: standalone`) and `sw.js` (makes it installable
and lets the shell load offline).

## Notes

- Data is stored in the browser's own storage on whichever device opens it
  (see the shim at the top of `index.html`). It's per-device, not synced —
  fine for one phone, not for two people sharing progress. Say the word if
  you want real sync later (Supabase would be the natural next step, and
  you're already set up there).
- Bump `CACHE` in `sw.js` (e.g. `tides-v2`) whenever you push a real update,
  so installed devices don't keep serving the old cached version.
