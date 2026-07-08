# Update: EE-focused redesign

You've already got real content in your live repo, so don't just overwrite
everything blindly. Here's exactly what changed:

## Safe to fully overwrite (no personalization risk)

These are templates/styles, not content — replace them wholesale:

- `assets/css/style.scss`
- `_includes/header.html`
- `_includes/project-grid.html`
- `_layouts/default.html`
- `_layouts/home.html`
- `_layouts/post.html`
- `projects.html`

## Needs manual merge (you've probably edited these)

**`_data/projects.yml`** — every entry now needs a `category: software` or
`category: hardware` line, or it won't show up on the homepage or /projects/
sections. Take your real project entries and add that one field to each.
New optional fields, add only where useful:
- `image` — path to a photo (hardware builds especially benefit — a fuzz
  pedal without a picture is a hard sell)
- `writeup` — link to a blog post about the build, if `repo` doesn't apply

`repo` and `demo` are now optional — leave `""` if a hardware project doesn't
have one.

**`_config.yml`** — only the `tagline` line changed. Update yours to mention
both sides of what you do, or leave your own wording.

## What got removed

- The `$ whoami` terminal eyebrow — gone.
- The blinking-cursor logo — gone, now a plain wordmark.
- The diff-hunk-header dividers (`@@ ... @@`) — replaced with a plain
  labeled rule that uses the same teal/amber dot system as the project
  cards, so software vs. hardware is visually consistent everywhere.

## Adding photos

Drop image files into `assets/img/` (create the folder), then reference them
in `projects.yml` as `image: /assets/img/your-photo.jpg`. Keep them under
~500KB each so the page loads fast — resize before uploading if your camera
shoots large files.
