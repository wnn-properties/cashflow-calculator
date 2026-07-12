# WNN Cashflow Calculator

A web replacement for the "WNN Cashflow Calculator.xlsx" spreadsheet. All formulas
live in code, so students can only type into the input fields — there is nothing
to accidentally delete or overwrite, and no file to re-download.

**The entire application is the single file `index.html`.** No server, no database,
no accounts, no build step, no dependencies. It works offline once loaded.

## What it does

- Replicates every formula from the workbook's *CF calculator* sheet: income,
  expenses, NOI, reserves, cash flow, principal reduction, appreciation, gross
  equity income, and the six financial indicators (DSCR, cash-on-cash ×2, ROI ×2,
  time-before-return), including the "infinity when cash left in is positive" rules
  from the workbook's cell comments (shown as ⓘ tooltips).
- Replicates the *Mortgage schedule* sheet as a second tab (full amortization
  table with running principal reduction).
- One intentional improvement: the spreadsheet's amortization sheet hard-coded a
  360-month term inside its PMT formula even when the "Terms (Months)" cell was
  changed. This app uses the entered term everywhere.

## Student experience

- Entries auto-save in the browser (localStorage) — closing the tab loses nothing.
- **Copy link** puts a shareable URL on the clipboard that carries the whole
  analysis — students send one link to their mentor instead of a file. Opening
  the link fills in every field.
- **Add to compare** saves the current deal (up to 4); the **Compare Deals** tab
  shows them side by side with the key metrics, and can load any saved deal back
  into the calculator.
- **Deal-quality colors**: cash flow, DSCR, and cash-on-cash show green/amber/red
  against target thresholds (see `THRESHOLDS` in `index.html`: cash flow ≥ $100/mo
  good / ≥ $0 acceptable; DSCR ≥ 1.2 / ≥ 1.0; CoC ≥ 8% / ≥ 4%).
- **Stress Test** panel shows cash flow and DSCR if rent comes in 10% low, the
  rate is 1% higher, or both — margin-of-safety at a glance.
- **Gentle input warnings** catch common mistakes (all-in below purchase price,
  monthly rent that looks like a daily number, taxes entered monthly instead of
  annual, interest entered as 0.07 instead of 7) without blocking anything.
- **Clear all entries** resets to a blank calculator (requires a second click to confirm).
- **Restore defaults** resets only the assumption percentages (10% appreciation,
  8% management, 5% vacancy/maintenance/CapX, 75% LTV, 360 months, 7% rate).
- **Download scenario / Load scenario** exports and imports a small `.json` file —
  useful for students submitting an analysis or moving between computers.
- **Print / PDF** produces a clean printout headed by the property address and date.

## Hosting (pick one — all are free)

1. **GitHub Pages (recommended for ownership transfer).** Push this folder to a
   GitHub repository, then in the repo: Settings → Pages → deploy from the `main`
   branch. The calculator is live at `https://<account>.github.io/<repo>/`.
2. **Netlify Drop** (drop.netlify.com): drag the folder onto the page. Done.
3. **Any static web host** — upload `index.html`.
4. **No hosting at all**: email or share `index.html`; it opens directly in any
   browser by double-clicking.

## Transferring ownership

- **GitHub Pages route:** repo Settings → Danger Zone → *Transfer ownership* to
  the new maintainer's GitHub account or org. The site moves with the repo.
  (Tip: create the repo under an organization account from the start, then
  handing it off is just adding/changing org owners.)
- **Any other route:** ownership is simply possession of `index.html`.

## Maintaining it

Everything is in `index.html`:

- **Default assumptions** — edit the `DEFAULT_ASSUMPTIONS` object near the top of
  the `<script>` block.
- **Formulas** — the pure `calc()` function, written in the same order as the
  spreadsheet, with the original cell references noted in comments.
- **Deal-quality thresholds** — the `THRESHOLDS` object next to `DEFAULT_ASSUMPTIONS`.
- **Branding** — matched to wnnproperties.com (verified against the WNN Properties
  YouTube channel and Facebook page): Montserrat type (embedded in the file, works
  offline), charcoal `#191C1E` dark theme, sky-blue `#23A9D0` accent, pale-yellow
  `#FCE588` announcement bar, white/navy light theme. Colors are CSS custom
  properties at the top of the `<style>` block; the logo is embedded as a base64
  data URI in the `<img>` tag.
