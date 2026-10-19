<div align="center">

<img src="icons/icon-192.png" width="96" alt="Petalouda icon">

# Petalouda

**A mobile-first meal planning and weight-loss companion.**

Personalised calorie targets, portion-scaled meal suggestions, hydration and activity tracking, and daily goals, all stored privately on the user's device.

[**Live demo**](https://giannismar94.github.io/Meal-Prep-app/) · [Features](#features) · [Getting started](#getting-started) · [Deployment](#deployment)

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![PWA](https://img.shields.io/badge/PWA-ready-5A0FC8?logo=pwa&logoColor=white)
![No dependencies](https://img.shields.io/badge/dependencies-none-2fa77c)

</div>

---

## Overview

Petalouda (Greek for *butterfly*) is a progressive web app that helps a user lose weight sustainably. After a short onboarding, it calculates daily energy, protein and water targets, then generates a daily meal plan with ingredient weights scaled to those targets. Progress is reinforced by **Lila**, an animated mascot that evolves from caterpillar to butterfly as the user completes daily goals.

The app is built with plain HTML, CSS and JavaScript. It has no framework, no build step and no backend, and runs entirely in the browser. The user interface is in Greek.

## Features

| Area | What it does |
| --- | --- |
| **Personalised targets** | Calculates BMR with the Mifflin–St Jeor equation, applies an activity multiplier and a chosen weekly loss rate (0.25 / 0.5 / 0.75 kg), and derives calorie, protein and water targets. |
| **Meal planning** | Builds a daily plan across five configurable meal slots from a library of 40+ meals, including traditional Greek home cooking. Ingredient weights are rescaled to fit each slot's calorie budget. |
| **Meal choice** | Each meal can be swapped for another suggestion, picked from a list, marked as a favourite (suggested more often) or hidden. Users can save their own custom meals. |
| **Food logging** | One-tap logging for planned meals, plus free-form entries for anything off-plan. Calories and protein are totalled live. |
| **Hydration** | Glass-based water tracker. The target rises automatically on training days. |
| **Activity** | A weekly home-workout and walking schedule with step-by-step instructions and estimated energy expenditure. |
| **Daily goals** | Configurable checklist. Water, calorie and activity goals complete automatically from logged data, and custom goals can be added. A 14-day grid shows what was and wasn't achieved. |
| **Progress** | Weight log with trend chart, goal line, weekly averages and a 7-day calorie chart. |
| **Gamification** | Each completed goal earns a 🦋. Lila evolves through four stages as they accumulate. |
| **History** | Any previous day can be opened and filled in after the fact. |

### Safety by design

- Calorie targets never fall below **1,200 kcal (women) / 1,500 kcal (men)**.
- The daily deficit is capped at 25% of estimated maintenance.
- Goal weights below a healthy BMI (18.5) are rejected at onboarding.
- Users must be 18 or older.
- Messaging stays supportive. Exceeding a target never triggers negative feedback.

## Privacy

All data stays on the device.

- Stored in the browser's `localStorage` under the key `petalouda_v1`, so data is isolated from other apps on the same `github.io` origin.
- No accounts, no server, no analytics, no third-party tracking.
- Each device and browser keeps its own independent data.
- Users can export a JSON backup from **Settings** and restore it on another device.

## Tech stack

- **HTML5 / CSS3 / vanilla JavaScript.** A single self-contained `index.html`.
- **Inline SVG** for the mascot, charts and icons. No image or chart libraries.
- **Service worker** for offline support, using network-first for the page and cache-first for assets.
- **Web App Manifest** for installation on iOS and Android home screens.

## Project structure

```
.
├── index.html             # App: markup, styles, logic, meal and exercise data
├── manifest.webmanifest   # PWA manifest
├── sw.js                  # Service worker (offline caching)
└── icons/
    ├── icon.svg
    ├── icon-192.png
    ├── icon-512.png
    └── apple-touch-icon.png
```

## Getting started

No installation is required. Serve the folder with any static server:

```bash
git clone https://github.com/giannismar94/Meal-Prep-app.git
cd Meal-Prep-app
python3 -m http.server 8000
```

Then open <http://localhost:8000>. The service worker only registers on `https` or `localhost`.

## Deployment

The app is hosted on **GitHub Pages**:

1. Push the files to the root of the `main` branch.
2. Go to **Settings → Pages** and set the source to *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. The site is published at `https://<username>.github.io/<repository>/`.

### Installing on a phone

- **iOS:** open the link in Safari, then *Share → Add to Home Screen*.
- **Android:** open the link in Chrome, then *⋮ → Install app*.

On iOS, launching from the home screen icon is recommended. Safari may clear storage for websites that have not been visited for several days, while home screen web apps are exempt.

### Releasing updates

After changing any file, increment the cache version in `sw.js`:

```js
const CACHE = 'petalouda-v2';
```

This makes installed clients fetch the new version. User data is not affected.

## Customisation

The data sets are defined at the top of the `<script>` block in `index.html`:

| Constant | Contents |
| --- | --- |
| `F` | Food database: kcal and protein per 100 g, or per unit |
| `MEALS` | Meal library: ingredients, default quantities and which items scale |
| `W` / `WEEK` | Workout library and default weekly schedule |
| `DEFAULT_GOALS` | Goals created at onboarding |

## Disclaimer

Petalouda provides general estimates for informational purposes only. It is not a substitute for advice from a doctor or registered dietitian. Consult a healthcare professional before making significant changes to diet or exercise, especially if you have a medical condition.

## Author

**Ioannis Maroufidis** · [@giannismar94](https://github.com/giannismar94)

Built with care for someone special 💜
