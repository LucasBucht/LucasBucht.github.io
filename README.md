# lucasbucht.github.io
 
Personal portfolio and blog, built with Jekyll, hosted on GitHub Pages.
Software projects and electrical/hardware projects (amp repairs, pedal
builds) both live here, split into their own sections.
 
This README is the single source for running and maintaining the
site. If future-me is wondering how something works, it should be answered
below before digging through files.
 
---
 
## Running the site locally
 
You need Ruby installed (3.3.x — GitHub Pages' build servers use an older
Ruby, and newer versions cause dependency errors). Check what you have:
 
```bash
ruby -v
```
 
One-time setup, from the repo root:
 
```bash
gem install bundler
bundle install
```
 
Every time you want to preview changes before pushing:
 
```bash
bundle exec jekyll serve
```
 
Open `http://localhost:4000`. Leave that terminal running while you edit —
Jekyll rebuilds automatically on file save. `Ctrl+C` to stop it.
 
**If a page looks unchanged after an edit:** hard-refresh the browser
(`Ctrl+F5` / `Ctrl+Shift+R`) on that specific page. Regular refresh can
serve a cached copy. If that doesn't fix it, stop the server (`Ctrl+C`) and
restart `jekyll serve` — it doesn't always pick up changes to `_includes/`
files while running.
 
---
 
## Adding a project
 
Everything lives in **`_data/projects.yml`** — you never touch template
files to add a project. Copy this block and fill it in:
 
```yaml
- name: your-project-name
  category: software          # exactly "software" or "hardware", lowercase
  description: "One plain-language line: what it does, not how it's built."
  tags: [Python, CLI]
  repo: https://github.com/lucasbucht/your-repo
  demo: ""
  image: ""
  writeup: ""
  year: 2026
```
 
Field notes:
 
- **`category`** is required and must be exactly `software` or `hardware`.
  This is what sorts it into the right section on the homepage and
  `/projects/` — miss this field or misspell it and the project silently
  doesn't show up anywhere.
- **`repo`, `demo`, `image`, `writeup`** are all optional. Leave `""` or
  drop the line entirely if it doesn't apply. Hardware builds usually have
  no `repo`, they might have an `image` and/or a `writeup` link instead.
- The homepage shows the 3 most recent per category. `/projects/` shows all
  of them. Both pull from this one file — no separate edit needed.
### Adding a project photo
 
Hardware projects are visual — a fuzz pedal without a picture undersells it.
 
1. Put the image file in `assets/img/` (create the folder if it's not there).
2. Keep it under ~500KB. Resize before uploading if your camera shoots large
   files — full phone-camera resolution is overkill for a web thumbnail.
3. Reference it in the project entry:
```yaml
   image: /assets/img/your-photo.jpg
```
 
---
 
## Writing a blog post
 
Add a new file to `_posts/`, named exactly like this:
 
```
YYYY-MM-DD-a-short-slug.md
```
 
Example: `_posts/2026-08-03-recapping-a-tweed-deluxe.md`
 
Contents:
 
```markdown
---
title: "Your Post Title Here"
---
 
Body goes here, written in normal Markdown. Headings, links, images, and
code blocks all work as expected.
```
 
That's it — it shows up on `/blog/` and the homepage automatically, newest
first. No config, no registering it anywhere else.
 
---
 
## Site structure, if you need to dig deeper
 
```
_config.yml          site title, tagline, author info (edit tagline/links here)
_data/projects.yml    all project entries — the only file for adding projects
_posts/               blog posts, one file per post
_layouts/             page templates (home, page, post, default)
_includes/            reusable pieces (header, footer, project card grid)
assets/css/style.scss the actual design — colors, fonts, spacing
index.html            homepage content (mostly just points at the home layout)
projects.html         /projects/ page
blog.html             /blog/ page
```
 
**Design system, if you want to tweak colors/fonts:** everything is defined
as CSS variables at the top of `assets/css/style.scss` (`--paper`, `--teal`,
`--amber`, `--display`, `--sans`, etc.). Change a value there and it updates
everywhere that uses it, rather than hunting through every section.
 
The small colored dot next to project cards and section headers marks
category — teal for software, amber for hardware. That's driven by the
`category` field in `projects.yml`, not something you set manually per page.
 
---
 
## Deploying (going live)
 
GitHub Pages rebuilds the live site automatically whenever `main` gets a new
push. Nothing else triggers it, not saving, not committing locally, only
`git push` to `main`.
 
```bash
git add -A
git commit -m "Describe what changed"
git push
```
 
Allow 30-90 seconds after pushing before the live site reflects the change.
 
**To test something without risking the live site:** work on a separate
branch, push that branch freely, and only merge into `main` once you're
happy with it.
 
```bash
git checkout -b dev
# make changes, commit, push dev as much as you want
git checkout main
git merge dev
git push origin main
```
 
---
 
## Troubleshooting
 
**`bundle install` says "could not locate Gemfile"** — you're not in the
repo folder. `cd` into it first, confirm with `ls` that `Gemfile` is there.
 
**Gem fails to install, especially `wdm`** — that gem is Windows-file-watch
only and not required. Remove its line from the `Gemfile` if it's blocking
install.
 
**`cannot load such file -- csv` / `logger` / `base64` / `bigdecimal` etc.**
— means Ruby is newer than what this old Jekyll stack expects (this stack
assumes Ruby 3.3.x). Either add the missing gem as its own line in the
`Gemfile` (quick patch, may need to repeat for each one that comes up), or
better, make sure you're actually running Ruby 3.3.x — see below.
 
**Two Ruby versions installed, wrong one keeps running:**
 
```bash
where ruby
where bundle
where gem
```
 
Each should print exactly one path, and all three should point into the
same Ruby install folder. If not, fix your Windows PATH (Environment
Variables → System variables → `Path`) so the 3.3.x folder comes before any
other Ruby folder, then open a **new** terminal window (PATH changes don't
apply to ones already open). If two full Ruby installs are actively
conflicting, uninstalling the unwanted one entirely is more reliable than
just reordering PATH.
 
**Header/nav or footer missing entirely on a page** — check that the layout
file for that page (`_layouts/home.html`, `_layouts/page.html`, or
`_layouts/post.html`) has this front matter at the very top:
 
```yaml
---
layout: default
---
```
 
Without it, that layout renders standalone and never nests inside
`_layouts/default.html`, which is where the header and footer live.
 
**A project isn't showing up on the homepage or `/projects/`** — check its
`category` field in `_data/projects.yml` is present and spelled exactly
`software` or `hardware`.
 
