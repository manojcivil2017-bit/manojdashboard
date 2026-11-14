# PD Rating Status Dashboard

Live app: https://manojkitecivil2017-bit.github.io/pd-dashboard/

A mobile app (PWA) showing project status from the PD Rating Excel file, with WhatsApp sharing.
It runs entirely on free GitHub Pages hosting, with no server and no outside libraries.

## Install on a phone
- **Android (Chrome):** open the link → menu ⋮ → **Add to Home screen / Install app**.
- **iPhone (Safari):** open the link → Share button → **Add to Home Screen**.

## View-only link vs admin login
- The link is **view-only** for everyone: no Upload Excel and no Settings.
- Admins tap **Admin login** at the bottom of the page and enter the username and password.
  The device stays logged in until **Settings → Log out of admin on this device**.
- Only a salted PBKDF2 hash of the password is stored in `index.html` (the `ADMIN_LOGIN` line), never the password itself.
- To change the password, generate a new salt and hash (PBKDF2-SHA256, same iteration count) and replace the `ADMIN_LOGIN` line.
- Publishing for everyone still needs the GitHub token, so a login alone cannot change what others see.

## Update the data (everyone sees it)
**Option 1, on GitHub (no setup):**
1. Rename your new Excel file to `status.xlsx`.
2. In this repository click **Add file → Upload files**, drop in `status.xlsx`, then click **Commit changes**.
3. Within 1–2 minutes everyone sees the new data.

**Option 2, from inside the app (after a one-time setup):**
1. On GitHub: profile photo → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
   - Repository access: **Only select repositories → pd-dashboard**
   - Permissions → Repository permissions → **Contents: Read and write**
   - Pick an expiry date, generate it, and copy the token.
2. In the app, open ⚙ Settings, paste the token, and Save. The token is stored only on that device.
3. Then: **Upload Excel** → check the preview → **Publish for everyone**.

Uploading in the app *without* publishing only previews the file on your own device.

## Excel format
The first sheet needs a header row with: UPN ID, RO, PIU, Project Name, Progress (%), Status, Last Updated.
Status values: COMPLETED / IN PROGRESS / NOT STARTED. Any file name works when you upload in the app.

## Files
- `index.html`: the whole app (dashboard, built-in Excel reader, WhatsApp sharing)
- `status.xlsx`: the published data
- `sw.js`, `manifest.webmanifest`, `icon-*.png`: make it installable and work offline
