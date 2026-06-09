# AGENTS.md — Tuinen Decoster website

> **Single source of truth for this project. Read this first.**
> Read by BOTH Claude Code and ChatGPT Codex. Codex reads `AGENTS.md` by default; `CLAUDE.md` points here.
> **Update the "Work log" at the bottom and the "Last verified" date at the end of every session, before switching tools.**
> Last verified: 2026-06-03.

## Status
Client-ready **DEMO** — finished and verified on desktop + mobile. **NOT yet published publicly.**
Several data points are invented and must be confirmed by the owner first (see *Real vs invented* + *Before-publish checklist*).

## What this project is
A **gardening-niche demo / sales preview** (not a specific client's live site). It shows a prospect "how a
site in your niche could look" — part of the Buissensis "free mockup first" sales approach. It began as a build
for a client (Arno), which is why the legacy "AD / ad-groenservice" names exist. Branded as the fictional
**Tuinen Decoster** (owner **Jan Decoster**), a one-man garden landscaping & maintenance business in
Brugge / West-Vlaanderen. Goal: a convincing example that drives the "I want this for my business" reaction.
Naming: GitHub repo is now **`tuinen-demo`**; the local folder is still `ad-groenservice-new` (legacy, internal only).

## Stack
- Vanilla HTML/CSS/JS in a single file `index.html` (~4200 lines, inline `<style>` + `<script>`). No build step. Node 24.x.
- AI chatbot: `api/chat.js` serverless function (Groq, model `llama-3.3-70b-versatile`). `GROQ_API_KEY` is a Vercel env var — never commit it.
- CDN libs: GSAP 3.12.5 + ScrollTrigger, Leaflet 1.9.4 (CARTO Positron tiles), Google Fonts.
- Deploy: **Cloudflare Pages**, auto-deploys on push to `master` (`adgroen/master` is the upstream, so a plain `git push` works). `adgroen` = `github.com/57gd7jymhs-spec/tuinen-demo` (renamed from AD-groenservice-template on 2026-06-02; GitHub auto-redirects the old URL).
  - Public preview URL prospects see: **`tuinen-demo.pages.dev`** (the Cloudflare project name, set up separately from the repo name).
  - ⚠️ The default `origin` remote points at the ORIGINAL template `dropwork-plumber-template` — **never push there**. (A legacy `.vercel/` config also exists; Cloudflare is the live host.)

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

## Template-site asset direction
- For generated assets across these trade/template sites, prioritize modern, premium, clean, professional residential photography. Favor bright natural light, clean architecture, polished interiors, tidy utility rooms, modern bathrooms/kitchens/carports/driveways, realistic local-business credibility, and crisp natural colors.
- Reject assets that look cheap, outdated, cluttered, dark, dirty, random-stock, or obviously AI-generated. Avoid ugly brick exteriors, poor lighting, warped tools/pipes/faucets/tiles/vehicles/hands, plastic skin, strange eyes, fake uniforms/logos, unreadable text, fake signage, impossible reflections, excessive blur, overdramatic HDR, and overly perfect showroom scenes unless specifically needed.
- Before/after assets must be slider-ready matched pairs: same exact location, framing, camera angle, camera height, lens perspective, object positioning, and lighting family; only the work result should meaningfully change. Generate as matched diptychs when helpful, then split/crop into separate before and after files.
- Person images should feel like real local business photography: natural expression, normal skin texture, believable posture/hands, practical work clothing, professional but not model-like or overly staged, no fake branding.
- Prompt every asset with explicit constraints for modern setting, clean realistic composition, natural daylight, professional photography, clear subject, no text/fake branding, and no AI artifacts. Prefer fewer stronger images over many weak fillers.

## Work log (newest first — append every session, date it)
### 2026-06-09 — Professional copy pass: "tuinman" → "tuinspecialist" (Claude Code)
- Pre-client copy polish on root `index.html`. Owner title elevated from casual "uw (vaste) tuinman" to **"uw vaste tuinspecialist"** across all 14 visible/meta/structured instances (meta description, OG, JSON-LD, hero meta, hero sub, about heading, "Even voorstellen" section, footer brand line, chatbot header + greeting + "Over Jan" answer, image alt/aria labels). Service-card line "Vaste prijs, vaste tuinman" → "Vaste prijs, vast aanspreekpunt".
- Full owner name **Jan Decoster** now used in hero meta, hero sub, about heading, footer, and alt text (was bare "Jan"). Hero sub tightened: "ik hou … netjes" → "ik houd … het hele jaar verzorgd" + "dezelfde vertrouwde persoon aan de lijn".
- Left the two chatbot keyword *matchers* (`tuinman sturen`) untouched — they match what a user might type, not displayed copy. No em dashes exist in visible copy (only in CSS/JS comments).
- Two-pass verified (1440 + 390): about heading wraps cleanly ("Ik ben Jan Decoster," / "uw tuinspecialist."), hero + mobile no regressions. Shots in `.screenshots/copy-pass/`. Not yet committed/pushed.
- **Mobile before/after CTA clip fix:** the `.ba-case` mobile rule had a fixed `height: clamp(380px,60vh,500px)` under `overflow:hidden`, which clipped the CTA's bottom padding when the green info panel ran taller than the cap. That cap was originally added to clear the sticky bottom call bar — but that bar was removed in the 2026-06-03 mobile pass, so the constraint was stale. Removed the fixed height (card sizes to content) and moved the flex-grow to the image (`.ba-slider-wrapper` min-height `clamp(220px,40vh,320px)`) so all carousel cards still match the tallest. Verified: all 5 cards 624px, consistent 20px button bottom gap, no clip. Desktop grid layout untouched (mobile-only media query). Shots in `.screenshots/ba-mobile-fix/`.

### 2026-06-09 — Image performance optimization (Claude Code)
- **Root cause of slow load:** `assets/` was ~68MB of uncompressed PNGs (most 2–4MB each, dimensions ~1500px). Converted all 21 referenced images to WebP (longest edge capped 1600px, quality 80, via `sharp` — installed then removed, not a runtime dep). **59.1MB → 5.44MB of imagery, 91% smaller**, no visible quality loss (two-pass verified hero + services + before/after at 1440).
- Swapped all 56 `.png` refs in `index.html` to `.webp` (`Detail shot.png` → clean `detail-shot.webp`). `og:image` + JSON-LD `image` now point to a dedicated `jan-owner-og.jpg` (1200px, 132KB) since some social scrapers still choke on WebP.
- Added `loading="lazy"` to 23 below-fold images (services "Wat Jan doet", before/after carousel, review avatars, chatbot); hero poster + main owner photo kept eager for fast first paint.
- **Repo slimming:** removed all 25 source PNGs from git (21 converted + 4 dead/unreferenced: `Correct picture jan owner.png`, `closup picture jan correct owner…png`, `jan-portrait.png`, `before-moss.png`). `assets/` now 5.7MB total (was 68MB). Masters remain in git history if ever needed.
- Network verified: all 21 WebP load 200, zero 404s. Shots in `.screenshots/perf-webp/`.

### 2026-06-04 — Template system cleanup (Claude Code)
- Full inventory and council-reviewed architecture plan for the Buissensis template factory.
- **ad-groenservice-new cleanup:** Deleted `styles.css`, `main.js`, `components/`, `images/`, `.vercel/` (55 files, 1732 deletions) — pre-flight grep confirmed zero references in `index.html`. Pushed to `adgroen/master` (commits `6786b0c`, `30e3613`).
- **Asset library:** Moved `handyman-assets/`, `locksmith-assets/`, `moving-company-assets/`, `window-cleaner-assets/` (≈170MB) to `C:\Users\Apollo\Desktop\Buissensis\websites\shared-assets\`. Zero git changes (all gitignored).
- **Temp demos:** Ported electrician and painter image-prompt docs to `buissensis-template/content-packs/elektricien.md` and `schilder.md`. Deleted `electrician-site-temp/` and `painter-site-temp/` folders.
- **gitignore:** Simplified to remove stale entries; `ad-groenservice-assets/` now properly ignored.
- **buissensis-template sync (Phase 5):** Ported mobile polish delta from this `index.html` into `buissensis-template/template/index.html` — mobile speed-dial FAB CSS + HTML + JS, legal modals CSS + HTML + JS, mobile logo-only header, BA top-align + footer pin, service pill scroll behavior. Template retains existing `[TODO]` scaffold (no overwrite).
- **REBRAND.md:** Added section −1 covering GitHub repo setup, Cloudflare Pages connection, shared-assets copy step, and remote verification.
- **Architecture decisions (council-reviewed):** Per-site repos (no monorepo); shared-assets local-only (not committed); template IS the canonical base — gardening site cherry-picks improvements to the template, not vice versa.

### 2026-06-03 — Index-only legal footer deploy (Codex)
- Deployed only root `index.html` to `adgroen/master` in commit `9506a71` (`feat: add legal footer dialogs`), adding footer legal links, modal legal/privacy content, and chatbot data-transfer disclosure.
- Left the generated industry asset folders (`window-cleaner-assets`, `handyman-assets`, `locksmith-assets`, `moving-company-assets`) untracked/local and did not include them in the deployment.
- Verified `https://tuinen-demo.pages.dev/` returns 200 and contains the new legal footer/dialog markup.

### 2026-06-03 — Mobile polish (12 fixes) + header refinements (Claude Code)
- Council-reviewed 12 mobile issues, implemented, then two-pass verified (desktop 1440 + mobile 390):
  (1) loader/video overlap → removed the always-on bottom call bar on mobile; (2) contact UX → mobile **speed-dial FAB** (Bel / WhatsApp / Stel een vraag), gently pulsing, replaces the bar; the standalone chat bubble folds into it; (3) header→marquee spacing widened; (4) tiny inline avatar hidden on mobile (kept on desktop); (5) before/after **dots now sit within the viewport** (card height → 60vh); (6) `ScrollTrigger.refresh` only on width change → kills the iOS address-bar scroll hitch (no `pin:` anywhere, so safe); (7) reload always lands at top + **intro plays once per session** (sessionStorage + `prefers-reduced-motion` skip); (8) tapping a service tag smooth-scrolls to the contact buttons + pulses them; (9) review cards no longer text-select on drag; (10) FAQ tap-highlight / press outline removed (keyboard focus kept); (11) final-CTA shows Jan as a **large avatar above the heading** (buttons stay in the fold); (12) white line at the page bottom fixed (`body` padding removed + dark `html` bg).
- Header refinements: mobile header shows the **logo mark only** (wordmark stays in the loader, footer, and desktop); mobile content side padding 5% → 6.5%.
- Desktop verified unchanged. Screenshots in `.screenshots/mobile-fixes/`. Skill hygiene: `find-skills` installed globally; removed the deprecated per-project `.agents/` + `.claude/skills/` + `skills-lock.json`. Also gitignored `painter-site-temp/`.

### 2026-06-02 — Painter temp site + asset set (Codex)
- Created `painter-site-temp` as a Kleurvast Schilderwerken painter concept based on the electrician/gardener structure, with painter-specific Dutch copy, placeholder business details, warm painter palette, inline brush mark, and local image references.
- Generated 21 active `v2-` painter assets: hero, owner full/closeup, six service images, two review/project images, and five matched before/after pairs created from diptychs and split into slider-ready files.
- Added painter docs: `docs/painter-assets-manifest.md`, `docs/painter-content-map.md`, `docs/painter-image-prompts.md`, and `REVIEW-NOTES.md`. Verified 21 unique image references, no missing assets, and captured desktop/mobile Playwright screenshots plus an asset contact sheet.

### 2026-06-02 — GitHub deployment push (Codex)
- Prepared the current local Tuinen Decoster changes for GitHub deployment and pushed via the safe `adgroen/master` remote so Cloudflare Pages can redeploy `tuinen-demo.pages.dev`.

### 2026-06-02 — Template asset direction + electrician v2 asset set (Codex)
- Added reusable template-site visual direction: modern premium realistic photography, no cheap/dated/obvious-AI assets, person-image constraints, and strict matched before/after slider rules.
- Rebuilt the electrician concept assets in `electrician-site-temp` with 21 active `v2-` referenced images, matching the original gardener site's 21 unique local image references.
- Generated five matched before/after diptychs and split/cropped them into slider pairs for panel upgrade, socket/switch replacement, renovation wiring, kitchen lighting, and EV charger install. Verified active electrician page uses only `v2-` images and all local references exist.

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
