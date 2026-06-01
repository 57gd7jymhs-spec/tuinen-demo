# AGENTS.md — Tuinen Decoster website

> **Single source of truth for this project. Read this first.**
> Read by BOTH Claude Code and ChatGPT Codex. Codex reads `AGENTS.md` by default; `CLAUDE.md` points here.
> **Update the "Work log" at the bottom and the "Last verified" date at the end of every session, before switching tools.**
> Last verified: 2026-06-01.

## Status
Client-ready **DEMO** — finished and verified on desktop + mobile. **NOT yet published publicly.**
Several data points are invented and must be confirmed by the owner first (see *Real vs invented* + *Before-publish checklist*).

## What this project is
Single-page Dutch marketing website for **Tuinen Decoster**, a one-man garden landscaping & maintenance
business (owner: **Jan Decoster**) in Brugge / West-Vlaanderen, Belgium. Goal: drive phone enquiries.
Positioning: duurzaam, vakkundig, ecologisch. The folder and Vercel project are still named
`ad-groenservice-new` (legacy name — keep it; it is not user-visible).

## Stack
- Vanilla HTML/CSS/JS in a single file `index.html` (~4200 lines, inline `<style>` + `<script>`). No build step. Node 24.x.
- AI chatbot: `api/chat.js` serverless function (Groq, model `llama-3.3-70b-versatile`). `GROQ_API_KEY` is a Vercel env var — never commit it.
- CDN libs: GSAP 3.12.5 + ScrollTrigger, Leaflet 1.9.4 (CARTO Positron tiles), Google Fonts.
- Deploy: `vercel --prod` (project `ad-groenservice-new`). Prod: https://ad-groenservice-new.vercel.app

## Brand tokens (authoritative copy lives in `index.html` `:root`)
- Palette: bg `#f5f5f0` · bg-2 `#ebebe7` · bg-3 `#e0e0dc` · ink/text `#111a0d` · lime `#66bb35` · lime-bright `#79cc47`
- Fonts: Space Grotesk (display / logo), Inter + Inter Tight (body); also Nunito, JetBrains Mono.
- Logo: lime (`#66bb35`) rounded-square SVG leaf mark + wordmark `Tuinen ` + lime `Decoster` (Space Grotesk 700).
- Legacy trap: `styles.css` still defines an old blue palette (`--color-primary: #1847ED`). IGNORE it — the live page uses the lime palette from `index.html`.

## Contact — real vs invented (CRITICAL)
**REAL** (routes to the client): phone **0491 32 45 09** (`tel:+32491324509`, `wa.me/32491324509`).

**INVENTED / UNCONFIRMED** (the client allowed inventing demo data; confirm before any public launch):
- Company name "Tuinen Decoster", email `info@tuinendecoster.be`
- Address: Gistelse Steenweg 142, 8200 Sint-Andries (Brugge)
- BTW: BE 0782.531.146 · opening hours · service area
- Reviews "4.9 / 47 Google reviews" + named testimonials + "Geplaatst op Google" badges — **no real Google Business Profile exists**
- Before/after prices (€1.450 / €275 / €135) and service from-prices.

## Before-publish checklist (from council review, 2026-05-30)
1. Replace the fabricated reviews + "Geplaatst op Google" framing with real ones (or restyle as plain testimonials). Fake review markup risks a Google penalty against the real business — the JSON-LD `aggregateRating` was already removed for this reason.
2. Owner confirms / replaces legal data: VAT, address, email; register the domain.
3. Owner confirms claims: BIO-gecertificeerd, BA verzekerd, "meer dan 15 jaar", "sinds 2010".
4. Rehost the hero video off the old `AD-groenservice-template` GitHub Releases URL onto an owned host.
5. Add a real favicon file + analytics; confirm the deploy domain.

## Key files
- `index.html` — the entire site (all sections, styles, JS, chatbot UI).
- `api/chat.js` — Groq chatbot backend.
- `assets/` — `jan-owner.png` (full owner photo), `jan-closeup.png` (closeup headshot), `Detail shot.png` (topiary bush), plus `before-*/after-*`, `action-*`, `testimonial-*`.
- `.screenshots/client-final/` — desktop + mobile verification shots (gitignored).
- `/archive/` — superseded docs from earlier sessions (TOMORROW.md, CONTENT.md). Historical only — do not follow.

## Image usage map
- Owner full photo (`jan-owner.png`): intro/about section + process step 1 (`object-position: 60% 30%`).
- Owner closeup (`jan-closeup.png`): `.about-face` + `.cta-face` heading avatars, chatbot header + bot message bubbles.
- Topiary bush (`Detail shot.png`): hero video poster + FAQ section image.

## Work log (newest first — append every session, date it)
### 2026-06-01 — Before/after: mobile knob-less reveal + responsive intro copy (Claude Code)
- Mobile keeps the auto-reveal animation playing (the thin line glides so you still see before↔after), but hides only the draggable knob so nothing looks draggable: CSS hides `.ba-handle::before/::after/.pulse-ring`, the 3px line stays. The compare slider still ignores touch on mobile (so swipe owns the gesture); the animation runs on all viewports via `onEnter: startAuto`. Desktop unchanged (knob + drag-to-compare).
- Intro paragraph is now responsive (two spans toggled by the media query): desktop keeps "slider beweegt automatisch … pijlen of stippen"; mobile shows "De beelden wisselen vanzelf tussen voor en na. Veeg opzij om door mijn realisaties te bladeren." Fixes the stale "arrows"/"drag" wording on mobile.
### 2026-06-01 — Before/after: panel alignment + dynamic swipe guard (Claude Code)
- Aligned the green info panels across all cards: `.ba-info` is now `justify-content: flex-start` (titles top-aligned) and `.ba-foot` uses `margin-top: auto` (price + CTA pinned to the bottom). Verified all 5 cards share titleTop 37 / ctaBottom 425 (was a 35px title spread from the old `justify-content: center`).
- Made the swipe/buttons switch explicitly dynamic: the carousel swipe now early-returns unless `matchMedia('(max-width:768px)')` matches (checked per-gesture), symmetric with the inner compare-slider's mobile guard. Confirmed live switching on resize without reload (arrows are CSS-media-gated).
### 2026-06-01 — Before/after carousel: mobile swipe + viewport-fit (Claude Code)
- Mobile (≤768px): carousel is now swipe-to-navigate (touchstart/touchend on `#baViewport`, threshold 40px, horizontal-dominant; vertical swipes still scroll the page via `touch-action: pan-y`). Prev/next arrows hidden on mobile; dots kept as the indicator.
- Resolved the gesture clash: the per-card drag-to-compare slider now ignores touch on mobile (returns early in its `touchstart`); its auto-animation keeps demonstrating before/after. Desktop drag-to-compare unchanged.
- Card now fits the viewport: `.ba-case` is a flex column capped at `clamp(440px, 80vh, 600px)`, image flexes to fill, info compacted. Verified the full card + CTA + dots clear the sticky call bar on a 390×844 screen. Desktop (grid, arrows, 16:10) untouched.
### 2026-06-01 — Before/after card white-space fix (Claude Code)
- Fixed white space under the slider image on 2-column widths (~769–1150px): the info panel grew taller than the slider, but `.ba-slider-wrapper`'s `aspect-ratio: 16/10` locked its height so it couldn't fill the grid row. Added `height: 100%` so the image stretches to match the panel. Verified 1440 / 1000 / mobile, no regression (aspect-ratio still governs when the slider is the taller column / on mobile).
### 2026-06-01 — Before/after carousel image additions (Codex)
- Generated and added a realistic mossy "before" image for the Assebroek driveway case while keeping the clean driveway as the "after".
- Added two non-ground-heavy before/after carousel cases: heg- & buxussnoei and boomverzorging, each with new project-local assets, Dutch copy, tags, and richtprijzen.
### 2026-05-30 — Client-ready finalization (Claude Code)
- Rebranded AD Groenservice → Tuinen Decoster everywhere (title, nav/footer logos, intro loader, copyright, map label, OG tags, JSON-LD).
- Wired the two new owner photos (see image map). Reused the topiary bush as the FAQ image. Localized 3 Unsplash project cards to local assets.
- Filled ALL placeholders; wired the real phone + WhatsApp into every CTA / tel / footer / sticky mobile bar / floating widget / chatbot.
- Added OG tags + LocalBusiness JSON-LD; removed the fake `aggregateRating` (Google-policy risk).
- Fixed a mobile logo bug — the responsive rule shrank the second word to 7px, making "Decoster" illegible; set to 16px.
- Two-pass screenshot verification (1440 + 390), zero broken images. Ran council review → produced the before-publish checklist above.
### 2026-05-30 — Setup migration (earlier, Claude Code)
- Migrated toward the global Buissensis Claude setup; moved local skills toward the global skills dir.
### 2026-05-26 — Prep session
- Site was built from a Dropwork plumber template; created the Dutch content guide + chatbot. Old planning docs are in `/archive/`.

## For future agents (Claude or Codex)
- This file is the source of truth. Do not duplicate these facts into other docs — update them here.
- Before ending a session: append to the Work log and bump "Last verified".
- Claude Code's `CLAUDE.md` and its private project memory both point here.
