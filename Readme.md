# Surfing Clube de Portugal — Website Project Brief

> Paste this into the Project's **knowledge / custom instructions** so any new chat starts with full context. Keep it updated as the source of truth.

## What this is
A simple, compelling one-page site for **Surfing Clube de Portugal**, a non-profit surf club in **São Pedro do Estoril (Cascais), Lisbon**. Goal: tell the club's story, show achievements + classes + contact, and use the club's **Instagram as the live "news" feed** so the site needs almost no manual updates. Client is not tech-savvy; low-maintenance is a hard requirement.

**Status as of 18 June 2026:** Domain live and pointing to GitHub Pages. Site accessible at `https://surfingclubeportugal.com`.

---

## COMPLETED — DNS & Hosting (18 June 2026)

**What was done:**
- Domain `surfingclubeportugal.com` migrated from WebHS server (`185.90.59.106`) to GitHub Pages hosting
- Root A records updated: four GitHub IPs (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`)
- www CNAME changed to `afonsoreyna.github.io.`
- `CNAME` file added to repo root containing `surfingclubeportugal.com`
- Custom domain `surfingclubeportugal.com` enabled in GitHub Pages settings (branch: `main`, root folder)
- Email routing (MX, SPF, DKIM) preserved — club email unaffected
- DNS has propagated globally (confirmed via dnschecker.org)


---

## Brand tokens (do not drift from these)
- Cyan (primary): `#00A8E8` — sampled from the logo
- Orange (accent/CTA): `#F7941E`
- Deep Atlantic ink (dark sections/text): `#0A2433`
- Sea-foam light background: `#EAF4F6`
- Granite secondary text: `#4E626E`
- Card white: `#FBFEFE`
- Fonts (Google Fonts): **Archivo** (display/headings, 800–900), **Inter** (body/UI), **Fraunces italic** (used sparingly: hero year + one pull-quote)

## Design direction
"Heritage meets Atlantic." Leans on the *oldest-club-in-Portugal / est. 1978* angle to avoid a generic tropical surf-school look. **Signature element:** a hand-drawn cyan+orange wave stroke (the `.wave-rule` SVG, pulled from the logo's swoosh) that underlines every section heading. Keep boldness in the hero; everything else stays quiet and disciplined.

## Page structure (section order, IDs, and edit markers)
Each section has a comment banner like `<!-- =================== HERO =================== -->` — reference these when asking for edits.
1. Sticky nav — logo, links, PT/EN toggle, "Inscreve-te" CTA → `#top`
2. Hero — full-bleed video background, headline, "EST. 1978", CTAs
3. Stats strip (47 anos / 1.º clube / 20+ ESF / 7 modalidades)
4. Aulas (4 class cards) → `#aulas`
5. Instagram (live feed from Behold.so JSON) → `#instagram` ✅ **LIVE**
6. História → `#historia`
7. Conquistas (horizontal timeline) → `#conquistas`
8. Galeria (lightbox grid) → `#galeria`
9. Contacto (info + spotlight video slideshow + Google Maps embed) → `#contacto`
10. Footer
- Floating: WhatsApp button · Instagram · Facebook · Email buttons · Cookie banner · PT/EN toggle (works via `data-pt`/`data-en` attributes)

## Section colour rhythm (do not flatten these — contrast is intentional)
| Section | Background |
|---|---|
| Hero | Dark ocean video |
| Stats | `--ink` (#0A2433) dark |
| Aulas | `--paper` (#FBFEFE) white |
| Instagram | `--ink` (#0A2433) dark |
| História | `--foam` (#EAF4F6) light |
| Conquistas | `--ink` (#0A2433) dark |
| Galeria | `--foam-2` (#DCEDF0) |
| Contacto | `--ink-2` (#10314a) deep ocean |
| Footer | `#061a25` near-black |

## Verified real facts (already used — no need to re-research)
- Founded **1978**; first & oldest surf club in Portugal; Praia de São Pedro do Estoril
- Modalities: **Surf, Longboard, Skimboard, Bodyboard, Stand-up Paddle, Bodysurf, Águas Livres** (7 total)
- **Estoril Surf Festival** — 20th edition in 2024, runs through November
- Phone **+351 919 661 659** · Email **surfingclubeportugal@gmail.com**
- Instagram **@surfingclubeportugal** (Business account, connected to Behold.so)
- Facebook **/surfingclubeportugal**
- Address: Centro de Surf, Avenida Marginal, Praia de São Pedro do Estoril, 2765-603 Estoril, Cascais

## File structure
```
index.html              ← the site (inline CSS + JS, logo referenced by path)
CNAME                   ← GitHub Pages custom domain (added 18 June 2026)
resources/
  logowide.png          ← wide colour logo (nav, height: 60px)
  logo-white.png        ← white logo (footer/dark sections)
  [client photos go here later]
```

---

## Video implementation — YouTube (unlisted)

### Why YouTube
Cloudflare Stream requires payment for storage. Large video files (250MB+) exceed GitHub's 100MB limit. YouTube unlisted is the chosen free solution.

### Hero background video
- **Current ID:** `JUig1YpxuGk`
- Embedded as a full-bleed iframe behind a dark gradient overlay
- Parameters: `autoplay=1&mute=1&loop=1&playlist=ID&controls=0&disablekb=1&playsinline=1&rel=0&modestbranding=1&iv_load_policy=3&enablejsapi=1`
- The `.hero::after` gradient overlay (z-index:1) sits on top of the iframe, blocking YouTube UI chrome and making text readable
- Hero content `.wrap` is z-index:3, above the overlay — text and CTAs remain clickable

### Loop gap
YouTube has a 1-2s black flash on loop. Workaround: duplicate the clip 3-4× in a video editor (Clipchamp recommended — free, browser-based) before uploading, so the gap happens every 10-15 min instead of every loop. When re-uploading, just swap the video ID in the two places it appears in the hero src URL.

### Spotlight slideshow (Contacto section)
- **Slide 1 ID:** `FzESpRp-suM` (src baked in, autoplays on page load)
- **Slide 2 ID:** `6m1jISE7iUQ` (loaded via `data-src`, injected fresh on activation)
- Cycles every 8 seconds with crossfade; orange progress bar + dot navigation
- Parameters: same as hero but no `enablejsapi`

### YouTube UI chrome fix (title/channel/share buttons)
`showinfo` parameter was deprecated in 2018 — it no longer hides the title. Two-part workaround in use:
1. **CSS `::after` overlay** on `.spotlight-slide` — transparent pseudo-element at `z-index:2` sits above the iframe, blocking all YouTube UI interaction while video plays through
2. **Lazy src swap in JS** — slide 2 has no `src` on page load (`data-src` only). JS injects `src` with `autoplay=1` when the slide activates, and removes it when leaving. This guarantees autoplay fires fresh every time and stops the video when not visible.

The hero avoids this problem entirely because `.hero::after` (the visible dark gradient) covers the iframe as a side effect.

### iOS Safari caveat
Autoplay of iframes is more aggressively blocked on iOS Safari regardless of parameters — nothing to do about this without a paid video host.

---

## Instagram feed — implementation notes

**Status:** ✅ Live and functioning

**Approach:** Behold.so free tier JSON feed (no iframe, no monthly subscription, no branding)

**Feed URL:** `https://feeds.behold.so/PiIe2YpnUh4rELRtiDFJ`

**Key technical detail:** Behold's response is an object with a nested `posts` array, not a bare array. Images must use `sizes.medium.mediaUrl` (Behold's CDN) rather than `mediaUrl` (Instagram's CDN, which blocks hotlinking).

**Client requirements met:**
- Zero monthly cost
- Zero manual maintenance (token refresh handled by Behold)
- Seamless visual integration (custom CSS, no iframe)
- Bilingual (PT/EN relative timestamps)
- Graceful fallback (skeleton to branded tiles if fetch fails)

**Future upgrade path:** If hosting infrastructure becomes available, Option A (Meta Graph API with server-side token refresh) can replace this without changing HTML/CSS structure.

---

## TODO — Immediate Priority (Launch Phase)

### ✅ Completed
- [x] Live Instagram feed — Behold.so JSON integration complete
- [x] Hero background video — YouTube unlisted, ID: `JUig1YpxuGk`
- [x] Spotlight slideshow — 2 videos, IDs: `FzESpRp-suM` and `6m1jISE7iUQ`
- [x] Section order — decided with client
- [x] Section colour contrast — alternating dark/light rhythm established
- [x] YouTube UI chrome — blocked via CSS transparent overlay + lazy src swap
- [x] **Domain DNS & hosting** — migrated to GitHub Pages, live at surfingclubeportugal.com

### Still needed — Content & Launch
- [ ] **Real club photos** — replace all Unsplash placeholders (`img.ph-img` slots)
  - Hero background (or use current video)
  - História section (main grid + archive strip)
  - Galeria section (7-item grid)
  - Estimated impact: **High** — visual authenticity critical for trust
- [ ] **Class details confirmation** — schedules, prices, age ranges (currently sensible placeholders)
  - Contact club to verify current offerings
- [ ] **Real championship results** — fill the timeline ("O teu título aqui" card) with actual club achievements
  - Dates, event names, athlete/team names
- [ ] **WhatsApp button** — update from placeholder `wa.me/351000000000` to real club number (currently: `+351 919 661 659`)

### Still needed — Legal & SEO
- [ ] **Privacy/GDPR policy page** — create standalone page (cookie banner links to it)
  - Must cover: data collection, cookie usage, contact info, data subject rights
  - Consider RGPD compliance — may need legal review
  - Estimate: 500–800 words
- [ ] **Google Search Console verification** — register domain and submit sitemap
  - Separate from Analytics; needed for search visibility
  - Add `sitemap.xml` to repo
- [ ] **Google Analytics 4 setup** — tracking code + consent flow
  - Integrate with cookie banner (only load GA if user accepts analytics)
  - Track: page views, scroll depth, CTA clicks, outbound links
- [ ] **Structured data (Schema.org)** — local business markup
  - Helps Google understand: location, phone, hours, modalities
  - Add JSON-LD to `<head>` or inline in HTML

### Still needed — Operations
- [ ] **Domain renewal reminder** — set calendar alert for **17 October 2026** (domain expires)
  - Reseller: `domains@domainprotect.pt` / `+351 308 802 611`
- [ ] **Email setup verification** — confirm club mailboxes are live
  - WebHS email hosting still active; verify it's being used or plan migration
- [ ] **Enforce HTTPS** — tick the box in GitHub Pages settings (pending DNS check clear)

### Not urgent — Enhancement
- [ ] Open Graph tags (improves social sharing previews)
- [ ] Sitemap.xml generation and submission
- [ ] Performance audit (Lighthouse, Core Web Vitals)
- [ ] Mobile UX refinement (currently responsive, but test real devices)

---

## How to edit efficiently (token-saving)
- Ask for **scoped edits** by section marker ("change the hero headline", "restyle the class cards"), not "redo the page"
- One focused change per message; batch related tweaks together
- When swapping video IDs: each ID appears **twice** in its src URL (once in the path, once in the `playlist=` parameter) — both must be updated
- The colour rhythm table above is intentional — don't flatten sections to the same background without checking the sequence
- Instagram feed is auto-updating — no edits needed unless Behold configuration changes or feed ID expires
- Nav links, mobile drawer links, and footer nav links must all be kept in sync when reordering sections
- before coding or doing a heavy task allways ask for green light
