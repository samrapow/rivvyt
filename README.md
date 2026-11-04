# RIVVYT — website

The public teaser site for RIVVYT, an American rugged digital watch company in development. Intended to live at [rivvyt.com](https://rivvyt.com).

It is a deliberately small, plain static site: one HTML page, one stylesheet, and a tiny progressive-enhancement script. There is no build step, no framework, no dependencies, and no backend. Every contact action is a real `mailto:` link.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site: hero, three tenets, contact, footer. |
| `404.html` | Not-found page (GitHub Pages serves it automatically). |
| `assets/css/site.css` | All styles. Design tokens are at the top in `:root`; sections use `.theme-ink` (dark) or `.theme-bone` (light). |
| `assets/js/site.js` | Reveal-on-scroll and the footer year. The site works without it. |
| `assets/favicon.svg`, `assets/favicon-32.png`, `assets/apple-touch-icon.png` | Icons. |
| `assets/og.png` | 1200×630 share image used by Open Graph and Twitter cards. |
| `robots.txt`, `sitemap.xml` | Search engine basics. Both reference `https://rivvyt.com`. |

Anything placed in a `private/` folder is gitignored and never published.

## Local development

Open `index.html` directly in a browser, or serve the folder so that the root-relative links on the 404 page work:

```bash
python3 -m http.server 8765
```

Then visit <http://localhost:8765/>.

## Editing content

All copy lives in `index.html`. The things most likely to change:

- **Hero headline and lede:** the `<section class="section theme-ink hero">` block.
- **The three tenets:** the `<ul class="tenets">` list.
- **Emails:** search for `sam@rivvyt.com` and `sourcing@rivvyt.com`. Subject lines are URL-encoded in the `mailto:` links.
- **Accent color and palette:** `assets/css/site.css`, the `:root` block at the top.
- **Share image:** replace `assets/og.png` with any 1200×630 PNG.

### What the site intentionally does not say

The site makes no present-tense "Made in USA" product claim and publishes no specifications, dates, prices, suppliers, partners, sourcing details, roadmap, or product architecture. Keep it that way until there is something ready to announce.

## Deployment

The site is meant to be hosted on **GitHub Pages** from the `main` branch of this repository (root folder). Pushing to `main` redeploys within a minute or two.

```bash
git add -A
git commit -m "Update copy"
git push
```

### Pointing rivvyt.com at the site

The domain is registered with Squarespace Domains. To serve the site at rivvyt.com:

1. In the GitHub repository, go to **Settings → Pages**, set **Custom domain** to `rivvyt.com`, and save. (This commits a `CNAME` file.)
2. In Squarespace Domains → rivvyt.com → **DNS settings**, remove the Squarespace parking records and add:

   | Type | Host | Value |
   | --- | --- | --- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | samrapow.github.io |

3. Wait for DNS to propagate, then in **Settings → Pages** tick **Enforce HTTPS** once GitHub has issued the certificate (usually under an hour).

No environment variables or secrets are needed. There is no form backend; if an email-list provider is added later, wire it up properly rather than adding a form that silently drops submissions.
