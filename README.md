# The Salem Trials

An online hidden-role card game for 4–12 players: witches, accusations, trials, the Pact and the Raven.
It's a plain static website (no build step). Multiplayer runs on **Firebase** (free), hosting on **Vercel** (free), code on **GitHub**.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The whole game |
| `firebase-config.js` | **You edit this once**: your Firebase project's settings |
| `firestore.rules` | Database rules you paste into Firebase |
| `vercel.json` | Small Vercel setting (always loads the newest config) |
| `README.md` | These instructions |

---

## Step 1: Firebase (the shared game database), about 5 minutes

1. Go to <https://console.firebase.google.com> → **Create a project** (any name, Analytics optional).
2. **Turn on anonymous sign-in:** Build → **Authentication** → Get started → *Sign-in method* → **Anonymous** → Enable → Save.
   (Players don't make accounts; each browser gets an invisible ID.)
3. **Create the database:** Build → **Firestore Database** → Create database → choose a location near you (e.g. `asia-southeast1` Singapore) → **production mode**.
4. **Paste the rules:** in Firestore open the **Rules** tab, replace everything with the contents of `firestore.rules`, click **Publish**.
5. **Get the web settings:** ⚙️ Project settings → General → *Your apps* → click **`</>`** (Web) → give it any nickname (no Hosting) → **Register app**. Copy the values inside `firebaseConfig`.
6. Open **`firebase-config.js`** and replace the placeholder values with yours. Save.

## Step 2: GitHub (stores the code)

1. Sign in at <https://github.com> → **New repository** → name it e.g. `salem-trials` → Public or Private → **Create repository**.
2. On the new repo page click **uploading an existing file**, drag in all the files from this folder (with your edited `firebase-config.js`), and click **Commit changes**.

## Step 3: Vercel (puts it online)

1. Sign in at <https://vercel.com> with your GitHub account → **Add New… → Project**.
2. **Import** your `salem-trials` repository.
3. Framework preset: **Other**. Leave the build command and output directory empty. Click **Deploy**.
4. You get an address like `https://salem-trials.vercel.app`. Every time you commit to GitHub, Vercel updates the site automatically.

## Step 4: Allow your Vercel address in Firebase (don't skip!)

Firebase → **Authentication** → **Settings** → **Authorized domains** → **Add domain** → enter your Vercel address *without* `https://` (e.g. `salem-trials.vercel.app`). Add any custom domain too.
If you skip this, players see "Couldn't connect to the game server".

## Step 5: Play

1. Open your Vercel link, enter your name, **Create a game**.
2. Click **Copy invite link** and send it to friends. The link opens straight into your game: they type a name and press **Join**.
3. Fill empty seats with **+ Add bot** if you like (4–12 players), then **Start game**.
4. Best with a voice call alongside.

If the host closes their tab, after about 40 seconds the others get a **Take over as host** button and the game continues.

---

## Notes

- **Cost:** Firebase's free tier (50,000 reads and 20,000 writes a day) covers plenty of casual games.
- **Fair play:** hidden cards live in the shared database. The game only shows you your own, but someone using browser developer tools could peek. Fine for friends, not for strangers or competitive play.
- **Cleaning up:** old games stay in Firestore. Now and then you can delete documents in the `games` collection from the Firebase console.
- **Without Firebase settings** the site still works as a solo practice game against bots.
- **Updating the game:** replace `index.html` in your GitHub repo (keep your `firebase-config.js`) and Vercel redeploys within a minute.
