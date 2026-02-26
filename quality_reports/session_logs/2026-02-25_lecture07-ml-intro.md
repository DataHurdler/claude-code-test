# Session Log: Lecture 07 — Machine Learning Introduction
**Date:** 2026-02-25
**Status:** COMPLETE
**Lecture:** `Slides/Lecture07_MLIntro.tex` + `scripts/Lecture07_MLIntro.ipynb`

---

## Goal

Create Lecture 07 (Machine Learning Introduction) as a full first draft — the bridge from classical forecasting (L01–L06) into the ML portion of the course (L07–L12).

---

## Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| Sections 5 & 6 are previews only (regularization, features) | Full treatments in L08 and L11; L07 establishes vocabulary and motivation without duplicating future content |
| Synthetic bias-variance illustration in notebook | RSXFS has no known ground truth; polynomial + sin example shows the U-curve cleanly with controlled σ² |
| Walk-forward evaluation AND TimeSeriesSplit CV in same notebook | L07 objective: distinguish "evaluation" (walk-forward, from L06) from "tuning" (TimeSeriesSplit CV, new in L07) |
| Validation color: `unogreen` (not orange) | `unoorange` not defined in header.tex; traffic-light convention: blue=train, green=val, red=test |
| `[fragile]` on frames with lstlisting | Required for verbatim environments inside Beamer frames |

---

## Compilation Issues Encountered and Resolved

### Issue 1: `\pgfmathsetmacro` inside Beamer frame
**Cause:** `\pgfmathsetmacro{\ybot}{(\fold-1)*0.7}` inside a `\foreach` loop fails
in Beamer because frames save and replay content.
**Fix:** Replaced with hardcoded y-coordinates for each of the 5 walk-forward folds.
**[LEARN:latex] Never use `\pgfmathsetmacro` inside Beamer frames — use hardcoded coordinates.**

### Issue 2: `unoorange`/`unolightorange` colors not defined
**Cause:** Validation band used `\unoorange` and `\unolightorange` which don't exist
in `header.tex`. Only blue, red, gray, green variants are defined.
**Fix:** Changed all validation colors to `unogreen` / `unolightgreen`.
**[LEARN:latex] header.tex palette: unoblue, unored, unogray, unogreen + light variants. No orange.**

### Issue 3: `lstlisting` inside `\column` without `[fragile]`
**Cause:** `lstlisting` is a verbatim environment; fails inside Beamer `columns`
unless the frame uses `[fragile]`.
**Fix:** Added `[fragile]` to both frames containing `lstlisting` blocks.
**[LEARN:latex] Any Beamer frame with verbatim/lstlisting must use `[fragile]`.**

### Issue 4: Overfull \hbox (55.27pt) on "Three Gaps" table
**Cause:** Three-column table with `\small` overflowed the left column (0.54\textwidth).
**Fix:** Switched to `\footnotesize` with explicit `p{...}` column widths and
shorter cell text.

### Issue 5: Overfull \vbox (5.3pt) on walk-forward CV frame
**Cause:** Frame content slightly too tall.
**Fix:** Reduced TikZ `yscale` from 0.72 to 0.60; increased `\vspace{-0.1cm}` to `\vspace{-0.3cm}`.

### Issue 6: `\end{frame}` unclosed — pipeline frame
**Cause:** TikZ `box/.style` was missing `align=center`; nodes with `\\` newlines
inside them triggered `! LaTeX Error: Not allowed in LR mode`.
**Fix:** Added `align=center` to `box/.style` in the pipeline TikZ.
**[LEARN:latex] TikZ node with `\\` newlines requires `align=center` in style.**

---

## Quality Review Findings and Fixes

### MAJOR
1. **`\log(\lambda)` ambiguous** — shrinkage path x-axis used `$\log(\lambda)$` but
   tick labels showed base-10 values. Fixed to `$\log_{10}(\lambda)$`.

### No CRITICAL issues found.

---

## New Bibliography Entries Added

```bibtex
Bergmeir2018  — Validity of CV for autoregressive TS prediction, CSDA 2018
Arlot2010     — Survey of cross-validation procedures, Statistics Surveys 2010
```

---

## Final State

| Item | Value |
|------|-------|
| PDF pages | 30 |
| Compilation errors | 0 |
| Overfull hboxes | 0 |
| Undefined citations | 0 |
| New bib entries | Bergmeir2018, Arlot2010 |
| Notebook sections | 9 |
| Notebook figures | lecture07_cv_tuning.png, lecture07_bias_variance.png, lecture07_horizon_profile.png, lecture07_lasso_path.png |

---

## [LEARN] Entries

- `[LEARN:latex] Never use \pgfmathsetmacro inside Beamer frames — Beamer's save/replay breaks it. Use hardcoded coordinates.`
- `[LEARN:latex] header.tex color palette: unoblue, unored, unogray, unogreen and light variants. No orange. Validation = unogreen.`
- `[LEARN:latex] Beamer frames with verbatim/lstlisting must use [fragile] option.`
- `[LEARN:latex] TikZ node styles with \\\\ newlines require align=center in the style definition.`
