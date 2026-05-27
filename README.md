# TA AI Labs — GitHub Pages Deploy Guide

This guide walks you through publishing your site for free on GitHub Pages so anyone on the internet can access it — no account required. Custom domain support is included at the end.

---

## What you'll need

- A free [GitHub account](https://github.com/signup) (if you don't have one)
- The files from this folder (`index.html`, `solution-template.html`, and any solution pages you create)

---

## Step 1 — Create a GitHub repository

1. Log in to [github.com](https://github.com)
2. Click the **+** in the top-right corner → **New repository**
3. Name it something like `ta-ai-solutions` (this will appear in your URL)
4. Set visibility to **Public** (required for free GitHub Pages)
5. Click **Create repository**

---

## Step 2 — Upload your files

### Option A — Drag & drop (easiest, no coding needed)

1. Open your new repository on GitHub
2. Click **Add file** → **Upload files**
3. Drag all your HTML files into the window
4. Click **Commit changes**

### Option B — Using Git (if you're comfortable with the terminal)

```bash
git init
git add .
git commit -m "Initial site launch"
git remote add origin https://github.com/YOUR-USERNAME/ta-ai-solutions.git
git push -u origin main
```

---

## Step 3 — Enable GitHub Pages

1. In your repository, click **Settings** (top tab)
2. In the left sidebar, click **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Choose branch: `main` and folder: `/ (root)`
5. Click **Save**

GitHub will display a message:
> "Your site is live at https://YOUR-USERNAME.github.io/ta-ai-solutions/"

It usually takes 1–3 minutes to go live. ✅

---

## Step 4 — Share the link

Your site is now public. The URL will be:

```
https://YOUR-USERNAME.github.io/ta-ai-solutions/
```

Anyone in the world can visit this link — no GitHub account needed.

---

## Adding a custom domain (later)

When you're ready to use a custom domain (e.g. `taailabs.com` or `ai.yourteam.com`):

1. **Buy a domain** — Options: [Namecheap](https://namecheap.com) (~$10–15/yr for .com), [Google Domains](https://domains.google), or [Cloudflare Registrar](https://www.cloudflare.com/products/registrar/) (at cost, no markup)
2. **In your GitHub repo**, create a file called `CNAME` (no extension) containing just your domain:
   ```
   taailabs.com
   ```
3. **In your domain registrar's DNS settings**, add:
   - 4 A records pointing to GitHub's IPs:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - Or a CNAME record: `www` → `YOUR-USERNAME.github.io`
4. Back in **GitHub Settings → Pages**, enter your custom domain and click Save
5. Check **Enforce HTTPS** (free SSL via GitHub + Let's Encrypt)

DNS changes can take up to 24 hours to propagate, but usually go live within an hour.

---

## Updating the site later

Whenever you make changes:

1. Edit your HTML files
2. Go back to **Add file → Upload files** (or use Git)
3. Commit the changes — GitHub Pages automatically redeploys within 1–2 minutes

---

## File structure reference

```
ta-ai-solutions/
├── index.html              ← Main landing page
├── solution-template.html  ← Template (keep as reference, don't link to directly)
├── solution-1.html         ← Tool 1 detail page (copy from template)
├── solution-2.html         ← Tool 2 detail page
├── ...
├── CNAME                   ← Add this only when using a custom domain
└── README.md               ← This file
```

---

## Cost summary

| Item | Cost |
|---|---|
| GitHub account | Free |
| GitHub Pages hosting | Free |
| Custom domain (optional) | ~$10–15 / year |
| SSL certificate | Free (automatic) |

**Total to get live: $0. Total with custom domain: ~$12/year.**

---

Questions? Reach out to Sam at sprieto@degreed.com
