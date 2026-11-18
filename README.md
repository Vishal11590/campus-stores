# Campus Stores

Campus Stores is a Product Engineer work sample set at a fictional campus media equipment desk. Work through a club’s screening, from equipment pickup to a partial return and the next morning’s handover. Open **Candidate brief** in the app for the assignment.

## Run the app

Open `index.html` in a modern browser. The app includes its scripts, styles, and icons and can run offline.

To serve it over local HTTP, run this from the repository folder and visit `http://localhost:8000`.

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Each browser stores its own sample shift locally when browser storage is available. **Restart sample shift** restores the fictional starting records.

## Source

- `index.html` contains the desk layout, candidate brief, and bundled icons.
- `app.js` contains the sample records and interactions.
- `styles.css` defines the desktop and mobile layouts.

Icon license notices are in [third-party/lucide-LICENSE.txt](third-party/lucide-LICENSE.txt).

## My submission: partial returns, made visible

**Where to look:** `app.js` (search for `followup`, `overdue`, `dueTimes`), one small rule in `styles.css` (`.late`). Nothing else changed.

### One moment the product handles well
At the Friday 3:45 pm pickup, the issue form only offers units that can actually leave: PR-06 (in repair) and anything already on loan are not selectable. The form also refuses a second projector against a request that approved one. Inventory status is derived from the loan register, so there is no separate flag to forget to update. I issued PR-04, SP-02 and AD-12 against RQ-214 without any risk of handing over a broken or double-booked unit.

### One moment I would change
At 7:30 pm Kabir returns the projector and speaker, and Leela still has the adapter. I clicked **Record return** twice and the product went quiet: the adapter's slip stayed open, but it still said *Kabir Sen, due Fri 8 pm*. The facts the morning shift needs (Leela has it, she is bringing it at 9 am) lived only in Kabir's free-text message and whatever I typed into the Desk book. The slips also showed only unit IDs (`L-404 · AD-12`), and AD-12 and AD-15 are identical adapters in the same bin, so on Saturday there was no quick way to match the object in Leela's hand to the right slip.

### The change
- **Prompt on partial return.** When a return leaves other units of the same request still out, the register opens with a "kit is not complete" panel asking *who has it now* and *expected back*. These are saved on the slip, and an entry is written to the Desk book automatically. "Not now" skips it.
- **Kit status on the request.** Each approved item shows Not issued / On loan with X, expected Y / Returned.
- **Readable slips.** Rows show item type and model next to the unit ID, plus the holder and expected time, and an **Overdue** tag when the original due time has passed.

### Same job with the change
Friday 3:45: issue the three units as before. 7:30: record the projector and speaker returns. The panel appears; I choose *Leela Das* and *Sat 9 am*. Saturday 9:00: the register shows `AD-12 · USB-C → HDMI adapter · Belkin AVC002 · Now with Leela Das, expected Sat 9 am · Overdue`. The Desk book and the request's kit status say the same thing. Leela hands over the adapter, I check the label reads AD-12, and I close that slip. The microphone slip (Debate Union, due Sat 10 am) is not touched.

### What I would keep, and what I left out
Keep: the approval and availability guards, one slip per physical unit, and the free-text Desk book for things the system can't model. I deliberately did not build multi-unit issue or a barcode scan; they would help Friday's pickup but I'd want counter evidence first. Times are a fixed ladder of the sample's four slots, not real timestamps, which a production version would need.

### Observation at a real counter
Count, over a week, how often the morning shift has to ask someone ("who has this?" / "which unit is this?") or read a paper note to close a partial loan. If the change works, that number should drop to near zero, and the time from a person arriving with an item to the slip being closed should fall.

*Built with AI assistance (Claude) and tested end to end in headless Chromium: issue, partial return, handover, close, reload.*

## Submit your work

1. [Fork Campus Stores](https://github.com/virinchi-healthcare/campus-stores/fork) into your GitHub account. Complete the candidate brief and push your changes to your public fork. In your README, point reviewers to your work and explain the decision you made.
2. In your fork, open **Commits**, select the final commit you want reviewed, and copy the page URL. It should look like `https://github.com/YOUR-USERNAME/campus-stores/commit/COMMIT-SHA`.
3. [Submit your work through the Google Form](https://docs.google.com/forms/d/e/1FAIpQLScvzoh1R4WS-SkiwAVBQbMvniieJYSoOEfLMyVo5CyjOvYUgQ/viewform). Your **roll number**, **email ID**, and **final commit link from your public fork** are required. Enter your roll number and email ID in the form only.
