# Publishing sbrt.in via GitHub Pages — click-by-click

Your website is fully static, so GitHub Pages hosts it free, forever, with HTTPS.
This guide assumes zero coding: every step is a click or a copy-paste.
Total time: ~15 minutes now, ~1 minute per future update.

Everything you upload lives in the folder **`sbrt-github/`** (also zipped as
`SBRT-github-repo.zip`). It contains 14 self-contained pages + sitemap + robots
+ `.nojekyll` + README. Nothing else is needed — no build, no server.

---

## Part 1 — Create the repository and upload (web method, no git)

1. Go to https://github.com and sign in.
2. Top-right **"+"** → **New repository**.
   - Name: `sbrt-website` · Public · **do not** tick README/gitignore/licence → **Create repository**.
3. On the empty repository page click **“uploading an existing file”**.
4. Open your `sbrt-github/` folder, select **all files inside it** (Ctrl+A), drag them
   onto the upload box. Wait for the green ticks (≈3 MB, fast).
5. Commit message: `SBRT website v1` → **Commit changes**.

## Part 2 — Switch on GitHub Pages

6. Repository → **Settings** (top row) → left sidebar **Pages**.
7. *Build and deployment*: Source = **Deploy from a branch**; Branch = **main** and folder **/(root)** → **Save**.
8. Wait ~1 minute, refresh: your temporary address appears at the top —
   `https://<your-username>.github.io/sbrt-website/` — open it. The site is live there already.

## Part 3 — Point sbrt.in at it (BigRock)

9. Still in Settings → Pages: in **Custom domain** type `sbrt.in` → **Save**.
   (GitHub adds a `CNAME` file to the repo automatically.)
10. New tab: log in at https://www.bigrock.in → **Domains** → click **sbrt.in** → **Manage DNS / DNS Management**.
11. Edit/create these records (delete any old A or CNAME records left by Google Sites;
    **never touch MX or mail records**):

    | Type | Host | Value |
    |---|---|---|
    | A | `@` | `185.199.108.153` |
    | A | `@` | `185.199.109.153` |
    | A | `@` | `185.199.110.153` |
    | A | `@` | `185.199.111.153` |
    | CNAME | `www` | `<your-username>.github.io` |

12. Back in GitHub Pages settings: the DNS check turns green within minutes–24 h
    (track it at https://dnschecker.org, type `sbrt.in`). Then tick **Enforce HTTPS** —
    the free certificate appears by itself a minute or two later.
13. Test all four: `sbrt.in`, `www.sbrt.in`, and the `https://` versions. Done — you are live.

*Until DNS propagates, visitors still see the old Google Sites page; nothing breaks.*

## Part 4 — Updating the site later (two ways)

**Way A — no git (recommended for you):**
edit a page in your folder (see EDITING-GUIDE), then repository → **Add file →
Upload files**, drag the changed file(s), commit. Live in ~1 minute.

**Way B — git, copy-paste (once you feel brave):**
One-time setup (Git for Windows installed, terminal open inside `sbrt-github/`):
```
git init
git add .
git commit -m "SBRT website v1"
git branch -M main
git remote add origin https://github.com/<your-username>/sbrt-website.git
git push -u origin main
```
Every later update:
```
git add .
git commit -m "what I changed"
git push
```

## Part 5 — Why this is a good idea (and one optional upgrade)

- **Backup + history:** every commit is a restore point; delete-proof.
- **Free HTTPS, free hosting, no renewals** (BigRock domain renewal stays as before).
- **404 page works** (`404.html` is honoured by Pages).
- Optional upgrade later: Netlify → *Import from Git* → pick this repo → every
  `git push` then also deploys to Netlify automatically, if you ever want its extras.

## If something looks wrong

| Symptom | Fix |
|---|---|
| `404` at the github.io address | Pages branch not saved — redo step 7; wait 1 min. |
| Custom domain shows “DNS check failed” | Records not propagated yet, or a typo in the four A IPs / CNAME. Re-check step 11. |
| Site loads without style | You uploaded a folder-inside-folder (e.g. `sbrt-github/index.html` instead of `index.html` at repo root). Move files to root. |
| HTTPS box greyed out | DNS not green yet; wait, then refresh the Pages settings. |
