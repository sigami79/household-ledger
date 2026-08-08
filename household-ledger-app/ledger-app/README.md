# Household Ledger — setup & deployment

## 1. Firebase project (5 min)

1. Go to console.firebase.google.com → **Add project** → name it e.g. `household-ledger`.
2. Left sidebar → **Build → Authentication** → Get started → enable **Email/Password**.
3. Left sidebar → **Build → Firestore Database** → Create database → **production mode** → pick a nearby region.
4. Left sidebar → **Firestore Database → Rules** tab → paste in the contents of `firestore.rules` (included in this folder) → Publish.
   This makes sure every person can only ever read or write their *own* income and spends — not anyone else's.
5. Gear icon (top left) → **Project settings** → scroll to "Your apps" → click **`</>`** (web) → register an app (any nickname, no need to tick Firebase Hosting) → copy the `firebaseConfig` object it shows you.
6. Open `firebase-config.js` in this folder and paste your values in over the `"REPLACE_ME"` placeholders.

## 2. Put it on GitHub Pages

1. Create a new GitHub repo (e.g. `household-ledger`).
2. Push all the files in this folder to it (`index.html`, `manifest.json`, `service-worker.js`, `firebase-config.js`, `icons/`).
3. Repo → **Settings → Pages** → Source: deploy from branch → `main` / `root` → Save.
4. After a minute or two, your app is live at `https://<your-username>.github.io/household-ledger/`.

## 3. Using it on iPhone / Android

Open that URL on the phone's browser.

- **iPhone (Safari):** tap Share → **Add to Home Screen**. It'll sit on the home screen and open full-screen, no browser bar — that's the "install."
- **Android (Chrome):** you'll usually get an **"Install app"** prompt automatically, or find it under the browser's ⋮ menu → "Install app."

There's no app store, no review process — anyone with the URL can sign up with their own email/password and get their own private ledger, in their own currency.

## Notes

- Each person's income, spends, and currency are private to their account (enforced by the Firestore rules above, not just hidden in the UI).
- `firebase-config.js` contains project identifiers, not secret keys — it's normal and expected for these to be visible in a public web app's source.
- If usage grows a lot, keep an eye on the Firebase free-tier quotas in the console (Usage tab) — for a household-scale app with a handful of users, you're extremely unlikely to hit them.
