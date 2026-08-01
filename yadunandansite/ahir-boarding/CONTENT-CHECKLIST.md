# Content checklist — Yadunandan Ahir Boarding, Rajkot

Nothing on this site was invented. Every fact that could not be verified is marked on the page
with a dotted gold underline and a ◇ symbol, and listed below.

Open the page with **`?review=1`** (or press **Alt + P**) to see this list on the site itself.

## Two facts were corrected

- ❌ **“Two sharing” room type — removed.** You said it is wrong. There is now one Rooms block
  with the configuration marked pending, rather than invented room tiers.
- ❌ **“Evening snack” — removed.** The meal table now lists breakfast, lunch and dinner only,
  with a note to confirm the full daily schedule.

## Confirmed from the logo and photographs

- ✅ **Name:** Yadunandan Ahir Boarding · **Motto:** Discipline · Education · Excellence
- ✅ **Managing body:** શ્રી યદુનંદન આહીર કેળવણી મંડળ, from the building sign
- ✅ **Principal donor:** સ્વ. વાલજીભાઈ ભુલાભાઈ ખુમલા
- ✅ **Boys' hostel** (કુમાર છાત્રાલય)
- ✅ **Study hall:** partitioned individual carrels, not shared tables
- ✅ **Fire safety:** extinguishers and marked fire exits
- ✅ **Sports:** a laid cricket pitch and a volleyball ground

> ⚠️ Check the English spelling of the donor's name (*Valjibhai Bhulabhai Khumla*). The Gujarati
> is reproduced exactly as it appears on the building; the English is a transliteration.

---

**21 items still to confirm** — down from 43, because the page was cut to only what
a family actually needs.

---

## `#food`

- [ ] **Confirm the breakfast time**  
  <sub>currently showing: “—”</sub>
- [ ] **Confirm the lunch time**  
  <sub>currently showing: “—”</sub>
- [ ] **Confirm the dinner time**  
  <sub>currently showing: “—”</sub>
- [ ] **Confirm how many meals are served each day and whether anything is served between lunch and dinner**  
  <sub>currently showing: “Confirm the full daily meal schedule before publishing.”</sub>

## `#rooms`

- [ ] **Confirm the room configuration: how many students share a room, and whether more than one room type is offered**  
  <sub>currently showing: “Room configuration and how many students share a room to be confirmed.”</sub>

## `#facilities`

- [ ] **Solar panels are visible on the roof; confirm what they power**  
  <sub>currently showing: “On the roof”</sub>

## `#fees`

- [ ] **Confirm the admission fee**  
  <sub>currently showing: “₹ —”</sub>
- [ ] **Confirm the refundable deposit**  
  <sub>currently showing: “₹ —”</sub>
- [ ] **Confirm the annual boarding and lodging fee**  
  <sub>currently showing: “₹ —”</sub>
- [ ] **Confirm the instalment schedule**  
  <sub>currently showing: “—”</sub>

## `#details`

- [ ] **State plainly whether admission is open to all students or restricted, and on what basis**  
  <sub>currently showing: “To be stated plainly by the management.”</sub>
- [ ] **Confirm how many passport photographs are required**  
  <sub>currently showing: “Passport-size photographs”</sub>
- [ ] **Confirm the daily in-time**  
  <sub>currently showing: “stated in-time”</sub>
- [ ] **Confirm the full mobile phone policy**  
  <sub>currently showing: “Full policy to be confirmed.”</sub>
- [ ] **Placeholder timing**  
  <sub>currently showing: “Morning”</sub>
- [ ] **Confirm the leave policy and any limits**  
  <sub>currently showing: “Exact leave policy to be confirmed.”</sub>
- [ ] **List nearby colleges with real distances or travel times**  
  <sub>currently showing: “List the nearby colleges with actual distances or travel times.”</sub>
- [ ] **Confirm the English spelling of the donor's name before publishing**  
  <sub>currently showing: “Valjibhai Bhulabhai Khumla”</sub>

## `#contact`

- [ ] **Insert the official contact number**  
  <sub>currently showing: “+91 — — — — —”</sub>
- [ ] **Insert the official email address**  
  <sub>currently showing: “office@—.—”</sub>
- [ ] **Insert the full postal address with landmark and pincode**  
  <sub>currently showing: “Full address with landmark, Rajkot — PIN”</sub>

---

## Photographs

The page now uses **8 photos, not 32.** Five are already supplied; three are still needed and
are the three that matter most to a family:

- [ ] `assets/images/room.jpg` — a student room. **The single most important missing photo.**
- [ ] `assets/images/dining.jpg` — the dining hall at meal time
- [ ] `assets/images/thali.jpg` — an actual served thali (used twice: Food section + photo wall)

✅ The logo, the cropped emblem and all five supplied photographs are already in the repo —
recovered from the session transcript, resized and compressed. Nothing to save by hand.

---

## Contact details live in one place

In `index.html`, find the `SITE` object near the bottom:

```js
const SITE = {
  phone:    "+919876543210",      // office number, with country code
  whatsapp: "919876543210",       // digits only — no +, no spaces
  email:    "office@example.org",
  mapQuery: "Yadunandan Ahir Boarding, Rajkot, Gujarat"
};
```

That one edit activates every Call button, every WhatsApp link, the enquiry form and the map.
