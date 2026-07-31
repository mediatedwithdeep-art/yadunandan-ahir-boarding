# Yadunanand Ahir Boarding, Rajkot — Design Specification

Companion to `index.html`. Every value here is the value actually in the build, not a
description of one.

---

## 0. The strategic call

**Product goal:** more completed admission enquiries from parents.
**User goal:** two different people, one page.

| | Student (16–22) | Parent (40–55) |
|---|---|---|
| Device | Phone, almost always | Phone, sometimes a relative's laptop |
| Wants to know | Where do I sleep, what's the food, is there Wi-Fi, is it strict | Is he safe, will he study, what does it cost, who is responsible |
| Decides on | Photos | Rules, fees, and whether the site hides anything |

The parent signs the cheque, so the page is written for the parent and photographed for the
student. Everything a parent would have to phone to find out — rules, fees, in-time, refund
policy — is on the page before the CTA, not behind it.

**The one metric:** completed WhatsApp enquiries (name + phone captured). Not visits, not
time-on-page.

**Conversion thesis:** a boarding is bought on *trust*, and trust here comes from
**disclosure**, not adjectives. Publishing the full rule list, the exact fee heads, and
what is *not* included is a stronger conversion lever than any hero animation. That is why
"Rules & Discipline" is a full dark section rather than a footer link — a family that reads
all ten rules and still enquires is a family that will actually enrol.

**The honest constraint:** the live site could not be reached from this environment
(network policy blocks `github.io`, and that repository is outside this session's scope), so
almost no real content was available. Nothing was invented to fill the gap.

What *is* real, from assets supplied directly: the institution's name (**Yadunanand Ahir
Boarding**), its motto (**Discipline · Education · Excellence**), its logo and therefore its
brand palette, its managing society and principal donor (both legible on the building sign),
confirmation that it is a boys' hostel, and five photographs. The remaining **43 unverifiable
facts** are marked on the page and listed in `CONTENT-CHECKLIST.md`.

**A photograph is not just an asset — it is evidence, and evidence outranks copy.** Where a
supplied photo contradicted or exceeded what the copy claimed, the copy was rewritten to match
the photo, not the other way round. The study hall turned out to have partitioned individual
carrels rather than shared tables, so that section now makes the stronger, truer claim; the
corridor photo showed extinguishers and marked fire exits, which earned Fire Safety its own
facility card.

---

## 1. Design system

### Colour — derived from the logo, measured not asserted

The palette is taken from the institution's own logo: deep brown, temple gold, cream. The
first build used navy and brass; once the real logo arrived, navy would have clashed with
the mark sitting directly above it in the header, so the whole palette was rebuilt. Token
*names* were kept, so the swap was values-only and no component CSS changed.

| Token | Hex | Where | Contrast |
|---|---|---|---|
| `--ink-950` | `#1C0F08` | Hero base, footer, band scrim | white on it **18.7:1** |
| `--ink-900` | `#2A1710` | Rules section | white on it **17.1:1** |
| `--brand-700` | `#4A2718` | All headings | on white **13.2:1** |
| `--brand-600` | `#5C3320` | Primary button, links | white on it **10.8:1** |
| `--brand-500` | `#8A5433` | Focus ring only | on white **6.2:1** |
| `--brass-500` | `#A8781F` | Rules, borders, graphics — **never text** | on white **3.9:1** |
| `--brass-text` | `#8A6318` | Eyebrows — the gold that *may* carry words | on white **5.4:1** |
| `--brass-400` | `#C79A3E` | Hero CTA background | ink-950 on it **7.2:1** |
| `--brass-300` | `#E3C078` | Accent text on dark | on ink-950 **10.8:1** |
| `--n-700` | `#3A3330` | Body copy | on white **12.4:1** |
| `--n-600` | `#4F4642` | Muted copy | on white **9.2:1** |
| `--n-450` | `#867B75` | Input borders | on white **4.1:1** ✅ non-text 3:1 |
| `--parchment` | `#FDF6EA` | Alternating sections | body on it **11.5:1** |

Four decisions worth naming:

1. **Gold is split into two tokens.** `--brass-500` (`#A8781F`) is **3.91:1** on white — fine
   for a rule or an icon, a fail for text. `--brass-text` (`#8A6318`) is **5.41:1** and is the
   only gold allowed to carry words on a light surface. Collapsing these into one "gold" is
   how premium palettes ship inaccessible.
2. **The warm ramp forced one fix.** `--n-500` measures **3.11:1** on `--ink-950` — it had been
   4.6:1 in the navy ramp. The footer's bottom line was moved to `--n-400` (**6.99:1**).
   Swapping a palette silently breaks pairs that used to pass; every pair was recomputed, not
   assumed to carry over.
3. **The header CTA changes state over the hero.** A solid brown button on the brown hero has
   almost no separation from its background, even though its *text* contrast is 10.8:1.
   Over the hero it becomes a gold outline — visible, and correctly secondary to the solid
   gold primary in the hero itself.
4. **WhatsApp green stays `#107C69`.** Brand `#128C7E` gives white text **4.14:1**. The
   darkened value is **5.11:1** and still unmistakably WhatsApp.

Brown/gold/cream also does the job navy was doing — brown carries institutional weight, gold
carries the warmth and the Krishna/temple association already present in the mark — without
the site and its own logo pulling in two directions. Accent stays under ~10% of any surface.

### Type

- **Display:** Fraunces variable (`opsz 9–144`), `SOFT 0, WONK 0` — the quirk dialled out so
  it reads institutional, not novelty. 400/600/700 only.
- **Body:** the system UI stack. **Zero bytes, zero FOUT, zero layout shift** — on a 3G phone
  in Rajkot that is worth more than a second webfont.
- Scale: `12 / 13.5 / 15 / 16 / 18 / 20 / 24 / 32 / 44 / 68`, headings via
  `clamp()` so there is no step-jump at breakpoints.
- Body 1.6 line-height; headings 1.06–1.15. Display type at `-0.025em`; all-caps eyebrows at
  `+0.1em`. Body copy capped at `62ch`, `text-wrap: balance` on headings.

### Spacing & layout

4/8pt scale only: `4 8 12 16 24 32 48 64 96 128`. No arbitrary value appears anywhere.
Container `1200px`, gutters `24px`. Breakpoints `640 / 768 / 900 / 960 / 1024 / 1100 / 1200`.
CSS Grid for all section layouts; Flexbox only inside components.

### Motion

| Interaction | Duration | Easing |
|---|---|---|
| Button hover, focus, input border | 140ms | `cubic-bezier(.16,.84,.44,1)` |
| Card lift, accordion chevron, header state | 260ms | ease-out |
| Drawer slide, scroll reveal | 420ms | ease-out |

Only `transform` and `opacity` are animated — never `box-shadow`, `height` or `width`.
Reveal stagger is `60ms` per card, capped at three steps; longer chains read as slow.
`prefers-reduced-motion: reduce` kills every animation and switches `scroll-behavior` to
auto — not reduced, *off*.

### Performance decisions

- One HTML file, no framework, no CDN script, no icon library. Icons are inline SVG.
- Every `<img>` carries explicit `width`/`height` and every media box a fixed
  `aspect-ratio` → **CLS ≈ 0** even while photos are still missing.
- Google Map is a **facade** — a static panel with a "Load Google Map" button. The iframe
  (~900 KB and several third-party requests) is never fetched unless a user asks for it.
- `backdrop-filter` appears on exactly one element (the header) behind a `@supports` guard.
  It is the expensive effect in this build and is confined to a 64px bar rather than a
  scrolling list.
- Hero image `fetchpriority="high"`; everything else `loading="lazy" decoding="async"`.

---

## 2. Sections

Format per the brief: **Goal · Layout · Animation · Content · Images · CTA · Mobile.**

---

### 1 — Hero
**UX goal.** Answer "what is this and is it for me" in under three seconds, and put the
primary action inside the thumb zone before any scroll.
**Layout.** Full-bleed dark stage. Photo at 40% opacity under a three-stop veil (brown radial,
gold radial, vertical fade to `--ink-950`) — so the headline is legible over *any*
photograph the boarding later supplies, including a badly exposed one. Content left-aligned
in a 52rem column; four-item trust row on a gold hairline rule.
**Animation.** Availability dot pulses 2.4s. Scroll chevron bobs 2s. Nothing blocks reading;
no hero entrance animation, because a delayed headline is a delayed decision.
**Content.** The institution's own motto — *Discipline · Education · Excellence*, lifted from
the logo ribbon — sits above the headline in gold small-caps. Then *"A disciplined home for
students who came to Rajkot to study."*: the place, the city and the promise in one line. Sub-copy leads with safety and routine, then comfort.
**Images.** `hero-building.jpg` — building exterior, morning light, 1920×1080+.
**CTA.** Primary `Apply for Admission` (solid gold — the only solid gold button above the fold;
the header CTA drops to a gold outline here so the two never compete).
Secondary `See the Boarding` for the majority who want proof before commitment.
**Mobile.** Headline `clamp()` down to 34px; CTAs go full-width stacked; trust row 2×2.
Header is transparent here and only becomes the glass bar after 8px of scroll.

---

### 2 — About the Boarding
**UX goal.** Draw the line between a boarding and a PG room — the distinction the whole
value proposition rests on.
**Layout.** 50/50 split. Copy left; right is a photo stack — one 4:3 hero plus two 1:1 tiles.
**Animation.** Column reveals with a 90ms offset so the eye lands on copy first.
**Content.** *"A hostel gives a student a bed. A boarding gives them a structure."* Then
four checkable claims — not-for-profit management, resident warden, recorded attendance,
proximity to colleges.
**Images.** `about-campus.jpg`, `about-warden.jpg` (the attendance register — a photo of the
register does more for trust than a photo of a lobby), `about-noticeboard.jpg`.
**CTA.** `Book a Visit` + `Read Our Rules` — routing the sceptical parent straight to the
hardest content is deliberate.
**Mobile.** Single column, copy first, photo stack after.

---

### 3 — Why Choose Us
**UX goal.** Six differentiators, each phrased as something a parent can verify in person.
**Layout.** 3-col card grid → 1-col on mobile. Dark gradient icon badge per card.
**Animation.** Fade + 18px rise, 60ms stagger across each row. Hover lifts 4px (pointer
devices only — `@media (hover:hover)`, so it never fires as a sticky tap state on touch).
**Content.** Security, protected study hours, vegetarian food, daily cleaning, discipline
without harshness, fees with nothing hidden. Each card ends in a concrete mechanism (a
register, a schedule, a receipt), never an adjective.
**Images.** None — inline SVG icons. Twelve card photos here would compete with the
Facilities section and cost a second of load time.
**CTA.** None. This section feeds the next one; a CTA here would interrupt the argument.
**Mobile.** Single column, full-width cards.

---

### 4 — Complete Facilities
**UX goal.** Prove every claim with a photograph. This is where an admission is won.
**Layout.** 12 photo cards, 3-col. Image → category tag → title → one-line detail.
**Animation.** Staggered reveal; hover lift on pointer devices.
**Content.** Furnished rooms · silent study hall · library · dining hall · kitchen · RO water
· bathrooms · CCTV & gate security · power backup · Wi-Fi · ground & sports · first aid.
Section lede commits to the standard: *"No renders, no stock photos… If something is under
renovation, we say so."*
**Images.** 12 photos, 16:10, min 800×500 — full brief per file in
`assets/images/README.md`. Until each exists, the card renders a labelled placeholder stating
the exact shot required.
**CTA.** None inline — the sticky mobile bar is always one thumb away.
**Mobile.** Single column. Cards stay photo-first; a 16:10 crop on a 375px screen is 234px
tall, big enough to judge a room by.

---

### 5 — Room Types
**UX goal.** Let a family self-select a room and a price band before they call.
**Layout.** Three comparison cards, price pinned to the card foot on a dashed rule so all
three prices align regardless of copy length.
**Animation.** Standard staggered reveal.
**Content.** Shared / two-sharing / single. Explicit equaliser: *"Every room type gets the
same food, the same facilities and the same rules. Only the sharing count changes."* — this
pre-empts the "is the cheap room worse" fear.
**Images.** `room-shared.jpg`, `room-double.jpg`, `room-single.jpg`, 4:3.
**CTA.** None per card — pricing is placeholder, and a CTA on unverified pricing is a
promise the boarding hasn't made.
**Mobile.** Stacked; sharing count and inclusions as chips so they scan without reading.

---

### 6 — Hostel Gallery
**UX goal.** Unstructured looking-around, for the student rather than the parent.
**Layout.** 10 tiles. Desktop: 4-col with tiles 1 and 6 spanning 2×2 for rhythm. Mobile: 2-col.
**Animation.** Scrim darkens 140ms on hover. Lightbox opens instantly — a zoom transition
here would delay the only thing the user asked for.
**Content.** Exterior · corridor · study hall in use · dining hall · room · evening ground ·
assembly · library · annual function · washing area. Photos of the boarding *in use* convert
better than empty rooms — a study hall with students in it is evidence.
**Images.** 10 square crops.
**CTA.** None. Exploration mode; the sticky bar carries the action.
**Mobile.** 2-col uniform grid, full-screen lightbox.
**Accessibility.** Each tile is a real `<button>` with a descriptive label. The lightbox is
`role="dialog" aria-modal`, traps Tab, restores focus to the tile that opened it, and takes
`←` `→` `Esc`.

---

### 7 — Food & Dining
**UX goal.** Neutralise the second-biggest parental worry after safety.
**Layout.** Flipped split — photo left, copy right — to break the alternating rhythm before
it becomes a pattern. Five-point checklist, then a meal-timing table.
**Animation.** Standard reveal, 90ms offset.
**Content.** Pure vegetarian, four servings, unlimited rotli/dal/bhaat, festival meals, and
*khichdi for a student who is unwell* — the small specific that signals actual care. Plus:
*"Students eat the same food the staff eats."*
**Images.** `food-thali.jpg` — a real served thali on a mess table, not a styled plate.
**CTA.** None.
**Mobile.** Photo first, then copy. The table scrolls horizontally inside its own container
with a "swipe sideways" hint and a `position: sticky` caption so the caption text stays
readable instead of being clipped off-screen.

---

### 8 — Study Environment
**UX goal.** State the single rational reason to choose a boarding over a rented room.
**Layout.** Split, copy left, wide photo right.
**Animation.** Standard reveal.
**Content.** *"A student living alone decides every night whether to study. Here, that
decision is already made — the hall is open, everyone is in it, and the phone is not."*
Then five mechanisms: two supervised sessions, enforced silence, extended exam hours,
senior–junior help, result review.
**Images.** `study-hall-wide.jpg` — the hall during an actual session, occupied.
**CTA.** None.
**Mobile.** Copy first — this section is argument, not image.

---

### 8b — Campus Band (added when the real ground photo arrived)
**UX goal.** Break a long text stretch with the single most convincing piece of evidence on
the page: a real, unretouched photograph of the campus in use.
**Layout.** Full-bleed, edge to edge, `clamp(260px, 44vw, 460px)` tall. Caption bottom-left
over a three-stop scrim that runs 15% → 88% opacity downward, so the text is readable
regardless of what is in the lower half of the photo.
**Animation.** None. The photograph is the moment; a parallax would fight it.
**Content.** *"Evening ground time."* — "A walled, floodlit ground inside the campus — so an
hour outdoors does not mean an hour outside the gate." Note that the copy describes what is
visibly true in the photograph: the wall, the lights along it, the volleyball net.
**Images.** `ground-aerial.jpg` — the supplied aerial shot, ~21:9.
**CTA.** None.
**Mobile.** Drops to 260px tall; the scrim ratio holds so the caption never loses contrast.

### 9 — Daily Routine
**UX goal.** Make the day concrete. Predictability is the product.
**Layout.** Two vertical timelines (morning / evening) side by side on desktop, sequential on
mobile. Brass gradient spine, ringed nodes.
**Animation.** Each column reveals as a unit, 90ms apart. Per-item stagger was rejected —
eleven sequential animations reads as a loading state, not a design.
**Content.** Wake → morning study → college → return & attendance → sports → dinner → night
study → lights out. Section lede states in bold that **all timings are placeholders**.
**Images.** None. A timeline is faster to read than a photo of a clock.
**CTA.** None.
**Mobile.** Columns stack; the timeline is already vertical so nothing reflows badly.

---

### 10 — Rules & Discipline
**UX goal.** The trust centrepiece. Publishing rules *before* the application, in full, is
the strongest signal on the page.
**Layout.** Full-width dark (`--ink-900`) section — the visual weight matches the content's
weight. Ten numbered cards, 2-col.
**Animation.** 40ms stagger, faster than elsewhere so ten items don't drag.
**Content.** In-time · written leave · compulsory study hours · zero tolerance for
tobacco/alcohol/drugs · no outsiders on residential floors · anti-ragging · property care ·
room cleanliness · phone policy · college attendance monitoring. Framed honestly:
*"Read these with your son before applying. If any of them is a problem, this is not the
right place — and it is better to know that now."* Self-selection is a feature: a family
that reads all ten and still applies is a family that stays.
**Images.** None — deliberately. A photo would soften content that should land plainly.
**CTA.** None. Closing this section with a CTA would read as a sales move.
**Mobile.** Single column; number and text on one row so each rule stays one glance.

---

### 11 — Fees Structure
**UX goal.** Win the comparison. Parents open three boarding sites side by side; the one
that publishes a complete table with a *"not included"* column wins on candour alone.
**Layout.** Full fee table, then two paired cards — **Included** (green ticks) vs **Not
included** (red crosses) — then a gold-bordered refund & concession note.
**Animation.** Standard reveal.
**Content.** Admission fee · refundable deposit · three room tiers, each with when-payable and
notes. Not-included is explicit: laundry, medical beyond first aid, travel, damages, outside
food. The lede states in bold that every amount is a placeholder.
**Images.** None. A number is the content.
**CTA.** None here — the fee table's job is qualification, and the sticky bar is present.
**Mobile.** Table scrolls horizontally in its own container (`min-width: 0` on the grid child
so the 460px table can't push the page wide — that bug shipped and was caught at 375px), with
a swipe hint and pinned caption. Included/not-included stack.

---

### 12 — Admission Process
**UX goal.** Remove procedural anxiety. Five steps, each with a known outcome.
**Layout.** 5-column stepper on wide screens → 2-col at tablet → 1-col mobile.
CSS `counter` numbering in brass, `decimal-leading-zero`.
**Animation.** 50ms stagger left-to-right, tracing the path the eye should take.
**Content.** Enquire → visit → submit form → interaction → pay & move in. Includes the honest
friction: *"Incomplete forms are not queued."*
**Images.** None.
**CTA.** **The page's primary conversion point** — `Start Your Enquiry` (jumps to the form)
plus `Ask on WhatsApp`. Two options, no more: Hick's Law.
**Mobile.** Vertical stack; both CTAs full-width.

---

### 13/14 — Eligibility & Required Documents
**UX goal.** Prevent a wasted journey, and let a family arrive with the right paperwork.
**Layout.** One split section, two checklists side by side.
**Animation.** Standard reveal, 90ms offset.
**Content.** Eligibility: enrolment in Rajkot, age/standard band, the community criterion,
signed rules agreement, no substance history, local guardian. Documents: form, both Aadhaar
copies, admission proof, last marksheet, photographs, rules undertaking.
**Images.** None.
**CTA.** None — the previous section's CTA is still in reach.
**Mobile.** Sequential, eligibility first.
**Note.** The community-eligibility line is flagged as a must-answer. A family that drives in
from a village to be turned away at the gate is the worst outcome this page can produce.

---

### 15 — Student & Parent Testimonials
**UX goal.** Social proof — **or an honest absence of it.**
**Layout.** Three greyed quote skeletons (`aria-hidden`) showing the built component, plus a
dashed-border brief addressed to the management.
**Animation.** Reveal only. The skeletons deliberately do not shimmer — a shimmer implies
content is loading, and none is.
**Content.** *"We would rather show nothing than show something invented."* The brief
specifies what each real testimonial needs: full name, relationship, course and year, consent,
photo. And: *"Do not publish anything that cannot be verified by a phone call."*
**Images.** None until real, consented headshots exist.
**CTA.** None.
**Mobile.** Stacked.
**Why.** The brief said no fake testimonials. Three invented quotes would have looked better
in a screenshot and would be the single fastest way to lose a parent who checks.

---

### 16 — Achievements
**UX goal.** Credibility through specifics.
**Layout.** Four stat tiles, then a "notable results" brief beside a felicitation photo.
**Animation.** Reveal only — **no count-up.** Counting from zero to a number that is
currently `—` is theatre; and once real, a count-up on a trust metric reads as a slot machine.
**Content.** Years serving · students housed · currently in residence · alumni in government
service. All `—`, with the instruction: fill from your own register, do not round up.
*"A boarding that says '147 students' is more credible than one that says '1000+ happy
students'."*
**Images.** `achievements-felicitation.jpg`.
**CTA.** None.
**Mobile.** 2×2 stat grid.

---

### 17 — FAQ
**UX goal.** Intercept the ten calls the office takes every week.
**Layout.** Native `<details>`/`<summary>` accordion, 860px column. **Zero JavaScript** —
it works with JS disabled, is keyboard- and screen-reader-correct by construction, and is
searchable by browser find-in-page when open.
**Animation.** Chevron rotates 260ms. Height is not animated — animating `height` costs
layout on every frame, and an accordion that snaps open feels faster.
**Content.** Visiting · community eligibility · safety · illness · weekend leave · phones ·
instalments · rule breaches · distance to colleges · waiting list. Written in a parent's
voice, answered without hedging.
**Images.** None.
**CTA.** None — Contact follows immediately.
**Mobile.** Full-width, 56px minimum summary height.
**SEO.** Mirrored in `FAQPage` JSON-LD — but only the five questions with verified answers.
Marking up a placeholder as structured data would publish a placeholder to Google.

---

### 18 — Contact + Map + WhatsApp
**UX goal.** Convert. Every path — call, WhatsApp, email, visit — in one screen.
**Layout.** Two columns: contact list + map facade left, enquiry form right. Stacks on mobile
with contact details first (a phone number outperforms a form for this audience).
**Animation.** Reveal, 90ms offset. Inputs: 140ms border colour + a 3px focus ring.
**Content.** Phone, WhatsApp, email, address, office hours. Form: student name*, parent's
mobile*, course, room preference, message — five fields, two required. Every extra field
costs completions, and the boarding only needs enough to call back.
**Images.** None. The map facade is a styled panel until requested.
**CTA.** `Send Enquiry on WhatsApp`. **The form has no backend** — it composes a pre-written
WhatsApp message and opens it. On a GitHub Pages site with no server this is the honest
architecture: nothing is stored, nothing is lost, and the enquiry lands where the office
actually reads it. Stated on the form: *"nothing is stored on this website."*
**Mobile.** Single column. 48px input height, 16px font size — **below 16px, iOS Safari zooms
on focus and the layout jumps**, which is the most common mobile form defect there is.
**Validation.** Inline, on submit, not on blur. Errors are red text *plus* a red border plus
`aria-invalid` — never colour alone. Focus moves to the first bad field. Status messages go
through `role="status" aria-live="polite"`.

---

### 19 — Footer
**UX goal.** Second-chance navigation and a final credibility statement.
**Layout.** 4 columns: the full logo lockup + motto + a line of copy · The Boarding ·
Admissions · Reach Us with a gold CTA.
**Animation.** None. The footer is a destination, not a moment.
**Content.** Full sitemap, contact details repeated, *"Built for students and their
families."*
**Images.** None.
**CTA.** `Apply for Admission` (solid gold).
**Mobile.** Stacked, with `padding-bottom` reserved so the sticky action bar never covers the
last row.

---

### 20 — Mobile Sticky Action Bar (added, not in the brief)
**UX goal.** The single highest-leverage conversion element on a phone.
**Layout.** Three equal 60px targets at the bottom edge: **Call · WhatsApp · Apply**, colour-
coded, `env(safe-area-inset-bottom)` respected for notched devices.
**Animation.** Slides up after 400px of scroll (420ms ease-out) — absent at the top where the
hero CTA already occupies that role, so it never competes with it.
**Content.** Icon + one word each.
**CTA.** All three.
**Mobile.** Mobile-only (`display:none` at ≥768px, where a persistent bar is just chrome).
**Why.** Fitts's Law: the bottom third of a phone screen is the thumb's natural resting arc.
A CTA in the header is measurably harder to hit one-handed than one in the same place on
every screen.

---

### 20 — Donor Tribute (added when the building sign was read)
**UX goal.** Acknowledge the principal donor named on the building. In a community-funded
institution this is not decoration — it is the social contract the boarding runs on, and a
family from that community will look for it.
**Layout.** Full-width card closing the About section: cream ground, 4px gold left border,
dark circular seal, donor's name in Gujarati at display size with the English below.
**Animation.** Reveal only. Anything more would be tasteless here.
**Content.** *મુખ્ય દાતાશ્રી* / Principal donor, the name exactly as it appears on the building,
then one line: *"His name is on the building because the students living here study on it."*
**Images.** None — a name set in the display face carries more weight than a photograph would.
**CTA.** None, deliberately. Attaching a conversion action to a memorial would cheapen both.
**Mobile.** Seal and text stack; the Gujarati clamps down to 19px.
**Accessibility.** Gujarati runs are marked `lang="gu"` so screen readers switch voice rather
than spelling the script out in English phonetics, and the body font stack gained
`"Noto Sans Gujarati"` so the script renders on devices without a system Gujarati face.

## 3. Accessibility — what was actually done

- **WCAG 2.2 AA contrast**, verified by computation for every pair in the palette table. Three
  failures found and fixed rather than shipped (brass-on-white, muted grey, WhatsApp green).
- **Keyboard:** skip link; visible 3px focus ring on every interactive element, recoloured to
  brass on dark surfaces; drawer and lightbox trap Tab and restore focus to their opener;
  `Esc` closes both; `←`/`→` navigate the lightbox.
- **Semantics:** one `<h1>`; landmarks throughout; `<address>` for the postal address;
  `<dl>` for stats; `<th scope>` on every table; `aria-labelledby` on every section;
  `aria-current` on the active nav item.
- **Targets:** every control ≥44×44px, ≥8px apart. Action-bar items are 60px.
- **Motion:** `prefers-reduced-motion: reduce` disables all animation *and* smooth scrolling.
- **Forms:** real `<label>` elements, `autocomplete` attributes, `inputmode="numeric"` on the
  phone field, errors conveyed by text + border + `aria-invalid`, live status region.
- **Images:** descriptive `alt` on all 32; decorative ones `alt=""`; skeletons `aria-hidden`.
- **Print:** a print stylesheet — parents genuinely print the rules and fee pages.

## 4. SEO

Title and meta description targeting *boarding / hostel + Rajkot + student*; canonical;
Open Graph and Twitter card; `EducationalOrganization` JSON-LD with `amenityFeature` for
each facility; `FAQPage` JSON-LD limited to verified answers; semantic heading order;
descriptive alt text; `lang="en"` with `og:locale en_IN`.

**Before launch:** add `telephone`, full `PostalAddress`, `geo` and `openingHours` to the
JSON-LD, and claim the Google Business Profile. For a local institution, the Business Profile
outranks the website for the query *"ahir boarding rajkot"* — the site's job is to be the
page that converts the click.

## 5. Named risks & tradeoffs

1. **Placeholders are visible.** The brass ◇ markers are honest but not pretty. That is the
   correct default — a live site showing `₹ —` is better than one showing an invented figure.
   Removing a marker is one deletion per item; the checklist enumerates all 45.
2. **The form has no backend.** WhatsApp handoff means no enquiry database and no analytics on
   drop-off. Correct for a static host today; if enquiry volume matters later, a Formspree or
   Google Apps Script endpoint slots in behind the same button.
3. **One webfont.** Fraunces costs one request. Judged worth it — the display face is most of
   the "premium" perception, and body text stays at zero bytes. If the Lighthouse mobile
   score matters more, drop to `ui-serif` and lose maybe 15% of the visual character.
4. **`backdrop-filter` on the header** is the one expensive effect. It is guarded by
   `@supports` and confined to a 64px bar. On a low-end Android it can cost a few frames
   while scrolling; the cheap substitute is a solid `rgba(255,255,255,.94)` — one line.
5. **English only.** Many parents in this audience read Gujarati more comfortably than
   English. A Gujarati version is the highest-value next addition — but writing one without
   the real content would produce two pages of placeholders instead of one.

## 6. What to build next

1. Fill the 45 checklist items and drop in the 32 photos. **Nothing else matters until this
   is done.**
2. Gujarati translation with a language toggle, `hreflang` pairs, `lang="gu"` on the content.
3. A downloadable admission-form PDF — offices are asked for it constantly.
4. A "Life at the Boarding" page for the student audience: festivals, sports, alumni.
5. Analytics on the three action-bar buttons to learn whether families call or message —
   then double down on whichever one wins.
