# Bunny's Tag

A small website for Bunny (aka Orleans), the roommate dog. Tap her NFC tag to log meals and walks (with pee/poop), reserve her for holidays, track her food supply and keep a shared shopping list.

It's a plain static site hosted on GitHub Pages. The shared log is stored in Google Firebase (Cloud Firestore, free plan).

## Setup

### 1. Firebase (the shared log)
1. Go to <https://console.firebase.google.com>, click **Create a project**, and name it (e.g. `bunny-tag`). Google Analytics isn't needed.
2. In the left menu open **Build → Firestore Database → Create database**. Pick a location near you (e.g. `northamerica-northeast2` for Toronto) and start in **production mode**.
3. Open the **Rules** tab, paste in the contents of `firestore.rules`, replace `YOUR-HOUSE-KEY` with your house key, and click **Publish**.
4. Go to **Project settings** (gear icon) → **Your apps** → the **</>** (Web) button. Register an app (no hosting needed) and copy the `firebaseConfig` values into `config.js`.

### 2. GitHub Pages (the website)
1. In this repo go to **Settings → Pages**.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, then pick `main` and `/ (root)`. Save.
3. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

### 3. The NFC tag
Write this URL to the tag with the NFC Tools app (Write → Add a record → URL):

```
https://<your-username>.github.io/<repo-name>/?k=YOUR-HOUSE-KEY
```

The first time a phone opens that link, it remembers the key, so the plain site address works on that phone afterwards. Send the same link to roommates so they can open it without the tag.

Anyone without the key still sees Bunny's photo and intro but can't see or change the log.

## Files
- `index.html`: the whole app
- `config.js`: Firebase connection settings
- `firestore.rules`: database access rules (template)
- `manifest.json`, `images/`: home-screen icon and photos
