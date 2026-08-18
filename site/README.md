# Magic Sun — site source

A Hugo site with three sections: **Bio** (home), **Articles**, and **Contact**.
Free to host on GitHub Pages.

## Structure

```
content/
  _index.md          → Bio (home) page text
  articles/
    _index.md         → Articles page (usually leave empty)
    welcome.md         → sample article — edit or delete
  contact.md           → Contact page text
layouts/                → templates (design lives here + static/css/style.css)
hugo.toml               → site title, tagline, email, nav
```

## Writing a new article (text only)

Create a new file in `content/articles/`, e.g. `content/articles/my-second-post.md`:

```markdown
---
title: "My Second Post"
date: 2026-09-01
summary: "One sentence that shows up in the article list."
---

Your writing goes here, in Markdown.
```

That's it — it'll automatically appear on the Articles page, newest first.

## Writing a new article with photos

For posts that mix images and text, make a **folder** instead of a single file —
this keeps the article's photos bundled together with its text. `content/articles/welcome/`
is a working example of this pattern.

1. Create a new folder: `content/articles/my-second-post/`
2. Inside it, create `index.md` with the same front matter as above
3. Drop your image files into that same folder (e.g. `photo1.jpg`, `photo2.jpg`)
4. Reference them anywhere in your text like this:
   ```markdown
   ![Caption shown under the photo](photo1.jpg)
   ```
5. Push the whole folder to GitHub — text and photos publish together automatically

Images are automatically styled with a thin border and the caption text (from the
`[...]` part) shown underneath, matching the rest of the site.

**Tip:** keep photos under ~1–2MB each (resize/export at a reasonable size before
adding them) so pages stay fast to load — this matters for both readers and search
ranking.

## Running locally (optional, to preview before publishing)

1. Install Hugo (extended version): https://gohugo.io/installation/
2. From this folder, run:
   ```
   hugo server
   ```
3. Open http://localhost:1313

## Publishing for free on GitHub Pages

1. Create a new **public** GitHub repository (e.g. `magic-sun-site`).
2. Push this folder's contents to the `main` branch of that repo.
3. In the repo, go to **Settings → Pages**, and under "Build and deployment" set
   **Source** to **GitHub Actions**. (The workflow file in `.github/workflows/hugo.yml`
   is already set up to build and deploy automatically on every push to `main`.)
4. Push a commit (or re-run the workflow from the Actions tab) — after ~1 minute
   your site will be live at `https://<your-username>.github.io/<repo-name>/`.

### Using your own custom domain

1. Buy a domain (e.g. from Namecheap, Cloudflare, or Google Domains) — this is the
   only part of this setup that typically costs money, usually $10–15/year.
2. In the repo, go to **Settings → Pages → Custom domain**, enter your domain,
   and save. GitHub will create a `CNAME` file automatically.
3. At your domain registrar, add the DNS records GitHub shows you (an `A` record
   set for the apex domain, or a `CNAME` record if using a subdomain like `www`).
4. Once DNS propagates (can take a few minutes to a few hours), update
   `baseURL` in `hugo.toml` to your real domain and push again.

## Editing the design

All visual styling lives in one file: `static/css/style.css`. Colors and fonts
are defined as CSS variables at the top of that file, so you can retheme the
whole site by editing the `:root` block.
