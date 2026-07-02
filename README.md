# NumeroHealth — marketing website (numerohealth.com)

Static marketing site for **numerohealth.com** (the public/apex domain).
The **app** lives separately at **app.numerohealth.com** (the Flask app on Render).

This is intentionally a **separate, static site** from the app: different concerns
(SEO, fast static delivery, marketing copy anyone can edit) and a different deploy
cadence than the product.

## Files
- `index.html` — the whole site (single page, inline CSS, no build step, no dependencies).
- `robots.txt` — allow crawling.

Preview locally: just open `index.html` in a browser (double-click), or run
`python3 -m http.server` in this folder and visit `http://localhost:8000`.

## Do we need a new repo? — Yes (recommended)
Keep the marketing site in its **own repo**, separate from the app repo
(`numerohealth-glp1app`). Reasons:
- Marketing copy changes shouldn't trigger app deploys (and vice-versa).
- Static hosting is cheaper, faster, and simpler than routing the apex through the
  Flask app.
- Non-engineers can safely edit copy without touching the product.

Suggested repo name: **`numerohealth-website`**.

## Recommended hosting + DNS
Host the static site on **Cloudflare Pages** (you already use Cloudflare for the
app's HTTPS) — or Netlify / Vercel / GitHub Pages. All are free for this.

DNS (at your registrar / Cloudflare):
- `numerohealth.com` (apex) + `www` → the static host (Cloudflare Pages).
- `app.numerohealth.com` → the Render app **(already set — leave as-is)**.

Deploy flow (Cloudflare Pages example):
1. `git init` in this folder, commit, push to a new GitHub repo `numerohealth-website`.
2. Cloudflare Pages → Create project → connect the repo → Framework preset **None**,
   build command **(none)**, output directory **/** (root).
3. Add custom domain `numerohealth.com` (+ `www` redirect to apex).

No build, no secrets, no server.

## Compliance notes (kept deliberately high-level)
Per the regulatory binder, the copy is intentionally **educational / general-wellness**:
- No medical, diagnostic, or device claims; "not medical advice, not a substitute for
  your provider" appears in the hero, FAQ, and footer.
- Features are described at a **benefit level only** — no dosing/engine internals,
  no drug brand names, no personalization mechanics.
- Footer carries the full educational-use disclaimer and the FDA statement.
- Legal links (Privacy, Terms) point to the app's existing in-app legal pages
  (`app.numerohealth.com/privacy`, `/terms`) so there's a single source of truth.

## Placeholders to fill before launch
- [ ] **Store badges** — the App Store / Google Play badges currently link to
      `app.numerohealth.com`. Swap to the real store URLs once the apps are listed
      (and remove the "Coming soon" notes in the hero + final CTA).
- [ ] **Real app screenshots** — the "A peek inside" section uses dashed phone-frame
      placeholders (Home / Nutrition / Progress). Drop in real screenshots.
- [x] **Founder section** — filled: "Dr. Sashi" + pharma-scientist bio (BPharm, PhD
      Pharmaceutical Sciences, 15 yrs biopharma/biotech). Add a real headshot to replace
      the 🔬 avatar when available.
- [ ] **Social proof** — the strip uses honest placeholders ("Loved by our early
      users", "Free", "Private"). Add real ratings/counts only once true.

## Contact form (Formspree) — REQUIRED before go-live
The Contact form posts to Formspree so messages land in an inbox automatically
(works without the visitor having a mail client). To activate it:
1. Create a free form at https://formspree.io and set its recipient to
   `info@numerohealth.com`.
2. Copy the form's endpoint (looks like `https://formspree.io/f/abcwxyz`).
3. In `index.html`, replace `YOUR_FORM_ID` in the form's `action=` with your real ID.
Until that's done, the form gracefully falls back to opening a `mailto:info@numerohealth.com`
draft, so it still works. (Host-agnostic — works on Cloudflare Pages, Netlify, Vercel, or
GitHub Pages. If you deploy on Netlify and prefer Netlify Forms instead, say so and we'll swap.)

## Before going live — quick review checklist
- [ ] **Wire the Formspree form** (see above) and confirm `info@numerohealth.com` is monitored.
- [ ] Decide pricing wording (currently "shown in the app" — no numbers on the site).
- [ ] Confirm the app-link targets (`app.numerohealth.com` in the hero + final CTA) are right
      (vs. an App Store / TestFlight link or a waitlist). Note: the top nav no longer has an
      "Open the app" button — the primary nav CTA is now "Contact us."
- [ ] Optional: add `og-image.png`, a favicon, and a `sitemap.xml`.
- [ ] Legal/counsel pass on marketing copy — especially the founder story, any social
      proof, and the "science/guidelines" section (RC2.0 marketing-claims item).
