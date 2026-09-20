# Mr. J's Math 8 — Claude Code Project Guide

## Project overview
Static GitHub Pages site (`anjohnso-sys/mrj-math8`) of interactive HTML math tools for classroom use.
All tools are self-contained single-file HTML/CSS/JS — no build step, no external dependencies,
works offline once loaded. Sister site to `mrj-math7` (same conventions, same design system).

## Course context
Elk Island Public Schools · Mathematics 8 · 2026-27
Textbook: Math Focus 8 (Nelson). Units 4, 7 and 8 are PILOT units on draft outcomes
(Rational and Irrational Numbers; Linear Equations; Linear Functions and Graphing) and have
no fully aligned textbook chapter.

## Curriculum structure

| Unit | Title | Organizing Idea |
|------|-------|-----------------|
| 1 | Square Roots and the Pythagorean Theorem | Number / Shape and Space |
| 2 | Integers | Number |
| 3 | Fractions | Number |
| 4 | Rational and Irrational Numbers | Number (pilot) |
| 5 | Proportional Reasoning | Number |
| 6 | Percents | Number |
| 7 | Linear Equations | Algebra (pilot) |
| 8 | Linear Functions and Graphing | Functions (pilot) |
| 9 | Surface Area and Volume | Shape and Space |
| 10 | 3-D Objects and Views | Shape and Space |

## File naming convention
```
unit{N}/Unit{N}_{ShortName}.html        ← general tool
unit{N}/Unit{N}_L{NN}_{ShortName}.html  ← lesson-specific tool
```
Examples: `unit1/Unit1_SquaresOnTriangles.html`, `unit8/Unit8_L03_SlopeExplorer.html`

## Design system — tool pages (dark navy theme)

```css
/* Backgrounds */
body bg:        #1F3864
card/panel bg:  #142850
canvas bg:      #0f1a2e
border:         #2d4f8e

/* Text */
primary text:   #f1f5f9
muted text:     #94a3b8

/* Accents */
gold (heading, highlight): #F5A623
blue (positive):           #60a5fa
red (negative):            #f87171
purple:                    #a78bfa

/* Font */
'Segoe UI', system-ui, sans-serif
```

## Design system — index.html only

```css
page bg:        #f0f4fa   /* light, not dark */
header:         linear-gradient(135deg, #1a3a6b 0%, #2d6be4 100%)
card header:    #1a3a6b
unit badge:     #2d6be4
```

## Canvas conventions
- Standard size: 640×280 (horizontal tools), adjust as needed — larger stages are fine when the
  activity needs a work area (e.g. `Unit1_SquaresOnTriangles.html` uses 1040×640).
- Rendering: `requestAnimationFrame` loop with `dt`-scaled movement
- Input: pointer events (touch-compatible), click-only from UI buttons (no drag from banks)
- Projector-friendly: large labels (≥17px), thick lines (lineWidth ≥ 4), high contrast

## Pedagogy constraints
- **Never display formulas or answers that give away the math** — tools support exploration, not shortcuts
- Tools should work without teacher explanation of the UI (intuitive affordances)
- Designed for classroom projector display — legibility over density

## Adding a new tool — checklist
1. Create `unit{N}/Unit{N}_{ShortName}.html`
2. Add a footer link back to the index:
   ```html
   <p class="foot"><a href="../index.html">&larr; Back to Mr. J's Math 8</a></p>
   ```
3. Open `index.html` and add a link inside the correct unit's `<ul class="resource-list">`:
   ```html
   <li><a href="unit{N}/FileName.html"><span class="icon">EMOJI</span> Title</a></li>
   ```
4. If the unit previously had only `<li><span class="coming-soon">Resources coming soon</span></li>`, remove that line.
5. Tell the user which files changed so they can upload them.

## Publishing — how this site actually gets updated
There is **no local git repository and no git commands**. The user publishes by hand on
github.com: *Add file → Upload files*, then drags the changed files and folders from
`~/Documents/Claude/mrj-math8` onto the page and commits there.

What this means in practice:
- Drag the **contents** of the project folder (`index.html`, `unit1/`, …) — never the
  `mrj-math8` folder itself. Dropping the parent nests the whole site one level deep and
  breaks the Pages URL.
- Re-uploading a file at the same path overwrites it. **Uploading never deletes.**
  Removing or renaming a file has to be done in the GitHub UI (open the file → delete icon).
- Leave no hidden files (`.DS_Store`) in a folder that is about to be dragged.

At the end of every session, tell the user:
1. which files changed, as full paths they can find in Finder, and
2. anything that must be **deleted** on GitHub — a drag-upload cannot do it.
