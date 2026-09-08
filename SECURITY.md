# Security Policy

This repository builds [lucasbucht.github.io](https://lucasbucht.github.io), a
static personal portfolio and blog. There's no backend, no database, no user
accounts, and no form that submits data anywhere — content is Markdown/YAML
compiled by Jekyll into static HTML, served directly by GitHub Pages.

## Scope

Given the above, most traditional web vulnerability classes (SQL injection,
auth bypass, session hijacking, etc.) don't apply here — there's no server-side
logic or data store to attack. Realistic areas of concern are limited to:

- **Dependency vulnerabilities** in the Ruby gems this site builds with
  (`Gemfile` / `Gemfile.lock`) — for example a `jekyll` or plugin version with
  a known CVE.
- **Client-side JavaScript issues** — this site includes a small vanilla JS
  tag filter on the `/projects/` page, and no other custom scripts. Any XSS
  or injection risk would have to come from there.
- **Exposed secrets** — API keys, tokens, or credentials accidentally
  committed to the repo. There shouldn't be any, since the site has no API
  integrations, but flag it if you spot one.

There is no supported-version table because there's only ever one live
version: whatever is currently deployed from `main`.

## Reporting a Vulnerability

If you find something in scope above, please open a
[GitHub issue](https://github.com/LucasBucht/LucasBucht.github.io/issues) on
this repo, or reach out directly via the email listed on
[the site itself](https://lucasbucht.github.io).

This is a personal project maintained by one person (me), so response time
is best-effort rather than guaranteed, but I'll take a look and patch
promptly if it's a real issue. There's no bug bounty, just my thanks.
