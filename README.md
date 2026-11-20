# Rating Exercises Dashboard

Live app: https://manojcivil2017-bit.github.io/pd-dashboard/

A mobile app (PWA) showing the status of the ongoing rating exercises, with WhatsApp sharing and PDF reports.
It runs entirely on free GitHub Pages hosting, with no server and no outside libraries.

| Exercise | Data file in this repository | Grouped by |
|---|---|---|
| NHAI · PD Rating | `nhai-pd.xlsx` | RO → PIU |
| NHIDCL · AE/IE Consultant Rating | `nhidcl-aeie.xlsx` | PMU |
| MoRTH · DPR Consultant Rating | `morth-dpr.xlsx` | RO |
| MoRTH · AE/IE Consultant Rating | `morth-aeie.xlsx` | RO |

Direct links open one exercise, e.g. `…/pd-dashboard/#nhai-pd`, `#nhidcl-aeie`, `#morth-dpr`, `#morth-aeie`.

## Install on a phone
- **Android (Chrome):** open the link → menu ⋮ → **Add to Home screen / Install app**.
- **iPhone (Safari):** open the link → Share button → **Add to Home Screen**.

## View-only vs admin
- Everyone sees the dashboards, filters, project details, WhatsApp sharing and PDF reports.
- **Upload Excel** and **Settings** appear only after **Admin login** (link at the bottom of the page).
- Only a salted PBKDF2 hash of the admin password is stored in `index.html` (`ADMIN_LOGIN`).

## Update the data
**From the app (admin):** Upload Excel → choose the exercise → **Status file** → choose the file → check the preview → **Publish for everyone**.
The app warns if a file looks like it belongs to a different exercise. Publishing needs a GitHub token in Settings (one-time):
GitHub → Settings → Developer settings → Fine-grained tokens → repository `pd-dashboard`, permission **Contents: Read and write**.

**On GitHub (no setup):** rename the Excel to the file name in the table above, then **Add file → Upload files** → Commit.

## Reviewed & Shared with field units
- **From a review tracker (any exercise):** Upload Excel → choose the exercise → **Review tracker** → choose the tracker.
  The app reads only the project ID (UPN/UPC) and **Tranche** columns (tab *Master Project List* if present).
  Any project with something in Tranche counts as reviewed & shared. It is matched to the daily status file by project ID,
  so progress data is never overwritten. Shown overall, by RO/PIU/PMU and per project. Saved as `<exercise>-review.json`.
- **Typed in by admin (overall figure only):** ⚙ Settings → **Update "Reviewed & Shared" numbers** → Publish for everyone.
  Saved in `shared.json`. Used for exercises that have no review tracker.

## Sharing and PDF reports
- Green **Share status** button: WhatsApp text summary, share PDF (on a phone pick WhatsApp), or download PDF.
- Overview screen → summary of all exercises. Inside an exercise → report for the current filters.
- Project-wise details are included in the PDF only when the lowest level is selected (PIU for NHAI, PMU for NHIDCL, RO for MoRTH).
