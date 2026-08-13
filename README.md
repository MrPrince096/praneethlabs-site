# Praneeth Labs

Umbrella landing page for praneethlabs.com. Static single-page site — deploys to Cloudflare Pages.

## ⚠️ Deploy config — action needed

The site's HTML lives in **`public/`**. In the Cloudflare Pages project's
**Settings → Builds & deployments → Build output directory**, set this to
`public` (it was previously the repo root).

This isn't cosmetic: with the output directory left at the repo root,
Cloudflare Pages was serving the entire checkout as static files — including
`.git/` itself. That meant `https://praneethlabs.com/.git/config` and
`/.git/HEAD` were both publicly readable (confirmed live, 2026-08-13),
exposing the repo's structure and history to anyone who checked. A
`_redirects` rule now blocks `.git/*` and a few other sensitive paths as an
immediate mitigation either way, but **switching the output directory to
`public` is the actual fix** — once that's set, nothing outside `public/`
(the repo's `.git`, this README, anything added later) is reachable at all.

## Files

- `public/index.html` — the actual served page
- `public/_redirects` — Cloudflare Pages redirect/block rules
- `index.html`, `_redirects` (repo root) — kept as a fallback only until the
  output directory setting above is switched; safe to delete afterward
