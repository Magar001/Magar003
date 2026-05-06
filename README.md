# shermagar.com.np

Personal portfolio + football prediction tracker. Single-file static site, no build step.

## Stack
- One `index.html` (HTML + CSS + vanilla JS, ~33 KB)
- Google Fonts (Fraunces + Inter), loaded via CDN
- `localStorage` for the predictions tracker (no backend required)

## Local preview
Open `index.html` in your browser, or run a tiny local server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy on GitHub Pages with custom domain (shermagar.com.np)

### 1. Create the repo
On GitHub, create a new public repo. The simplest approach for a user-site URL is to name it:

```
shermagar.github.io
```

Or any name you like (e.g. `portfolio`) and host it at `shermagar.github.io/portfolio` — but for a custom domain it doesn't matter what you name it.

### 2. Push these files
From the folder where this README lives:

```bash
git init
git add .
git commit -m "Initial portfolio"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### 3. Turn on GitHub Pages
Repo settings → **Pages**:
- Source: **Deploy from a branch**
- Branch: `main` / root
- Save

GitHub will publish at `https://<your-username>.github.io/<repo>` within a minute.

### 4. Point shermagar.com.np at GitHub Pages
In your domain registrar's DNS panel, add these records:

| Type  | Host  | Value                     |
|-------|-------|---------------------------|
| A     | @     | 185.199.108.153           |
| A     | @     | 185.199.109.153           |
| A     | @     | 185.199.110.153           |
| A     | @     | 185.199.111.153           |
| CNAME | www   | <your-username>.github.io |

Then, in repo settings → Pages → **Custom domain**, enter `shermagar.com.np` and tick **Enforce HTTPS** once the cert is issued (takes a few minutes).

The `CNAME` file in this repo already declares the domain — GitHub uses it automatically.

## Adding your photo
Drop a square JPG/PNG named `profile.jpg` into the `assets/` folder. The portrait in the About section auto-uses it; if missing, it falls back to the "SM" initials. Aim for ~600×600 px for a crisp image.

```
assets/
  profile.jpg     ← your photo
  resume.pdf      ← your resume PDF (optional, powers the download button)
```

## Adding your resume PDF
Drop `resume.pdf` into `assets/`. The "Download resume" button on the contact section already links to `assets/resume.pdf`.

## Updating predictions
The tracker on `#predictions` reads/writes to your browser's `localStorage`. Picks you submit on your laptop won't be visible to other visitors — they each see the seeded sample picks until they add their own.

If you want a *shared* tracker so visitors see your latest picks too, swap the `localStorage` block in `index.html` for a tiny backend (Supabase, Firebase, or a Cloudflare Worker + KV). Happy to help with that next.

## Editing tips
- Hero copy: edit the `<header class="hero">` block.
- Work history: each `<div class="job">` inside `#work`.
- Featured matches: the soccer/Nepal `featured-card` blocks inside `#predictions`.
- Color palette: the CSS variables at the top of `<style>` (`--accent`, `--accent-2`, `--good`, `--cool`).
- Hidden treat: try the Konami code anywhere on the page.
