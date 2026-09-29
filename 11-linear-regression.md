# Linear Regression

> **Supervised learning** · L18, L19 · Week 10, 11  
> **Quiz:** Q10 — L18, L19

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L18 — Linear Regression | W10 (Oct 26-30) | not posted yet — `15-linear-regression.pdf` | not posted yet — `15-linear-regression-note.pdf` |
| L19 — Linear Regression (contd) | W11 (Nov 2-6) | not posted yet — `15-linear-regression.pdf` | not posted yet — `15-linear-regression-note.pdf` |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Anything marked *not posted yet* 404s as of Sep 6, 2026; re-check with `../scripts/check-slides.sh`.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [Simple linear regression in matrix format (CMU notes, PDF)](https://mahdi-roozbahani.github.io/CS46417641-fall2026/other/regression-cmu.pdf) — *W10*
- [Adding noise to regression predictors](http://madrury.github.io/jekyll/update/statistics/2017/08/12/noisy-regression.html) — *W10*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- The Elements of Statistical Learning — Hastie, Tibshirani & Friedman
- Learning from Data — Abu-Mostafa

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] Derive the normal equation from scratch: minimize ||y - Xw||^2, get w = (X'X)^-1 X'y.
- [ ] When is X'X singular, and what do you do about it? (Leads straight into regularization.)
- [ ] MLE view: least squares equals maximum likelihood under Gaussian noise. Show it.
- [ ] Bias-variance decomposition — write the three terms and say which one model complexity moves.

## Notes on this topic

The matrix-calculus identities from [Linear Algebra](02-linear-algebra.md) are the whole derivation here.

## My notes

### Before lecture


### During lecture


### After lecture — what I still don't get



## Quiz prep

- [ ] Re-read the professor's annotated notes
- [ ] Redo any worked example from the deck without looking
- [ ] Write my own one-paragraph summary of the topic


---

[Schedule](https://mahdi-roozbahani.github.io/CS46417641-fall2026/docs/course-info/course-schedule-mahdi/) · [All topics](README.md)
