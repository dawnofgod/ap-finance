# AP Finance

Offline hostel finance app for Nepal: rooms, admissions, students, monthly fees, income, expenditure, profit/loss and PDF reports, with Bikram Sambat dates. It installs from the browser (no Play Store, no .exe, no Smart App Control problem) and updates itself.

* **Live app (real users):** branch `main`, on `https://ap-finance.vercel.app` (see Vercel for the exact address)
* **Test copy:** branch `test`, with its own address. It uses separate test data and the Drive folder "AP Finance – TEST".
* **Admin panel:** `/admin.html` on either address. Only the admin Gmail can open it.

## How people start

Sign in with Google → hostel name (one hostel, or two sections such as Boys/Girls) → hostel logo → profile name → username + password for this computer → app.

Anyone can sign up. Records stay on the hostel's computer (works offline). A copy, the data backup plus PDFs, goes to the hostel's folder inside **AP Finance** in the admin's Google Drive. The sign-up screen tells users that the admin can view their records.

## Admin panel

* Each hostel appears as a profile card with its logo, showing:
  * online/offline status
  * when it was last active
  * students and records
  * Drive storage used
  * last backup
  * app version
  * a link to its Drive folder
* **View records** is read-only. It opens the hostel's students, monthly fees, income, expenditure, admissions and rooms from its latest backup.
* **Freeze** locks the app on the hostel's computers. **Remove** deletes the account, and the app goes back to "Sign in with Google". Their local data and the Drive files are kept.

## Publishing updates

1. Change the files and bump `VERSION` in `sw.js` (and `APP_VERSION` in `js/ap-web.js`).
2. Push to the **`test`** branch. The test copy updates, so check it there.
3. When it works, merge `test` into **`main`**. Real users see "Update now".

## Server settings (Vercel → Settings → Environment Variables)

| Name | Where | What |
|---|---|---|
| `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET` | all | Google OAuth web client. Redirect URIs: `https://<address>/api/callback` for the live and test addresses |
| `GEMINI_API_KEY` | all | form scanner |
| `KV_REST_API_URL`, `KV_REST_API_TOKEN` | all | Upstash Redis (added by connecting the database) |
| `APP_ENV` = `test` | **Preview only** | makes the test copy use separate data (`apf-test:` keys, Drive "AP Finance – TEST") |
| `ADMIN_EMAIL` | optional | the admin Gmail (default arunpoudel9957@gmail.com) |

Never put keys or secrets in the code; this repository is public.

`js/core.js` is generated from `tools/core-src/*.js` with `python3 tools/build-core.py`.
