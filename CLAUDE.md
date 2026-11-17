# Push-Ups

Ross's personal six-week push-up plan (goal: 50 in a row) as an iPhone home-screen app. Live at
<https://rossdavilla.github.io/push-ups/>.

`README.md` holds the plan itself — the weekly workouts, the progression rules, the taper and the
max-test days. **That table is the spec.** When a workout looks wrong, check it against the README
before changing the code, and change both together.

## Layout

```
index.html              the whole app — HTML, CSS and JS in one file, no dependencies
sw.js                   service worker: makes it work offline from the home screen
manifest.webmanifest    PWA manifest
icon-180/192/512.png    home-screen icons
```

## Things to know before changing it

- **It is a PWA.** `sw.js` is network-first with a cache fallback (`CACHE = 'pushups-v1'`,
  `skipWaiting()`), so an edit to `index.html` reaches his phone as soon as it is online and the
  app still opens without a connection. Bump that cache name when you change the `SHELL` list of
  precached files; the old cache is deleted on activate.
- **The plan is date-driven.** The app reads today's date and shows that day's workout, so the
  plan has a real start date (Monday, Nov 16, 2026 for the current block). Changing the start
  date reshuffles every workout; be explicit about it.
- **The log is the only copy.** Sets, rest timings and max tests live in `localStorage` on the
  phone — no backend, no sync. Progress → Backup copies it out as text. Never ship a change that
  clears or reshapes stored log data without a migration, and say so if one is unavoidable.

## Publishing

GitHub Pages serves `main` from the repository root, so a push to `main` is the deploy. Already
listed in `data/sites.json` in the
[`rossdavilla.github.io`](https://github.com/rossdavilla/rossdavilla.github.io) repo under the
`personal` tag.
