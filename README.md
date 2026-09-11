# Sprout Planner

A cozy personal planner: to-do list, hourly day schedule, calendar view, and theme
customization — installable on your phone's home screen with real Google Calendar
notifications.

## 1. Put it on GitHub Pages (free hosting)

1. Go to [github.com/new](https://github.com/new) and create a new **public**
   repository, e.g. `sprout-planner`.
2. Upload all the files in this folder (`index.html`, `manifest.json`,
   `service-worker.js`, `icon-192.png`, `icon-512.png`) to the repository —
   easiest way is the "Add file → Upload files" button on the repo page.
3. Go to **Settings → Pages**. Under "Build and deployment", set **Source** to
   "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
4. After a minute, your app will be live at:
   `https://YOUR-USERNAME.github.io/sprout-planner/`
5. Open that link on your phone in Safari (iOS) or Chrome (Android), then use
   **Share → Add to Home Screen**. It'll launch full-screen with its own icon,
   like a real app — this is the service worker + manifest at work.

## 2. Connect Google Calendar (optional, ~10 minutes, one time)

This step is what makes reminders actually reliable — the event becomes a real
Google Calendar entry, so your phone notifies you even if Sprout Planner isn't
open. Skip this and the app still works fine: tapping the calendar icon on any
task just opens a one-tap "add to calendar" link instead.

1. Go to the [Google Cloud Console](https://console.cloud.google.com/) and
   create a new project (top-left project dropdown → New Project).
2. Go to **APIs & Services → Library**, search for **Google Calendar API**,
   and click **Enable**.
3. Go to **APIs & Services → OAuth consent screen**.
   - User type: **External**.
   - Fill in an app name (e.g. "Sprout Planner") and your email where asked.
   - On the "Test users" step, add your own Google account email. (Personal
     apps in "Testing" mode work fine for just yourself — no Google review
     needed.)
4. Go to **APIs & Services → Credentials → Create Credentials → OAuth client
   ID**.
   - Application type: **Web application**.
   - Under **Authorized JavaScript origins**, add your GitHub Pages URL
     *without* a trailing slash, e.g. `https://YOUR-USERNAME.github.io`.
   - Click **Create**. Copy the **Client ID** shown (looks like
     `123456-abc.apps.googleusercontent.com`).
5. Open Sprout Planner → **Theme** tab → paste the Client ID into the "Google
   Client ID" box → **Save** → **Connect Google Calendar** → sign in and
   approve access.
6. Optionally flip on **Auto-sync new items** so anything you add gets pushed
   to Google Calendar automatically, with a popup reminder right at its start
   time.

Each hourly item and dated task also has its own small calendar icon if you'd
rather sync things one at a time.

## Notes & limits

- Sprout Planner also has its own in-app notifications (Theme → Enable
  notifications), but those only fire while the page is open in a browser
  tab — that's a hard limitation of web apps, not something this app can work
  around. Google Calendar sync is the reliable path for phone alerts.
- The OAuth access token is kept in memory only (not saved to disk), so
  you'll reconnect once per browser session — this is intentional for safety.
- If Google sign-in doesn't seem to trigger, double check the Authorized
  JavaScript origin in step 4 matches your GitHub Pages URL exactly (no
  trailing slash, correct `https://`).
