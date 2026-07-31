# Yadunanand Ahir Boarding, Rajkot — website

A complete, mobile-first admissions website for the boarding. One HTML file, no build step,
no dependencies, no framework. Open `index.html` in a browser and it works.

```
ahir-boarding/
├── index.html              the entire site
├── DESIGN.md               design system + section-by-section specification
├── CONTENT-CHECKLIST.md    the 43 facts to confirm before going live
└── assets/
    ├── brand/              logo, cream logo, emblem  ← save these first
    └── images/
        └── README.md       every photo needed, with a shot brief for each
```

## Save the supplied assets first

The logo and five photographs came through in conversation and could not be written to disk from
there. **Save them yourself at these exact paths:**

| Path | What |
|---|---|
| `assets/brand/logo.png` | Logo, transparent background — footer |
| `assets/brand/logo-cream.png` | Cream version — WhatsApp/Facebook link previews |
| `assets/brand/emblem.png` | **Crop the circular emblem out, square** — header and tab icon. The full lockup is unreadable at 40px; the emblem alone is not. |
| `assets/images/building-dusk.jpg` | The lit building at dusk — hero background |
| `assets/images/study-hall.jpg` | The partitioned study carrels — Study Environment + facility card |
| `assets/images/corridor.jpg` | The corridor with fire exit and extinguishers — Fire Safety card + gallery |
| `assets/images/ground-aerial.jpg` | Aerial of the volleyball ground — Sports card + campus band |
| `assets/images/ground-cricket.jpg` | The cricket pitch — gallery large tile |

If `emblem.png` is missing the header falls back to a lettermark rather than a broken image.

**26 photographs are still to be shot** — see `assets/images/README.md`. The biggest gaps are a
student room, the dining hall and kitchen, and one photo of a served thali.

## Then — three things

**1. Fill in the contact details.** Open `index.html`, scroll to the `SITE` object near the
bottom of the file, and set four values:

```js
const SITE = {
  phone:    "+919876543210",      // office number, with country code
  whatsapp: "919876543210",       // digits only — no +, no spaces
  email:    "office@example.org",
  mapQuery: "Yadunanand Ahir Boarding, Rajkot, Gujarat"
};
```

One edit activates every Call button, every WhatsApp link, the enquiry form and the map.
Until then those buttons are inert **by design** — better than pointing somewhere wrong.

**2. Replace the placeholder content.** Every fact that could not be verified is marked on
the page with a dotted gold underline and a ◇ symbol. All 43 are listed in
`CONTENT-CHECKLIST.md`. Add `?review=1` to the URL, or press **Alt + P**, to see the list as
a panel on the site itself.

**3. Add the photographs.** Drop real JPEGs into `assets/images/` at the filenames listed in
`assets/images/README.md`. Each one appears automatically — no code change. Until a file
exists, that slot renders a labelled placeholder stating exactly which shot is needed, so
the page never shows a broken image and never shows a stock photo.

## Two sections are intentionally empty

**Testimonials** and **Achievements** are fully built but show no quotes and no numbers.
Inventing either is the fastest way to lose a parent who checks. Publish them once you have
named, consented testimonials and figures from your own records. Both sections carry a brief
explaining what to collect.

## Deploying

It is a static site — any host works. For GitHub Pages, serve this folder (or move
`index.html` and `assets/` to the repository root) and set Pages to that branch.

Then update the two absolute URLs in the `<head>` — `<link rel="canonical">` and
`og:url` — to the final domain.

## What the supplied photographs changed

They were not just dropped in — each one carried information that corrected the page:

- The **building sign** names the managing society (શ્રી યદુનંદન આહીર કેળવણી મંડળ), confirms this
  is a **boys' hostel** (કુમાર છાત્રાલય), and names the **principal donor**, who is now
  acknowledged in the About section. Three placeholders resolved.
- The **study hall** photo shows partitioned individual carrels, not the shared tables the copy
  had assumed. The copy was corrected upward — it is a stronger claim than the one it replaced.
- The **corridor** photo shows extinguishers and marked fire exits, so Fire Safety became its own
  facility card. It also confirms the CCTV claim.
- The **cricket pitch** photo means Sports is now a cricket pitch *and* a volleyball court.

> ⚠️ The donor's name is reproduced in Gujarati exactly as it appears on the building. The
> English transliteration is marked for confirmation — getting a donor's name wrong is not a
> small error.

## How it was built

- **No live-site access.** The existing site could not be reached from the build environment
  (network policy blocks `github.io`, and that repository is outside this session's scope),
  so no existing copy, photo, fee or timing was available. Nothing was invented to fill the
  gap — every unverifiable fact is marked and listed instead.
- **Contrast is measured, not assumed.** Every colour pair was computed against WCAG 2.2.
  Three failures were found and fixed before shipping: brass `#C9922F` on white (2.75:1),
  the muted grey `#6E7C91` (4.24:1), and WhatsApp brand green with white text (4.14:1).
- **Verified in a real browser** at 375 / 768 / 1440px: no horizontal overflow, no console
  errors, no layout shift. A genuine mobile overflow bug — a 520px fee table forcing the page
  to 546px on a 375px screen — was caught this way and fixed.

Full reasoning, tokens, motion specs and per-section rationale: **`DESIGN.md`**.
