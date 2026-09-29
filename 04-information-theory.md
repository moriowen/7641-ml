# Information Theory

> **Foundations** · L7, L8 · Week 4  
> **Quiz:** Q3 — L7, L8

## Keyword definitions

### Information and entropy

- **Information content (self-information, surprisal):** The information carried by a *single outcome* `x`: `I(x) = log_2(1/p(x)) = -log_2 p(x)`. Measured in bits when the log is base 2. Rare outcomes carry more information than common ones.
- **Bit:** The unit of information when logs are base 2. `I(x) = 2` bits means the optimal code spends 2 characters on that outcome.
- **Nat:** The unit when logs are base `e`. Changing the log base rescales every quantity in this deck by the same constant factor, so it changes the numbers but never a comparison or an identity.
- **Entropy `H(X)`:** The *expected* information content of a random variable: `H(X) = E[I(x)] = sum_x p(x) log_2(1/p(x)) = -sum_x p(x) log_2 p(x)`. A measure of uncertainty.
- **Entropy as code length:** `H(Y)` is the expected number of bits needed to encode a randomly drawn value of `Y` under the most efficient code. That code assigns `-log_2 P(Y = k)` bits to the message `Y = k`.
- **Uniform distribution:** Every outcome equally likely, `p_i = 1/k`. This is the maximum-entropy distribution over `k` outcomes, with `H = log_2 k`.
- **Deterministic (degenerate) distribution:** All the mass on one outcome. Minimum entropy, `H = 0`.
- **`0 log 0 = 0` convention:** An outcome with zero probability contributes nothing to entropy. Justified as the limit `p log(1/p) -> 0` as `p -> 0`.
- **Compression framing:** Frequently occurring events should get short encodings, rare events long ones, so that information-per-character is maximized. Entropy is the floor on the average code length.

### Joint, conditional, and mutual quantities

- **Joint entropy `H(X,Y)`:** The entropy of the pair, treating `(x,y)` as one outcome: `H(X,Y) = sum_{x,y} p(x,y) log_2(1/p(x,y))`.
- **Conditional entropy given one value `H(Y|X = x)`:** The entropy of the conditional distribution `p(y|x)` for one fixed `x`. This is a per-value quantity, not an average.
- **Conditional entropy (average) `H(Y|X)`:** The `p(x)`-weighted average of those per-value entropies: `H(Y|X) = sum_x p(x) H(Y|X = x) = sum_{x,y} p(x,y) log_2(p(x)/p(x,y))`. Also called **equivocation**.
- **Chain rule for entropy:** `H(X,Y) = H(Y|X) + H(X) = H(X|Y) + H(Y)`. The direct analogue of `p(x,y) = p(y|x)p(x) = p(x|y)p(y)`.
- **Mutual information `I(X,Y)`:** The reduction in uncertainty about `Y` from observing `X`: `I(X,Y) = H(Y) - H(Y|X)`. Equivalently `sum_{x,y} p(x,y) log_2( p(x,y) / (p(x)p(y)) )`.
- **Information gain:** The same quantity as mutual information, under the name used when choosing a decision-tree split — the split's feature is `X`, the label is `Y`.
- **Subadditivity:** `H(X,Y) <= H(X) + H(Y)`, with equality exactly when `X` and `Y` are independent. The gap is `I(X,Y)`.
- **Conditioning reduces entropy:** `H(Y|X) <= H(Y)` *on average*. Equivalent to `I(X,Y) >= 0`.

### Cross entropy and divergence

- **Cross entropy `H(P,Q)`:** The expected number of bits paid when the *wrong* distribution `Q` is assumed while the data actually follows `P`: `H(P,Q) = -sum_x p(x) log q(x) = sum_x p(x) log(1/q(x))`. `P` is the actual pdf/pmf, `Q` is the predicted one.
- **KL divergence `KL[P||Q]`:** The *excess* bits paid for using `Q` instead of `P`: `KL[P||Q] = sum_x P(x) log( P(x)/Q(x) ) = H(P,Q) - H(P)`.
- **Gibbs' inequality:** For any `Q` other than `P`, `H(P) < H(P,Q)`. Entropy is the strict minimum of cross entropy over the choice of `Q`. This *is* `KL >= 0` rewritten.
- **Jensen's inequality:** For a concave function `f`, `E[f(Z)] <= f(E[Z])`. Since `log` is **concave**, `sum_s P(s) log(Q(s)/P(s)) <= log sum_s P(s)(Q(s)/P(s)) = log 1 = 0`, which proves `KL[P||Q] >= 0`.
- **"A kind of distance":** KL measures how far `Q` is from `P`, but it is not a metric — it is asymmetric and fails the triangle inequality. The professor's slide phrases this as "KL Divergence is a **KIND OF** distance measurement."
- **Actual vs predicted pdf:** His labels for `P` and `Q` throughout: `P` is the true/label distribution, `Q` is the model's prediction. This is the framing that becomes the classification loss later.

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L7 — Info Theory | W4 (Sep 14-18) | [05-info-theory.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/05-info-theory.pdf) | **[05-info-theory-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/05-info-theory-note.pdf)** |
| L8 — Info Theory (contd) | W4 (Sep 14-18) | [05-info-theory.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/05-info-theory.pdf) | **[05-info-theory-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/05-info-theory-note.pdf)** |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Both files are live as of Sep 21, 2026; re-check with `../scripts/check-slides.sh`.

The annotated PDF runs 31 pages, and he **inserts blank whiteboard pages** mid-deck — one after the Information slide, another after the first Entropy slide — where he works derivations from scratch. Those inserted pages carry material that appears nowhere in the plain deck. Slide numbers below refer to the printed page numbers on the slides themselves.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [Visual Information Theory — Chris Olah](http://colah.github.io/posts/2015-09-Visual-Information/) — *W1*. The CE/MI bar diagram on slide 29 is lifted straight from this post.
- [Cross entropy as a loss function](https://medium.com/data-science-bootcamp/understand-cross-entropy-loss-in-minutes-9fb263caee9a) — *W3*
- [Cross entropy and KL divergence (Machine Learning Mastery)](https://machinelearningmastery.com/cross-entropy-for-machine-learning/) — *W3*
- [Why cross entropy over MSE for classification](https://susanqq.github.io/tmp_post/2017-09-05-crossentropyvsmes/) — *W4*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Pattern Recognition and Machine Learning — Bishop (entropy & KL sections)
- Deep Learning — Goodfellow, Bengio & Courville

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] Entropy, cross entropy, KL divergence — write each formula and say in one line what it measures.
- [ ] Why is KL divergence not a distance? (Asymmetry, no triangle inequality.)
- [ ] Information gain = entropy reduction — this is exactly the decision-tree split criterion later.
- [ ] Why cross entropy beats MSE for classification: what does the gradient look like in each case?

## Notes on this topic

Olah's *Visual Information Theory* is assigned in Week 1 but is the single best prep for this topic — read it before L7, not in Week 1.

Information gain shows up again in [Decision Trees & Random Forests](16-decision-trees-and-random-forests.md); cross entropy shows up again in [Logistic Regression](13-naive-bayes-and-logistic-regression.md) and [Neural Networks](14-neural-networks.md). The outline slide before the Cross-Entropy section (slide 30) carries his own note: *"Let's work on this subject in our Optimization lecture."* The loss-function treatment is deferred to [Optimization](05-optimization.md); this deck only sets up the definitions and the identities between them.

### Deck outline

Repeated on every section divider slide:

Motivation → Entropy → Conditional Entropy and Mutual Information → Cross-Entropy and KL-Divergence

**Joint entropy** does not appear in that outline but gets its own slide (23), tucked into the third section. It is the hinge between everything else, so don't let its absence from the outline fool you.

### 1. Motivation — uncertainty, information, compression

- The DIKA chain: Data → Information → Knowledge → Action. *"Information is processed data whereas knowledge is information that is modeled to be useful."*
- Two weather days: `{75% sunny, 25% rainy}` vs `{50% sunny, 50% rainy}`. The 50/50 day is more uncertain. Slide's own summary: **high entropy correlates to high information, or the more uncertain**.
- **Compression** framing: we want the shortest representation that preserves all information. Coin tosses `T,T,T,T,H` with `H -> 0`, `T -> 00` costs 9 characters; swapping to `H -> 00`, `T -> 0` costs 6. Since `P(T) = 4/5 > P(H) = 1/5`, the frequent symbol should get the short code.
- His annotation there: `P(X=H) = 1/5 ~~> more bits of information`. Low probability, high surprisal, long code.
- The four questions information theory answers (slide 16): how much information a random variable carries; how efficient a hypothetical code is; how much better or worse another code would do; whether the information in different random variables is complementary or redundant.
- Also written on slide 16, well ahead of where it's needed: `P(x,y) = P(x|y)P(y) = P(y|x)P(x)`, and directly beneath it `H(x,y) = H(x|y) + H(y) = H(y|x) + H(x)`. He builds the entropy chain rule as a deliberate copy of the probability chain rule.

### 2. Information and entropy (inserted whiteboard pages + slides 15, 18-21)

The worked example he writes by hand, `[cat, cat, cat, dog]`:

- `P(X = cat) = 3/4`, `P(X = dog) = 1/4`
- `I(x) = log_2(1/p(x))`, so `I(X = dog) = log_2 4 = log_2 2^2 = 2` bits of information
- `E[I(x)] = sum_x p(x)I(x) = (3/4)log_2(4/3) + (1/4)log_2 4` — this expectation **is** `H(X)`
- Rerun on the balanced set `[cat, cat, dog, dog]`: `E[I(x)] = (1/2)log_2 2 + (1/2)log_2 2 = 1` bit. With `k = 2` categories, `log_2 k = 1`, so the balanced set sits exactly at the ceiling.

The die example on the next inserted page:

- `X = {1,...,6}`, `p(x) = 1/6` for all `x`
- `H(X) = 6 * (1/6) log_2 6 = log_2 6 = log_2 k`
- He then notes `k -> +inf` sends `log_2 k -> +inf`: **entropy is unbounded above as the alphabet grows**, even though it's bounded for any fixed `k`
- `H(X) >= 0`, and the two ways of writing entropy are the same thing: `sum p log(1/p) = -sum p log p`, the minus sign coming from `log(1/a) = -log a`

Slide 18 states the code-length reading: `H(Y) = -sum_{k=1..K} P(y = k) log_2 P(y = k)` is the expected number of bits to encode a randomly drawn `Y` under the most efficient code, which assigns `-log_2 P(Y = k)` bits to the message `Y = k`.

Slide 19, binary entropy: `H(S) = -p_+ log_2 p_+ - p_- log_2 p_-`. The curve peaks at `p_+ = 0.5` with value 1, and his annotation at the peak reads `log_2 k = 2 -> 1` — the peak is `log_2 k` for `k = 2`. It falls to 0 at both ends.

Slide 20, the worked entropies on 6 flips:

| heads | tails | P(h) | P(t) | Entropy |
|---|---|---|---|---|
| 0 | 6 | 0 | 1 | 0 |
| 1 | 5 | 1/6 | 5/6 | 0.65 |
| 2 | 4 | 2/6 | 4/6 | 0.92 |

The `0 log 0` term is where he annotates `0.000001` and sketches `log x -> -inf` as `x -> 0`: the limit of `p log(1/p)` is 0, so the convention isn't a fudge.

**Slide 21 — Properties of Entropy.** Five properties, and the highest-density quiz slide in the deck:

1. **Non-negative:** `H(P) >= 0`
2. **Invariant under permutation of its inputs:** `H(p_1,...,p_k) = H(p_tau(1),...,p_tau(k))`
3. **For any *other* distribution `{q_1,...,q_k}`:** `H(P) = sum_i p_i log(1/p_i) < sum_i p_i log(1/q_i)` — he labels the left `actual pdf` and the right `predicted pdf`
4. `H(P) <= log_2 k`, **with equality iff `p_i = 1/k` for all `i`**
5. *"The further `P` is from uniform, the lower the entropy."*

Property 3 is Gibbs' inequality, and its right-hand side is the cross entropy `H(P,Q)` that doesn't get named for another ten slides. His margin work proves it: `sum p_i log(1/p_i) - sum p_i log(1/q_i) = sum p_i (log(1/p_i) - log(1/q_i)) = sum p_i log(q_i/p_i) < 0`, using `log a - log b = log(a/b)`. That last expression is `-KL[P||Q]`.

His side examples for multi-class classification (cat / dog / fish) are the endpoints of property 5: `P(x) = [1, 0, 0]` (zero entropy), then `q(x) = [0.7, 0.2, 0.1]` and `q(x) = [0.8, 0.1, 0.1]`. Beneath the slide he sketches three densities numbered 1-2-3 from flat to peaked, the flattest carrying the most entropy.

### 3. Joint entropy (slide 23)

The running example for the rest of the deck. Joint distribution of temperature `T` and humidity `M`:

| | cold | mild | hot | |
|---|---|---|---|---|
| **low** | 0.1 | 0.4 | 0.1 | **0.6** |
| **high** | 0.2 | 0.1 | 0.1 | **0.4** |
| | **0.3** | **0.5** | **0.2** | **1.0** |

- `H(T) = H(0.3, 0.5, 0.2) = 1.48548`
- `H(M) = H(0.6, 0.4) = 0.970951`
- `H(T) + H(M) = 2.456431`
- `H(T,M) = H(0.1, 0.4, 0.1, 0.2, 0.1, 0.1) = 2.32193` — the joint entropy sums over the **six cells**, not the margins
- Slide's own emphasis: **`H(T,M) <= H(T) + H(M)` !!!**
- `H(T,M) = H(T|M) + H(M) = H(M|T) + H(T)`

His margin notes make the marginal-vs-conditional bookkeeping explicit: `P(M=low, T=cold) = 0.1`, `P(M=low) = 0.6`, `P(T=mild | M=low) = 0.4/0.6`, `P(M=low | T=mild) = 0.4/0.5`. Same cell, two different conditionals, two different denominators. He also writes `P(a,b) = P(a|b)P(b) = P(a)P(b)` with `a & b independent` under the second equality — that equality only holds under independence, and that is exactly when the `<=` above becomes `=`.

### 4. Conditional entropy (slides 24-26)

`H(Y|X) = sum_{x in X} p(x) H(Y|X = x) = sum_{x,y} p(x,y) log( p(x) / p(x,y) )`

Conditioning `T` on `M` — `P(T = t | M = m)`, rows normalized:

| | cold | mild | hot | |
|---|---|---|---|---|
| **low** | 1/6 | 4/6 | 1/6 | 1.0 |
| **high** | 2/4 | 1/4 | 1/4 | 1.0 |

- `H(T | M = low) = H(1/6, 4/6, 1/6) = 1.25163`
- `H(T | M = high) = H(2/4, 1/4, 1/4) = 1.5`
- `H(T|M) = 0.6 * 1.25163 + 0.4 * 1.5 = 1.350978`

Conditioning `M` on `T` — `P(M = m | T = t)`, columns normalized:

| | cold | mild | hot |
|---|---|---|---|
| **low** | 1/3 | 4/5 | 1/2 |
| **high** | 2/3 | 1/5 | 1/2 |
| | 1.0 | 1.0 | 1.0 |

- `H(M | T = cold) = H(1/3, 2/3) = 0.918296`
- `H(M | T = mild) = H(4/5, 1/5) = 0.721928`
- `H(M | T = hot) = H(1/2, 1/2) = 1.0`
- `H(M|T) = 0.3(0.918296) + 0.5(0.721928) + 0.2(1.0) = 0.8364528`

The averaging weights come from the *conditioning* variable's marginal — `P(M)` when averaging `H(T|M = m)`, `P(T)` when averaging `H(M|T = t)`. Getting that backwards is the standard way to lose the question.

He calls the average "**equivocation**" on both slides. Slide 26 gives the mixed continuous/discrete form:
`H(Y|X) = -integral ( sum_{k=1..K} p(y = k|x) log_2 p(y = k|x) ) p(x) dx` — the sum over `y` stays a sum, the average over `x` becomes an integral.

### 5. Mutual information (slides 27-28)

`I(X_i, Y) = H(Y) - H(Y|X_i)` — the reduction in uncertainty in `Y` after seeing feature `X_i`. *The more the reduction in entropy, the more informative a feature.*

Symmetric forms, all the same number:

- `I(X,Y) = I(Y,X) = H(X) - H(X|Y) = H(Y) - H(Y|X)`
- `I(X,Y) = sum_{x,y} P(x,y) log( P(x|y) / P(x) ) = sum_{x,y} P(x,y) log( P(x,y) / (P(x)P(y)) )`

Properties (slide 28): **symmetric**, **non-negative**, **zero iff `X` and `Y` are independent**.

His annotation here is the decision-tree preview, and it's why this slide matters: he draws a parent node holding `50 cats, 50 dogs`, splits on a feature (`< 1 ft` / `> 1 ft`), and writes child counts `30` and `70`. `H(Y)` is the parent's entropy, `H(Y|X_i)` is the weighted average of the children's entropies, and the difference is the information gain that picks the split. Same formula, different vocabulary — see [Decision Trees & Random Forests](16-decision-trees-and-random-forests.md).

Slide 29 is Olah's bar diagram, and it encodes every identity in one picture: a full bar `H(X,Y)`; that bar split as `H(X) + H(Y|X)` and alternately as `H(X|Y) + H(Y)`; and the overlap view where `H(X)` and `H(Y)` overlap in the middle, the overlap being `I(X,Y)` and the non-overlapping ends `H(X|Y)` and `H(Y|X)`. If you can redraw this bar from memory you can re-derive every identity in the deck.

### 6. Cross entropy and KL divergence (slides 31-32)

**Cross entropy** (slide 31): the expected number of bits when a wrong distribution `Q` is assumed while the data actually follows `P`.

`H(p,q) = -sum_x p(x) log q(x) = H(P) + KL[P||Q]`

Derivation as written: `H(p,q) = E_p[l_i] = E_p[ log(1/q(x_i)) ] = sum_i p(x_i) log(1/q(x_i)) = -sum_x p(x) log q(x)`. He annotates `p` = actual pdf, `q` = predicted pdf, circles the whole thing with **Min**, and crosses out the `H(P)` term in `H(P) + KL[P][Q]` — because `H(P)` does not depend on `Q`, minimizing cross entropy over the model's predictions is the same optimization as minimizing KL.

**KL divergence** (slide 32):

`KL[P(S)||Q(S)] = sum_s P(s) log( P(s)/Q(s) ) = sum_s P(s) log(1/Q(s)) - H[P] = H(P,Q) - H(P)`

*Excess cost in bits paid by encoding according to `Q` instead of `P`.* Margin note: **KL Divergence is a KIND OF distance measurement**.

The non-negativity proof, which is the slide's own question `log function is concave or convex?` — **concave**, so Jensen runs `E[log Z] <= log E[Z]`:

```
-KL[P||Q] = sum_s P(s) log( Q(s)/P(s) )
         <= log sum_s P(s) (Q(s)/P(s))      (Jensen, log concave)
          = log sum_s Q(s) = log 1 = 0
```

So `KL[P||Q] >= 0`, **with equality iff `P = Q`**.

### 7. Take-home messages (slide 33)

His own list of what to know, which reads as a quiz blueprint:

- **Entropy** — a measure for uncertainty; *why it is defined in this way* (optimal coding); its properties
- **Joint entropy, conditional entropy, mutual information** — the physical intuitions behind their definitions; **the relationships between them**
- **Cross entropy, KL divergence** — the physical intuitions behind them; **the relationships between entropy, cross-entropy, and KL divergence**

Two of the three bullets say *relationships*, not definitions.

## My notes

### Before lecture


### During lecture


### After lecture — what I still don't get



## Quiz prep

- [ ] Re-read the professor's annotated notes
- [ ] Redo any worked example from the deck without looking
- [ ] Write my own one-paragraph summary of the topic

Things he flagged, asked, or deliberately left open in lecture — the likeliest quiz material:

- [ ] "Which day is more uncertain?" and "how do we quantify uncertainty?" (slide 6 — the 50/50 day; entropy)
- [ ] "Which one has a higher probability: T or H? Which one should carry more information: T or H?" (slide 11 — `T` is likelier, so `H` carries more information; the two answers point opposite ways *on purpose*)
- [ ] "log function is concave or convex?" (slide 32 — **concave**, which is what makes the Jensen step run in the direction that gives `KL >= 0`)
- [ ] Hand-derive `E[I(x)] = H(X)` for `[cat, cat, cat, dog]` and for `[cat, cat, dog, dog]` (inserted page after slide 15)
- [ ] Show `H(X) = log_2 k` for a fair die, and say what happens as `k -> inf` (inserted page after slide 15 — unbounded)
- [ ] Prove property 3 of slide 21 from `log a - log b = log(a/b)`, and name the two things it turns out to be (Gibbs' inequality; `KL >= 0`)
- [ ] Reproduce the full `T`/`M` workflow: margins → `H(T)`, `H(M)` → `H(T,M)` → both conditional tables → `H(T|M)`, `H(M|T)` → `I(T,M)` computed two different ways, and check they agree
- [ ] Redraw Olah's bar diagram (slide 29) from memory and read all five identities off it
- [ ] Why does crossing out `H(P)` in `H(P,Q) = H(P) + KL[P||Q]` justify training with cross entropy? (slide 31)

### The relationship map

Everything in the deck is one of these. He said twice on the take-home slide that the *relationships* are the point, so memorize this block rather than the individual formulas.

```
I(x)      = log2(1/p(x))                          single outcome
H(X)      = E[I(x)] = -sum p log2 p               expected surprisal

H(X,Y)    = H(X|Y) + H(Y) = H(Y|X) + H(X)         chain rule
H(X,Y)   <= H(X) + H(Y)                           equality iff independent
H(Y|X)   <= H(Y)                                  on average only
I(X,Y)    = H(Y) - H(Y|X) = H(X) - H(X|Y)
          = H(X) + H(Y) - H(X,Y)
          = H(X,Y) - H(X|Y) - H(Y|X)
         >= 0, = 0 iff independent
I(X,X)    = H(X)                                  MI of a variable with itself

H(P,Q)    = H(P) + KL[P||Q]                       cross entropy
KL[P||Q]  = H(P,Q) - H(P) >= 0, = 0 iff P = Q
H(P)     <= H(P,Q)                                Gibbs; strict if Q != P
0        <= H(X) <= log2 k                        = 0 iff deterministic,
                                                  = log2 k iff uniform
```

Sanity numbers from his own `T`/`M` table, useful because every identity above can be checked against them:

`H(T) = 1.48548`, `H(M) = 0.970951`, `H(T,M) = 2.32193`, `H(T|M) = 1.350978`, `H(M|T) = 0.8364528`

- `H(T|M) + H(M) = 1.350978 + 0.970951 = 2.321929 = H(T,M)` ✓
- `H(M|T) + H(T) = 0.836453 + 1.485480 = 2.321933 = H(T,M)` ✓
- `I(T,M) = H(T) - H(T|M) = 0.134502`
- `I(T,M) = H(M) - H(M|T) = 0.134498` ✓ same number from the other side
- `I(T,M) = H(T) + H(M) - H(T,M) = 2.456431 - 2.321930 = 0.134501` ✓

### Traps — the things that are implied but never said out loud

These are the gaps between the formulas, which is where the last two quizzes went wrong. Each one is answered.

1. **`H(Y|X) <= H(Y)` is an average statement. `H(Y|X = x)` for one particular `x` can be *larger* than `H(Y)`.** His own numbers prove it: `H(T) = 1.48548` but `H(T | M = high) = 1.5`. Learning that humidity is high made temperature *more* uncertain. It's only the `P(M)`-weighted average, `1.350978`, that is forced below `H(T)`. A quiz asking "can observing a feature increase uncertainty?" has two different correct answers depending on whether it says *on average*.

2. **`H(P,Q)` (cross entropy) and `H(X,Y)` (joint entropy) are written identically and are completely different quantities.** Joint entropy takes two *random variables* and one joint distribution; cross entropy takes two *distributions over the same variable*. Joint entropy is symmetric, `H(X,Y) = H(Y,X)`; cross entropy is **not**, `H(P,Q) != H(Q,P)`. Read the arguments, not the comma.

3. **Mutual information `I(X,Y)` and self-information `I(x)` also share a letter.** One argument, lowercase outcome → surprisal of an event. Two arguments, uppercase variables → mutual information. Slide 15 uses `I(X)` for surprisal and slide 27 uses `I(X_i, Y)` for MI, in the same deck.

4. **KL is asymmetric *and* fails the triangle inequality, so it isn't a distance — but it isn't a "similarity" either.** It's a directed excess-bits cost. `KL[P||Q]` and `KL[Q||P]` answer different questions and can differ by a lot. The slide hedges with "a KIND OF distance"; if a quiz offers "KL is a distance metric," that's false, and "KL is symmetric" is false too.

5. **`I(X,Y) >= 0` always, but the entropy *change* `H(Y) - H(Y|X = x)` for a single `x` can be negative.** Same root cause as trap 1. MI is non-negative only because it's an expectation.

6. **Entropy depends only on the *multiset of probabilities*, never on the outcome values or their labels.** That's property 2, permutation invariance, and it implies more than it says: a fair die over `{1,...,6}` and a fair die over `{100, 200, ..., 600}` have identical entropy. Entropy has no notion of mean, variance, ordering, or distance between outcomes. Anything comparing entropies of distributions with different *supports but the same probabilities* is testing this.

7. **Adding an outcome with probability zero doesn't change the entropy** (`0 log 0 = 0`). So the `k` in `H <= log_2 k` should be read as the number of outcomes with **non-zero** probability. Padding a distribution with impossible classes doesn't raise its entropy bound in any meaningful sense.

8. **Property 5 — "the further `P` is from uniform, the lower the entropy" — is about *shape*, not about any single parameter.** Both `[1, 0, 0]` and `[0.98, 0.01, 0.01]` are far from uniform and have near-zero entropy; `[0.34, 0.33, 0.33]` is near-uniform and near `log_2 3`. Don't try to make it a monotone function of one probability.

9. **Maximum entropy is `log_2 k` for a *fixed* alphabet, but entropy itself is unbounded above.** He wrote `k -> +inf` next to `log_2 k` for exactly this reason. "Entropy is bounded by 1 bit" is only true for binary variables.

10. **Changing the log base changes every number but no relationship.** Bits (base 2) → nats (base `e`) multiplies everything by `ln 2`. Every identity, inequality, and "which is larger" answer is unaffected. If a quiz gives an answer in nats, convert rather than re-deriving.

11. **`H(P) < H(P,Q)` is strict for `Q != P`, and that strictness is the whole content of "entropy is the best you can do."** A code built for the wrong distribution *always* costs more, never the same. It's also why the cross-entropy loss bottoms out at `H(P)` rather than at 0 — and for one-hot labels, where `H(P) = 0`, it does bottom out at 0. The achievable minimum of cross-entropy loss is `H(P)`, which happens to be zero only because the labels are deterministic.

12. **Minimizing cross entropy and minimizing KL are the same optimization, but not the same *number*.** They differ by the constant `H(P)`. A question asking for the *value* at the optimum has two different answers.

13. **`I(X,Y) = 0` iff independent — "iff", both directions.** Zero mutual information isn't just "no linear relationship" (that would be zero correlation). Zero MI means no statistical dependence of any kind. This is the information-theoretic strengthening of the correlation-vs-independence trap from [Probability & Statistics](03-probability-and-statistics.md): uncorrelated does not imply independent, but zero MI does.

14. **`I(X,Y) <= min(H(X), H(Y))`.** Not stated on any slide, but it falls straight out of `I = H(Y) - H(Y|X)` and `H(Y|X) >= 0`. A feature can never tell you more about `Y` than `Y`'s own entropy, however informative it is. Useful for eliminating impossible numeric options.

15. **`H(Y|X) = 0` means `Y` is a deterministic function of `X`, not that `X` and `Y` are the same.** Then `I(X,Y) = H(Y)` and `H(X,Y) = H(X)`. Many-to-one functions satisfy this asymmetrically: `H(Y|X) = 0` while `H(X|Y) > 0`.

16. **Information gain (decision trees) *is* mutual information.** Parent entropy is `H(Y)`, the weighted child entropies are `H(Y|X)`, the gain is the difference. Because `I >= 0`, a split can never increase expected entropy — which is exactly why information gain alone can't tell you when to stop splitting.

17. **The weights in `H(Y|X) = sum_x p(x) H(Y|X = x)` come from the marginal of the *conditioning* variable.** For `H(T|M)` they're `P(M = low) = 0.6` and `P(M = high) = 0.4`. Using `P(T)` there produces a plausible-looking wrong number, which is the worst kind.

### Self-test

Cover the answers. These are written to break on the relationships, not the definitions.

1. `X` is uniform over 8 outcomes. What is `H(X)`? Now let `Y = X mod 2`. Give `H(Y)`, `H(Y|X)`, `H(X|Y)`, `I(X,Y)`, `H(X,Y)`.
2. True or false: if `H(Y|X = x_0) > H(Y)` for some `x_0`, then `X` and `Y` must be dependent.
3. `P = [0.5, 0.5]`, `Q = [0.9, 0.1]`. Compute `H(P)`, `H(P,Q)`, `KL[P||Q]`, then `KL[Q||P]`. What does the comparison show?
4. Two variables have `H(X) = 3`, `H(Y) = 2`, `H(X,Y) = 4`. Find `I(X,Y)`, `H(X|Y)`, `H(Y|X)`. Are they independent?
5. Someone claims `I(X,Y) = 2.5` for the variables in question 4. Why is that impossible without computing anything?
6. A classifier's labels are one-hot. What is the minimum achievable value of the cross-entropy loss, and why?
7. Does `H(X,Y) = H(X) + H(Y)` ever hold when `I(X,Y) > 0`?
8. Distribution `A` is uniform over `{1, 2, 3, 4}`. Distribution `B` is uniform over `{10, 20, 30, 40}`. Distribution `C` is `[0.25, 0.25, 0.25, 0.25]` over `{cat, dog, fish, bird}`. Rank their entropies.
9. You compute `H(T|M) = 1.42` for the deck's weather table. Without redoing the arithmetic, how do you know it's wrong?
10. `KL[P||Q] = 0`. What can you say about `H(P,Q)`?
11. Feature `X_1` gives information gain 0.3; feature `X_2` gives 0.0. Does `X_2` being useless for this split mean `X_2` is independent of `Y`?
12. Why is entropy the *minimum* of cross entropy rather than the maximum?

**Answers**

1. `H(X) = log_2 8 = 3`. `Y` is uniform over `{0,1}`, so `H(Y) = 1`. `Y` is a deterministic function of `X`, so `H(Y|X) = 0` and `I(X,Y) = H(Y) - H(Y|X) = 1`. Then `H(X|Y) = H(X) - I = 2`, and `H(X,Y) = H(X) + H(Y|X) = 3`. Note `H(X,Y) = H(X)`: `Y` adds nothing once you know `X`.
2. **True.** If they were independent, `p(y|x) = p(y)` for every `x`, so every per-value conditional entropy would equal `H(Y)` exactly. Any deviation in either direction proves dependence. (And it does *not* contradict `H(Y|X) <= H(Y)`, which is only about the average.)
3. `H(P) = 1`. `H(P,Q) = -(0.5 log_2 0.9 + 0.5 log_2 0.1) = 0.5(0.152) + 0.5(3.322) = 1.737`, so `KL[P||Q] = 0.737`. Reversed: `H(Q) = 0.469`, `H(Q,P) = -(0.9 log_2 0.5 + 0.1 log_2 0.5) = 1`, so `KL[Q||P] = 0.531`. The two differ — KL is asymmetric, and neither ordering is "the" divergence.
4. `I = H(X) + H(Y) - H(X,Y) = 3 + 2 - 4 = 1`. `H(X|Y) = H(X) - I = 2`. `H(Y|X) = H(Y) - I = 1`. Not independent, since `I > 0` (equivalently `H(X,Y) < H(X) + H(Y)`).
5. `I(X,Y) <= min(H(X), H(Y)) = 2`. Mutual information can't exceed the entropy of the smaller variable.
6. **Zero.** Cross entropy bottoms out at `H(P)`, and one-hot labels are a deterministic distribution, so `H(P) = 0`. With soft labels — say `[0.7, 0.3]` — the loss could never drop below `H(P) = 0.881` no matter how good the model.
7. **No.** `I(X,Y) = H(X) + H(Y) - H(X,Y)`, so the two conditions are the same statement rearranged. Additivity of joint entropy and zero mutual information are one fact wearing two hats, and both are equivalent to independence.
8. **All three are equal**, at `log_2 4 = 2` bits. Entropy is a function of the probability vector alone; the outcome values and labels are irrelevant (property 2).
9. `H(T|M)` must be at most `H(T) = 1.48548`, and it must also satisfy `H(T|M) = H(T,M) - H(M) = 2.32193 - 0.970951 = 1.350979`. 1.42 fails the second check outright, and anything above 1.48548 would violate `H(Y|X) <= H(Y)`.
10. `KL = 0` iff `P = Q`, so `H(P,Q) = H(P) + 0 = H(P) = H(Q)`. Cross entropy collapses to plain entropy exactly when the predicted distribution is correct.
11. **No.** Zero information gain at a node means `I(X_2, Y) = 0` *for the distribution at that node*, which is a conditional statement given the path taken to get there. Globally `X_2` may well be dependent on `Y`, and may become useful deeper in the tree once other splits change the conditioning. Only when the gain is computed on the full unconditioned distribution does `I = 0` imply independence.
12. Because the optimal code for `P` is optimal — any other code (built for `Q`) is still a valid code for the same data, just a worse one, so it can only cost more bits, never fewer. The extra cost is exactly `KL[P||Q] >= 0`. This is property 3 of slide 21 read as a coding statement rather than an algebraic one.


---

[Schedule](https://mahdi-roozbahani.github.io/CS46417641-fall2026/docs/course-info/course-schedule-mahdi/) · [All topics](README.md)
