# Mars Field Sales Run

Team sales-training game: drive the Mars van through Maadi, check the store, place POSM, negotiate. Private teams with join codes, live leaderboard, facilitator Control room, English/Arabic.

## Update an existing setup (from the previous version)
1. **Firestore rules**: Firebase console → Firestore Database → Rules → replace everything with `firestore.rules` from this folder → **Publish**.
   (Adds private team codes: `saves`, `keys`, `members` collections.)
2. **GitHub**: upload `index.html` (and `firebase-config.js` only if you changed it) to the repo's main folder → Commit.
3. Open the game → Facilitator sign-in → **Control room → Teams**:
   - Old teams show **Issue code**: press it once per team to give it a private code.
   - New teams: type a name → **Create team**, or **Quick add** N numbered teams.
   - **Copy all codes** gives you every team's code and join link to send out.

## How players join
- Open the link → pick their team → type the 6-character code → **Join and play** (or open the team's join link directly).
- The device remembers the team, so next time it's one tap: **Continue as …**
- Wrong code = no access. **New code** in the Control room locks out the old code instantly.

## Free plan budget (Firebase Spark: 50k reads / 20k writes per day)
The game is tuned for this:
- Progress saves at most every 30 s while playing, plus right away on important moments (deal closed, leaving a store, day end, pause, phone locked).
- The leaderboard only reloads a team when its score changes, not on every save.
- Team "in use" locks renew every 3 minutes.
- Offline cache: reloading the page doesn't re-download everything.

Rough use per team per hour: ~100 writes and ~60 reads, plus ~60 reads per hour for each open leaderboard or projector screen.
**About 25 teams playing for 4 hours fits comfortably in one day's free quota.** Running over doesn't charge you; saving just pauses until the next day.

## GitHub Pages (free)
Single self-contained `index.html` (~310 KB, ~90 KB gzipped). 3D graphics load in the background after the lobby appears.
Settings → Pages → Branch `main`, folder `/ (root)`.

## Notes
- Full screen starts automatically when a player joins (Android and desktop). iPhone Safari doesn't allow full screen for websites; there the game still uses the whole screen.
- Facilitator emails: `firebase-config.js` (FACILITATOR_EMAILS) **and** `firestore.rules` (facilitator()) must list the same emails.

## Realistic people (models folder)
The `models/` folder holds the 3D people (sales rep, kiosk owners, store managers) and their walk, idle and talk animations.
Upload the **whole `models` folder** next to `index.html` in the repository root. Without it the game still works, but uses the simple built-in characters.
The people come from the Microsoft Rocketbox avatar library (MIT licence, free for commercial use); see `models/ROCKETBOX-LICENSE.txt`.
Players can switch between Realistic and Simple people in Settings.
