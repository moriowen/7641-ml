# Hierarchical Clustering

> **Unsupervised learning** · L13 · Week 7  
> **Quiz:** Q6 — L13

## Keyword definitions

### The idea

- **Hierarchical vs partitional clustering** (p. 4): **partitional** (k-means) returns one flat split into `k` groups. **Hierarchical** returns a **tree** of nested clusters with **parent–child** relationships. Two ways to build it: **agglomerative** (bottom-up) and **divisive** (top-down).
- **Dendrogram:** The tree drawn with merge height on the vertical axis. Leaves are single points; each internal node is the cluster formed by merging its two children, drawn at the distance where that merge happened.
- **Cutting the dendrogram** (p. 10): draw a horizontal line at some height. Each connected component hanging below the line is one cluster. A higher cut gives fewer, coarser clusters. A lower cut gives more, finer ones. This is what he means by "organizing data at **multiple granularities**". You don't fix `k` before running; you choose the granularity afterwards by choosing where to cut.

### The two paradigms (p. 12)

- **Bottom-up agglomerative:** start with every object as its own cluster → repeatedly join the **closest pair of clusters** → stop when only **one** cluster is left.
- **Top-down divisive:** start with **all** objects in one cluster → recursively split each cluster into **two** sub-clusters → stop when every cluster holds **one** object.
- Same tree, read in opposite directions (p. 13). Agglomerative step 0 is divisive's last step.

### Distance between clusters (linkage) (pp. 20-25)

Once a cluster has more than one point you have to decide what "distance between two clusters" means. That choice is the **linkage**:

| Linkage | `d(A, B)` = | His margin note |
|---|---|---|
| **Single** (nearest neighbour) | `min` over pairs `a in A, b in B` of `d(a, b)` | "the shortest of shortests" — merge with the cluster whose *closest* pair is shortest |
| **Complete** (furthest neighbour) | `max` over pairs `d(a, b)` | "the shortest of longests" — merge with the cluster whose *farthest* pair is shortest |
| **Average** | mean of all `|A|·|B|` cross-cluster pair distances | — |
| **Centroid** | distance between the two clusters' centres of gravity | — |

Different linkages can give **different trees** from the same data (p. 26).

### Clustering evaluation (pp. 47-50)

- **Internal measures** (no labels): elbow method, silhouette coefficient, graph-based measures (Beta-CV, normalized cut). The goal behind all of them: points **within** a cluster as close as possible, clusters as far apart from each other as possible. Silhouette is only named; the deck doesn't develop it.
- **`W`:** the pairwise **distance** matrix over all points. For point sets `S, R`: `W(S, R) = sum_{x_i in S} sum_{x_j in R} w_ij`.
- **`W_in = (1/2) sum_i W(C_i, C_i)`** (cohesion) — the `1/2` because `W(C_i, C_i)` counts every pair twice (`ab` and `ba`).
- **`W_out = (1/2) sum_i W(C_i, C̄_i) = sum_{i<j} W(C_i, C_j)`** (separation). `C̄_i` is everything not in `C_i`.
- **`N_in = sum_i C(n_i, 2)`** distinct intra-cluster pairs; **`N_out = sum_{i<j} n_i n_j`** distinct inter-cluster pairs.
- **Beta-CV** `= (W_in / N_in) / (W_out / N_out)` = mean intra-cluster distance ÷ mean inter-cluster distance. **Smaller is better.**
- **Normalized cut** `NC = sum_i W(C_i, C̄_i) / vol(C_i)`, with `vol(C_i) = W(C_i, V) = W(C_i, C_i) + W(C_i, C̄_i)`. Equivalently `sum_i 1 / (W(C_i, C_i)/W(C_i, C̄_i) + 1)`. With `W` as distances, **higher is better**.

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L13 — Hierarchical Clustering | W7 (Oct 5-9) | [10-hierarchical-clustering.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/10-hierarchical-clustering.pdf) | **[10-hierarchical-clustering-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/10-hierarchical-clustering-note.pdf)** |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Both files are live as of Oct 12, 2026; re-check with `../scripts/check-slides.sh`.

The annotated PDF is 50 pages; the plain deck is 47. The extra pages are a k-means recap whiteboard (p. 1) and two whiteboard examples (p. 44, the 1-D five-point example; pp. 45-46, the ring of 21 points). Page numbers below are PDF page numbers of the note file, not the slide numbers printed in the corner.

**Ed practice quiz:** [hierarchical-clustering.pdf](https://static.us.edusercontent.com/files/5YapMbaScDkVZFhjsRder6gl) — 8 questions, posted on Ed with a partial answer key. Its figures reuse the lecture's example data. Worked answers are under *Quiz prep* below.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [Understanding hierarchical clustering](https://towardsdatascience.com/understanding-the-concept-of-hierarchical-clustering-technique-c6e8243758ec) — *W7*
- [Dendrogram visualization (Data-to-Viz)](https://www.data-to-viz.com/graph/dendrogram.html) — *W7*
- [K-Means and DBSCAN (course notebook)](https://mahdi-roozbahani.github.io/CS46417641-fall2026/other/06-and-08-plot_dbscan.ipynb) — *W7*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Data Mining: Concepts and Techniques — Han, Kamber & Pei
- The Elements of Statistical Learning — Hastie, Tibshirani & Friedman

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] Agglomerative vs divisive — which is actually used, and why?
- [ ] Linkage criteria (single, complete, average, Ward): what cluster shape does each favor, and where does single linkage chain badly?
- [ ] How do I read a dendrogram, and how does cutting it at a height give a flat clustering?
- [ ] Complexity — why does this not scale to large n the way k-means does?

These were written before the deck was posted. The deck answers the second and third. It has **no Ward linkage** and **no complexity analysis** — the only speed claim is that single link is "faster in general" and complete link "generally slower" (p. 23). Every worked example is agglomerative; divisive is defined (p. 12) but never run.

## Notes on this topic

**Week 7 has Fall Break Oct 5-6**, so this is a single-lecture week and Q6 covers only L13.

### Flow of the lecture

K-means recap → what hierarchical clustering is and why (taxonomies, phylogeny, granularity) → agglomerative vs divisive → the key question, "how do you measure the distance between two clusters?" → single / complete / average / centroid → three worked runs on 5 points → three whiteboard examples of single vs complete → evaluating a clustering (Beta-CV, normalized cut).

### 0. K-means recap (p. 1, whiteboard)

`k` = number of clusters; k-means is **hard clustering**; it follows **EM** — Expectation = cluster membership, Maximization = recompute the centres; convergence is checked on the objective (distortion). Three drawbacks: (1) sensitive to outliers, (2) hyperparameters — `k`, threshold, distance function, (3) assumes spherical clusters because of Euclidean distance. The second drawback motivates this lecture: hierarchical clustering doesn't need `k` up front.

### 1. Why hierarchies (pp. 4-10)

- **p. 4:** orange + apple as a parent node with orange and apple as children — "tree structure (parent–child relationship)". A red arrow points **up**: agglomerative builds from the leaves. Next to it, the k-means picture: two clusters, similar within, dissimilar between.
- **p. 5:** organizing CS papers into a topic tree (AI → machine learning → clustering, deep learning, …).
- **p. 6:** animal taxonomy. He draws **two cut lines**: just under "animal" gives 2 clusters (vertebrate, invertebrate); one level lower gives 7 (fish, reptile, amphibian, mammal, worm, insect, crustacean). Same tree, two granularities. Applications: web pages, news articles, scientific papers.
- **p. 7:** DNA phylogeny. Merge order bottom → top: brown + polar bear; + black bear; + spectacled bear; then that group + giant panda, and separately raccoon + red panda (same height); then the root. His purple cut line sits just below the giant-panda / raccoon merges → **4 clusters**: {brown, polar, black, spectacled}, {giant panda}, {raccoon}, {red panda}. Caption: hierarchical clustering placed the giant panda **closer to the bears** than to the red panda.
- **pp. 8-9:** photos (a panda, cherry blossoms) — no content.
- **p. 10:** names across languages (Piotr/Pyotr, Petros/Pietro/Pedro/Pierre/Piero, Peter/Peder/Peka/Peadar) coloured by cutting the dendrogram, next to a map of Europe coloured the same way. "Cutting the dendrogram at a desired level leads to a sub-cluster: each connected component forms a cluster."

### 2. Agglomerative vs divisive (pp. 12-18)

p. 13 is the picture to remember. Five points `a..e`, agglomerative left → right:

```
step 0: a  b  c  d  e
step 1: {a b}  c  d  e
step 2: {a b}  c  {d e}
step 3: {a b}  {c d e}
step 4: {a b c d e}
```

Divisive is the same diagram read right → left: step 0 is `{a b c d e}`, step 1 splits it into `{a b} | {c d e}`, and so on. With `n` points there are `n - 1` merges (or splits).

pp. 14-18 animate the agglomerative loop on a scatter of ~40 points: (1) every point is its own cluster, (2) find the most similar pair of clusters, (3) merge them into a parent cluster, (4) repeat. The tree grows underneath: the green pair becomes one node, the blue pair becomes a node, then a red point joins the blue node to make a bigger parent.

### 3. Linkage (pp. 20-26)

**pp. 21-22** use the same layout, three clusters `A`, `B`, `C`, and ask "I am going to merge A with either B or C. Which one?":

- **Single link** (p. 21): measure the *closest* pair between `A` and each candidate. `d(A, B) < d(A, C)` → merge with `B`. Margin note: "the shortest of shortests".
- **Complete link** (p. 22): measure the *farthest* pair. Now `d(A, C) < d(A, B)` → merge with `C`. Margin note: "the shortest of longests".

Same clusters, opposite decision. That's the whole lecture in one slide.

**p. 23 — the comparison he wants you to know:**

| | Behaviour | Outliers | Speed |
|---|---|---|---|
| **Single** | **Chaining**: a chain of points can be extended for long distances without regard to the overall shape of the emerging cluster | sensitive | faster in general |
| **Complete** | Cutting at the last merge tends to give two groups of **roughly equal size**; generally a more useful organization than chains; avoids chaining | more robust | generally slower |
| **Average** | "When you don't know which one may be better for you, start with the average link method" | — | — |

Below it, two dendrograms of `a b c d`. Single link is a **staircase**, `((a, b), c), d` — he draws a diagonal through the steps and circles the bottom. Complete link is **balanced**, `(a, b), (c, d)` — he loops the two halves.

**p. 25** — the four definitions with pictures (single = closest members, complete = furthest members, centroid = centres of gravity, average = all cross-cluster pairs). **p. 26:** "Different distance functions can lead to different results!"

### 4. Worked runs on five points (pp. 27-40)

**Dataset 1** (p. 27): `A (1,1)`, `B (1,0)`, `C (0,2)`, `D (2,4)`, `E (3,5)`.

```
      A    B    C    D    E
A     0    1    1.4  3.2  4.5
B     1    0    2.2  4.1  5.4
C     1.4  2.2  0    2.8  4.2
D     3.2  4.1  2.8  0    1.4
E     4.5  5.4  4.2  1.4  0
```

`1.4` is `√2 ≈ 1.414`, rounded. That matters for the Ed practice question (cut at 1.41).

**Average link on dataset 1** (pp. 28-31, titled "distance based on average point"):

| Step | Merge | Height | How the new row is computed |
|---|---|---|---|
| 1 | `A + B` | 1 | `d((A,B), C) = (1.4 + 2.2)/2 = 1.8`; to `D`: `(3.2 + 4.1)/2 = 3.6`; to `E`: `(4.5 + 5.4)/2 = 4.9`. Margin: `(a + b)/2`. |
| 2 | `D + E` | 1.4 | `d((A,B), (D,E)) = (3.6 + 4.9)/2 = 4.25`; `d(C, (D,E)) = (2.8 + 4.2)/2 = 3.5` |
| 3 | `(A,B) + C` | 1.8 | `d(((A,B),C), (D,E)) = (4.25 + 3.5)/2 = 3.875` |
| 4 | everything | 3.875 | — |

He draws a cut line at ~1.3 on p. 29 (giving `{A,B}, C, D, E`) and at ~1.7 on p. 31 (giving `{A,B}, C, {D,E}`).

⚠️ **How the slide averages.** Each new entry is the plain mean of the two rows being merged, *not* the mean over every cross-cluster pair. They agree when both sides have one point. They differ later: the mean of all four `(A,B)–(D,E)` pairs is `(3.2 + 4.5 + 4.1 + 5.4)/4 = 4.3`, not 4.25. Over all six `((A,B),C)–(D,E)` pairs it's ≈ 4.03, not 3.875. The merge **order** is the same either way on this data. The p. 25 definition ("average similarity of all cross-cluster pairs") is the textbook one; the worked tables use the shortcut. If a quiz asks for a number, check which one its options match.

**Dataset 2** (p. 32): same, but `D` moves to `(1.5, 3.5)`. New distances: `A–D 2.55`, `B–D 3.53`, `C–D 2.12`, `D–E 2.12`.

**Single link on dataset 2** (pp. 33-36):

| Step | Merge | Height |
|---|---|---|
| 1 | `A + B` | 1 |
| 2 | `(A,B) + C` | 1.4 — `min(1.4, 2.2)`, via `A` |
| 3 | `D + E` | 2.12 — tie with `((A,B),C)–D = 2.12`; the slide merges `D, E` |
| 4 | everything | 2.12 — `min` cross distance is `C–D` |

The `DE` and root nodes sit at the **same height**. Cut at 1.7 → `{A,B,C}, D, E`.

**Complete link on dataset 2** (pp. 37-40):

| Step | Merge | Height |
|---|---|---|
| 1 | `A + B` | 1 |
| 2 | `D + E` | 2.12 — **tie** with `C–D = 2.12`; the slide picks `D, E` |
| 3 | `(A,B) + C` | 2.2 — `max(1.4, 2.2)`, via `B` |
| 4 | everything | 5.4 — `B–E` |

Cut at 1.7 → `{A,B}, C, D, E`. **Same data, same cut height, single link gives 3 clusters and complete link 4.** The difference is all in step 2: `C` is 1.4 from `A` but 2.2 from `B`.

The step-2 tie matters. Break it the other way (merge `C, D`) and complete link builds `(A,B)+(C,D)` at 3.53, then `E` last at 5.4. Two clusters would then be `{A,B,C,D} | {E}` instead of the slide's `{A,B,C} | {D,E}`.

Slide errata: p. 38's `(A,B)–D` entry reads **3.55**; it should be `max(2.55, 3.53) = 3.53`. p. 39 is titled "**Single** Link" but its numbers (2.2, 5.4) are complete link.

**p. 41** — a dendrogram of face images (Bien et al. 2011) with a representative face drawn at each internal node. No numbers.

### 5. Single vs complete — three whiteboard examples (pp. 42-46)

**Eight points in two rows** (pp. 42-43, credit David Sontag): top row `1 2 · 5 6`, bottom row `3 4 · 7 8`. The close pairs `{1,2}, {5,6}, {3,4}, {7,8}` form first under both linkages. Then:

- **Single** merges along **rows**: `{1,2,5,6}` and `{3,4,7,8}`. The horizontal gap `2–5` is shorter than the vertical gap `1–3`.
- **Complete** merges into **columns**: `{1,2,3,4}` and `{5,6,7,8}`. Joining a row means spanning `1–6`, which is long. Joining a column means spanning the diagonal `1–4` of a small box, which is shorter.

**1-D, five points** (p. 44): `a = 0.5, b = 2, c = 5, d = 6, e = 10`. Both start with `c+d` (1), then `a+b` (1.5). Then:

| | Next merge | Then | 2 clusters |
|---|---|---|---|
| **Single** | `{a,b} + {c,d}` at 3 (`b–c`) | `+ e` at 4 (`d–e`) | `{a,b,c,d} | {e}` |
| **Complete** | `{c,d} + e` at 5 (`c–e`) — beats `{a,b}–{c,d}` = 5.5 (`a–d`) | all at 9.5 (`a–e`) | `{a,b} | {c,d,e}` |

**Ring of 21 points** (pp. 45-46): 20 points evenly spaced around a loop, point 21 alone in the middle. **Single link** grows one chain around the ring — nested loops spiralling outward. Point 21 is far from every ring point, so it joins near the end. **Complete link** builds compact local groups of 2-4 neighbours (labelled `a`, `c`, `d`, `e`, `f`, …, `P`), never one long chain. Point 21 is linked into a nearby group. This is chaining vs compactness drawn out.

### 6. Clustering evaluation (pp. 47-50)

**Beta-CV** (pp. 48-49). His whiteboard:

- `C(n, 2) = n(n-1)/2` — a triangle has 3 nodes and `3·2/2 = 3` edges.
- Inside one cluster `{a, b, c, d}`, `W(C_i, C_i)` sums `ab + ac + ad + ba + bc + bd + …` — each pair appears twice, hence the `1/2` in `W_in` ("the distance of each point is measured two times").
- Three clusters of 2, 3 and 2 points: `N_in = 1 + 3 + 1 = 5`. Two clusters of 2 and 3 points: `N_out = 2 · 3 = 6`.
- `BetaCV = (W_in / N_in) / (W_out / N_out)`. He circles the two averages: mean distance inside clusters over mean distance between clusters. **The smaller, the better.**

**Normalized cut** (p. 50). His whiteboard, three clusters:

```
NC = NC_1 + NC_2 + NC_3
NC_1 = (W(C1,C2) + W(C1,C3)) / (W(C1,C1) + W(C1,C2) + W(C1,C3))
```

…and so on for `C2`, `C3`. Each term is "distance going out of the cluster ÷ all distance touching the cluster". **The higher, the better** — because `W` holds distances, not similarities. A sketch shows `a, b` in one cluster with a large `w_2` between them and a small `w_1` to `c` outside — the kind of split he's warning against.

Since each term is at most 1, `NC <= k`.

## My notes

### Before lecture


### During lecture


### After lecture — what I still don't get



## Quiz prep

- [ ] Re-read the professor's annotated notes
- [ ] Redo any worked example from the deck without looking
- [ ] Write my own one-paragraph summary of the topic
- [ ] Practice bank: [`../quizzes/hc.html`](../quizzes/hc.html)
- [ ] Ed practice quiz (linked under *Slides*), then check the worked answers below

Things he worked by hand or circled — the likeliest quiz material:

- [ ] Agglomerative vs divisive: start, repeat, stop (p. 12); read p. 13 in both directions
- [ ] Cut a dendrogram at a height and list the clusters (pp. 6, 7, 29, 31)
- [ ] Single vs complete on p. 21/22 — same clusters, opposite merge
- [ ] Chaining, outlier sensitivity, balanced splits, speed (p. 23)
- [ ] Rebuild dataset 1's average-link table and dendrogram (pp. 28-31)
- [ ] Single vs complete on dataset 2, and why the cut at 1.7 gives 3 vs 4 clusters (pp. 33-40)
- [ ] 1-D example `0.5, 2, 5, 6, 10` under both linkages (p. 44)
- [ ] Rows vs columns in the 8-point example (pp. 42-43)
- [ ] Beta-CV: `W_in`, `W_out`, `N_in`, `N_out`, smaller is better (pp. 48-49)
- [ ] Normalized cut: per-cluster ratio, higher is better, `NC <= k` (p. 50)

### Ed practice quiz — worked answers

The posted key fills in 1a-c, 1f, 2, 3, 5-8 and leaves 1d, 1e, 1g and 4 as "[Student Answer]". Those four below are my answers, not the key.

| Q | Answer | Why |
|---|---|---|
| 1a | **False** | Top-down starts with *all* points in one cluster. Every point on its own is the bottom-up start (p. 12). |
| 1b | **True** | When every cluster is a single point, all linkages reduce to point-to-point distance, so the first merge is always the closest pair. |
| 1c | **False** | pp. 21-22: the same three clusters, single picks `B`, complete picks `C`. |
| 1d | **False** *(mine)* | Distance between averages ≠ average of distances. 1-D: `A = {0}`, `B = {-1, 1}`, `C = {0.5}`. Centroid: `B` is at 0 (closest). Average link: `A–B = 1`, `A–C = 0.5` → `C` is closest. |
| 1e | **False** *(mine)* | No linkage is best. Different ones give different results (p. 26); his default when unsure is average (p. 23). |
| 1f | **True** | Agglomerative only merges; nothing ever splits a cluster again. |
| 1g | **True** *(mine)* | Agglomerative is greedy — it takes the best merge at each step and never revisits it. The deck doesn't discuss global optimality, so this one is outside the lecture. |
| 2 | **(A, B)** | Dataset 1. The first merge is the closest pair under any linkage: `d(A,B) = 1`. |
| 3 | **(A,B), C, D, E** | Dataset 1's average-link tree. `D–E` merges at `√2 ≈ 1.414`, just **above** 1.41, so `D` and `E` are still separate. |
| 4 | **{Brown, Polar, Black, Spectacled bear, Giant panda}, {Raccoon, Red panda}** *(mine)* | The root's two children (p. 7). |
| 5 | **Consider both** | Compactness (cohesion) and distance between clusters (separation) both matter (p. 47). |
| 6 | **Different linkages emphasize different relationships** | Single sees only the closest pair, complete only the farthest — a few far points move one and not the other. |
| 7 | **Multiple granularities** | The point of p. 6 / p. 10. |
| 8 | **Different criteria capture different aspects** | Beta-CV and NC weigh cohesion and separation differently. |

### The relationship map

```
hierarchical (tree, nested)            partitional (flat, needs k)
  agglomerative: n singletons -> merge closest pair -> 1 cluster   (n-1 merges)
  divisive:      1 cluster    -> split in two      -> n singletons
  pick granularity AFTER: cut dendrogram at height h -> components below = clusters
    lower cut -> more clusters;  higher cut -> fewer

linkage d(A,B):
  single   = min pair    "shortest of shortests"  chaining, outlier-sensitive, faster
  complete = max pair    "shortest of longests"   compact, ~equal halves, slower
  average  = mean pair   default when unsure
  centroid = d(mean A, mean B)
  always: single <= average <= complete;  all equal when both are single points

evaluation (W = pairwise DISTANCE matrix)
  BetaCV = (W_in/N_in) / (W_out/N_out)        smaller = better
  NC     = sum_i W(Ci, ~Ci) / vol(Ci)         higher  = better,  <= k
  N_in + N_out = C(n, 2)
```

### Traps — the things that are implied but never said out loud

1. **Top-down starts with one cluster, bottom-up with `n`.** The practice quiz's first question swaps them.
2. **The first merge doesn't depend on linkage.** With singletons, min = max = mean = centroid distance. Linkage only matters from the second merge on.
3. **Single and complete can disagree on the very next merge** (pp. 21-22). "Closest under single ⇒ closest under complete" is false.
4. **Distance of the averages ≠ average of the distances.** Centroid and average link are different linkages.
5. **The lecture's "average" tables average the two merged rows**, not all cross pairs. Same order here, different numbers (4.25 vs 4.3).
6. **`1.4` on the slides is `√2 = 1.414`.** A cut at 1.41 lands *below* the `D–E` merge.
7. **Lower cut → more clusters.** And cuts of one tree are always nested; two k-means runs with different `k` need not be.
8. **Ties change trees.** Dataset 2, complete link: `C–D` and `D–E` both 2.12. The slide's choice gives `{A,B,C} | {D,E}`; the other gives `{A,B,C,D} | {E}`.
9. **Per this lecture, single link is the outlier-sensitive one** and complete is "more robust to outliers" (p. 23). Go with the lecture's claim on his quiz.
10. **Single link can put several merges at the same height** (dataset 2: `DE` and the root both at 2.12). The dendrogram looks flat there; that's correct.
11. **Merges are never undone.** An early merge you'd regret later stays.
12. **Beta-CV smaller is better, NC higher is better** — opposite directions, both because `W` holds *distances*.
13. **The `1/2` in `W_in` and `W_out`** is because summing over `C_i × C_i` (or over every `i` with `C̄_i`) counts each pair twice. `N_in`, `N_out` count each pair once.
14. **Deck errata:** p. 38 `3.55` should be `3.53`; p. 39 says "Single Link" but shows complete link.

### Self-test

Cover the answers.

1. Agglomerative clustering on 6 points: how many merges until it stops? How many clusters after 2 merges?
2. Dataset 1. After `A + B`, give `d((A,B), C)` under single, complete and the lecture's average.
3. Dataset 1, average link. Cut the dendrogram at 1.5. At 2.0. At 4.0.
4. Dataset 2. Why does a cut at 1.7 give 3 clusters under single link but 4 under complete?
5. 1-D points `{0.5, 2, 5, 6, 10}`. Two clusters under single link? Under complete?
6. Give 1-D clusters `A`, `B`, `C` where single link merges `A` with `B` but complete link merges `A` with `C`.
7. Clusters of sizes 3, 3, 4. `N_in`? `N_out`? Check that they sum to `C(10, 2)`.
8. One clustering has BetaCV 0.2, another 0.6. Which is better and why?
9. `k = 4` clusters. What's the maximum possible NC, and when is it reached?
10. Bear tree (p. 7): which cluster counts can a single horizontal cut produce? Can you get exactly 3?

**Answers**

1. `n - 1 = 5` merges. After 2 merges: `6 - 2 = 4` clusters.
2. Single `min(1.4, 2.2) = 1.4`; complete `max = 2.2`; average `(1.4 + 2.2)/2 = 1.8`.
3. 1.5: `{A,B}, C, {D,E}` (`D–E` at 1.414 is below; `ABC` at 1.8 is above). 2.0: `{A,B,C}, {D,E}`. 4.0: everything (root at 3.875).
4. `C` is 1.4 from `A` but 2.2 from `B`. Single link uses the 1.4 → `C` joins `{A,B}` below the cut. Complete uses the 2.2 → above the cut, `C` stays alone.
5. Single: `{0.5, 2, 5, 6} | {10}`. Complete: `{0.5, 2} | {5, 6, 10}`.
6. One option: `A = {0}`, `B = {2, 10}`, `C = {5}`. Single: `A–B = 2 < A–C = 5`. Complete: `A–B = 10 > A–C = 5`.
7. `N_in = 3 + 3 + 6 = 12`. `N_out = 3·3 + 3·4 + 3·4 = 33`. `12 + 33 = 45 = C(10, 2)` ✓.
8. 0.2 — mean intra-cluster distance is a fifth of the mean inter-cluster distance. Tighter clusters, further apart.
9. `4`. Each term `1/(W(C_i,C_i)/W(C_i,C̄_i) + 1)` hits 1 when `W(C_i, C_i) = 0` —10. Merge heights, bottom up: brown+polar, +black, +spectacled, then giant panda and raccoon+red panda at the **same** height, then the root. Cuts give 7, 6, 5, 4, 2 or 1 clusters. **Exactly 3 is impossible** — the two merges that share a height split together. p. 7's purple line is the 4-cluster cut.his tree, because those two merges share a height.


---

[Schedule](https://mahdi-roozbahani.github.io/CS46417641-fall2026/docs/course-info/course-schedule-mahdi/) · [All topics](README.md)
