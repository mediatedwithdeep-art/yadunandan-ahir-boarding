# Yadunandan Ahir Boarding, Rajkot — website

A fast, photo-first website for the boarding. One HTML file, no build step, no dependencies,
no framework, **no webfont**. Open `index.html` in a browser and it works.

```
ahir-boarding/
├── index.html              the entire site (68 KB)
├── DESIGN.md               design decisions and per-section notes
├── CONTENT-CHECKLIST.md    the 21 facts to confirm before going live
└── assets/
    ├── brand/              logo, cream logo, emblem
    └── images/
        └── README.md       the 8 photos used, with a brief for each
```

## Built for someone who has thirty seconds

Most visitors will not read a long page. This one is ordered so the answer arrives before the
scrolling does:

1. **Hero** — what it is, in one line. Three buttons: Photos, Fees, Enquire.
2. **Four quick facts** — boys only, pure vegetarian, own study desk, CCTV and warden.
3. **Photos** — immediately. This is what people came for.
4. Food → Rooms → Facilities → Fees → How to apply.
5. **Details** — rules, routine, eligibility, documents and FAQ, all collapsed. Open only
   what you need.
6. Contact.

The mobile page is roughly **a third the length** it was before, and a bar pinned to the bottom
of the screen keeps Call, WhatsApp and Photos one thumb away at all times.

## Assets are in the repo

The logo and five photographs were recovered from the session transcript and written into the
repo — nothing to save by hand. The header emblem was cropped from the logo (the full lockup is
unreadable at 38px), and everything was resized and compressed for mobile data.

| File | Size | Used for |
|---|---|---|
| `assets/brand/logo.png` | 63 KB | Footer lockup |
| `assets/brand/logo-cream.png` | 82 KB | WhatsApp/Facebook link previews |
| `assets/brand/emblem.png` | 17 KB | Header mark and browser tab |
| `assets/images/building-dusk.jpg` | 165 KB | Hero background + photo wall |
| `assets/images/study-hall.jpg` | 122 KB | Photo wall |
| `assets/images/corridor.jpg` | 148 KB | Photo wall |
| `assets/images/ground-aerial.jpg` | 277 KB | Photo wall |
| `assets/images/ground-cricket.jpg` | 222 KB | Photo wall |

Total assets: **1.1 MB**, and only the hero image loads eagerly — the rest are lazy.

## Three photos are still needed

The page now uses **8 photos instead of 32** — only the ones that actually persuade a family.
Three are missing, and they are the three that matter most:

| File | Why it matters |
|---|---|
| `assets/images/room.jpg` | **The single most important missing photo.** Every parent wants to see where their son sleeps. |
| `assets/images/dining.jpg` | The dining hall at meal time. |
| `assets/images/thali.jpg` | An actual served thali. Used twice — the Food section and the photo wall. One honest photo of the food beats any paragraph about it. |

Drop them in at those filenames and they appear automatically. Until then each slot shows a
labelled placeholder stating the shot needed — never a broken image, never a stock photo.
Those three are the only placeholders left on the page.

## Two more things

**1. Fill in the contact details.** Open `index.html`, find the `SITE` object near the bottom:

```js
const SITE = {
  phone:    "+919876543210",      // office number, with country code
  whatsapp: "919876543210",       // digits only — no +, no spaces
  email:    "office@example.org",
  mapQuery: "Yadunandan Ahir Boarding, Rajkot, Gujarat"
};
```

One edit activates every Call button, every WhatsApp link, the enquiry form and the map.
Until then those buttons are inert **by design** — better than pointing somewhere wrong.

**2. Replace the placeholder content.** Every unverified fact is marked with a dotted gold
underline and a ◇. All 21 are in `CONTENT-CHECKLIST.md`. Add `?review=1` to the URL, or press
**Alt + P**, to see the list as a panel on the site itself.

## What changed in this revision

- **Two wrong facts removed.** "Two sharing" is gone — Rooms is now one block with the
  configuration marked pending rather than invented tiers. "Evening snack" is gone — the meal
  table lists breakfast, lunch and dinner, with a note to confirm the full schedule.
- **The font was dropped, not swapped.** No webfont at all now: the page uses each device's own
  system typeface. It renders instantly, never reflows, and shows Gujarati on every device
  without a second download.
- **Animations removed.** No scroll reveals, no pulsing dot, no bobbing arrow. What is left is
  functional only: buttons, the accordion arrow, the menu drawer, the photo viewer.
- **Glow removed.** The radial glows behind the hero, the gold halos and the drop shadows are
  gone. Flat colour and 1px borders do the work.
- **The page was cut hard.** 20 sections became 9, 32 photos became 8, and everything text-heavy
  moved into collapsed accordions.

## Deploying

Static site — any host works. For GitHub Pages, serve this folder (or move `index.html` and
`assets/` to the repository root) and point Pages at that branch. Then update the two absolute
URLs in the `<head>` — `<link rel="canonical">` and `og:url` — to the final domain.

## Verified

Rendered in Chromium at 375 / 768 / 1440 px: no horizontal overflow, no console errors, and 14
functional and accessibility assertions passing — focus trapping and restoration on the menu and
photo viewer, Escape and arrow keys, form validation by text and border rather than colour alone,
accordions closed by default, and every tap target at least 44 px.

Contrast is measured, not assumed. Gold is split into two tokens because `#A8781F` is fine for a
rule (3.91:1) but fails as text; `#8A6318` (5.41:1) is the only gold allowed to carry words on a
light background.
