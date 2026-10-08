# Praneeth Labs

Umbrella site for praneethlabs.com — a small static site on Cloudflare Pages.

## Files

Everything that's served lives in **`public/`**; nothing outside it is uploaded.

- `index.html` — home page (product list)
- `about.html`, `contact.html`, `privacy.html`, `terms.html` — served at
  `/about`, `/contact`, `/privacy`, `/terms` (Pages strips `.html`)
- `404.html` — returned with a real 404 status for unknown paths (without it,
  Pages serves the home page for every URL)
- `site.css` — shared styles for every page
- `ads.txt`, `robots.txt`, `sitemap.xml`, `favicon.svg`
- `_redirects` — blocks a few sensitive paths outright

Every page carries the `google-adsense-account` meta tag; AdSense reviews this
root domain for all `*.praneethlabs.com` products.

## Deploy

The Pages project `praneethlabs-clean` (serves praneethlabs.com and
www.praneethlabs.com) is a direct upload, not git-connected:

```bash
npx --yes wrangler@latest pages deploy public --project-name praneethlabs-clean --branch main --commit-dirty=true
```

Note: a zone-level redirect rule in the Cloudflare dashboard currently sends
`/ads.txt` to `paperfinder.praneethlabs.com/ads.txt` (same publisher line), so
`public/ads.txt` is only served if that rule is removed.
