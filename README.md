# lucasbucht.github.io
 
Personal portfolio and blog, built with Jekyll, hosted on GitHub Pages. Below are the steps to update the site or run it locally.


---
 
## Running Locally
Check Ruby Installation (3.3.x):
 
```bash
ruby -v
```
 
Setup from the repo:
 
```bash
gem install bundler
bundle install
```
 
Start local instance:
 
```bash
bundle exec jekyll serve
```
 
Open `http://localhost:4000`. Leave the terminal running while editing. 
Jekyll rebuilds automatically on file save. `Ctrl+C` to stop it.
 
 ---
 
## Templates
 
### Projects
Project metadata lives in **`_data/projects.yml`**. Project template:
 
```yaml
- name: your-project-name
  category: hardware or software
  description: "One line: what it does, not how it's built."
  tags: [tag 1, tag 2]
  repo: 
  demo: ""
  image: ""
  writeup: ""
  year: 2026
```
### Certifications
Certification metadata lives in **`_data/certifications.yml`**. Certification template:

```yaml
- name: "Certification Name"
  issuer: "Issuing Organization"
  date: 2026
  url: ""
```

 
---
 
## Blog Post
 
Add a new file to `_posts/`:
 
```
YYYY-MM-DD-title.md
```
 
Contents:
 
```markdown
---
title: "Post Title"
---
 
Body goes here, written in Markdown. Headings, links, images, and
code blocks all work as expected.
```
 
---
 
## Site Structure
 
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
 
**Design system:** everything is defined
as CSS variables at the top of `assets/css/style.scss` (`--paper`, `--teal`,
`--amber`, `--display`, `--sans`, etc.). Change a value there and it updates
everywhere that uses it, rather than hunting through every section.

 