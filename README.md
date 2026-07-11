[README_2.md](https://github.com/user-attachments/files/29929610/README_2.md)
# The Wealth Brief — Website

A single-page cinematic marketing site for The Wealth Brief, a financial education brand selling eBooks, workbooks, planners, and Notion templates. Built as static HTML/CSS/JS — no build step, no framework, no server required.

## File structure

```
/
├── index.html                  ← the main site (everything lives in this one file)
├── 404.html                    ← branded not-found page
├── assets/
│   ├── og-image.png            ← social share preview image
│   └── covers/                 ← 8 product cover images
│       ├── mastering-credit.png
│       ├── credit-dispute-toolkit.png
│       ├── budget-and-goals.png
│       ├── command-center.png
│       ├── reading-your-credit-report.png
│       ├── wealth-tracker.png
│       ├── saving-on-autopilot.png
│       └── investing-101.png
└── legal/
    ├── privacy-policy.html
    ├── terms-of-use.html
    └── refund-policy.html
```

**Keep this folder structure intact when you deploy.** The links between pages (footer → legal pages, legal pages → back to home, cover images) are all relative paths that depend on this exact layout. If you move `index.html` without moving `assets/` and `legal/` alongside it, images and links will break.

## What's still a placeholder (do this before launch)

### 1. Payhip product keys — 7 of 9 remaining
Checkout is powered by Payhip's embedded buy-button widget. Search `index.html` for `REPLACE` to find every remaining spot — each placeholder key appears in two places (an `href` and a `data-product` attribute) that both need updating.

| Key | Product | Status |
|---|---|---|
| `COLLECTION-KEY` | Complete Collection bundle | ⬜ still placeholder |
| `NOTION-KEY` | Notion System template | ⬜ still placeholder |
| `MASTERING-CREDIT-KEY` | Mastering Credit | ⬜ still placeholder |
| `DISPUTE-TOOLKIT-KEY` | Credit Dispute Toolkit | ⬜ still placeholder |
| `BUDGET-GOALS-KEY` | Budget & Goals | ⬜ still placeholder |
| `COMMAND-CENTER-KEY` | Command Center | ✅ done (`7Mbc5`) |
| `READING-REPORT-KEY` | Reading Your Credit Report | ⬜ still placeholder |
| `DEBT-PAYOFF-KEY` | Wealth Tracker | ✅ done (`MtS9H`) |
| `SAVING-AUTOPILOT-KEY` | Saving on Autopilot | ⬜ still placeholder |
| `INVESTING-101-KEY` | Investing 101: The Basics | ⬜ still placeholder |

To get a key: Payhip dashboard → the product → **Share/Embed** → copy the code after `payhip.com/b/`.

### 2. Legal pages need real details
All three files in `/legal` have `[YOUR CONTACT EMAIL]` and `[MONTH DAY, YEAR]` placeholders, and are general-purpose templates — not lawyer-reviewed. Worth a real legal review before launch, especially the Terms of Use disclaimer section, given the financial-education niche.

### 3. Analytics — not connected
Search `index.html` for `G-XXXXXXXXXX` — that's a placeholder Google Analytics 4 Measurement ID. Until it's replaced with a real one, no visitor data is tracked (this is intentional — analytics only loads after a visitor accepts the cookie banner).

### 4. Newsletter — not connected to a real list
The footer newsletter and the lead-magnet popup both currently just show a "thanks" message in the browser — nothing is actually captured or stored anywhere. Needs a real email service provider (Mailchimp, ConvertKit, Flodesk, etc.) wired in.

### 5. Product preview content
Each product card has a "Preview" button that opens a modal — right now it just shows placeholder text telling you to add real sample pages. Worth doing before launch since real previews measurably help conversion on digital products.

### 6. Domain
The canonical URL, `og:image` URL, and JSON-LD structured data all currently point to a placeholder domain (`thewealthbrief.com`). Update these once you have a real domain — search for `REPLACE with your live domain`.

## Design system

| Role | Value |
|---|---|
| Midnight Navy | `#0B1320` |
| Charcoal Slate | `#1F2937` |
| Antique Gold | `#D4AF37` |
| Warm Ivory | `#F8F6F2` |
| Cocoa accent | `#8B5E3C` |
| Headings | Sora, weight 700 |
| Body | Inter |
| Buttons | Inter, weight 600 |
| Numbers/stats | Space Grotesk, weight 600 |

Signature visual motif: the credit-score arc gauge, used as a fixed scroll-progress indicator (top right of every page) and repeated throughout as a design element.

## Going live

This is a static site — any static host works. The simplest path if you don't want to touch a command line:

1. Go to **[app.netlify.com/drop](https://app.netlify.com/drop)**
2. Drag the entire project folder (containing `index.html`, `assets/`, `legal/`, `404.html`) into the drop zone
3. Your site is live instantly at a `*.netlify.app` URL
4. To use your own domain: in the Netlify dashboard, go to **Domain settings → Add a domain**, and follow the instructions to point your domain's DNS at Netlify

Other static hosts that work the same way: Vercel (`vercel.com/drop`), Cloudflare Pages, GitHub Pages.

**Note on Payhip:** Payhip's advanced embed features are documented as requiring a real custom domain rather than a raw file or a free `*.netlify.app` preview URL — connect your domain before going fully live with checkout.

## Making changes later

- **Adding/renaming a product**: each product appears in up to 4 places — the product grid card, the showcase shelf tag, the 3D carousel array (in the JS near the bottom of the file), and its cover image. Search for the product's current name to find all instances.
- **Changing a price**: search for `Buy — $` to find every displayed price; remember this only changes what's *displayed* — the real charge is set inside Payhip itself.
- **Cover art**: located in `assets/covers/`, generated at 900×1260px. If you regenerate one, keep the same filename or update the `background-image:url(...)` reference in the matching product card.

## Known limitations

- No build step or bundler — it's intentionally a single dependency-free HTML file plus a folder of static assets, which keeps it simple to host anywhere but means it doesn't scale well as a large multi-page site.
- Performance hasn't been measured with real tooling (e.g. Lighthouse) — only reasoned about (particle counts were trimmed as a precaution, not measured).
- No CMS — every content change is a direct HTML edit.
