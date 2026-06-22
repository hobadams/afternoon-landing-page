# Afternoon Studio — Landing Page

A single-page, zero-build static landing page for **Afternoon Studio**. It stands in
place of the (paused) `afternoonstudio.co.uk` Shopify store: a logo, tagline, a button
through to the live collection on Pepper You, and an Instagram link.

Products are still shopped at:
<https://pepperyou.co.uk/collections/brand-afternoon-studio>

## Structure

```
.
├── index.html          # markup + all SEO meta + JSON-LD
├── styles.css          # warm, nature-inspired styling
├── robots.txt
├── sitemap.xml
├── CNAME               # custom domain for GitHub Pages (afternoonstudio.co.uk)
├── .nojekyll           # serve files as-is on GitHub Pages
└── assets/
    ├── logo.svg            # "Afternoon" wordmark (inline-tinted to the ink colour)
    ├── favicon.svg
    ├── favicon-96x96.png
    ├── apple-touch-icon.png
    ├── instagram.svg
    └── og-image.jpg        # social share image (559×559)
```

No framework, no build step — just static files.

## Local preview

Any static file server works, e.g.:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploying to GitHub Pages (free)

1. Create a GitHub repo and push this folder.
2. In **Settings → Pages**, set **Source = Deploy from a branch**, branch `main`, folder `/ (root)`.
3. GitHub serves the site at `https://<user>.github.io/<repo>/`.

### Custom domain (`afternoonstudio.co.uk`)

The `CNAME` file is already set to `afternoonstudio.co.uk`. To use it:

1. In **Settings → Pages → Custom domain**, confirm `afternoonstudio.co.uk`.
2. At your DNS provider, point the apex domain at GitHub Pages:
   - `A` records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - (and a `CNAME` for `www` → `<user>.github.io`)
3. Enable **Enforce HTTPS** once the certificate is issued.

> If you host somewhere other than this custom domain (e.g. a `*.github.io` URL or
> another host), **delete the `CNAME` file** and update the absolute URLs noted below.

## Regenerating the OG image

`assets/og-image.jpg` (1200×630) is rendered from `scripts/og-template.html`:

1. Serve the project root: `python3 -m http.server 8000`
2. Open `http://localhost:8000/scripts/og-template.html` at a 1200×630 viewport and
   screenshot it (or use a headless browser to capture a 1200×630 clip).
3. Save/export as `assets/og-image.jpg`.

Edit the tagline/wording in `scripts/og-template.html` and re-capture to update it.

## SEO notes

- Absolute URLs (canonical, Open Graph, Twitter, JSON-LD) are hard-coded to
  `https://afternoonstudio.co.uk/`. If the production domain changes, find/replace that
  base URL across `index.html`, `robots.txt`, and `sitemap.xml`.
- Structured data uses two JSON-LD blocks:
  - an **Organization** describing the Afternoon Studio brand (logo, founder, founding
    date), and
  - a **WebSite** that references the Organization as its publisher.
- The brand's **other web presences** are declared via `sameAs` — the Instagram profile
  and the Pepper You collection. `sameAs` is the correct schema.org property for "this is
  the same entity, elsewhere on the web", which is exactly the relationship to the Pepper
  You shop. (We intentionally do **not** copy Pepper You's own canonical/OG tags onto this
  page — each site keeps its own canonical so they aren't treated as duplicates.)
