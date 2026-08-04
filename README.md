# NEXORAT ROUTER — Link Tree

Static link page for the NEXORAT ROUTER brand. Dark terminal theme, boot-sequence
intro, 5 link cards: AI Gateway, Router Store, Telegram bot, Telegram community,
WhatsApp community.

## ⚠️ Domain decision — read this first

You said you'd point `nexoratrouter.name.ng` (root) at this link tree and move the
AI Gateway to a subdomain. Before you do that: the AI Gateway site's own integration
docs (Claude Code, Cline, LobeChat, etc.) tell **paying customers** to set their
Base URL to `https://www.nexoratrouter.name.ng/v1`. If you repoint the root domain
to this static link tree, every customer using that Base URL breaks instantly,
including anyone with it saved in `.claude/settings.json`, Cline configs, etc.

Two safe options:

1. **Recommended:** keep `nexoratrouter.name.ng` on the AI Gateway (no breakage),
   and put this link tree on a subdomain — e.g. `links.nexoratrouter.name.ng` or
   `hub.nexoratrouter.name.ng`. Update the `CNAME` file and all canonical/OG URLs
   in `index.html` and `sitemap.xml` to match.
2. **If you still want root domain for the link tree:** first migrate the AI
   Gateway to its new subdomain (e.g. `api.nexoratrouter.name.ng`), update every
   integration guide on that site, give existing customers notice, *then* repoint
   root to this repo.

The files below assume you go with the root domain as-is (per your instructions),
but swap the domain everywhere if you pick option 1.

## Deploy to GitHub Pages

1. Create a repo (e.g. `nexorat-links`) and push these files to it.
2. In the repo: **Settings → Pages → Source** = deploy from branch `main`, folder `/root`.
3. **Settings → Pages → Custom domain** → enter `nexoratrouter.name.ng` → Save.
   This writes the `CNAME` file automatically (or keep the one included here).
4. At your domain registrar (name.ng), add these DNS records pointing at GitHub Pages:
   - `A` records for the apex domain → `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153`
   - `CNAME` for `www` → `<your-github-username>.github.io`
5. Wait for DNS to propagate, then tick **Enforce HTTPS** in the Pages settings once
   it's available.

## Get Google to index it

1. Go to [Google Search Console](https://search.google.com/search-console) → **Add property** → enter `https://nexoratrouter.name.ng`.
2. Verify ownership — easiest method here since you don't control server headers:
   **HTML tag** method. Search Console gives you a code like:
   ```
   <meta name="google-site-verification" content="AbC123...")>
   ```
   Copy the `content` value and paste it into `index.html`, replacing
   `REPLACE_WITH_YOUR_VERIFICATION_TOKEN` in the existing
   `<meta name="google-site-verification">` tag. Commit and push, then click
   **Verify** in Search Console.
3. Once verified, go to **Sitemaps** in the left sidebar, and submit:
   `https://nexoratrouter.name.ng/sitemap.xml`
4. Go to **URL Inspection**, paste `https://nexoratrouter.name.ng/`, and click
   **Request Indexing**. This is what gets it into results fastest — usually
   within a few days rather than waiting for an organic crawl.
5. Also link this domain from somewhere Google already crawls — e.g. add the
   link-tree URL to the footer of `nexoratrouter.name.ng` and `shop.nexoratrouter.name.ng`,
   your GitHub profile bio, and your Telegram/WhatsApp community descriptions.
   Inbound links speed up discovery and ranking for brand-name searches.

## Files

- `index.html` — the page itself (no build step, pure HTML/CSS/JS), light theme
- `favicon.ico`, `favicon-16.png`, `favicon-32.png`, `favicon-48.png`,
  `favicon-180.png` — browser tab icon (the .ico covers most browsers,
  `favicon-180.png` is the apple-touch-icon for iOS home screens)
- `og-image.png` — the 1200×630 preview image that shows up when the link is
  shared on Telegram, WhatsApp, X, etc.
- `sitemap.xml` — tells Google what to crawl
- `robots.txt` — allows crawling, points to the sitemap
- `CNAME` — GitHub Pages custom domain config (already set to `nexoratrouter.name.ng`)

All of these need to sit in the **repo root** (same level as `index.html`) for the
paths in `index.html` (`favicon.ico`, `og-image.png`, etc.) to resolve.

## Link preview & description

The description that shows up under the link when it's shared (WhatsApp, Telegram,
X, etc.) comes from the `og:description` / `twitter:description` meta tags near the
top of `index.html` — already set to describe the link hub and what it contains.
If you ever change the set of links on the page, update that description to match.
