# Mental Performance Course — Setup Notes

## 1. Add your real content
Open `index.html`, find the `WEEKS` array near the top of the `<script>` block
(around line "1. COURSE DATA"). For each of the 7 weeks, replace:

- `title` — the week's title
- `videoUrl` — your YouTube **embed** URL. For an unlisted video at
  `https://youtu.be/XXXXXXXXXXX`, the embed URL is
  `https://www.youtube.com/embed/XXXXXXXXXXX`
- `worksheetUrl` — path to that week's PDF (see step 2)

## 2. Add the worksheet PDFs
Put your 7 PDFs in the `worksheets/` folder next to `index.html`, named
however you like (e.g. `week-1.pdf`), and make sure each `worksheetUrl` in
the data array matches the filename exactly.

## 3. Test the unlock logic before sending the real link
- `yourpage.html?reset=1` — clears the stored start date, so the page acts
  like a brand-new client opening it for the first time.
- `yourpage.html?debug=4` — previews the page as if it's currently week 4
  (try 1 through 7) without changing real dates. Remove the param to go
  back to real behavior. A banner at the top confirms you're in debug mode.
- `yourpage.html?start=2026-06-01` — sets an explicit start date (useful if
  you want to hand-set a specific client's clock; survives across devices
  since it's baked into the link rather than relying on localStorage from
  first visit).

## 4. Deploy
Easiest free options, either works:
- **Netlify Drop**: go to https://app.netlify.com/drop and drag the whole
  `course` folder (containing `index.html` and `worksheets/`) onto the page.
  You'll get a public URL in seconds.
- **GitHub Pages**: push the folder to a repo, enable Pages in repo
  settings, pointed at the root.

Paste the resulting URL into Trainerize.

## How the gating works (for your own reference)
- First visit: today's date is saved in the browser's localStorage.
- Every visit after that: the page checks how many full 7-day periods have
  passed since that saved date, and unlocks that many weeks (capped at 7).
- This is intentionally soft — anyone could clear their browser storage or
  edit it in dev tools to skip ahead. Per the brief, that's an accepted
  trade-off, not a bug.
- localStorage is per-browser. If a client switches from phone to laptop,
  the laptop will think it's their first visit and start a new clock. Use
  the `?start=` param above if you want to hand-set a date that's consistent
  across their devices.
