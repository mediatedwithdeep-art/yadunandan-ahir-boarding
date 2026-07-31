# Photo & brand-asset manifest — Yadunanand Ahir Boarding, Rajkot

Every file below is referenced by `index.html`. Drop the real file in at the exact path and it
appears automatically — no code change. Until then the page renders a labelled placeholder
stating the shot required, so nothing on the live site pretends to be a photo it is not.

---

## 1. Assets supplied — save these to disk

These came through in conversation and could not be written to disk from there. **Save them
yourself at these exact paths.**

### Brand

| Path | Source |
|---|---|
| `assets/brand/logo.png` | The logo on a transparent background — used in the footer |
| `assets/brand/logo-cream.png` | The cream-background version — used for WhatsApp/Facebook link previews |
| `assets/brand/emblem.png` | **Crop the circular emblem out of the logo, square** — header and browser-tab icon. The full lockup is unreadable at 40px; the emblem alone is not. |

If `emblem.png` is missing the header falls back to a lettermark, not a broken image.

### Photographs

| Path | Aspect | Used for |
|---|---|---|
| `assets/images/building-dusk.jpg` | 1852:853 — 1852×853 | Hero background (the dusk shot with the lit Gujarati name sign) |
| `assets/images/study-hall.jpg` | 8:5 — 800×500 | Study Environment section **and** the Silent Study Hall facility card |
| `assets/images/ground-aerial.jpg` | 8:5 — 800×500 | Sports facility card **and** the full-bleed campus band |
| `assets/images/corridor.jpg` | 8:5 — 800×500 | The new Fire Safety facility card **and** gallery tile 2 |
| `assets/images/ground-cricket.jpg` | 1:1 — 1000×1000 | Gallery large tile (the cricket pitch) |

Save the originals at full resolution — the CSS crops them to each aspect ratio.

---

## 2. Photographs still needed — 26 shots

| File | Aspect / min size | Shot required |
|---|---|---|
| `about-campus.jpg` | 4:3 — 1200×900 | ABOUT — the campus courtyard or main entrance with the name board visible. 4:3, min 1200×900. |
| `about-warden.jpg` | 1:1 — 600×600 | ABOUT — warden's desk with the attendance register / reception counter. Square, min 600×600. |
| `about-noticeboard.jpg` | 1:1 — 600×600 | ABOUT — notice board with timetable / rules sheet pinned. Square, min 600×600. |
| `fac-rooms.jpg` | 8:5 — 800×500 | FACILITY — student room: beds made, cupboards, study table, window light. 16:10, min 800×500. |
| `fac-library.jpg` | 8:5 — 800×500 | FACILITY — library / reading corner with books, newspapers, seating. 16:10, min 800×500. |
| `fac-mess.jpg` | 8:5 — 800×500 | FACILITY — dining hall during a meal, clean tables, serving counter. 16:10, min 800×500. |
| `fac-kitchen.jpg` | 8:5 — 800×500 | FACILITY — kitchen: clean cooking area, covered storage, staff in place. 16:10, min 800×500. |
| `fac-water.jpg` | 8:5 — 800×500 | FACILITY — RO purifier + water cooler station. 16:10, min 800×500. |
| `fac-washroom.jpg` | 8:5 — 800×500 | FACILITY — washroom / bathing area, clean and dry, taken respectfully. 16:10, min 800×500. |
| `fac-cctv.jpg` | 8:5 — 800×500 | FACILITY — CCTV camera in corridor, or the DVR monitor at the warden's desk. 16:10, min 800×500. |
| `fac-power.jpg` | 8:5 — 800×500 | FACILITY — inverter / generator installation. 16:10, min 800×500. |
| `fac-wifi.jpg` | 8:5 — 800×500 | FACILITY — router/network point, or students studying with laptops. 16:10, min 800×500. |
| `fac-firstaid.jpg` | 8:5 — 800×500 | FACILITY — first-aid cabinet / sick room bed. 16:10, min 800×500. |
| `room-shared.jpg` | 4:3 — 800×600 | ROOM — multi-sharing room, wide angle showing all beds and cupboards. 4:3, min 800×600. |
| `room-double.jpg` | 4:3 — 800×600 | ROOM — two-sharing room with two beds and two study tables. 4:3, min 800×600. |
| `room-single.jpg` | 4:3 — 800×600 | ROOM — single room with one bed, table and cupboard. 4:3, min 800×600. |
| `gal-01.jpg` | 1:1 — 1000×1000 | GALLERY 1 (large tile) — full building exterior with name board. Square crop, min 1000×1000. |
| `gal-03.jpg` | 1:1 — 600×600 | GALLERY 3 — study hall occupied during study hours. Square, min 600×600. |
| `gal-04.jpg` | 1:1 — 600×600 | GALLERY 4 — dining hall at meal time. Square, min 600×600. |
| `gal-05.jpg` | 1:1 — 600×600 | GALLERY 5 — student room, made bed, tidy desk. Square, min 600×600. |
| `gal-07.jpg` | 1:1 — 600×600 | GALLERY 7 — morning assembly / prayer gathering. Square, min 600×600. |
| `gal-08.jpg` | 1:1 — 600×600 | GALLERY 8 — library reading area. Square, min 600×600. |
| `gal-09.jpg` | 1:1 — 600×600 | GALLERY 9 — annual function / festival celebration on campus. Square, min 600×600. |
| `gal-10.jpg` | 1:1 — 600×600 | GALLERY 10 — clothes washing / drying area. Square, min 600×600. |
| `food-thali.jpg` | 4:3 — 1200×900 | FOOD — an actual served thali on a mess table: rotli, shaak, dal, bhaat, salad. 4:3, min 1200×900. |
| `achievements-felicitation.jpg` | 8:5 — 800×500 | ACHIEVEMENTS — felicitation ceremony, prize distribution, or the trophy shelf. 16:10, min 800×500. |

---

## Shooting guidance

The five supplied photographs set the standard: real, in use, unretouched, properly lit.
Match them.

- Shoot in daylight where possible; avoid flash. Turn interior lights on.
- Photograph the boarding **as it is today** — do not stage, borrow or download images.
- Wipe surfaces and make the beds first; that is honest, not misleading.
- Get written consent before publishing any photo in which a student's face is identifiable.
  For minors, consent must come from a parent or guardian.
- Export as JPEG, quality ~80, each file **under 300 KB**. One 4 MB photo undoes a page built
  to load fast on mobile data.
- Optionally export a `.webp` beside each `.jpg` and switch the `<img>` to `<picture>` for a
  further ~30% saving.

## Highest-value shots still missing

1. **A student room** — the single thing every parent wants to see and the one gap left in the
   Rooms section. Three shots: shared, two-sharing, single.
2. **The dining hall and kitchen** — the second-biggest parental question after safety.
3. **A served thali** — one honest photo of the actual food does more than any paragraph.

## Alt text

Every `<img>` carries descriptive `alt` text. When you replace a photo, check the `alt` still
describes what is actually in the new picture — screen reader users and Google both rely on it.
