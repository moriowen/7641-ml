# Optimization

> **Foundations** · L9, L10 · Week 5  
> **Quiz:** Q4 — L9, L10

## Keyword definitions

### Objective functions and the cross-entropy loss

- **Objective function:** The function being minimized or maximized. He uses *objective function*, *loss*, and *error* interchangeably for the thing training minimizes. *"Optimization = training."*
- **Probabilistic vs non-probabilistic objective:** His taxonomy (inserted page after the dot-product slide): if the model outputs a probability distribution the objective is **cross entropy**; otherwise it is something non-probabilistic (left blank on the page — squared error is the obvious example, and it's the one he writes on the labeling slide).
- **Likelihood `L(theta | X)`:** `prod_{i=1..N} f(x^(i) | a, b)` — how probable the observed data is under parameters `theta = {a, b}` (for a Gaussian, `a = mu`, `b = sigma`). Maximized over `theta`.
- **Log-likelihood `l(theta | X)`:** `sum_i log f(x^(i) | a, b)`. Same maximizer as the likelihood, because `log` is monotone.
- **Negative average log-likelihood (NLL):** `-(1/N) sum_i log f(x^(i) | a, b) = E[-log q(x)]`. **This is the cross entropy.** Maximizing likelihood = minimizing NLL = minimizing cross entropy.
- **Cross entropy (as a loss):** `CE = -sum_{i=1..N} y_a^(i) log(y_hat_p^(i))^T`, with `y_a` the actual (one-hot) label and `y_hat_p` the predicted distribution.
- **`CE = H(P) + KL[P||Q]`:** Derived on the whiteboard by adding and subtracting `log p(x)` inside the expectation. `H(P)` is fixed by the labels, so minimizing CE over the model is minimizing KL.

### Label encoding

- **Label (ordinal) encoding:** `cat, fish, dog -> 0, 1, 2`. Turns classes into numbers with a fake order and fake distances; a regressor happily predicts `1.1` or `0.5`, which mean nothing.
- **One-hot encoding:** `cat = [1 0 0]`, `fish = [0 1 0]`, `dog = [0 0 1]`. He circles each row and writes **pmf** on it — a one-hot vector *is* a probability distribution (all mass on the true class), which is what lets it play `P` in cross entropy.
- **Softmax:** Turns a row of raw model scores (e.g. `[237.2, 10, 7]`) into a pmf (e.g. `[0.8, 0.1, 0.1]`), so predictions and labels live in the same space.

### Convexity

- **Convex function:** Bowl-shaped; `f'' >= 0` in 1-D, Hessian positive semi-definite in n-D. Any local minimum is global. `x^2` (`f'' = 2`) is his standard example.
- **Concave function:** Cap-shaped; `f'' <= 0`. `-x^2` (`f'' = -2`) and `log x` are his examples. Minimizing a concave function sends you to the boundary; *maximizing* it is the easy direction.
- **Strictly concave/convex:** Strict inequality — a unique optimum. He writes "Strictly concave" next to `-x^2`.
- **Hessian `H`:** The matrix of second partials, `H_ij = d^2 f / (dx_i dx_j)`. For `f(x, y)` it is `[[f_xx, f_xy], [f_yx, f_yy]]`.
- **Positive definite (PD):** `v^T H v > 0` for every non-zero `v` → strictly convex.
- **Positive semi-definite (PSD):** `v^T H v >= 0` → convex (possibly flat in some direction).
- **Jensen's inequality:** Concave `f`: `E[f(X)] <= f(E[X])`. Convex `f`: `E[f(X)] >= f(E[X])`. He drew both; the concave one is what proves `KL >= 0`.

### Constrained optimization

- **Unconstrained problem:** Take the derivative of the objective and set it to zero.
- **Equality constraint:** `g(x) = 0`. Solved with a **Lagrange function** `L(x, delta) = f(x) - delta g(x)`.
- **Inequality constraint:** `g(x) <= 0`. Solved with a Lagrange function **plus the KKT conditions**.
- **Lagrange multiplier:** `delta` in his notation (also called `alpha`, `beta` elsewhere — he says so). One per constraint: `delta_1, delta_2, ...`.
- **Stationarity:** `grad L = 0`, i.e. `grad f = delta grad g` — at the optimum the objective's gradient is parallel to the constraint's.
- **Primal feasibility:** The constraint holds, `g(x) <= 0`.
- **Dual feasibility:** `delta >= 0`.
- **Complementary slackness:** `delta g(x) = 0` — either the constraint is **active** (`g = 0`, `delta >= 0`) or **inactive** (`g < 0`, `delta = 0`).
- **Active / inactive constraint:** Active: the optimum sits on the boundary and the constraint behaves like an equality. Inactive: the unconstrained optimum already satisfies the constraint, so it has no effect.
- **Closed-form solution:** The optimum written directly as a formula (`M = delta/12`, ...). Contrast with gradient descent, used when `f'(x) = 0` can't be solved algebraically.

### Duality

- **Primal form:** The original problem, `min_x L(x, delta)` — he writes "primal form" next to the step solving for `M`, `S` in terms of `delta`.
- **Dual form:** What you get by substituting those back into `L`: a function of `delta` only. For a convex primal minimization, the dual is **concave** and is **maximized**.
- **Weak duality:** The dual's max is at or below the primal's min; the difference is the **(duality) gap**.
- **Strong duality:** The gap is zero — primal min = dual max. His taxonomy page brackets **linear and quadratic programming** under strong duality.
- **Linear / quadratic / non-linear programming:** Objective and constraints linear; quadratic objective with linear constraints; anything else (`exp`, `sin`, high powers).

### Gradient descent

- **Gradient descent (GD):** `x^(t+1) <- x^(t) - alpha grad f(x^(t))`. Step opposite the gradient to go downhill.
- **Gradient ascent (GA):** Same with `+`. For maximization.
- **Learning step `alpha`:** How far each step moves. A **hyperparameter** — chosen by you, not learned. His example uses `alpha = 0.02`.
- **Batch gradient descent (BGD):** He writes `GD ~> BGD`: plain GD computes the gradient on the whole dataset each step.

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L9 — Optimization | W5 (Sep 21-25) | [06-optimization.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/06-optimization.pdf) | **[06-optimization-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/06-optimization-note.pdf)** |
| L10 — Optimization (contd) | W5 (Sep 21-25) | [06-optimization.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/06-optimization.pdf) | **[06-optimization-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/06-optimization-note.pdf)** |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Both files are live as of Sep 28, 2026; re-check with `../scripts/check-slides.sh`.

The schedule page lists **no** annotated-notes link for L9/L10, but the file exists at the usual `-note.pdf` path anyway — found by URL, not from the schedule.

**The deck is almost entirely whiteboard.** The annotated PDF is 24 pages; only six are typed slides (title, outline, Cross Entropy, Labeling target values, Why cross entropy and not dot product?, KL Divergence), and they are recycled from the info-theory deck. Everything from convexity onward — Lagrange, KKT, duality, gradient descent — exists **only** as handwriting on inserted blank pages. The plain deck is therefore close to useless for this topic. Page numbers below are PDF page numbers of the note file, since the inserted pages carry no printed number.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [KKT conditions for inequality-constrained optimization (video)](https://www.youtube.com/watch?v=TqN-8fxYUYY) — *W4*
- [Gradient descent and momentum (course video, mp4)](https://mahdi-roozbahani.github.io/CS46417641-fall2026/other/GD%20and%20momentum.mp4) — *W4*
- [KKT and SVM (Stanford notes, PDF)](https://mahdi-roozbahani.github.io/CS46417641-fall2026/other/kkt-svm-stanford.pdf) — *W16*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Deep Learning — Goodfellow, Bengio & Courville (numerical optimization chapter)
- Learning from Data — Abu-Mostafa

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] Convexity: how do I check it, and why does it guarantee a global optimum?
- [ ] Gradient descent vs SGD vs momentum — what problem does each added piece solve?
- [ ] Lagrange multipliers for equality constraints, KKT for inequality constraints. Set up one of each by hand.
- [ ] How is the learning rate chosen, and what does divergence vs slow convergence look like?

## Notes on this topic

KKT is set up here and cashed in at [Support Vector Machines](17-support-vector-machines.md). The Stanford KKT/SVM PDF is listed in Week 16 but is worth skimming now. Cross entropy was deferred here from [Information Theory](04-information-theory.md) (its outline slide says *"Let's work on this subject in our Optimization lecture"*), and reappears as the loss in [Logistic Regression](13-naive-bayes-and-logistic-regression.md) and [Neural Networks](14-neural-networks.md).

**Not covered in the annotated notes despite the prep questions and the W4 reading:** SGD, momentum, learning-rate schedules, divergence. Gradient descent gets one page with a single step. The `GD and momentum.mp4` video is the only course source for momentum.

### Flow of the two lectures

Cross entropy as a loss (pp. 2-7) → KL and Jensen, re-proved (pp. 8-10) → optimization taxonomy (p. 11) → convexity and the Hessian (p. 12) → unconstrained → one equality constraint → two equality constraints (pp. 13-16) → inequality constraints and KKT (pp. 17-18) → primal/dual and duality gap (pp. 19-20) → gradient descent (p. 21) → derivative rules (p. 22) → a convolution worked in numpy (pp. 23-24).

### 1. From maximum likelihood to cross entropy (pp. 3-5)

p. 3 is the info-theory Cross Entropy slide unchanged: `H(p,q) = -sum_x p(x) log q(x) = H(P) + KL[P][Q]`.

p. 4, whiteboard. He draws a histogram of data (`p_i`, **actual**) with a Gaussian over it (`q_i = f(x^(i) | mu, sigma)`, **predicted**), then:

1. An objective function example: `f(x) = x^2`, `f'(x) = 2x = 0`, `x = 0`. Then `f(x) = (1/4)x^2` and `(1/4)x^2 + 1` — **same minimizer `x = 0`**. Scaling by a positive constant or adding a constant doesn't move the argmin. That's the licence for the `1/N` that appears two lines later.
2. `max_{a,b} L(theta | X) = prod_{i=1..N} f(x^(i) | a, b)` → take logs → `max l(theta | X) = sum_i log f(x^(i) | a, b)`
3. Flip the sign to minimize: `min sum_i -log f(x^(i) | a, b)`
4. Divide by `N`, since `(1/N) sum (.) = E[.]`: `(1/N) sum -log f(x^(i) | a, b) = E[-log f(x | a, b)] = E[-log q(x)]`
5. He circles the `1/N` and labels the whole thing **negative average log-likelihood**.

p. 5, whiteboard — the decomposition, using `E[a + b] = E[a] + E[b]` and `log a - log b = log(a/b)`:

```
E[-log q(x)] = E[ -log p(x) + log p(x) - log q(x) ]
             = E[-log p(x)] + E[ log (p(x)/q(x)) ]
             = sum p(x) log 1/p(x) + sum p(x) log p(x)/q(x)
        CE   = H(p(x))         +  KL[P][Q]
```

and then, boxed: **`-(1/N) sum log f(x^(i) | a, b)` = negative avg log-likelihood = CE** — both marked **Min**. Boxed below it: `CE = -sum_{i=1..N} p(x)^(i) log q(x)^(i)`.

So there are two separate routes to the same loss: *coding* (info theory: bits wasted by the wrong distribution) and *statistics* (maximum likelihood). Know both.

### 2. Labeling target values (p. 6)

Data matrix `X` is `n x d` (columns like `h`, `w`, `a` — height, weight, age). Labels `y_a` is `n x 1`.

- **Label encoding:** `y_a = [cat, fish, dog, cat, ...] = [0, 1, 2, 0, ...]` → ML → `y_hat_p = [0.1, 0.5, 1.1, ...]`. The predictions are real numbers between/beyond the codes — the encoding has invented an ordering (`cat < fish < dog`) and a distance (`dog` is "twice as far" from `cat` as `fish`).
- **One-hot encoding:** rows `[1 0 0]`, `[0 1 0]`, `[0 0 1]`, `[1 0 0]` → ML → raw scores `[237.2, 10, 7]`, `[2, 73, 2]`, `[1, 2, 85.2]` → **Softmax** → `[0.8, 0.1, 0.1]`, `[0.2, 0.7, 0.1]`, `[0.1, 0.1, 0.8]`. (The softmax outputs are illustrative — the real softmax of `[2, 73, 2]` is essentially `[0, 1, 0]`. The point is the shape of the pipeline, not the arithmetic.)

Two candidate objectives on the one-hot setup:

- **Squared error:** `min sum_i ||y_a^(i) - y_hat_p^(i)||_2^2 = [(1-0.8)^2 + (0-0.1)^2 + (0-0.1)^2] + ...` — **best result = 0**.
- **Dot product:** `max sum_i y_a^(i) y_hat_p^(i)T = [1 0 0][0.8 0.1 0.1]^T + ...` — **best result = N** (each row contributes at most 1). He crosses out the sum and writes the matrix form `Y_a Y_p^T`.

### 3. Why cross entropy and not the dot product? (p. 7)

Error / loss / objective function: `CE = -sum_i y_a^(i) log(y_hat_p^(i))^T`.

With `y_a = [1 0 0]` and `y_hat_p = [0.8 0.1 0.1]`: `CE = -([1 0 0][log 0.8, log 0.1, log 0.1]^T) + ...`. Because the label is one-hot, **only the log-probability of the true class survives**. He then contrasts `log 0.999999` with `log 0.000001`.

He sketches the two objectives side by side:

1. `min -sum y_a y_hat_p^T` — error is **linear** in the predicted probability, bottoming out at a finite floor (he marks `-100`).
2. `min -sum y_a log(y_hat_p)^T` — error follows the **log** curve, and a confident wrong prediction sends it to enormous values (he marks `1,000,000` on the axis). In natural log, `-log(0.000001) = 13.8` per sample versus `-log(0.999999) = 0.000001`.

Between them he draws `f(x) = x^2` with gradient-descent steps zig-zagging down to `f'(x) = 2x = 0`.

My reading of the page (the sketch doesn't state a conclusion in words): with one-hot labels the dot product and CE both look only at the true-class probability `p_c`; the dot product scores `-p_c` and CE scores `-log p_c`. The dot product's penalty for being confidently wrong (`p_c = 0.000001`) is barely worse than for being unsure (`p_c = 0.3`) and its gradient is constant, whereas `-log` grows without bound and gives a large gradient exactly where the model is most wrong. CE is also the principled choice — it is the NLL from section 1.

### 4. KL divergence and Jensen, again (pp. 8-10)

p. 8 is the info-theory KL slide, plus a handwritten `KL[P][Q] >= 0` and `P = actual`, `Q = predicted` on the ratio. New typed line at the bottom: **When `P = Q`, `KL[P||Q] = 0`.**

p. 9 — Jensen's inequality, drawn out properly this time:

- **Concave**, `f(x) = -x^2`, `f''(x) = -2`, "Strictly concave". `E[f(x)] <= f(E[x])`; he labels the left side **lb** (lower bound) and the right **ub** (upper bound).
- Worked: `x in {-2, 2}`, `p(x) = [1/2, 1/2]`. `E[f(x)] = (1/2)(-4) + (1/2)(-4) = -4`. `E[x] = (1/2)(-2) + (1/2)(2) = 0`, so `f(E[x]) = 0`. Indeed `-4 <= 0`. The chord between the two points lies *below* the curve. He also writes `p(x) = [1/4, 3/4]` as a second case to try.
- **Convex**, `f(x) = x^2`: the inequality flips, `E[f(x)] >= f(E[x])` — chord *above* the curve.
- A wavy function (neither convex nor concave) at the bottom: a chord can cross the curve, so Jensen gives nothing.

p. 10 — the `KL >= 0` proof, rewritten with `g(x) = Q(x)/P(x)`:

```
-KL[P][Q] = sum P(x) log (Q(x)/P(x)) = sum p(x) log g(x) = E[log g(x)]
          <= log E[g(x)]                 (log is concave)
           = log sum P(x) Q(x)/P(x)      (the P's cancel)
           = log sum Q(x)                (circled: e.g. [0.8 0.1 0.1] sums to 1)
           = log 1 = 0
  KL[P][Q] >= 0
```

(He writes `<=` at every line; only the first step is an inequality, the rest are equalities.)

### 5. Optimization taxonomy (p. 11)

```
Optimization = Training ~> Objective function ~> Probabilistic function ~> Cross entropy
                     |                           Non-probabilistic  "   ~> (blank)
                     |-> NO constraints ~> take a derivative of your objective function
                     |-> Constraints -+-> Equality   ~> Lagrange function
                                      +-> Inequality ~> Lagrange function + KKT
```

Programming types, with his examples:

| Type | Objective | Constraints |
|---|---|---|
| Linear | `f(x,y) = x + 2y` | `x + y < 10`, `x + y = 20` |
| Quadratic | `f(x,y) = x^2 + 2y` | `x + y < 10`, `x + y = 20` |
| Non-linear (circled) | `f(x,y) = exp(x^2) + 2y^3` | `sin(x) + exp(y) < 10`, `x^100 + y^20 = 20` |

He brackets linear and quadratic with **→ Strong duality**. (The paired constraints `x + y < 10` and `x + y = 20` are jointly infeasible as written — they're illustrating the *form* of each constraint type, not a single solvable problem.)

Side example, circled: `max f(x) = x` on `[-5, 5]`. A linear objective has no stationary point; without the constraint it's unbounded, and with it the answer is the boundary, `x = 5`.

### 6. Convexity and the Hessian (p. 12)

- `f(x) = x^3`: `f''(x) = 6x = 0` at `x = 0`, an inflection point. For `x < 0`, `f'' < 0` (concave); for `x > 0`, `f'' > 0` (convex). ⚠️ **His sketch appears to label the left side "convex" and the right "concave", which is backwards** — trust `f'' = 6x`, not the labels. Either way, `x^3` is neither convex nor concave overall.
- `f(x) = |x|`: `f'(x) = -1` for `x < 0`, `+1` for `x > 0`, **no derivative at 0**, yet the minimum is at 0 and the function is convex. Setting `f' = 0` finds nothing — convexity does not need differentiability.
- `f(x, y) = x^2 + y` and its Hessian `[[d^2f/dx^2, d^2f/dxdy], [d^2f/dydx, d^2f/dy^2]]`. Then `v^T H v > 0` (1xd · dxd · dx1) → **positive definite**; `>= 0` → **positive semi-definite**.
- `f(x) = x^2 => f''(x) = 2` in the corner — the 1-D version of the same test.

Worked (mine, not on the page): for `x^2 + y`, `H = [[2, 0], [0, 0]]`, so `v^T H v = 2 v_1^2 >= 0` — PSD, not PD. Convex, but flat along `y` — and since it's linear in `y`, it has no minimum at all.

### 7. Unconstrained and equality-constrained (pp. 13-16)

The running example is personal: `M` = hours you study ML per day, `S` = hours you sleep per day.

**Unconstrained (p. 13):** `min f(M, S) = 6M^2 + 3S^2`. `df/dM = 12M = 0 => M = 0`; `df/dS = 6S = 0 => S = 0`. The answer is correct and useless — you need a constraint to make the problem mean anything.

**One equality constraint (p. 14):** add `M + S = 24`, i.e. `g(M, S) = M + S - 24 = 0`.

```
L(M, S, delta) = f(M, S) ± delta g(M, S)
               = 6M^2 + 3S^2 - delta (M + S - 24)

dL/dM     = 12M - delta = 0   =>  M = delta/12      (closed-form)
dL/dS     =  6S - delta = 0   =>  S = delta/6
dL/ddelta = 0                 =>  M + S = 24   =>  delta/12 + delta/6 = 24  =>  delta = 96

M = 96/12 = 8,  S = 96/6 = 16      check: 8 + 16 = 24
```

`f(8, 16) = 384 + 768 = 1152` (my arithmetic). Note that `dL/ddelta = 0` just gives back the constraint — that's the whole trick.

**Geometry (p. 15):** `grad L = grad(f - delta g) = 0  =>  grad f(M, S) = delta grad g(M, S)`. At the optimum the objective's gradient and the constraint's gradient are **parallel**, and `delta` is the scale factor. Next to `delta` he writes *large value*, `delta = 0.001`, `delta = 0` — the size of `delta` says how hard the constraint is pushing against the objective; `delta = 0` means it isn't pushing at all. Sketch: `f(x) = x^2` with a vertical constraint line at `x = 3`, arrows for `grad f` and `delta grad g`.

**Two equality constraints (p. 16):** `M + S = 24` (`g`, multiplier `delta_1`) and `M - S = 10` (`h`, multiplier `delta_2`): `L(M, S, delta_1, delta_2) = f(M, S) - delta_1 g(M, S) - delta_2 h(M, S)`. One multiplier per constraint. He stops at the setup. Finished by me: the two constraints already pin `M = 17`, `S = 7`, so `f = 1734 + 147 = 1881`; with two constraints in two unknowns the objective has no freedom left.

### 8. Inequality constraints and KKT (pp. 17-18)

`min f(M, S) = 6M^2 + 3S^2` s.t. `M + S <= 24`, i.e. `g(M, S) = M + S - 24 <= 0`.

Solutions come in two kinds: **Active** (on the boundary, `M + S = 24` — behaves like the equality case) or **Inactive** (`M + S < 24` — interior).

**KKT conditions**, numbered as he numbers them:

1. **Stationary:** `min L(M, S, delta) = 6M^2 + 3S^2 + delta (M + S - 24)`; `grad L = 0`. (He writes `+` and `-` above `delta`; for `g <= 0` with `delta >= 0`, the `+` is the consistent choice.)
2. **Primal feasibility:** `g(M, S) <= 0`
3. **Dual feasibility:** `delta >= 0`
4. **Complementary slackness:** `delta g(M, S) = 0`
   - Active: `g(M, S) = 0 -> delta > 0` (strictly, `delta >= 0` is allowed)
   - Inactive: `g(M, S) != 0 -> delta = 0`

He circles `g(M, S) > 0` as the forbidden case (violates primal feasibility). Sketch: a bowl with the constraint `x <= 3`.

Applied to this problem (mine): the unconstrained optimum `(0, 0)` already satisfies `0 + 0 <= 24`, so the constraint is **inactive**, `delta = 0`, and the answer is `M = S = 0`. Flip it to `M + S >= 24` (`g = 24 - M - S <= 0`) and it becomes active, reproducing `M = 8, S = 16`.

**p. 18 — active vs inactive in 1-D**, four pictures:

| Objective | Constraint(s) | Candidates | Minimum |
|---|---|---|---|
| `x^2` | `x <= 3` | ① `x = 3` active, `f = 9`; ② `x = 0` inactive, `f = 0` | ② — inactive, `f = 0` |
| `x^2` | `x <= -3` (rewritten `x + 3 <= 0 -> g(x) <= 0 -> primal feasibility`) | ① `x = -3` active; ② `x = 0` inactive but infeasible | ① — active |
| `x^2` | `x >= -3`, `x <= 3` | ①, ③ boundaries active; ② `x = 0` inactive | ② |
| concave cap (`-x^2`-like) | `x >= -3`, `x <= 2` | ① `x = -3` active; ② the peak, inactive; ③ `x = 2` active | an **active** boundary — the stationary point ② is a *max* |

The last picture is the one to understand: minimizing a concave function, the interior stationary point is the worst place to be, and the minimum is at whichever active boundary is lower. KKT candidates must still be *compared*.

### 9. Primal and dual (pp. 19-20)

`min f(M, S) = (1/2)M^2 + (1/2)S^2` (convex) s.t. `M + S = 24`.

```
① L(M, S, delta) = (1/2)M^2 + (1/2)S^2 - delta (M + S - 24)
   dL/dM = 0  =>  M = delta          ("primal form")
   dL/dS = 0  =>  S = delta

② L(delta) = (1/2)delta^2 + (1/2)delta^2 - delta (2 delta - 24)
           = delta^2 - 2 delta^2 + 24 delta
           = -delta^2 + 24 delta           concave → Max      ("dual form")
   dL/ddelta = -2 delta + 24 = 0  =>  delta = 12
```

So `M = S = 12`. Checks (mine): primal value `f(12, 12) = 72 + 72 = 144`; dual value `-144 + 288 = 144`. Equal — **strong duality**.

p. 20: two pictures. **Weak duality**: the primal (convex bowl, minimized) sits above the dual (concave cap, maximized) with a **Gap** between the primal's min and the dual's max. **Strong duality**: the two touch; gap zero.

Why this matters later: in SVMs the dual is the problem actually solved, and it's where kernels come from — see [Support Vector Machines](17-support-vector-machines.md).

### 10. Gradient descent (p. 21)

`f(x) = x^2 + exp(x)`, `f'(x) = 2x + exp(x) = 0` — **"this does NOT have a closed form solution"**. That is the whole motivation for GD.

`x^(t+1) <- x^(t) ± alpha grad f(x)`: `+` is **GA** (gradient ascent), `-` is **GD**. `alpha` is the **learning step**, a **hyperparameter**, here `alpha = 0.02`. `GD ~> BGD`.

One step from `x^(t) = 3`:

`x^(t+1) = 3 - 0.02 (2*3 + exp(3)) = 3 - 0.02 (26.0855) = 2.4783`

and `f(x^(t)) > f(x^(t+1))` — checked (mine): `f(3) = 29.09`, `f(2.478) = 18.06`. The true minimum (Newton's method, mine) is at `x ≈ -0.3517`, `f ≈ 0.827`. The sketch shows big steps on the steep side shrinking as the slope flattens — step size is `alpha * |f'|`, so GD slows down automatically near the minimum even with fixed `alpha`.

### 11. Derivative rules (p. 22)

1. Quotient: `(f/g)' = (f'g - fg') / g^2`
2. Product: `(fg)' = f'g + fg'`
3. Chain (power form): `(u^n)' = n u' u^(n-1)`

### 12. Convolution in numpy (pp. 23-24)

Not optimization — likely a preview for the numpy toolbox session (L11) or [CNNs](15-convolutional-neural-networks.md). A 3x3 filter `F` slides over an 8x8 image (pixel values up to 255). At the top-left position:

```
F                patch          elementwise product    np.sum()
[ 1  0 -1]       [0 1 2]        [0 0 -2]
[ ?  0  ?]   *   [2 1 3]   =    [2 0 -3]          ->     -3
[ 1  0 -1]       [1 2 1]        [1 0 -1]
```

⚠️ The middle row of `F` is overwritten on the page (it looks like `2` and `-2` scribbled over the originals). The product matrix and the `-3` are consistent with a middle row of `[1 0 -1]` (a Prewitt filter). With `[2 0 -2]` (a Sobel filter) the answer would be `-4`. The output grid is 8x8 with the border filled with zeros — the valid 3x3 convolution of an 8x8 image produces only a 6x6 interior.

## My notes

### Before lecture


### During lecture


### After lecture — what I still don't get



## Quiz prep

- [ ] Re-read the professor's annotated notes
- [ ] Redo any worked example from the deck without looking
- [ ] Write my own one-paragraph summary of the topic

Things he worked by hand or left open — the likeliest quiz material:

- [ ] Derive "max likelihood = min NLL = min cross entropy" from `prod f(x^(i) | a, b)` (p. 4)
- [ ] Derive `CE = H(P) + KL[P||Q]` by adding and subtracting `log p(x)` (p. 5)
- [ ] Why one-hot and not label encoding; what "best result" is for squared error (0) and for the dot product (`N`) (p. 6)
- [ ] Why cross entropy and not the dot product? (p. 7)
- [ ] "log function is concave or convex?" (p. 8 — **concave**); Jensen for `-x^2` with `x in {-2, 2}` (p. 9)
- [ ] Solve `min 6M^2 + 3S^2` s.t. `M + S = 24` without looking: `delta = 96`, `M = 8`, `S = 16` (p. 14)
- [ ] State all four KKT conditions and the active/inactive cases of complementary slackness (p. 17)
- [ ] For each of the four 1-D pictures on p. 18, say which candidate is the minimum and whether the constraint is active
- [ ] Derive the dual of `min (1/2)M^2 + (1/2)S^2` s.t. `M + S = 24` and show primal = dual = 144 (p. 19)
- [ ] One GD step on `x^2 + exp(x)` from `x = 3` with `alpha = 0.02` (p. 21)

### The relationship map

```
max L(theta|X) = prod f(x_i|theta)
  <=> max sum log f(x_i|theta)                log is monotone
  <=> min -(1/N) sum log f(x_i|theta)         sign flip, positive scaling
   =  E[-log q(x)] = CE = H(P) + KL[P||Q]     H(P) fixed -> min CE = min KL

no constraints   : grad f = 0
equality g = 0   : L = f - delta g,  grad f = delta grad g,  delta any sign
inequality g <= 0: L = f + delta g,  + KKT:
                   stationarity   grad L = 0
                   primal feas.   g <= 0
                   dual feas.     delta >= 0
                   comp. slack.   delta g = 0   (active: g = 0; inactive: delta = 0)

convex primal (min)  -> concave dual (max)
dual max <= primal min   weak duality (gap >= 0)
dual max  = primal min   strong duality (gap 0; LP and QP)

GD: x <- x - alpha grad f      GA: x <- x + alpha grad f
convex: f'' >= 0 / H PSD       strictly convex: H PD
Jensen: concave E[f(X)] <= f(E[X]),  convex E[f(X)] >= f(E[X])
```

### Traps — the things that are implied but never said out loud

1. **Scaling or shifting an objective changes its value, not its argmin.** `x^2`, `(1/4)x^2` and `(1/4)x^2 + 1` all minimize at `x = 0`. That's why `1/N`, `log`, and the constant `H(P)` can all be added or dropped freely — as long as the scale is *positive*. Multiplying by `-1` turns a min into a max.
2. **Minimizing NLL, minimizing CE and minimizing KL are the same optimization, but not the same number.** CE = NLL (averaged); CE and KL differ by `H(P)`. For one-hot labels `H(P) = 0`, so all three coincide numerically too.
3. **Maximum likelihood is a *max*; cross entropy is a *min*.** The sign flip in `-log` is what turns one into the other. A question offering "maximize cross entropy" is wrong.
4. **The one-hot label is `P` (actual), the softmax output is `Q` (predicted).** Swapping them gives `-sum q log p`, which is undefined whenever `p` has a zero — and one-hot labels are mostly zeros.
5. **With one-hot labels, cross entropy only sees the true class's predicted probability.** `CE = -log q_true`. The other predicted probabilities affect the loss only through softmax normalization.
6. **Label encoding is wrong for nominal classes because it invents order and distance, not because numbers are bad.** One-hot is a pmf; an integer code isn't.
7. **Best squared error is 0; best dot-product score is `N`.** One is minimized, one is maximized — watch which direction the question states.
8. **Jensen's direction depends on convex vs concave.** Concave (`log`, `-x^2`): `E[f(X)] <= f(E[X])`. Convex (`x^2`): `>=`. Getting it backwards "proves" `KL <= 0`.
9. **In the `KL >= 0` proof only the Jensen step is an inequality.** Cancelling `P` and `sum Q = 1` are equalities, even though his page writes `<=` down the whole column.
10. **`f'' = 0` at a point doesn't make it a minimum or a maximum.** `x^3` has `f''(0) = 0` and it's an inflection. And his left/right convex/concave labels on that sketch look swapped — trust `f'' = 6x`.
11. **Convex doesn't require differentiable.** `|x|` is convex with its minimum at the kink where `f'` doesn't exist. Setting `f' = 0` finds nothing there.
12. **PSD vs PD is convex vs *strictly* convex.** `x^2 + y` has a PSD Hessian — convex, but not strictly, and unbounded below along `y`. Convexity guarantees any minimum is global; it doesn't guarantee a minimum exists.
13. **`dL/ddelta = 0` gives back the constraint.** It's not a new equation — it's how the constraint enters the system.
14. **Equality multipliers can have any sign; inequality multipliers must be `>= 0`.** Dual feasibility is an inequality-only condition. And the sign convention in `L = f ± delta g` is a choice — for equality it only flips the sign of `delta`.
15. **Inactive means `delta = 0`, not "the constraint doesn't exist".** The constraint still has to hold (primal feasibility) — it just isn't binding.
16. **Complementary slackness is an "or", not an "and".** `delta g = 0` allows `g = 0` or `delta = 0` (or both). It forbids both non-zero.
17. **KKT points must still be compared.** For a concave objective minimized on an interval, the stationary point satisfies stationarity but is the *maximum*; the minimum is at an active boundary.
18. **The dual of a convex minimization is a concave *maximization*.** `L(delta) = -delta^2 + 24 delta` is maximized, not minimized. Minimizing it gives `-infinity`.
19. **Weak duality always holds; strong duality needs conditions.** His notes attach strong duality to linear and quadratic programming. Dual optimum `<=` primal optimum always.
20. **GD vs GA is one sign.** `-alpha grad f` descends; `+alpha grad f` ascends. `alpha` is a hyperparameter — never learned by the same gradient step.
21. **Fixed `alpha` doesn't mean fixed step size.** The step is `alpha * grad f`, so it shrinks as the gradient shrinks near the minimum.
22. **"No closed form" is the reason for GD, not non-convexity.** `x^2 + exp(x)` is strictly convex (`f'' = 2 + e^x > 0`) with a unique minimum — it just can't be solved algebraically.

### Self-test

Cover the answers.

1. Show that maximizing `prod_i f(x^(i) | theta)` gives the same `theta` as minimizing `-(1/N) sum_i log f(x^(i) | theta)`. Which two facts make that legal?
2. Labels are soft, `P = [0.7, 0.3]`. What's the lowest cross entropy any model can reach, in bits?
3. `min 6M^2 + 3S^2` s.t. `M + S = 30`. Solve for `delta`, `M`, `S`.
4. Same objective, s.t. `M + S <= 30`. What's the answer, and is the constraint active?
5. `min x^2` s.t. `x >= 2`. Active or inactive? What's `x*`?
6. Is `f(x, y) = x^2 + 2y^2` convex? Strictly? Give its Hessian.
7. Derive the dual of `min (1/2)M^2 + (1/2)S^2` s.t. `M + S = 10` and verify strong duality.
8. One GD step on `f(x) = x^2` from `x = 5` with `alpha = 0.1`. And with `alpha = 1.5`?
9. Why can't you just set `f'(x) = 0` for `f(x) = x^2 + exp(x)`?
10. `y_a = [0 1 0]`, `y_hat_p = [0.2 0.7 0.1]`. Compute the CE (natural log), the squared error, and the dot product.
11. With the Sobel filter `[[1,0,-1],[2,0,-2],[1,0,-1]]` and the patch on p. 23, what does `np.sum` give?

**Answers**

1. `log` is monotone increasing, so it keeps the argmax: max `prod` = max `sum log`. Negating turns max into min, and multiplying by a positive `1/N` doesn't move the argmin.
2. `H(P) = -(0.7 log_2 0.7 + 0.3 log_2 0.3) = 0.881` bits. CE bottoms out at `H(P)` when `Q = P`.
3. `M = delta/12`, `S = delta/6`, so `delta/4 = 30`, `delta = 120`, `M = 10`, `S = 20`.
4. `M = S = 0`. The unconstrained minimum `(0, 0)` satisfies `0 <= 30`, so the constraint is **inactive** and `delta = 0`.
5. **Active.** The unconstrained minimum `x = 0` violates `x >= 2`, so the optimum is on the boundary, `x* = 2`.
6. `H = [[2, 0], [0, 4]]`, `v^T H v = 2v_1^2 + 4v_2^2 > 0` for `v != 0` → positive definite → **strictly** convex.
7. `M = S = delta`; `L(delta) = delta^2 - delta(2 delta - 10) = -delta^2 + 10 delta`, max at `delta = 5`. Primal `f(5, 5) = 25`; dual `-25 + 50 = 25`. Equal → strong duality.
8. `f' = 2x = 10`. `alpha = 0.1`: `x = 5 - 1 = 4` (converging). `alpha = 1.5`: `x = 5 - 15 = -10` — overshoots and gets farther from 0 every step (`x -> -2x`); diverges.
9. You can set it — `2x + e^x = 0` — you just can't *solve* it in closed form. That's the whole reason to iterate.
10. CE `= -log 0.7 = 0.357`. Squared error `= 0.2^2 + 0.3^2 + 0.1^2 = 0.14`. Dot product `= 0.7`.
11. `0 - 2 + 4 - 6 + 1 - 1 = -4`.


---

[Schedule](https://mahdi-roozbahani.github.io/CS46417641-fall2026/docs/course-info/course-schedule-mahdi/) · [All topics](README.md)
