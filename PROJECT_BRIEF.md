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
3. Stats strip (47 anos / 1.º clube / 20+ ESF / 3 modalidades)
4. História → `#historia`
5. Conquistas (horizontal timeline) → `#conquistas`
6. Aulas (4 class cards) → `#aulas`
7. Galeria (lightbox grid) → `#galeria`
8. Instagram (placeholder grid + live-feed slot) → `#instagram`
9. Contacto (info + Google Maps embed) → `#contacto`
10. Footer
- Floating: WhatsApp button · Cookie banner · PT/EN toggle (works via `data-pt`/`data-en` attributes)

## Verified real facts (already used — no need to re-research)
- Founded **1978**; first & oldest surf club in Portugal; Praia de São Pedro do Estoril
- Modalities: **Surf, Longboard, Skimboard, Skate**
- **Estoril Surf Festival** — 20th edition in 2024, runs through November
- Phone **+351 214 678 002** · Email **info@surfingclubeportugal.com**
- Instagram **@surfingclubeportugal** · Facebook **/surfingclubeportugal**
- Address: Centro de Surf, Avenida Marginal, Praia de São Pedro do Estoril, 2765-603 Estoril, Cascais

## TODO / placeholders to replace
- [ ] **Photos** — all images are placeholder Unsplash shots over branded gradients; swap for client photos (`img.ph-img` slots)
- [ ] **WhatsApp number** — float currently points to `wa.me/351000000000`
- [ ] **Class schedules / prices / ages** — currently sensible placeholders
- [ ] **Real championship results** — fill the timeline ("O teu título aqui" card)
- [ ] **Live Instagram feed** — paste a widget iframe into the `<!-- LIVE INSTAGRAM FEED GOES HERE -->` slot
- [ ] **Privacy/RGPD page** — cookie banner links to it
- [ ] Optional: donation/"Apoia o clube" link, inscrições-abertas banner, Google Business Profile

## Instagram feed approach (decided)
Do **not** use Instagram's official oEmbed/Graph API (token expires ~60 days = manual upkeep). Use an auto-refreshing third-party widget: **Behold.so / EmbedSocial / SnapWidget / LightWidget / Tagembed**. Paste its iframe once into the slot; no ongoing maintenance.

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
