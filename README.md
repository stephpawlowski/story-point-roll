# Story Point Roll

A Fibonacci D8 die roller for agile story point estimation. Built as a fun internal team tool.

**Live URL:** https://stephpawlowski.github.io/story-point-roll/

---

## What it is

A single-page interactive prototype of an 8-sided die (d8) with Fibonacci story point values: **1, 2, 3, 5, 8, 13, 21**, and a **Pantheon lightning bolt** wild card. Roll it when your team can't agree on a story point estimate and just needs to pick something.

The die uses weighted randomness — 3, 5, and 8 land more often than 1, 2, or 13, and 21 and the lightning bolt are rare.

---

## Where it lives

| Thing | Location |
|---|---|
| GitHub repo | https://github.com/stephpawlowski/story-point-roll |
| Live site | https://stephpawlowski.github.io/story-point-roll/ |
| Local source file | `/Users/stephaniepawlowski/work/fun/fibonacci-d8.html` |
| Local repo folder | `/Users/stephaniepawlowski/story-point-roll/` |

The source of truth for editing is `fibonacci-d8.html` in the `fun` folder. The repo contains a copy of that file renamed to `index.html` (required for GitHub Pages to serve it at the root URL).

---

## How it was built

**Single file** — the entire prototype is one self-contained HTML file with no external dependencies beyond two Google Fonts imports (Poppins). No framework, no build step, no npm.

**Rendering** — the die is a 3D octahedron drawn on an HTML `<canvas>` element using raw JavaScript. It uses:
- Gouraud shading (per-vertex lighting with linear gradients) for the 3D face appearance
- A perspective projection with a painter's algorithm (back-to-front face sorting)
- Blinn-Phong lighting with a key light from upper-left-front
- CSS `translateY` physics (gravity + bounce) for the drop animation
- Time-based exponential deceleration for the roll

**Pantheon branding** — uses exact PDS design token values (no PDS components):
- Face colors interpolate from `#3017a1` (shadow) to `#f4f3fc` (lit)
- Gold edges: `#ffdc28` (brand secondary)
- The lightning bolt uses the official Pantheon brand mark SVG paths from the `PantheonLogo` PDS component (icon-only variant, viewBox `0 0 20 50`)
- Typography: Poppins (PDS default font)
- Card elevation: PDS `elevation-raised` box-shadow tokens
- All colors sourced from `pds-react.pantheon.io`

**Hosting** — GitHub Pages serving directly from the `main` branch root. `<meta name="robots" content="noindex, nofollow">` prevents search engine indexing. The URL is shareable but not discoverable.

---

## How to make edits

All edits happen in the source file:

```
/Users/stephaniepawlowski/work/fun/fibonacci-d8.html
```

Open it in a browser directly to test changes locally (just double-click the file, or `open fibonacci-d8.html` in Terminal).

Once you're happy with the change, deploy it with these three commands:

```bash
cp /Users/stephaniepawlowski/work/fun/fibonacci-d8.html /Users/stephaniepawlowski/story-point-roll/index.html
cd /Users/stephaniepawlowski/story-point-roll
git add index.html && git commit -m "Update prototype" && git push
```

GitHub Pages rebuilds automatically. The live URL is usually updated within 30–60 seconds of pushing.

---

## Things you might want to tweak

**Fibonacci values / faces**
The sequence is defined at the top of the `<script>` block:
```js
const FIB = [1, 2, 3, 5, 8, 13, 21, BOLT];
```
`BOLT` is a sentinel value (`null`) that triggers the Pantheon lightning bolt to render instead of a number.

**Weighted probabilities**
Right below `FIB`, the weights control how often each face lands:
```js
const WEIGHTS = [5, 5, 6, 7, 7, 5, 2, 1]; // index matches FIB above
```
Higher number = more likely. The current setup makes 3, 5, and 8 land a bit more often, and 21 and the bolt are rare.

**Roll duration**
```js
rollDuration = (2 + Math.random() * 4) * 1000; // 2–6 seconds
```
Adjust the `2` (minimum) and `4` (added range) to change how long the die rolls.

**Colors**
All colors are defined as plain hex values near the top of the script. They match PDS tokens but are hardcoded so the file stays dependency-free.

---

## Sharing with the team

Send teammates the live URL: **https://stephpawlowski.github.io/story-point-roll/**

No login required. Works on mobile and desktop. The page is not indexed by search engines — it can only be reached by someone who has the link.
