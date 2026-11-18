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

## My submission: make a partial return impossible to lose

**Where to look:** `app.js` (search `followup`, `overdue`, `dueTimes`, `whereabouts`) and a few rules in `styles.css` (`.late`, `.acts`). `index.html` is unchanged.

### The job, as I worked it
Friday 3:45 pm: issue the Film Society kit (projector, speaker, adapter) to Kabir against RQ-214. 7:30 pm: take back the projector and speaker; Leela still has the adapter. Saturday 9:00 am: Leela arrives, and I have to close the right loan.

### One moment the product handles well
At pickup, the issue form only offers units that can actually leave the desk. PR-06 (in repair) and anything already on loan can't be selected, and a second projector against a request that approved one is refused. Availability is derived from the loan register, so there is no separate status to forget to update. When I issued PR-04, SP-02 and AD-12, the product guaranteed I could not hand out a broken or double-booked unit.

### One moment I would change
At 7:30 pm I recorded the projector and speaker returns. The adapter's slip stayed open and still read *Kabir Sen, due Fri 8 pm*, but the real situation was that Leela had it and was bringing it at 9 am. That fact lived only in Kabir's free-text message and whatever I typed into the Desk book. On Saturday the register could not tell me who held the adapter, that it was already past its original due time, or which of two identical adapters (AD-12 and AD-15, same bin) to look for, because slips showed only unit IDs. The hand-off depended on a person remembering to write a note.

### The change: the kit is the unit of attention, the slip stays per-unit
The register keeps one slip per physical unit, which is right. What was missing is a view that knows the unit belongs to a kit.
- **Partial-return prompt.** When a return leaves other units of the same request out, the register opens a "kit is not complete" panel (focus moves to it) asking *who has it now* and *expected back*. It is saved on the slip, and a Desk book entry is written automatically. "Not now" is allowed.
- **Safety net for "Not now".** A slip from a partly returned kit with no whereabouts shows a *Whereabouts not recorded* tag, so skipping the prompt can't silently recreate the old problem.
- **Kit status on the request.** Each approved item shows Not issued / On loan with X, expected Y / Returned. At pickup, each issue confirmation also lists what is still to issue for that request.
- **Readable, ordered slips.** Rows show type, model, collector, current holder and expected time. Overdue slips carry a tag and sort to the top. Action buttons carry the unit in their accessible name ("Record return of AD-12"), and rows stack on narrow screens.
- **Fixable.** *Update whereabouts* lets the desk correct the holder or time later (for example, "Leela is running late").

### The same job with the change
Friday: issue three units; after the first, the confirmation says the speaker and adapter are still to issue. 7:30 pm: return projector and speaker; the panel appears; I pick *Leela Das*, *Sat 9 am*. The Desk book gets the entry without me typing. Saturday 9:00: the top row is `L-403 · AD-12 · USB-C → HDMI adapter · Belkin AVC002 · Now with Leela Das, expected Sat 9 am · Overdue`. I check the label on Leela's adapter reads AD-12 and close that slip. The Debate Union microphone slip (due Sat 10 am) is untouched.

### What I would keep
The approval and availability guards, per-unit slips, derived inventory status, and the free-text Desk book for things the system can't model.

### What I chose not to build, and risks
- No multi-unit "issue whole kit" button or barcode scan. They would speed up Friday's pickup, but I would want counter evidence first, and a scan step could slow a busy desk.
- Times are the sample's four fixed slots, not real timestamps; a real version needs date-times and a real clock.
- The prompt adds one step to a return. If desk staff find it annoying and always press "Not now", the *Whereabouts not recorded* tag is the signal to look at.
- Tested end to end in headless Chromium (issue, partial return, skip, update, close, reload) and checked at phone width.

### How I would know at a real counter
Shadow the morning shift for a week before and a week after. Count (1) how often someone has to ask "who has this?" or read a paper note to close a partial loan, and (2) the time from a person arriving with an item to its slip being closed. Also count how often "Not now" is pressed. I would call it a success if the first number drops to near zero without the third climbing, and I would revert or simplify the prompt if staff skip it most of the time.

*Built with AI assistance (Claude); I reviewed and tested the result.*

## Submit your work

1. [Fork Campus Stores](https://github.com/virinchi-healthcare/campus-stores/fork) into your GitHub account. Complete the candidate brief and push your changes to your public fork. In your README, point reviewers to your work and explain the decision you made.
2. In your fork, open **Commits**, select the final commit you want reviewed, and copy the page URL. It should look like `https://github.com/YOUR-USERNAME/campus-stores/commit/COMMIT-SHA`.
3. [Submit your work through the Google Form](https://docs.google.com/forms/d/e/1FAIpQLScvzoh1R4WS-SkiwAVBQbMvniieJYSoOEfLMyVo5CyjOvYUgQ/viewform). Your **roll number**, **email ID**, and **final commit link from your public fork** are required. Enter your roll number and email ID in the form only.
