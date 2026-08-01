# Photos — Yadunandan Ahir Boarding, Rajkot

The page uses **8 photographs**, down from 32. Only the ones that actually persuade a family
were kept — a shorter page with eight good photos beats a long one with thirty-two slots.

Drop a real file in at the exact path and it appears automatically — no code change. Until
then that slot shows a labelled placeholder stating the shot needed, so the page never shows
a broken image and never shows a stock photo.

---

## In the repo already

Recovered from the session transcript, resized and compressed. Nothing to save by hand.

| Path | Aspect | Used for |
|---|---|---|
| `assets/images/building-dusk.jpg` | 1852:853 | Hero background + photo wall |
| `assets/images/study-hall.jpg` | 1:1 | Photo wall |
| `assets/images/corridor.jpg` | 1:1 | Photo wall |
| `assets/images/ground-cricket.jpg` | 1:1 | Photo wall |
| `assets/images/ground-aerial.jpg` | 1:1 | Photo wall |

All are JPEG, quality ~82, under 300 KB each. The CSS crops them to each aspect ratio.

### Brand

| Path | Notes |
|---|---|
| `assets/brand/logo.png` | Full lockup, transparent background — footer |
| `assets/brand/logo-cream.png` | Cream background — social link previews |
| `assets/brand/emblem.png` | Cropped from the logo — the Krishna figure, square, 192px. The full lockup is unreadable at 38px, so the emblem alone is used in the header. |

If `emblem.png` is ever removed the header falls back to a lettermark, not a broken image.

---

## Still needed — 3 photographs

These three are the highest-value shots on the whole site.

| File | Aspect | Shot |
|---|---|---|
| `room.jpg` | 1:1 | STILL NEEDED — a student room: beds made, cupboards, study table. Square, min 600×600. |
| `dining.jpg` | 1:1 | STILL NEEDED — dining hall at meal time. Square, min 600×600. |
| `thali.jpg` | 1:1 | STILL NEEDED — an actual served thali on a mess table. Square, min 600×600. |

**Shoot the room photo first.** Every parent wants to see where their son sleeps, and it is
the one thing the page currently cannot show. **The thali photo is second** — it appears twice
(the Food section and the photo wall), and one honest photo of the actual food does more than
any paragraph about it.

---

## Shooting guidance

The five supplied photographs set the standard: real, in use, unretouched, properly lit.

- Shoot in daylight where possible; avoid flash. Turn interior lights on.
- Photograph the hostel **as it is today** — do not stage, borrow or download images.
- Wipe surfaces and make the beds first; that is honest, not misleading.
- Get written consent before publishing any photo where a student's face is identifiable.
  For minors, consent must come from a parent or guardian.
- Export as JPEG, quality ~80, each file **under 300 KB**. One 4 MB photo undoes a page built
  to load fast on mobile data.

## Alt text

Every `<img>` carries descriptive `alt` text. When you replace a photo, check the `alt` still
describes what is actually in the new picture.
