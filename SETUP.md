# Setup guide

## 1. Merge into your existing repo

You already have `lucasbucht.github.io` with a README, LICENSE, and `_config.yml`.
Don't clone this as a new repo — copy these files into your existing one instead:

```bash
cd path/to/lucasbucht.github.io
# copy every file from this bundle into the repo root, overwriting the
# existing _config.yml (it's just the GitHub default, safe to replace)
git add -A
git commit -m "Set up Jekyll portfolio + blog"
git push
```

GitHub Pages will pick it up automatically. Give it 1-2 minutes, then check
`https://lucasbucht.github.io`.

## 2. What to edit before you call it done

- **`_config.yml`** — set `author.linkedin` and `author.email` (leave `""` to hide
  that footer link entirely).
- **`_layouts/home.html`** — replace the placeholder bio paragraph with 2-3 real
  sentences about what you build and what you're looking for.
- **`_data/projects.yml`** — replace the 4 placeholder entries with your real
  projects. This is the only file you touch to add/remove/reorder projects —
  the homepage and `/projects/` page both read from it automatically.
- **`_posts/2026-07-08-hello-world.md`** — delete or replace with a real first
  post.

## 3. Writing new blog posts

Add a file to `_posts/` named `YYYY-MM-DD-slug.md`:

```markdown
---
title: "Your title here"
---

Body in Markdown. Code blocks, images, links all work normally.
```

That's it — it shows up on `/blog/` and the homepage automatically, sorted by date.

## 4. Testing locally before you push (optional but recommended)

Requires Ruby. One-time setup:

```bash
gem install bundler
bundle install
```

Then, every time you want to preview:

```bash
bundle exec jekyll serve
```

Open `http://localhost:4000`. Ctrl+C to stop.

If you don't want to install Ruby locally, you can skip this and just push —
GitHub Pages builds it for you, you'll just see changes live instead of in
preview.

## 5. Custom domain (optional, later)

If you ever want `lucasbucht.dev` instead of the `.github.io` URL, add a
`CNAME` file with just the domain in it, and point your domain's DNS at
GitHub Pages. Not needed now — just flagging it's a later, easy upgrade.
