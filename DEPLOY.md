# Ski Ready — Publish and connect login

Ski Ready v6 app files are already in this repository:
- `index.html` — approved purple/black/yellow app (Meals, Workouts, Drinks, Resorts, health-data import)
- `cloud-config.js` — public, browser-safe Supabase project URL and **publishable** key

## 1. Enable the website (GitHub Pages)

1. Open [repository Pages settings](https://github.com/callumcr27/Ski-ready/settings/pages).
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Set branch **main**, folder **/ (root)**, then **Save**.
4. The site address will normally be `https://callumcr27.github.io/Ski-ready/`. Wait for GitHub to confirm it is published before opening it.

## 2. Allow email sign-in to return to this website (Supabase)

1. Open [Supabase Authentication URL Configuration](https://supabase.com/dashboard/project/qxngltvddsgywaoyfuup/auth/url-configuration).
2. Set **Site URL** to the exact GitHub Pages URL displayed by GitHub, e.g. `https://callumcr27.github.io/Ski-ready/`.
3. Under **Redirect URLs**, allow the same HTTPS URL, and `https://callumcr27.github.io/Ski-ready/index.html` if you ever open that path. Save.

## 3. Test on Apple devices

1. In Safari open the *website URL* (not an HTML attachment in WhatsApp). Check each of the four tabs.
2. In **Cloud sync**, enter your email and request the one-time sign-in link.
3. Open the emailed link using the same browser and verify it brings you back to the website.
4. Before changing devices, export your data as a JSON backup from the old local app.
5. Import the backup in the new hosted app, **choose the local device copy to upload** if prompted, and allow the sync to complete.
6. On a second device, sign in with the same email and **choose the cloud copy**. Verify a test entry appears on both after refresh.

**Critical:** Do not choose the empty cloud copy instead of the device containing your historical data on first login. Keep your JSON backup until cross-device syncing has been verified.

## Current integration boundaries

- Ski Resorts: links to official resort status and webcams; direct live lift/run totals need an approved data feed.
- Oura / Apple Health / Fitbit / Samsung: tracker linking is not yet live; health CSV import is available. Apple Health needs a native iOS integration.
- Data is private via Supabase per-user row-level security. No private health records or API secrets belong in this repository.
- Email delivery from Supabase's default service can be restricted/rate-limited; a sender configuration may be necessary.
- The app uses local-first saves and revision-aware sync. Concurrent changes on two devices can require choosing the copy to keep rather than being merged automatically.
