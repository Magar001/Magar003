# How to update shermagar.com.np — newbie walkthrough

Your repo: **https://github.com/Magar001/Magar003**
Your live site: **https://shermagar.com.np**
DNS provider: **Cloudflare** (already correctly pointing at GitHub Pages — don't touch it)

You're going to swap the contents of the `Magar003` repo with this new site. Your domain keeps working. **No DNS changes needed.**

Two ways to do this:

- **Option 1 — GitHub Desktop (easiest, click-only).** Recommended.
- **Option 2 — Command line.** For the brave.

Pick whichever feels less scary. Result is identical.

---

# Before you start: a quick reality check

## "I see 'There are no verified domains' on GitHub — should I be worried?"

**No.** That message lives on a different page (account settings) than the page that controls your site. It's an optional security feature for organizations. Your site has been working without it for 5 years; ignore it for now.

## "How do I check my site's actual status?"

Open this URL in your browser (sign in to GitHub first):

**https://github.com/Magar001/Magar003/settings/pages**

You should see a green box at the top that says **"Your site is live at https://shermagar.com.np"**. If you do, you're golden — just push the new code.

If you see a yellow or red box, it'll tell you what's wrong. The most common message after 5 years is "Custom domain — DNS check failed." Usually that just means GitHub re-checked and didn't like something temporarily; it self-resolves within minutes.

## "Where does Cloudflare fit in?"

Cloudflare is your DNS provider — it tells the internet that `shermagar.com.np` lives at GitHub's servers. **It's already configured.** You don't need to touch Cloudflare to update the site's content. Skip to Option 1 below.

(If you're curious or something later breaks: see the **Cloudflare reference** at the bottom.)

---

# OPTION 1 — GitHub Desktop (click-only)

## Step 1. Install GitHub Desktop (skip if you already have it)

1. Go to https://desktop.github.com
2. Click the big purple **Download for macOS** button.
3. Open the `.zip`, drag **GitHub Desktop.app** into your **Applications** folder.
4. Open GitHub Desktop from Applications.
5. Sign in with the same GitHub account that owns `Magar001/Magar003`.
6. When asked about Git config: **Use my GitHub account name and email** → **Finish**.

## Step 2. Clone your repo

1. In GitHub Desktop: **File** menu → **Clone repository…**
2. Click the **GitHub.com** tab.
3. You'll see your repos. Click **Magar001/Magar003** (or type "Magar003" in the filter box).
4. **Local path:** click **Choose…** and pick where to save it. Desktop is fine — e.g. `~/Desktop`.
5. Click **Clone**.

GitHub Desktop downloads everything. When it finishes, click **Show in Finder** to see the folder it created (called `Magar003`).

## Step 3. Wipe the old site files

1. In Finder, open the `Magar003` folder.
2. **Critical:** there's a hidden folder called `.git` you must NOT delete. Press **⌘ + Shift + .** to show hidden folders if you can't see it.
3. Select everything *except* `.git` and move it to Trash.

> If you accidentally delete `.git`, the folder loses its connection to GitHub. Easy fix: delete the whole `Magar003` folder and re-clone (Step 2).

## Step 4. Drop in the new site

1. Open this `shermagar-portfolio/` folder (the one I sent you).
2. Select **everything inside it** — `index.html`, the `assets/` folder, `CNAME`, `.nojekyll`, `.gitignore`, `README.md`, `UPLOAD.md`.
3. Drag everything into your `Magar003` folder.

> ⚠️ Copy the **contents** of `shermagar-portfolio/`, not the folder itself. After this step, opening `Magar003/` should show `index.html` directly inside it — NOT `Magar003/shermagar-portfolio/index.html`. If you see the nested folder, drag the contents up one level.

## Step 5. Commit & push using GitHub Desktop

1. Switch back to GitHub Desktop. The left panel now shows a long list of changes — added files in green, deleted files in red. That's exactly right.
2. At the bottom-left, in the **Summary** text box, type something like:
   ```
   Modernize site with portfolio + predictions tracker
   ```
3. Click the blue **Commit to main** button at the bottom.
   (If your branch is `master` instead of `main`, the button says **Commit to master** — same thing, just click it.)
4. After committing, the top of the window shows a big **Push origin** button. Click it.

Done. GitHub Desktop sends everything to GitHub.

## Step 6. Verify it's live

1. Wait about 60 seconds.
2. Open https://shermagar.com.np in your browser.
3. **Hard refresh** to skip the cache: **⌘ + Shift + R** on Mac.
4. You should see the new design — dire wolf favicon in the tab, your photo in the About section, predictions tab on scroll.

If the old site is still showing 5 minutes later:
- Go to **https://github.com/Magar001/Magar003/actions** → click the latest run. If it has a green checkmark, the site is deployed and your browser is just caching aggressively. Try an incognito/private window.
- If the run failed (red X), click into it and the error message tells you what broke.

---

# OPTION 2 — Command line (for the brave)

## Step 1. Make sure git is installed

Open Terminal (**⌘ + Space**, type "Terminal", hit Enter). Run:
```bash
git --version
```
If you see a version number, you're set. Otherwise:
```bash
xcode-select --install
```
Click through the popup — it installs git as part of Apple's command line tools.

## Step 2. Clone your repo

```bash
cd ~/Desktop
git clone https://github.com/Magar001/Magar003.git
cd Magar003
```

## Step 3. Wipe old files (keeps git history)

```bash
git rm -rf .
git clean -fdx
```
This removes every tracked file but keeps the hidden `.git` folder so the repo stays wired to GitHub.

## Step 4. Copy in the new files

```bash
# Adjust ~/Downloads/shermagar-portfolio if you unzipped somewhere else
cp -R ~/Downloads/shermagar-portfolio/. .
```
The `/.` at the end is intentional — it copies the **contents**, not the folder.

Verify:
```bash
ls -la
# you should see index.html, assets/, CNAME, .nojekyll, README.md, UPLOAD.md, etc.
```

## Step 5. Commit & push

```bash
git add .
git commit -m "Modernize site with portfolio + predictions tracker"
git push origin main
```

(If your default branch is `master`, use `git push origin master`.)

If git asks for a password and rejects it: GitHub no longer accepts passwords (since 2021). You either need a Personal Access Token, or — easier — switch to Option 1 (GitHub Desktop handles auth automatically).

## Step 6. Verify

Same as Option 1, Step 6.

---

# After-deploy checklist

Open https://shermagar.com.np in a fresh tab and check:

- [ ] Browser tab icon is the dire wolf
- [ ] About section shows your photo (not "SM" initials)
- [ ] Predictions section shows the canyon "Off the clock" photo
- [ ] LinkedIn link in Contact opens your profile
- [ ] Click the dark/light toggle in the nav — flips the theme
- [ ] Predictions Lab → switch tabs between **Soccer · World Cup** and **Nepal Sport**
- [ ] Add a test pick in the form, refresh page, pick is still there
- [ ] On your phone, save the page to home screen — icon should be the dire wolf

---

# Troubleshooting

**"It still shows my old site after pushing."**
GitHub Pages caches aggressively. Hard refresh (`⌘ + Shift + R`) once or twice. Try an incognito/private window. If still stuck after 10 minutes, check **https://github.com/Magar001/Magar003/actions** for a failed deploy.

**"My custom domain disconnected and now I see a 404 from GitHub."**
Go to https://github.com/Magar001/Magar003/settings/pages → re-type `shermagar.com.np` in the **Custom domain** box → click **Save**. The `CNAME` file in the new repo should prevent this, but sometimes GitHub forgets after a wipe.

**"GitHub Desktop says 'Authentication failed'."**
Sign out and back in: GitHub Desktop menu (top left) → **Settings** → **Accounts** → **Sign out** → **Sign in to GitHub.com** → follow the browser flow.

**"After pushing, the site loads but has no styling — it's all unstyled HTML."**
That means the assets folder didn't push. Check that `assets/profile.jpg`, `assets/sport.jpg`, and the favicon files are in the repo on github.com (browse to the `assets/` folder there). If they're missing, drag them in via GitHub Desktop and push again.

**"I see this `.nojekyll` file and a `CNAME` file with no extension. Are they broken?"**
Both are intentional. `.nojekyll` (with the leading dot) tells GitHub Pages not to run Jekyll on the site. `CNAME` (no extension) tells GitHub which domain to serve — it's already set to `shermagar.com.np` for you.

---

# Cloudflare reference (only if something breaks)

You don't need to touch Cloudflare to update the site's content. This section is for if/when DNS itself breaks.

## Sign in
https://dash.cloudflare.com → pick the `shermagar.com.np` zone → **DNS** in the left sidebar.

## Records that should be there
Either of these setups works for GitHub Pages:

**Setup A — Four A records on root:**

| Type  | Name | Content              | Proxy status      |
|-------|------|----------------------|-------------------|
| A     | @    | 185.199.108.153      | DNS only (gray)   |
| A     | @    | 185.199.109.153      | DNS only (gray)   |
| A     | @    | 185.199.110.153      | DNS only (gray)   |
| A     | @    | 185.199.111.153      | DNS only (gray)   |
| CNAME | www  | magar001.github.io   | DNS only (gray)   |

**Setup B — CNAME flattening (Cloudflare-only feature):**

| Type  | Name | Content              | Proxy status      |
|-------|------|----------------------|-------------------|
| CNAME | @    | magar001.github.io   | DNS only (gray)   |
| CNAME | www  | magar001.github.io   | DNS only (gray)   |

## Cloudflare-specific gotchas

- **Proxy status (orange vs. gray cloud).** If you click the cloud icon to orange (proxy on), Cloudflare sits in front of your site. This can break GitHub's auto-issued SSL cert on first setup. Recommendation: leave it **gray (DNS only)**. Your site already works gray; switching to orange has minor caching benefits but isn't worth the headache.
- **SSL/TLS mode.** Cloudflare dashboard → **SSL/TLS** → set the mode to **Full** (NOT "Flexible"). Flexible causes redirect loops with GitHub Pages.
- **Page Rules / "Always Use HTTPS".** Safe to leave on. Cloudflare → **Rules** → **Page Rules**.
- **If shermagar.com.np stops resolving entirely:** check that the zone's nameservers (Cloudflare → Overview → bottom right) are still set on your domain registrar. Domain registrars for `.com.np` can periodically reset NS records during renewal.

## "Should I 'verify' my domain on GitHub?"

Optional. It's a security feature: only verified accounts can publish a Pages site at `shermagar.com.np`. Without verification, in theory someone else could fork your repo and try to claim your domain — but they'd need to also control DNS, which they don't, so the practical risk is near zero.

If you want to do it anyway:
1. Go to https://github.com/settings/pages → **Verified domains** → **Add a domain** → enter `shermagar.com.np`.
2. GitHub gives you a `TXT` record. Add it in Cloudflare DNS (Type: TXT, Name: the string GitHub gave, Content: the value, Proxy: gray).
3. Back on GitHub, click **Verify**. Done.

You can do this any time — doesn't have to be now.

---

# Optional polish after the site is live

- **Add your resume PDF.** Drop a `resume.pdf` into the `assets/` folder, commit, push. The "Download resume" button on the Contact section already links to `assets/resume.pdf`.
- **Swap photos later.** Replace `assets/profile.jpg` (square) or `assets/sport.jpg` (4:3 landscape) with new files. Same names, commit + push, live in a minute.
- **Edit copy.** Open `index.html` in TextEdit / VS Code / Sublime. Find the text, change it, save. In GitHub Desktop, type a commit message and push. No build step.
