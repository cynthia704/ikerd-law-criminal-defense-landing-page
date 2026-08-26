# Ikerd Law Firm — Criminal Defense Landing Page (MOCKUP)

**This is a mockup and reference guide, not a page to deploy.**

It exists so the build can be worked from something clickable rather than a written spec.
Rebuild it in WordPress on **staging**. The staging link then goes to Dimitry and Brian for
approval. **Nothing replaces the live page until they sign off.**

**Preview this build:** https://cynthia704.github.io/ikerd-law-criminal-defense-landing-page/
**Current live page** (do not touch yet): https://www.ikerdlawcriminaldefense.co/

> The preview is served by GitHub Pages and is blocked from search engines two ways —
> a `noindex` meta tag in `index.html` and `robots.txt` — so it cannot compete with the
> client's live page. **Do not copy either to production.** `robots.txt` disallows
> everything, and the `noindex` tag is marked with a comment saying when to remove it.

This is the **criminal defense** page. The firm's **DUI/DWI** landing page is a separate
build with a separate phone number: https://github.com/cynthia704/ikerd-law-dui-landing-page

---

## Sequence

1. Dev team rebuilds this in WordPress, on staging
2. Staging link comes back to Infintech
3. Infintech takes it to Dimitry and Brian for approval
4. Any changes they ask for get made
5. Only then does it go live

---

## Running the mockup

There is no build step and no package manager. One HTML file plus an `assets/` folder.

```bash
# open directly
open index.html            # macOS
start index.html           # Windows

# or serve locally
python -m http.server 8000
```

CSS and JS are inline. Icons are an inline SVG sprite at the top of `<body>` — 35 symbols
referenced with `<use href="#i-name">`, no icon library and no external request.

The only external call on the whole page is **Google Fonts** (Merriweather for headings,
Source Sans 3 for body), which matches the typography in Dimi's design. Both have real
fallbacks — Georgia and system sans — so the page holds its shape if the fonts fail.

---

## ⚠️ Read before you change anything

### 1. The phone number is (337) 279-2748. Do not "fix" it.

**This is the call-tracking number for this specific landing page.** It is not the number
published on `ikerdlaw.com`, and it is **not** the number on the firm's DUI landing page,
which is (337) 426-9348.

Those are three separate lines on purpose. If you swap in a different one, the phone still
rings but **call attribution drops to zero**, and it will look like the new page destroyed
campaign performance. There is a comment at the top of `index.html` saying the same thing.

If the tracking provider is ever changed, this number changes with it — confirm with
Infintech before editing.

> Separately: the **current live page has a different number buried in one link** — the
> "Call or send us a message today" link points at (337) 366-8994 while every other button
> on that page points at (337) 279-2748. That looks like a mistake on the live page. It is
> not carried into this rebuild. Flag it, do not copy it.

### 2. The forms are intentionally not live

There are two — the Free Case Review in the hero and the short Free Consultation at the
bottom. Both have an empty `action` and **a disabled submit button**.

That is deliberate. A form that posts nowhere loses leads silently, which is worse than no
form. Underneath each one are the firm's real Clio Grow intake and booking links plus the
phone number, which do work.

**To wire them up:** set the form `action`, remove the `disabled` attribute on the submit
button, and send confirmed leads to a thank-you page. **Ask Infintech for the destination
email address first** — nobody has specified it yet.

**Before launch: submit a test lead and confirm it actually arrives.**

### 3. Some copy is still pending verification

Several factual claims on this page — bar admissions, a review count, and a years-of-
experience figure — are **marked `PENDING-VERIFICATION` in HTML comments** and are waiting
on written confirmation from the firm.

This is an attorney advertising page. **Do not remove those markers, and do not add legal,
statutory, or regulatory claims to it** without confirming with Infintech that the firm has
signed off in writing. If a section looks like it is missing detail, ask before filling it in.

All eight FAQ answers are Dimi's own text, copied from his design. Seven of them sit
collapsed in his build, so they do not show up in a plain page scrape and had to be opened
one at a time to recover. **Do not rewrite them.**

### 4. Things this mockup does not include

- **No analytics and no Ads conversion tracking.** Both must be added before this replaces
  anything live, or campaign data is lost from day one.
- **No trust badges.** Left out deliberately, pending a decision from the firm.
- **HTML comments ship as-is.** Strip them when minifying for production.

---

## What to keep when you rebuild

These were checked in the browser at 390px, 900px, 1000px, 1440px and 1700px. If the
WordPress build changes them, it is a regression.

| | |
|---|---|
| **Contrast** | 305 text elements, zero WCAG failures at every width |
| **Schema** | A full `Attorney` JSON-LD block — name, address, phone, fax, six parishes, opening hours. Keep it. |
| **FAQ** | Native `<details>`/`<summary>`, so the accordions work with JavaScript disabled |
| **Motion** | The stat carousel pauses on hover and on keyboard focus, and goes static under `prefers-reduced-motion` |
| **Images** | All carry `width`/`height` so the layout does not shift while they load |
| **Horizontal scroll** | None at any width. The carousel is wider than the viewport by design and is clipped. |

---

## Credits

Structure and copy follow Dimi's design mockup. Design tokens and typography were read
from that build's compiled CSS rather than approximated, so the dev team is matching one
source rather than two.
