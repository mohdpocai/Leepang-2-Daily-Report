# Leepang 2 Daily Report

Daily productivity report for Leepang 2 Estate. One page (`index.html`), no build step.
Reports are saved in Firebase (Realtime Database), so the same data shows on every phone and computer you sign in on.

Until Firebase is set up, the page still works and saves on the device you are using.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole report page and editor |
| `firebase-config.js` | Your Firebase settings (you paste them in once) |
| `database.rules.json` | Who may read and change the data |
| `firebase.json` | Only needed if you host on Firebase Hosting |

## Quick setup: open to everyone (free, no sign-in)

`firebase-config.js` has `openAccess: true`, so the page needs no login. In Firebase **Realtime Database > Rules**, paste the contents of `database.rules.json` and press **Publish**. Anyone with the page link can then see and change the reports. Firebase's free Spark plan is enough.

To require a sign-in instead, use the steps below (they use a private-rules version; set `openAccess: false`).

## Set up Firebase with sign-in (about 10 minutes, once)

1. Go to <https://console.firebase.google.com> and choose **Add project**. Name it, for example, `leepang2-report`. Google Analytics is not needed.
2. **Build > Realtime Database > Create database.** Choose **Locked mode**. (Already created for this project, in Singapore.)
3. **Build > Authentication > Get started > Sign-in method > Email/Password > Enable.**
4. **Authentication > Users > Add user.** Enter your email and a password. Copy the **User UID** shown in the list.
5. **Realtime Database > Rules.** Paste the contents of `database.rules.json`, replace both `PASTE_USER_UID` with the UID you copied, and press **Publish**.
6. **Project settings (gear icon) > General > Your apps > Web (`</>`).** Register an app, then copy the `firebaseConfig` values into `firebase-config.js`.
7. Commit the change to `firebase-config.js`. The config values are not secrets. The data is protected by the sign-in and the rules in step 5.

Open the page, sign in with the email and password from step 4, and tap **Edit figures**.

## Put the page online

**GitHub Pages** (needs a public repository on a free GitHub account): repository **Settings > Pages > Build and deployment > Deploy from a branch > `main` / root**. The page will be at `https://<your-github-name>.github.io/<repository-name>/`.

**Firebase Hosting** (works with a private repository): install the Firebase CLI, then run `firebase login`, `firebase init hosting` (keep `firebase.json` as it is) and `firebase deploy`.

If sign-in says the domain is not allowed, add the page's domain under **Authentication > Settings > Authorized domains**.

## Move data from another copy of the page

In the old copy, open **Edit figures > Backup > Download backup**. In this copy, sign in, open **Edit figures > Backup > Import backup** and choose the file. Reports with the same date are replaced.

## Daily use

1. Tap **New day**. The Todate figures carry forward from the previous saved day.
2. In **Update daily**, type Today Crop, the gang figures and Rainfall today.
3. Tap **Save as image** to share the report, for example on WhatsApp.

## Budget table

The 2026/2027 monthly yield budget (July to June) is in `index.html` under `YIELD_BUDGET_2026_2027`. Add the next year's table there each year.
