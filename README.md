# Wiseman Library Scanner — GitHub API Test

This repository is currently being used as the **test frontend** for the GitHub Pages + Google Apps Script backend architecture.

## Safety / rollback

- Production-oriented code before this experiment is preserved on branch `pre-api-test-backup`.
- The former root barcode scanner is also preserved at `scanner.html`.
- The long-term `wiseman-library` repository is untouched.

## Test architecture

- GitHub Pages serves the visible Library UI directly.
- A hidden Apps Script bridge iframe handles calls to existing server functions through `google.script.run`.
- PINs, session validation, permissions, Google Sheets access, Personal Books rules, users, loans, quotes, and all sensitive logic stay in Apps Script.
- GitHub stores only the UI and a browser-side session token.
- The test UI has a visible **TEST** badge.

## Apps Script setup required

1. Add `Bridge.html` from the 0925A test package to the existing Apps Script project.
2. Replace `Code.gs` with the supplied 0925A test copy. The only architectural change is `doGet(e)`; the existing library backend remains intact.
3. Save.
4. Deploy > Manage deployments > Edit the existing Web app deployment > New version > Deploy.
5. Open the GitHub Pages root for this repository.

Normal Apps Script `/exec` requests still serve the existing `Index.html`. Only `/exec?bridge=1` serves the API bridge.
