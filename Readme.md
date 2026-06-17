# Surfing Clube de Portugal — Website Project Brief

> Paste this into the Project's **knowledge / custom instructions** so any new chat starts with full context. Keep it updated as the source of truth.

## What this is
A simple, compelling one-page site for **Surfing Clube de Portugal**, a non-profit surf club in **São Pedro do Estoril (Cascais), Lisbon**. Goal: tell the club's story, show achievements + classes + contact, and use the club's **Instagram as the live "news" feed** so the site needs almost no manual updates. Client is not tech-savvy; low-maintenance is a hard requirement.

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
1. Sticky nav — logo, links, PT/EN toggle, "Inscreve-te" CTA  → `#top`
2. Hero — full-bleed photo, headline, "EST. 1978", CTAs
3. Stats strip (47 anos / 1.º clube / 20+ ESF / 7 modalidades)
4. História → `#historia`
5. Conquistas (horizontal timeline) → `#conquistas`
6. Aulas (4 class cards) → `#aulas`
7. Galeria (lightbox grid) → `#galeria`
8. Instagram (live feed from Behold.so JSON) → `#instagram` ✅ **COMPLETE**
9. Contacto (info + Google Maps embed) → `#contacto`
10. Footer
- Floating: WhatsApp button · Cookie banner · PT/EN toggle (works via `data-pt`/`data-en` attributes)

## Verified real facts (already used — no need to re-research)
- Founded **1978**; first & oldest surf club in Portugal; Praia de São Pedro do Estoril
- Modalities: **Surf, Longboard, Skimboard, Bodyboard, Stand-up Paddle, Bodysurf, Águas Livres** (7 total)
- **Estoril Surf Festival** — 20th edition in 2024, runs through November
- Phone **+351 214 678 002** · Email **info@surfingclubeportugal.com**
- Instagram **@surfingclubeportugal** (Business account, connected to Behold.so)
- Facebook **/surfingclubeportugal**
- Address: Centro de Surf, Avenida Marginal, Praia de São Pedro do Estoril, 2765-603 Estoril, Cascais

## TODO / placeholders to replace

### ✅ Completed
- [x] **Live Instagram feed** — Behold.so JSON integration complete. Renders 6 most recent posts with captions, timestamps, and media badges. Auto-updates whenever new posts are added to Instagram.

### Still needed
- [ ] **Photos** — all remaining Unsplash placeholders (hero, história, galeria sections) to be swapped for real club photos (`img.ph-img` slots)
- [ ] **WhatsApp number** — float currently points to `wa.me/351000000000`; update to real club number
- [ ] **Class schedules / prices / ages** — currently sensible placeholders; confirm with club
- [ ] **Real championship results** — fill the timeline ("O teu título aqui" card) with actual club achievements
- [ ] **Privacy/RGPD page** — cookie banner links to it
- [ ] **Hosting decision** — domain registered but hosting platform not yet decided
- [ ] **gdpr compliance**

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

## File structure
```
index.html              ← the site (inline CSS + JS, logo referenced by path)
resources/
  logo.png              ← colour logo (nav)
  logo-white.png        ← white logo (footer/dark sections)
  [client photos go here later]
```

## How to edit efficiently (token-saving)
- Logo is **referenced from /resources**, not embedded — keeps the file small.
- Ask for **scoped edits** by section marker ("change the hero headline", "restyle the class cards"), not "redo the page".
- One focused change per message; batch related tweaks together.
- For visual-only changes, consider externalizing CSS to `styles.css` / JS to `script.js` so edits never touch index.html.
- Instagram feed is auto-updating — no edits needed unless Behold configuration changes or feed ID expires.
