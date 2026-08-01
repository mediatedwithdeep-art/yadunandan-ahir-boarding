# Yadunandan Ahir Boarding, Rajkot — Design Notes

Companion to `index.html`. Every value here is the value actually in the build.

---

## The brief that shaped this revision

> "everyone have not time to watch full website and read every thing — make they see site for
> the see hostels photo and food and other required details"

That is a hard constraint, and it invalidated the first build. The first version was a long,
disclosure-heavy page: twenty sections, a thousand words of argument, scroll animations,
thirty-two photo slots. It was designed for a parent who reads everything. Most people do not.

**The rebuild inverts the order: show, then tell, then explain only on request.**

| | Before | After |
|---|---|---|
| Mobile page height | ~32,000 px | ~9,000 px |
| File size | 120 KB | 68 KB |
| Sections | 20 | 9 |
| Photo slots | 32 | 8 |
| Webfonts | 1 (Fraunces) | 0 |
| Scroll animations | 40+ staggered reveals | none |
| Placeholders to fill | 43 | 21 |

Nothing true was deleted. Rules, routine, eligibility, documents and FAQ are all still there —
they moved into a collapsed accordion, so they cost a tap instead of a thousand pixels of scroll.
Transparency was the first build's whole thesis and it survives; it just stopped being mandatory
reading.

---

## Page order, and why

1. **Hero** — one line of what it is, three buttons. No essay.
2. **Four quick facts** — boys only · pure vegetarian · own study desk · CCTV and warden. The
   four things every family asks first, answered before any scrolling.
3. **Photos** — third on the page, because the user said this is what people come for. Eight
   tiles, tap to enlarge.
4. **Food** — the second question after safety. Photo first, four bullets, meal table.
5. **Rooms · Facilities · Fees · How to apply** — short, scannable, one screen each.
6. **Details** — rules, routine, eligibility, documents, FAQ, about. All closed.
7. **Contact** — phone, WhatsApp, email, address, map facade, five-field form.

**Facilities went from thirteen photo cards to a twelve-item icon list.** Thirteen photos of
corridors and water coolers is a lot of scrolling to prove something a one-line label proves just
as well. The photos that persuade are in the photo wall; the rest are facts, and facts scan
faster as a list.

---

## Type

**No webfont.** Fraunces is gone entirely — not swapped for another download.

```css
--font: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial,
        "Noto Sans", "Noto Sans Gujarati", sans-serif;
```

One family for everything. This means:

- **Zero bytes and zero requests.** Nothing to download on a 3G phone in Rajkot.
- **No flash of unstyled text and no reflow.** Text is final the moment it paints.
- **Gujarati renders everywhere.** The page carries the society's name, the donor's name and
  *કુમાર છાત્રાલય* in Gujarati; the stack falls through to Noto Sans Gujarati on devices without a
  system Gujarati face.
- Each device shows its own native typeface — San Francisco on iPhone, Roboto on Android, Segoe
  on Windows. Familiar rather than decorative, which suits an institution.

Hierarchy is carried by size and weight alone: headings at `clamp(23px, 4.4vw, 32px)`, weight
700, `-0.02em` tracking. Body 16px / 1.55.

---

## Motion

Everything decorative was removed:

- ❌ Scroll reveals on every section and card (was 40+ staggered fades)
- ❌ The pulsing "admissions open" dot
- ❌ The bobbing scroll arrow
- ❌ Card hover-lift transforms
- ❌ Header state transition on scroll

What is left is functional only — motion that tells you something happened:

| Interaction | Duration |
|---|---|
| Button and input colour change | 140ms |
| Accordion chevron rotate | 180ms |
| Menu drawer slide, scrim fade | 220ms / 200ms |

`prefers-reduced-motion: reduce` still collapses all of it to ~0.

## Glow and depth

- ❌ Radial "glow" gradients behind the hero → a flat two-stop dark gradient
- ❌ Gold halo on the brand mark, glowing pill border
- ❌ All three box-shadow elevation levels → 1px borders
- ❌ `backdrop-filter` blur on the header → solid white

The page now has exactly one gradient (the hero veil) and one on the photo captions. Depth comes
from borders and background steps, which cost nothing to render and never fight the photographs.

---

## Colour

Unchanged from the logo-derived palette, and still measured rather than assumed.

| Token | Hex | Where | Contrast |
|---|---|---|---|
| `--ink-950` | `#1C0F08` | Hero base, footer | white on it **18.7:1** |
| `--ink-900` | `#2A1710` | Brand mark, step numbers | white on it **17.1:1** |
| `--brand-700` | `#4A2718` | Headings | on white **13.2:1** |
| `--brand-600` | `#5C3320` | Primary button | white on it **10.8:1** |
| `--brand-500` | `#8A5433` | Focus ring | on white **6.2:1** |
| `--gold-500` | `#A8781F` | Borders and graphics — **never text** | on white **3.9:1** |
| `--gold-text` | `#8A6318` | The gold that may carry words | on white **5.4:1** |
| `--gold-400` | `#C79A3E` | Hero button | ink on it **7.2:1** |
| `--gold-300` | `#E3C078` | Text on dark | on ink-950 **10.8:1** |
| `--n-700` | `#3A3330` | Body | on white **12.4:1** |
| `--n-600` | `#4F4642` | Muted | on white **9.2:1** |
| `--n-450` | `#867B75` | Input borders | on white **4.1:1** ✅ 3:1 non-text |
| `--wa` | `#107C69` | WhatsApp actions | white on it **5.1:1** |

Two rules worth keeping in mind when editing:

1. **`--gold-500` never carries text on a light surface.** 3.91:1 fails AA. Use `--gold-text`.
2. **WhatsApp brand green is not used as-is.** `#128C7E` gives white text 4.14:1; the darkened
   `#107C69` gives 5.11:1 and still reads as WhatsApp.

---

## Two factual corrections

- **"Two sharing" removed.** It was wrong. Rather than guess what replaces it, Rooms is now a
  single block — what every student gets — with the sharing configuration marked pending. An
  invented room tier on a fees page is exactly the kind of thing a family checks and catches.
- **"Evening snack" removed.** The meal table is breakfast, lunch and dinner, with an explicit
  note to confirm the full daily schedule.

Both are in `CONTENT-CHECKLIST.md` as open items.

---

## Accessibility

Nothing was traded away for the shorter page.

- **Contrast** computed for every pair, including after the palette change.
- **Keyboard:** skip link; 3px focus ring on everything; the menu drawer and photo viewer trap
  Tab and restore focus to whatever opened them; Escape closes both; arrow keys move between
  photos.
- **The accordion is native `<details>`/`<summary>`.** No JavaScript, correct semantics for
  screen readers by construction, works with JS disabled, and findable by browser find-in-page
  when open. Height is not animated — animating height costs layout every frame, and an
  accordion that snaps open feels faster.
- **Targets** ≥44px everywhere; the bottom bar is 58px.
- **Forms:** real labels, `autocomplete`, `inputmode="numeric"` on the phone field, errors shown
  by text *and* border *and* `aria-invalid` — never colour alone. 16px inputs, because anything
  smaller makes iOS Safari zoom on focus and jump the layout.
- **Gujarati runs marked `lang="gu"`** so screen readers switch voice instead of reading the
  script as English phonetics.
- **Images:** explicit `width`/`height` and fixed `aspect-ratio` on every media box, so layout
  never shifts — including while photos are still missing.

## Performance

- One file, no framework, no CDN, no icon library, **no webfont**. Icons are inline SVG.
- Hero image `fetchpriority="high"`; everything else lazy.
- Google Map is a facade — the iframe and its third-party requests load only if someone taps
  "Load map".
- The photo wall is eight images, not thirty-two. That alone is most of the weight saved.

---

## Known trade-offs

1. **The accordion hides content from people who would have read it.** A parent who *wants* the
   full rule list now has to tap. That is the deliberate trade the brief asked for; the rules are
   still complete, still public, and still ahead of the contact form.
2. **System fonts look different on every device.** The page will not be pixel-identical across
   phones. In exchange it loads instantly and never reflows — the right trade for this audience.
3. **Facilities as a list is less persuasive than photos.** If photography improves later, the
   three or four most convincing facilities could earn photo cards again — but as a considered
   addition, not a default.
4. **English only.** A Gujarati version remains the highest-value next addition. It was not
   attempted here because most of the page's specifics are still placeholders; translating
   placeholders produces two pages to fix instead of one.

## Next

1. Fill the 21 checklist items and save the eight photos. **Nothing else matters until then** —
   in particular the room photo and the thali photo.
2. Gujarati version with a language toggle and `hreflang`.
3. Once real fee figures exist, consider a single "fees at a glance" number in the quick-facts
   bar. Price is the most-searched fact and it is currently four taps deep.
