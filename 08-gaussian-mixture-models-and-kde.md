# Gaussian Mixture Models, EM & Kernel Density Estimation

> **Unsupervised learning** · L14, L15 · Week 8  
> **Quiz:** Q7 — L14, L15

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L14 — GMM — Part 1 | W8 (Oct 12-16) | not posted yet — `09-gaussian-mixture.pdf` | not posted yet — `09-gaussian-mixture-note.pdf` |
| L15 — GMM — Part 2 | W8 (Oct 12-16) | not posted yet — `09-gaussian-mixture.pdf` | not posted yet — `09-gaussian-mixture-note.pdf` |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Anything marked *not posted yet* 404s as of Sep 6, 2026; re-check with `../scripts/check-slides.sh`.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [KDE interactive visualization](https://mathisonian.github.io/kde/) — *W8*
- [Drawing samples from a kernel density estimate (CrossValidated)](https://stats.stackexchange.com/questions/321542/how-can-i-draw-a-value-randomly-from-a-kernel-density-estimate) — *W8*
- [KernelDensity in scikit-learn (docs + sampling)](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KernelDensity.html) — *W8*
- [Kernel density example (course notebook)](https://mahdi-roozbahani.github.io/CS46417641-fall2026/other/06-and-08-plot_dbscan.ipynb) — *W8*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Pattern Recognition and Machine Learning — Bishop (mixture models & EM)
- The Elements of Statistical Learning — Hastie, Tibshirani & Friedman

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] GMM as soft k-means: what exactly is the responsibility gamma(z_nk), and what does k-means look like as a limiting case?
- [ ] EM: write the E step and M step, and say what quantity is guaranteed to increase each iteration.
- [ ] Why can the GMM likelihood diverge to infinity, and what stops it in practice?
- [ ] KDE: role of the kernel vs role of the bandwidth — which one actually matters?

## Notes on this topic

EM is the piece most likely to show up on a quiz as a derivation rather than a definition. Budget prep time for writing the E and M steps from scratch.

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
