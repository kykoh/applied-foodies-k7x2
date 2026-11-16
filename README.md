# Applied Foodies

Come for the food, stay for the stories. A live map, food trail and photo wall for our Applied Foodies lunches around the Applied Materials SOC.

- **Map**: Google Maps-style map of Singapore with every lunch pinned, routes from the SOC by transit, walking, cycling or driving, and a button to open real directions in Google Maps.
- **Our journey**: lunches logged, friends made, neighbourhoods explored, average score, leaderboard and friends list.
- **Food trail**: every lunch in order, plus the photo wall.

It's a static site (GitHub Pages) with Firebase (Firestore + Google sign-in) as the shared live database. Anyone with the link can view; signed-in guests can add scores out of 10; only editors can log, edit or delete lunches.

## One-time setup

1. **Create a Firebase project** at https://console.firebase.google.com (the free Spark plan is enough).
2. **Firestore**: Build > Firestore Database > Create database (production mode, region `asia-southeast1`).
   Then open the **Rules** tab, paste in the contents of `firestore.rules`, and click **Publish**.
3. **Sign-in**: Build > Authentication > Get started > Sign-in method > enable **Google**.
   Under Authentication > Settings > **Authorized domains**, add `<your-github-username>.github.io`.
4. **Web app config**: Project settings > Your apps > add a **Web** app, copy the `firebaseConfig` object
   into `firebase-config.js` (replace `null`), and commit.
5. **Make yourself an editor**: open the site, click **Sign in**, then click your name to see your **editor ID**.
   In Firestore, create a collection `editors` and add a document whose **Document ID** is that editor ID
   (add any field, e.g. `name: "Kian Yew"`). Repeat for your friend. Reload the page; your name shows "· Editor".
6. **GitHub Pages**: repo Settings > Pages > Source: *Deploy from a branch*, Branch: `main`, folder `/ (root)`.

## Notes

- Photos are resized in the browser and stored in Firestore (about 1280 px for the full photo plus a small thumbnail), so no paid Firebase Storage is needed.
- Pages are marked `noindex`, so search engines won't list them. Anyone who has (or guesses) the URL can still view the site.
- Map data © OpenStreetMap contributors (via protomaps tiles in cheeaun/busrouter-sg). Rail lines and stations from cheeaun/sgraildata (LTA data). Road routes are drawn on the OpenStreetMap road network; times are estimates.
