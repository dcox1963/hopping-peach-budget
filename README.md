# Hopping Peach Budget

A small, mobile-friendly monthly budget app that runs from a single HTML file. It works locally in a browser and can optionally share live data through Firebase Realtime Database.

## Files

- `hopping-peach-budget.html` — the budget app
- `Hopping Peach Monthly Budget.xlsx` — matching Excel budget workbook
- `SETUP-GUIDE.md` — local-use and optional Firebase setup instructions
- `firebase.rules.json` — recommended Realtime Database rules

## Quick start

1. Open `hopping-peach-budget.html` in a browser.
2. Enter the default access code: `328`.
3. Follow `SETUP-GUIDE.md` if you want live sharing between devices.

The app starts in local-only mode. Browser storage keeps changes on that device. Firebase values are intentionally left as `PASTE_HERE`; do not commit real private configuration unless you understand that Firebase web configuration is visible to anyone who receives the file.

## Verification

The app has been checked for JavaScript syntax errors and tested in a local browser for:

- access-code unlock
- initial totals and section rendering
- marking a bill paid/unpaid
- adding and deleting a bill
- recalculated totals
- local persistence after reload
- absence of browser console errors

The Excel workbook was also checked for formula errors and visually rendered sheet by sheet.

## Security note

The access code is a convenience lock, not strong authentication. The supplied Firebase rules require an authenticated Firebase session, but anonymous sign-in still does not identify a particular person. Keep the hosted URL and file private, avoid putting account numbers or other highly sensitive identifiers in the app, and prefer local-only mode when sharing is unnecessary.
