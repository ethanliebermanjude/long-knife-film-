# Long Knife — longknifefilm.com — Build Plan

**Status:** Draft v1 — for Greg's review
**Author:** Claude Code (working with Greg Palast)
**Date:** 2026-05-14

---

## 1. What we're building

A standalone, modern, cinematic website for the documentary **Long Knife** at **longknifefilm.com**, replacing the current page at palastinvestigativefund.org/long-knife-documentary.

**V1 goal:** ship a single, high-impact landing page that drives three actions, in priority order:
1. Watch the trailer
2. Donate (via existing Donorbox)
3. Subscribe for screening updates (into the existing Palast list)

---

## 2. Locked decisions

| Decision | Choice |
|---|---|
| Framework | **Astro** (static site, fast, content-friendly) |
| Scope (v1) | **Single long landing page** |
| Visual direction | **Cinematic dark / film-noir** |
| Trailer host | **YouTube** (embedded) |
| Donations | **Keep Donorbox** (embed existing forms) |
| Newsletter | **Funnel to existing Palast list** with a "Long Knife" tag |
| Assets in hand | Trailer, stills, key art/poster, EPK — all available |

## 3. Open decisions / dependencies

| Item | Why it matters | Owner |
|---|---|---|
| **Newsletter integration mechanics** | Need to know which platform powers the Palast list (Mailchimp? ConvertKit? Substack? CRM?) so we can wire the form correctly | Greg to confirm |
| **Git repo URL** | Vercel is connected to a git repo already — need the remote URL (GitHub/GitLab) so this local folder can be wired up to it | Greg to provide |
| **Osage consultation** | The film centers the Osage Nation. Strongly recommend a content/imagery review by Chief Standing Bear's office before launch — they are a producer of the film. | Greg to coordinate |
| **YouTube URL for the trailer** | Need the actual video ID to embed | Greg to provide |
| **Donorbox embed codes** | Need the two existing embed codes ("Support the Film" + "Get a Screen Credit") | Greg to provide |

---

## 4. Site architecture — the single landing page

Top to bottom, the v1 page will have these sections:

### 4.1 — Hero
- Full-viewport, dark
- **Trailer**: YouTube embed front and center (option: poster image with a play overlay, expanding to full embed on click — keeps initial page light)
- Title treatment: **LONG KNIFE** in a heavy condensed display face
- Sub-line: "A true crime documentary"
- Credit line: "Narrated by Robert De Niro"
- Tagline overlay: *"A gang so powerful they don't operate on the street… they work from Koch Oil corporate headquarters."*
- Two primary CTAs anchored bottom: **Watch the trailer** / **Support the film**

### 4.2 — Pull quote
- Full-bleed, dark, single line of large type:
  *"Behind every great fortune is a great crime. This is the crime."*
- Scroll-driven fade-in

### 4.3 — Synopsis / The story
- Two- or three-paragraph synopsis frame
- Positioning line: **"The documentary sequel to *Killers of the Flower Moon*"**
- Surrounded by key stills (Osage land, Koch infrastructure, archival evidence)
- Subtle parallax on the imagery

### 4.4 — The Osage story
- A short, respectful section that centers Osage sovereignty — not just Koch villainy
- Photography of Osage Nation members and land, in their voice where possible
- This is the section to develop with Chief Standing Bear's office

### 4.5 — Cast & crew
- **Narrated by** Robert De Niro
- **Directed by** David Ambrose
- **Written & Produced by** Greg Palast
- **Produced by** David Ambrose, Stephen Nemeth, George DiCaprio, Geoffrey Standing Bear
- **Starring** Principal Chief Geoffrey Standing Bear, Everett Waller, Joe Ben Mashunkashey, FBI Agent Jim Elroy, Federal Prosecutor Ken Ballen
- **With support from** Leonardo DiCaprio
- Grid of portrait stills, hover/tap reveals role + short bio

### 4.6 — Press kit (compact)
- "For press: [Download the EPK]" — single CTA to the PDF/zip
- Press contact email
- Logo lockup / still pack download
- Sized small for v1 — full press page can come later

### 4.7 — Support the film
- Donorbox embeds for **Support the Film** and **Get a Screen Credit**
- Short copy framing why it matters (independent journalism, fiscal sponsor PIF, donations are tax-deductible if applicable — Greg to confirm)

### 4.8 — Stay informed (newsletter)
- Single email field → "Get screening updates"
- Submits to Palast list with a "Long Knife" tag
- One-line confirmation message

### 4.9 — Footer
- Long Knife logo / wordmark
- Credits one-liner
- Links: Terms of Use, Privacy Policy, California Notice (carry over from existing PIF site)
- © Palast Investigative Fund 2026
- Cross-links to gregpalast.com and palastinvestigativefund.org

---

## 5. Visual direction — cinematic dark

**Mood:** thriller documentary. Severe, evidence-laden, but with reverence for the Osage subjects. Not horror, not exploitative.

**Type:**
- Display: a heavy condensed sans (think *Marfa* / *Druk Wide*) or a slab serif (think *Tiempos Headline*) — pick during mockup phase
- Body: a clean editorial sans (Inter, Söhne, or similar)

**Color:**
- Background: near-black (`#0A0908` range), not pure black — feels filmic, not generic dark mode
- Foreground: bone white (`#F5F1E8` range), not pure white — paper / archival feel
- Accent: a single rust/oil tone (deep amber/copper) used sparingly — the only color besides photography

**Photography treatment:**
- Stills get to fill the frame, mostly untreated, sometimes with a subtle film-grain or duotone in the rust/copper accent
- Koch infrastructure stills can lean into industrial coldness
- Osage portraits should be presented with respect — no overlay text crowding them

**Motion:**
- Scroll-driven reveals, sparing
- One or two parallax moments (the hero, the pull-quote handoff)
- No big swooping animations — restraint, like an opening credit sequence

I'll mock this up in HTML/CSS during the implementation phase so you can react to something real, not just words.

---

## 6. Technical plan

### 6.1 Stack
- **Astro 5+** with TypeScript
- **Tailwind CSS** for styling (fast iteration, consistent design tokens)
- **`astro:assets`** for image optimization (auto WebP/AVIF, lazy-loading, responsive sizes)
- **`@astrojs/sitemap`** for SEO
- **View Transitions API** for smooth navigation (low-cost, big modern feel)
- **Lite YouTube embed** (`@paulirish/lite-youtube`) — page stays fast, embed only loads on click

### 6.2 Repository layout
```
Long Knife Code Repo/
├─ PLAN.md                    (this file)
├─ README.md                  (setup + deploy instructions)
├─ astro.config.mjs
├─ package.json
├─ public/                    (favicon, OG image, robots.txt)
├─ src/
│  ├─ pages/index.astro       (the landing page)
│  ├─ components/             (Hero, PullQuote, Synopsis, OsageStory, Credits, PressKit, Support, Newsletter, Footer)
│  ├─ content/                (text content as MDX so non-devs can edit copy)
│  ├─ assets/                 (stills, poster, logo — version-controlled)
│  └─ styles/global.css
└─ assets-source/             (full-resolution originals — git-ignored, stored separately)
```

### 6.3 Performance budget
- Lighthouse mobile **≥ 95** on performance, accessibility, best practices, SEO
- Hero loads under 2s on a mid-tier mobile + 4G
- No web fonts blocking first paint
- Total page weight under 1.5 MB on first load (trailer thumbnail only — actual video loads on click)

### 6.4 Accessibility & SEO
- Full keyboard navigation
- Alt text on every still, prioritizing dignified descriptions of Osage subjects
- Captions on the embedded trailer (assumes Greg's YouTube upload has them)
- Open Graph + Twitter Card meta with the poster as the share image
- Schema.org `Movie` structured data so Google understands what this is
- Sitemap, robots.txt, canonical URL

### 6.5 Hosting & deployment
**Host: Vercel** — already set up and connected to the project's git repository.
- Excellent first-class Astro support
- Per-branch preview deployments out of the box
- Global edge CDN
- Free HTTPS, custom domains, image optimization included
- `longknifefilm.com` is owned and ready to point at the Vercel project

**Setup steps:**
1. Wire this local working directory to the existing git remote (clone or set remote)
2. Scaffold the Astro project, commit, push
3. Vercel auto-builds and serves a preview URL
4. Final cutover: point longknifefilm.com DNS records at Vercel (when v1 is approved)

### 6.6 What's NOT in v1 (parked for later)
- Multi-page structure (About, Press, Screenings, etc.)
- Screenings/festivals calendar with auto-updating tour dates
- Press clipping wall
- Multi-language support
- Interactive timeline of the Osage / Koch story
- CMS layer (right now, edits are made in code and committed)

---

## 7. Asset workflow

**What we need from Greg (in priority order):**
1. **Trailer YouTube URL** (or video ID)
2. **Poster / key art** — full resolution
3. **6–12 stills** that we'll feature on the page (Osage subjects, Koch infrastructure, archival, Palast on-camera)
4. **Press kit / EPK** — current PDF or zip
5. **Donorbox embed codes** for both campaigns
6. **Newsletter platform** + how to feed subscribers in
7. **Any logos** (Long Knife wordmark, PIF logo, partner logos if any)

**Where they go:**
- Lower-resolution display copies → version-controlled in `src/assets/` (Astro will optimize on build)
- Full-resolution originals → kept in `assets-source/` (git-ignored), backed up to Greg's storage of choice (Google Drive, Dropbox, etc.)

---

## 8. Phased delivery

| Phase | What ships | Who needs to do what |
|---|---|---|
| **0 — Plan approval** | This document, approved | Greg reviews + answers open questions in §3 |
| **1 — Scaffold** | Astro project initialized, deployed to a Cloudflare Pages preview URL with placeholder content | Claude scaffolds, deploys preview |
| **2 — Visual mockup** | Hero + first section styled, viewable on preview URL | Claude builds, Greg reacts |
| **3 — Full v1 build** | All sections complete with real content + assets | Greg delivers assets; Claude builds |
| **4 — Review & polish** | Osage office consultation, accessibility audit, performance pass | Greg coordinates Osage review |
| **5 — Launch** | Site live on longknifefilm.com with DNS cut over | Claude handles deploy; Greg manages DNS access |

No hard timeline — each phase moves when the prior is approved.

---

## 9. Risks to flag now

1. **Osage representation.** This is a story about a community's stolen wealth. The site should not feel like Koch-villain content with Osage faces used as evidence. Building in time for Chief Standing Bear's office to review imagery and language is non-negotiable for the launch checklist.
2. **Domain ownership uncertainty.** If longknifefilm.com isn't already owned or is locked in a registrar without easy access, deployment gets delayed. Worth resolving early in Phase 1.
3. **YouTube embed branding.** YouTube embeds carry YouTube branding and "up next" suggestions even with parameters tuned. If that becomes a problem for premiere-readiness, we can revisit Vimeo or a self-hosted hero loop later.
4. **Single-page constraint.** A landing page is the right v1, but as press starts rolling and screenings get booked, you will outgrow it. The architecture leaves room to grow into a multi-page site without a rewrite.

---

## 10. What I need from Greg to start Phase 1

To unblock scaffolding the project and standing up a preview URL:

1. ✅ Tech stack — locked (Astro)
2. ✅ Visual direction — locked (cinematic dark)
3. ✅ Scope — locked (single landing page)
4. ✅ Domain — owned
5. ✅ Hosting — Vercel, already connected to the git repo
6. ⬜ **Git remote URL** so this local folder can be wired up
7. ⬜ This plan approved or noted for revision

Once the remote URL is in, I can scaffold the repo and have a Vercel preview URL up the same session.
