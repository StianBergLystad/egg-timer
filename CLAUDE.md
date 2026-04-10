# Egg Timer PWA — CLAUDE.md

## Prosjekt
Fysikkbasert eggtimer-PWA på stianberglystad.github.io/egg-timer. Single-file HTML/CSS/JS med service worker.

## Stack
- Vanilla HTML/CSS/JS, ingen rammeverk
- Capacitor (iOS + Android-bygg i `ios/` og `android/`)
- Hosting: GitHub Pages (ikke Webhuset)
- GitHub: https://github.com/StianBergLystad/egg-timer

## Filer
- `index.html` / `www/index.html` — hele appen
- `sw.js` — service worker, cache-first (cache-nøkkel må bumpes ved endringer)
- `manifest.json` — PWA-manifest
- `capacitor.config.json` — Capacitor-konfig

## Viktige detaljer
- **Williams-formel:** K=30.47, kalibrert til medium egg ved romtemperatur
- **Temaer:** CSS custom properties + `body[data-theme]` for norske høytidstemaer (påske/jul/mai17/pinse)
- **i18n:** `TRANS`-objekt + `t(key)` helper, localStorage-nøkkel: `egg-timer-lang`
- **Timer-persistens:** lagrer `endTime`-timestamp til localStorage (`egg-timer-state`) ved start
- **AudioContext:** nettlesere suspenderer den — kall alltid `resume()` før `playBeep()`
- **`frame-ancestors` CSP:** ignoreres i meta-tags (browser-advarsel, ikke feil)
- **Umami:** sender til `api-gateway.umami.dev` (ikke `cloud.umami.is`) — CSP `connect-src` må ha begge

## KRITISK ved deploy
Bump cache-versjonen i `sw.js` (for øyeblikket v4) **hver gang** `index.html` endres vesentlig.
Uten dette ser brukere utdatert innhold til cachen tømmes manuelt.

## Deploy
Push til `main`-branchen — GitHub Pages publiserer automatisk.
