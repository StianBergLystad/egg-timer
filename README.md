# 🥚 egg-timer

A mobile-friendly Progressive Web App for cooking eggs perfectly — powered by the **Williams formula**, a physics-based equation that calculates the exact boiling time based on egg size and starting temperature.

**Live app → [stianberglystad.github.io/egg-timer](https://stianberglystad.github.io/egg-timer/)**

---

## Features

### Egg types
| Type | Target yolk temp | Base time (medium, room temp) |
|---|---|---|
| 🥚 Soft-boiled | 63 °C | 6 min |
| 😊 Smiling (jammy) | 71 °C | 8 min |
| 💪 Hard-boiled | 78 °C | 10 min |

### Physics-based timing
Cook time is calculated using a calibrated version of the **Williams formula**:

```
t = K · M^(2/3) · ln( (T_w − T_0) / (T_w − T_y) )
```

| Variable | Meaning |
|---|---|
| `M` | Egg mass (g) |
| `T_w` | Boiling water temperature (100 °C) |
| `T_0` | Starting temperature of the egg |
| `T_y` | Desired yolk temperature |
| `K` | Calibration constant (30.47) |

This means the timer automatically adjusts when you change:
- **Egg size** — Small (~50 g), Medium (~60 g), Large (~70 g)
- **Starting temperature** — Fridge (~4 °C) or Room temperature (~20 °C)

### Manual time adjustment
Fine-tune the calculated time with **±30 s** and **±1 min** buttons before or during a paused timer.

### Norwegian holiday themes
The app detects the current date against the Norwegian public holiday calendar and automatically switches to a seasonal theme — reverting to the default when the holiday ends.

| Holiday | Period | Theme | Icons |
|---|---|---|---|
| 🐣 Easter (*Påske*) | Palm Sunday → Easter Monday | Spring green | 🐣 🐥 🐔 |
| 🎄 Christmas (*Jul*) | Dec 1 → Jan 6 | Christmas red | ⛄ 🎄 🎅 |
| 🇳🇴 Constitution Day (*17. mai*) | May 17 | Norwegian blue + red | 🇳🇴 🎉 🏆 |
| 🕊️ Whitsun (*Pinse*) | Whit Sunday → Monday | Sky blue | 🌸 🕊️ 🌺 |

Easter is computed dynamically for any year using the **Gregorian (Gauss) algorithm** — no hardcoded dates.

### PWA — installable on your phone
The app is a fully offline-capable Progressive Web App:
- **Android (Chrome):** tap `⋮` → *Add to Home screen*
- **iPhone/iPad (Safari):** tap `⎙` → *Add to Home Screen*

Once installed it opens fullscreen, with no browser chrome, and works without an internet connection.

---

## Tech stack

- **Single HTML file** — all HTML, CSS and JavaScript in `index.html`
- **Service worker** (`sw.js`) — cache-first offline strategy, v2 cache key
- **Web Manifest** (`manifest.json`) — PWA metadata and icons
- **SVG icon** (`icon.svg`) — scalable egg icon

No frameworks, no build tools, no dependencies.

---

## Security

- Content Security Policy (CSP) with `object-src 'none'`, `base-uri 'self'`, `frame-ancestors 'none'`, `upgrade-insecure-requests`
- `Referrer-Policy: no-referrer`
- Service worker only caches `response.ok && response.type === 'basic'` responses
- Holiday theme ID whitelist-validated before DOM assignment

> `unsafe-inline` is required for `script-src` and `style-src` by design (single-file architecture). No user input is rendered as HTML.

---

## Formula reference

> C.D.H. Williams, *"The Mathematics of Eggs"*, University of Exeter.
>
> *"Some people buy an egg timer. Others get a PhD."*

---

## License

MIT
