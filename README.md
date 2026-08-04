# OneKilo Patient Portal — Deployable Build

A single, self-contained `index.html`. No build step, no dependencies to install.

## Run / deploy
- **Locally:** open `index.html` in a browser (or `npx serve .`).
- **Host:** drop `index.html` on any static host — GitHub Pages, Netlify, Vercel, S3, etc. That's the whole app.

## How it's built (kept intentionally simple)
- Plain **React 18** + **Babel** loaded from CDN (`<script>` tags in `<head>`).
- The entire app is one JSX block in `<script type="text/plain" id="appsrc">`, compiled in-browser at load (classic JSX runtime → global `React.createElement`) and mounted into `#root`.
- All styling is inline style objects + a small `<style>` block for fonts, resets, and keyframe animations. Design tokens (colors, radii) live at the top of the script as small helper functions (`seg`, `slotSt`, `vstep`, …).

## What's inside (all screens & interactions preserved)
Onboarding: eligibility sliders + live BMI, "What brings you here?" (4 sequential questions), medical history (2 questions), pincode serviceability check, consult booking, OTP bottom-sheet, account-created, payment. Dashboard: Home (stat tiles + program-stage cards + locked journey), Lab booking, Appointments, Lab & Reports, Medication (pharmacy dispatch), Progress, Notifications, Profile — with the hamburger drawer nav.

## Going to production (optional, recommended)
In-browser Babel is fine for demos but recompiles on every load. For production, move the JSX into a Vite + React + TypeScript project:
```
npm create vite@latest onekilo -- --template react-ts
```
Paste the components from `index.html` into `src/`, replace the CDN scripts with `npm i react react-dom`, and `npm run build`. Same code, precompiled.
