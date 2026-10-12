# Clustering & K-Means

> **Unsupervised learning** · L11, L12 · Week 6  
> **Quiz:** Q5 — L11 (Toolbox P2), L12 (K-Means)

## Keyword definitions

### Clustering and distance

- **Clustering:** Grouping objects so that points *within* a cluster are similar and points *across* clusters are not. You pick the similarity/dissimilarity function; the algorithm finds the grouping under that function. Three design questions he lists: how to represent objects (vector space? normalization?), which similarity function, which algorithm steps.
- **Clustering is subjective:** The same Simpsons characters split into *family vs school employees* or *females vs males* depending on what you call similar. There is no single right clustering without a chosen distance.
- **Data matrix `X`:** `n x d`. Each row `x^(i)` is one data point, each column one feature. He draws this twice (pp. 11, 13) — row = sample, column = dimension.
- **Desired properties of a dissimilarity `d`** (p. 12):
  - **Symmetry** `d(x, y) = d(y, x)` — otherwise "Alex looks like Bob, but Bob looks nothing like Alex".
  - **Positive separability** `d(x, y) = 0` iff `x = y` — otherwise two different objects can't be told apart.
  - **Triangle inequality** `d(x, y) <= d(x, z) + d(z, y)` — otherwise "Alex is very like Bob and very like Carl, but Bob is very unlike Carl".
- **Minkowski (`L_p`) distance:** `d(x, y) = (sum_{i=1..d} |x_i - y_i|^p)^(1/p)`.
  - `p = 2` **Euclidean** (circled on p. 13 — the one k-means uses).
  - `p = 1` **Manhattan**, `sum |x_i - y_i|`.
  - `p = inf` **"inf"-distance** (Chebyshev), `max_i |x_i - y_i|`.
- **Hamming distance:** Manhattan distance when every feature is binary — the count of positions where two bit vectors differ.
- **Edit distance:** Cost of transforming one object into the other with deletions, substitutions and insertions, each with its own cost. Used for strings, where vectors don't apply.
- **Curse of dimensionality** (p. 15, whiteboard): in `d` dimensions a ball's volume is `c r^d`, so the fraction in an outer shell is `1 - (r_i / r)^d -> 1` as `d -> inf`. Almost all volume sits in the thin shell, data gets sparse, and Euclidean distances stop discriminating.

### K-Means

- **`k`:** The number of clusters. A **hyperparameter** — chosen before running, not learned (p. 18).
- **Hard clustering:** Each point belongs to exactly one cluster, `pi(i) in {1, ..., k}`. (Contrast with GMM's soft assignment next week.)
- **Cluster assignment step:** `pi(i) = argmin_{j=1..k} ||x^(i) - c_j||^2`. He labels it **Expectation**.
- **Center adjustment step:** `c_j = (1 / |{i : pi(i) = j}|) sum_{i : pi(i) = j} x^(i)` — the mean of the points assigned to `j`, written `c_g = (1/N_g) sum x^(i)`. He labels it **Maximization**. Together: k-means is an **EM**-style alternation.
- **Stopping rule:** Repeat while any cluster center changed.
- **Distortion (objective):** `min_{c, pi} sum_{i=1..n} ||x^(i) - c_{pi(i)}||^2` — sum of squared distances from each point to its own center. Also called the *distortion score*; it's the y-axis of the elbow plot. Whiteboard: `distortion = C_1 + C_2 + C_3`, the per-cluster sums.
- **K-medians:** Same loop with `|x|` (L1) in place of the square; the center becomes the median. Margin note on p. 22, next to a circled **outlier** — the median isn't dragged by one far point.
- **Elbow method:** Plot distortion against `k`; pick the `k` where the curve bends. Left of the elbow is **under-clustering**, right is **over-clustering**.
- **Time complexity:** `O(Iknd)` — `I` iterations, `k` centers, `n` points, `d` features.

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L11 — Data analysis toolbox — Part 2 | W6 (Sep 28-Oct 2) | [02-numpy_broadcasting_tutorial.ipynb](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/02-numpy_broadcasting_tutorial.ipynb) | — none listed on the schedule |
| L12 — Clustering & K-Means | W6 (Sep 28-Oct 2) | [08-clustering.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/08-clustering.pdf) | **[08-clustering-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/08-clustering-note.pdf)** |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Both clustering files are live as of Oct 7, 2026; re-check with `../scripts/check-slides.sh`.

The annotated PDF is 37 pages; the plain deck is 34. The extra pages are inserted whiteboard work — the centroid derivation (p. 32) and the `k^n` enumeration (p. 34). Page numbers below are PDF page numbers of the note file.

**L11 is the toolbox notebook, part 2** — the same notebook as L2 (Week 1), so Q5 can draw on NumPy broadcasting as well as k-means. Part 1's readings and footguns live in [Course Overview & Logistics](00-course-overview-and-logistics.md#data-analysis-toolbox-l2-l11). The overlap with this topic is the vectorized distance computation in k-means' assignment step — see section 7 below.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [K-Means and DBSCAN (course notebook)](https://mahdi-roozbahani.github.io/CS46417641-fall2026/other/06-and-08-plot_dbscan.ipynb) — *W5, W7*. The k-means half covers the three drawbacks (need `k`, outliers, non-spherical data) with scikit-learn demos, plus **silhouette analysis** and `init='k-means++'` — neither of which is in the deck.
- [Visualizing K-Means Clustering (Naftali Harris)](https://www.naftaliharris.com/blog/visualizing-k-means-clustering/) — linked from the deck, p. 22.

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Data Mining: Concepts and Techniques — Han, Kamber & Pei
- Pattern Recognition and Machine Learning — Bishop (k-means is the opening of the mixture-models chapter)

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] K-means objective (within-cluster sum of squares) and why Lloyd's algorithm is guaranteed to converge but not to the global optimum.
- [ ] Choosing k: elbow method, silhouette score — and why both are heuristics.
- [ ] Initialization sensitivity and what k-means++ fixes.
- [ ] Which cluster shapes does k-means fundamentally fail on? (Motivates GMM and DBSCAN.)

## Notes on this topic

The Week 5 reading list also included a *curse of dimensionality* article, but that link is dead (404) and has been dropped. The deck's p. 15 whiteboard covers the idea instead.

**What is *not* in the deck:** silhouette score and k-means++. Both are in the course notebook only. The deck's answer to "how to choose `k`" is the elbow method, and its answer to initialization is "randomly" plus the p. 30 question showing it matters.

### Flow of the lecture

Motivation (what clustering is, why it's subjective) → distance functions → the k-means algorithm and a worked 3-cluster run → analysis: the formal objective, NP-hardness, convergence, complexity, choosing `k`, drawbacks.

### 1. What clustering is (pp. 3-10)

Images, flags, names across languages (`Piotr / Pyotr / Petros / Pietro / Pedro / Pierre / Peter / Peder / Peadar`), handwritten digits. On the flags he draws **several different nested groupings** — the point is that more than one grouping is defensible (Union Jack flags; then tricolours; Brazil on its own or not). Same lesson as the Simpsons slide: "clustering is subjective". The long-haired man vs the cocker spaniel (p. 9) — similar under a hair-colour feature, not under any sensible one.

### 2. Distance functions (pp. 11-17)

Worked example (p. 14): `x` and `y` differ by 4 horizontally and 3 vertically.

| Distance | Computation | Value |
|---|---|---|
| Euclidean (`p = 2`) | `sqrt(4^2 + 3^2)` | **5** |
| Manhattan (`p = 1`) | `4 + 3` | **7** |
| inf-distance (`p = inf`) | `max{4, 3}` | **4** |

In general `L_inf <= L_2 <= L_1`.

**Problems with Euclidean distance** (p. 15): the Manhattan map — straight-line distance between two points isn't the walking distance on a street grid, so `L_1` is the right metric there. Then the shell argument for high dimension (see *Curse of dimensionality* above), and a sketch of a 1-D histogram spreading into a sparse 2-D cloud as a feature is added.

**Hamming** (p. 16): two 17-bit vectors differing at positions 4, 6, 10, 11, 16 → `d = 5`.

**Edit distance** (p. 17): `INTENTION -> EXECUTION`, aligned as

```
x:  I N T E * N T I O N
y:  * E X E C U T I O N
    d s s   i s
```

1 deletion (cost 5) + 3 substitutions (cost 1) + 1 insertion (cost 2) = `5 + 3 + 2 = 10`. The answer depends entirely on the cost table — change the costs and the distance changes.

### 3. K-Means results (pp. 19-21)

Vegetables clustered on **intensity alone** vs **colour alone** give different segmentations (p. 19); 11 colour clusters segment a castle photo (p. 20). The feature you cluster on decides what "similar" means — same message as section 1.

### 4. The algorithm (pp. 22-28)

```
initialize k centers c_1..c_k randomly
do
    (1) assignment  (E):  pi(i) = argmin_j ||x^(i) - c_j||^2        for every i
    (2) update      (M):  c_j   = mean of { x^(i) : pi(i) = j }      for every j
while any c_j changed
```

pp. 24-28 animate three centers on a 2-D toy set: from a bad start (`c_1` top-middle, `c_2` left, `c_3` bottom-middle) they migrate to the top-right, left and bottom-right groups in about two rounds.

Margin notes on p. 22: `f(x) = |x|` and **k-medians**, a diamond (the `L_1` unit ball), and an isolated point labelled **outlier**. Reading: squared error lets one far point drag a mean a long way; `|x|` gives the median, which an outlier can't move much.

### 5. Analysis (pp. 30-35)

**Two in-class questions** (p. 30), both circled **Yes**:

- *Will different initialization lead to different results?* **Yes.** His sketch: a round blob with two outlying points, split vertically by one initialization and horizontally by another.
- *Will the algorithm always stop after some iteration?* **Yes** — not "no, we need a max-iterations cap".

**Formal statement** (p. 31): given `x^(1..n) in R^d`, find centers `c_1..c_k in R^d` and an assignment `pi(i) in {1..k}` minimizing `sum_i ||x^(i) - c_{pi(i)}||^2`. Whiteboard: distortion = `C_1 + C_2 + C_3`, where `C_1 = a + b + c` is the sum of squared spokes from cluster 1's points to `c_1`.

**Why the center is the mean** (p. 32, derivation). For one cluster `g` with `N_g` points:

```
D = sum_{i=1..N_g} ||x^(i) - c_g||^2
  = sum x^(i)^2  -  2 c_g sum x^(i)  +  N_g c_g^2         (first term doesn't depend on c_g)
dD/dc_g = -2 sum x^(i) + 2 N_g c_g = 0
=>  c_g = (1/N_g) sum_{i=1..N_g} x^(i)
```

The boxed result on the page writes the sum's upper limit as `N`; it should be `N_g` — the sum runs over cluster `g` only.

**NP-hard** (p. 33): jointly minimizing over `c` and `pi` is a search over discrete assignments. With `n` points and `k` clusters there are `k^n` assignments; the assignment determines the centers and vice versa. The loss surface over that space has local minima — k-means finds one of them.

**Counting `k^n`** (p. 34): `X = {A, B, C}`, `k = 2` → `2^3 = 8` rows, listed by hand: `{A,B,C}|{}`, `{}|{A,B,C}`, `A|BC`, `B|AC`, `C|AB`, `BC|A`, `AC|B`, `AB|C`. Note what that count includes: two rows with an **empty** cluster, and each split twice with the labels swapped. Distinct partitions into two non-empty groups: only **3**.

**Convergence** (p. 35): "Will the k-means objective oscillate?" No:

1. The objective is `>= 0`, so its minimum is finite.
2. The assignment step can only lower it — each point moves to its nearest center.
3. The update step can only lower it — the mean is the `argmin_c` of the cluster's squared distances (p. 32).

A non-increasing sequence over finitely many (`k^n`) assignments must stop changing. It converges to a **local** minimum, not necessarily the global one.

Slide-text typos on p. 35: the assignment line is printed `argmin_j ||x_i - c_{pi(j)}||^2` and the update line `c_i = ...`; read them as `||x_i - c_j||^2` and `c_j`.

### 6. Complexity, choosing `k`, drawbacks (pp. 36-37)

**Time** (p. 36):

| Step | Cost |
|---|---|
| One distance `||x^(1) - x^(2)||^2` | `O(d)` — one term per feature |
| Reassign all points | `O(knd)` — `k` distances for each of `n` points (`O(kn)` with one feature) |
| Recompute centroids | `O(nd)` — each point added once to its center |
| `I` iterations | **`O(Iknd)`** |

**Choosing `k`** (p. 37): the **elbow method**. Plot distortion against `k`; distortion keeps falling as `k` grows (at `k = n` it's 0, every point its own center), so you can't just minimize it. Pick the bend — his example circles `k = 3`. Left of it: under-clustering. Right: over-clustering, buying little distortion per extra cluster.

**Drawbacks of k-means** (p. 37, handwritten):

1. Sensitive to outliers.
2. Works best for spherical-shaped clusters.
3. You need to know `k` in advance.

The course notebook demos all three, and shows DBSCAN fixing 1 and 2 without needing `k` — the setup for [DBSCAN](08-density-clustering-dbscan.md) and [GMM](07-gaussian-mixture-models-and-kde.md).

### 7. Toolbox P2 tie-in: vectorizing the assignment step

Not from the deck — my own bridge between L11 and L12, since the assignments are graded on vectorized NumPy.

```python
# X: (n, d) points, C: (k, d) centers
diff  = X[:, None, :] - C[None, :, :]   # (n, 1, d) - (1, k, d) -> (n, k, d)
dist2 = (diff ** 2).sum(axis=2)          # (n, k)
pi    = dist2.argmin(axis=1)             # (n,)   cluster index per point
C_new = np.stack([X[pi == j].mean(axis=0) for j in range(k)])   # (k, d)
```

Broadcasting rule: align shapes from the right; each pair of dims must be equal or one of them `1`. `(n, 1, d)` and `(1, k, d)` broadcast to `(n, k, d)`. `axis=2` sums over features; `argmin(axis=1)` picks the nearest center per row. An empty cluster makes `X[pi == j].mean(axis=0)` return `nan` (with a warning) — the `k^n` count above includes those cases.

## My notes

### Before lecture


### During lecture


### After lecture — what I still don't get



## Quiz prep

- [ ] Re-read the professor's annotated notes
- [ ] Redo any worked example from the deck without looking
- [ ] Write my own one-paragraph summary of the topic
- [ ] Practice bank: [`../quizzes/km.html`](../quizzes/km.html)

Things he worked by hand or left open — the likeliest quiz material:

- [ ] Euclidean / Manhattan / inf-distance for the 4-by-3 example: `5 / 7 / 4` (p. 14)
- [ ] Hamming distance between two bit vectors (p. 16); edit distance `INTENTION -> EXECUTION` with costs 5/1/2 → 10 (p. 17)
- [ ] State the three properties of a distance and the "Alex/Bob/Carl" failure each prevents (p. 12)
- [ ] Shell volume fraction `1 - (r_i/r)^d -> 1` — what it says about distances in high `d` (p. 15)
- [ ] Write both k-means steps from memory, and which one is E and which is M (p. 23)
- [ ] Derive `c_g = (1/N_g) sum x^(i)` from `dD/dc_g = 0` (p. 32)
- [ ] Why `k^n` assignments; enumerate the 8 for `{A, B, C}`, `k = 2` (p. 34)
- [ ] The three-step convergence argument, and why it gives a local minimum only (p. 35)
- [ ] `O(Iknd)` and where each factor comes from (p. 36)
- [ ] Elbow method, under/over-clustering, and the three drawbacks (p. 37)
- [ ] Toolbox: predict a broadcast shape, or say why it errors

### The relationship map

```
distance d(x, y):  symmetric · d = 0 iff x = y · triangle inequality
L_p = (sum |x_i - y_i|^p)^(1/p)
      p = 1 Manhattan (binary features -> Hamming)
      p = 2 Euclidean           <- k-means
      p = inf  max_i |x_i - y_i|
      L_inf <= L_2 <= L_1

k-means objective (distortion):   J(c, pi) = sum_i ||x_i - c_pi(i)||^2
  E-step: fix c,  pi(i) = argmin_j ||x_i - c_j||^2    J can only go down
  M-step: fix pi, c_j   = mean of cluster j            J can only go down
  J >= 0  +  finitely many (k^n) assignments  ->  stops, at a LOCAL min
  joint min over (c, pi) is NP-hard

swap squared L2 for L1  ->  center = median  ->  k-medians (outlier-robust)
cost per iteration O(knd) + O(nd);  total O(Iknd)
choose k: elbow on distortion vs k  (distortion -> 0 at k = n)
```

### Traps — the things that are implied but never said out loud

1. **Squared Euclidean isn't a metric; Euclidean is.** `||x - y||^2` fails the triangle inequality (`0, 1, 2` on a line: `4 > 1 + 1`). K-means minimizes the *squared* distance anyway — the argmin over centers is the same, since squaring is monotone for non-negative values.
2. **Hamming is Manhattan on binary features**, not a separate formula. On bits, `|x_i - y_i|` is 1 exactly where they differ.
3. **`p = inf` takes the max, not the sum.** For the 4-by-3 example it's 4, not 7.
4. **Edit distance depends on the cost table.** With costs 5/1/2 the example is 10; with all costs 1 it would be 5.
5. **`k` is a hyperparameter.** K-means doesn't learn it, and you can't pick it by minimizing distortion — that always picks `k = n`.
6. **"Different initialization → different results" is Yes; "always stops" is also Yes.** The tempting wrong answers are "Sometimes" and "No, we need a max iteration count". A max-iterations cap is a practical safeguard, not what guarantees termination.
7. **Convergence ≠ global optimum.** Monotone decrease plus finitely many states gives termination at a local minimum. The global problem is NP-hard.
8. **Neither step can increase the objective** — that's the whole proof. If a question says the update step "may temporarily increase" distortion, it's wrong.
9. **The assignment step is E, the update step is M.** He labels them on p. 23. Don't swap them; GMM next week keeps the same split with soft assignments.
10. **`k^n` counts labelled assignments, including empty clusters.** For `{A, B, C}`, `k = 2`: 8 assignments, but only 3 distinct ways to split into two non-empty groups.
11. **The mean is optimal for squared L2; the median for L1.** That's why k-medians resists outliers and k-means doesn't.
12. **Distortion uses *squared* distances to each point's *own* center.** Not the distance to every center, not un-squared.
13. **Reassignment is `O(knd)`, centroid update is `O(nd)`.** The update has no `k`, because each point is added to exactly one center.
14. **"Spherical" is about shape, not size.** K-means' Voronoi boundaries can't separate concentric rings or long thin clusters even with the right `k`.
15. **Random init in the deck vs data-point init in the notebook.** The deck says "initialize k centers randomly"; the notebook picks `k` data points. k-means++ (notebook only) spreads the initial centers out.
16. **Broadcasting aligns from the right.** `(n, d)` with `(k, d)` errors unless `n = k` or one is 1 — you need `X[:, None, :]` to get `(n, 1, d)` first.

### Self-test

Cover the answers.

1. `x = (1, 2)`, `y = (4, 6)`. Give the `L_1`, `L_2` and `L_inf` distances.
2. Hamming distance between `10110` and `11100`?
3. Which distance property does `d(x, y) = (x - y)^2` violate?
4. 1-D points `{1, 2, 3, 10, 11}`, `k = 2`, initial centers `c_1 = 1`, `c_2 = 11`. Run k-means to convergence. Final centers and distortion?
5. Same points, initial centers `c_1 = 1`, `c_2 = 2`. Run one full iteration. What happened?
6. Cluster `{(0, 0), (2, 0), (1, 3)}`. What's its center, and what's its contribution to distortion?
7. `n = 4` points, `k = 3`. How many assignments does exhaustive search check?
8. `n = 10,000`, `k = 5`, `d = 20`, `I = 30`. Order of the operation count?
9. Distortion for `k = 1..6`: `100, 55, 20, 17, 15, 14`. Which `k` does the elbow method pick?
10. Why does adding a single point at `x = 1000` to question 4 wreck k-means but barely affect k-medians?
11. `X.shape = (500, 3)`, `C.shape = (4, 3)`. Shape of `X[:, None, :] - C`? Of `((X[:, None, :] - C) ** 2).sum(axis=2).argmin(axis=1)`?

**Answers**

1. Differences `3, 4`. `L_1 = 7`, `L_2 = 5`, `L_inf = 4`.
2. Positions 2 and 4 differ → **2**.
3. **Triangle inequality.** `d(0, 2) = 4 > d(0, 1) + d(1, 2) = 2`. Symmetry and separability hold.
4. Assign: `{1, 2, 3}` → `c_1`, `{10, 11}` → `c_2`. Update: `c_1 = 2`, `c_2 = 10.5`. Reassign: unchanged → stop. Distortion `= (1 + 0 + 1) + (0.25 + 0.25) = 2.5`.
5. Assign: `{1}` → `c_1`, `{2, 3, 10, 11}` → `c_2` (2 is closer to `c_2 = 2`). Update: `c_1 = 1`, `c_2 = 6.5`. Iteration 2: 2 and 3 are now closer to `c_1` (`1` vs `4.5`, `2` vs `3.5`), giving `{1, 2, 3} | {10, 11}`, `c_1 = 2`, `c_2 = 10.5`. Iteration 3 changes nothing → same answer as question 4, one round later. On this data the bad start recovers; on other data it can settle in a worse local minimum — the p. 30 point.
6. Center `(1, 1)`. Squared distances `2 + 2 + 4 = 8`.
7. `3^4 = 81`.
8. `I k n d = 30 · 5 · 10,000 · 20 = 3 × 10^7`.
9. **`k = 3`** — the drop from 2 → 3 is 35, from 3 → 4 only 3.
10. The mean of a cluster containing 1000 is pulled far from the rest; the median of `{10, 11, 1000}` is 11.
11. `(500, 4, 3)`; then `(500,)`.


---

[Schedule](https://mahdi-roozbahani.github.io/CS46417641-fall2026/docs/course-info/course-schedule-mahdi/) · [All topics](README.md)
