# Mars Field Sales Run

Team sales-training game: drive the Mars van, audit the store, place POSM, negotiate. Live leaderboard, save & resume, facilitator panel for scenarios.

Runs free on Firebase Spark plan (Firestore + Auth) and either GitHub Pages or Firebase Hosting.

## 1. Firebase project (10 min, free)
1. https://console.firebase.google.com → **Add project** (Google Analytics off is fine). Stay on the free **Spark** plan.
2. **Build → Authentication → Get started → Sign-in method**: enable **Anonymous** and **Email/Password**.
3. **Authentication → Users → Add user**: create the facilitator login (e.g. abdelrahman.mohsen@r-kain.com).
4. **Build → Firestore Database → Create database** → production mode → location `europe-west` (closest to Egypt).
5. **Firestore → Rules**: paste the contents of `firestore.rules` → **Publish**. Edit the email list if needed.
6. **Project settings (gear) → Your apps → Web (</>)** → register app → copy the `firebaseConfig` values into `docs/firebase-config.js`.

## 2a. Host on GitHub Pages
1. Create a repo on github.com (e.g. `mars-sales-run`), upload this folder (keep the `docs/` folder).
2. Repo **Settings → Pages** → Source: *Deploy from a branch* → Branch `main`, folder `/docs` → Save.
3. Your game: `https://<your-username>.github.io/mars-sales-run/`
4. Firebase console → **Authentication → Settings → Authorized domains** → add `<your-username>.github.io`.

## 2b. Or host on Firebase Hosting
```
npm install -g firebase-tools
firebase login
firebase use --add          # pick your project
firebase deploy             # deploys docs/ and firestore.rules
```
Your game: `https://<project-id>.web.app`

## 3. Before the event
1. Open the game → **Facilitator sign-in** (bottom of the lobby) → sign in.
2. **Facilitator → Scenarios** → adjust prices, owners, policy → **Save scenario** (this also stores the default in the database).
3. **Event** tab → pick the scenario, add a message → **Apply**.
4. Share the link. Players just open it, create a team and play. No accounts needed.

## Free-tier limits (Spark plan)
50,000 reads / 20,000 writes / 1 GiB per day. Comfortable for ~30 teams playing a full session.
If you go over, the game stops saving until the next day (no charges unless you upgrade to Blaze).

## Notes
- Mars logo and brand names are client material: keep the repo **private** if Mars requires it (GitHub Pages on private repos needs a paid GitHub plan; Firebase Hosting works either way).
- Players are anonymous per browser. A team can be resumed from any device; only one device plays a team at a time.
