# Probability & Statistics

> **Foundations** · L5, L6 · Week 3  
> **Quiz:** Q2 — L5, L6

## Keyword definitions

### Sample space, random variables, distributions

#### Building blocks

- **Sample space:** The collection of all possible outcomes of an experiment.
- **Random variable (`X`):** A variable whose value is an outcome in the sample space. `p(x)` is shorthand for `p(X = x)`, and every probability satisfies `p(x) >= 0`.
- **Event:** A subset of the sample space — a set of outcomes whose probability can be asked for.
- **Discrete random variable:** A random variable taking countably many values, such as a coin flip or a dice roll (integers).
- **Continuous random variable:** A random variable taking real values, such as temperature.

#### Describing a distribution

- **Probability mass function (PMF):** The distribution of a discrete random variable. Each value is a genuine probability, and they sum to one: `sum_{x in A} p(x) = 1`.
- **Probability density function (PDF):** The distribution of a continuous random variable. Its values are *densities*, not probabilities, and it integrates to one: `integral p(x) dx = 1`. A density may exceed 1; only the area under it is bounded by 1.
- **Density (likelihood) value:** The height `p(x)` of a PDF at a point. Probability comes only from integrating it over an interval, so `p(X = x) = 0` for any single point of a continuous variable.
- **Cumulative distribution function (CDF):** `F_x(x) = p(X <= x)`, the probability of landing at or below `x`.

#### Named distributions

- **Uniform density:** `f_x(x) = 1/(b - a)` for `a <= x <= b`, and `0` otherwise. Every point in the interval is equally likely.
- **Exponential density:** `f_x(x) = (1/mu) e^(-x/mu)` for `x >= 0`, with CDF `F_x(x) = 1 - e^(-x/mu)`.
- **Bernoulli distribution:** The distribution of a **single** trial with two outcomes: `p(x = 1) = p`, `p(x = 0) = 1 - p`.
- **Binomial distribution:** The number of successes in `n` independent Bernoulli trials: `P(X = k) = C(n,k) p^k (1-p)^(n-k)`, where `k` is the number of successes and `n - k` the number of failures.
- **Binomial coefficient `C(n,k)`:** The number of ways to select `k` distinct combinations out of `n` trials, **irrespective of order**.
- **Gaussian (normal) density:** `f(x | mu, sigma^2) = 1/sqrt(2 pi sigma^2) * exp(-(x - mu)^2 / (2 sigma^2))`. Fully determined by its mean `mu` (where it is centred) and variance `sigma^2` (how wide it is).

### Joint, conditional, and independence

#### Three kinds of probability

- **Joint probability:** The probability of two outcomes occurring together, `p(X = x_i, Y = y_j) = n_ij / N`, where `n_ij` counts the trials in which both happened and `N` is the total number of trials.
- **Marginal probability:** The probability of one variable on its own, `p(X = x_i) = c_i / N`, recovered from a joint distribution by summing out the other variable.
- **Conditional probability:** The probability of one outcome **given** another is known, `p(Y = y_j | X = x_i) = n_ij / c_i`. Verbally: the fraction of the worlds in which `Y` is true among those where `X` is already true.

#### Rules that connect them

- **Sum rule (marginalization):** `p(X) = sum_Y p(X, Y)` — summing a joint distribution over one variable returns the marginal of the other.
- **Product rule (chain rule):** `p(X, Y) = p(Y | X) p(X)`. It follows directly from the counts: `n_ij/N = (n_ij/c_i)(c_i/N)`.

#### Independence

- **Independence:** `X` and `Y` are independent when knowing one tells you nothing about the other: `p(X | Y) = p(X)`, equivalently `p(X, Y) = p(X) p(Y)`.
- **Conditional independence:** `X` and `Y` are independent *once `Z` is known*: `p(X | Y, Z) = p(X | Z)`. The deck's example: `P(Flu | Virus, DrinkBeer) = P(Flu | Virus)` — beer drops out of the conditioning set once the virus is known. Conditional independence neither implies nor is implied by plain independence.
- **Factorizing a joint distribution:** Repeated use of the product rule writes a joint over many variables as a chain of conditionals; conditional-independence assumptions then delete variables from each conditioning set, which is what makes large joints tractable. This is the machinery behind [Naive Bayes](13-naive-bayes-and-logistic-regression.md).

### Bayes' rule

#### The rule

- **Bayes' rule:** `P(X | Y) = P(X, Y) / P(Y) = P(Y | X) P(X) / P(Y)`. It reverses the direction of a conditional — turning what you can measure into what you want to know.

#### Its four pieces

- **Prior `P(X)`:** The belief about `X` before seeing evidence.
- **Likelihood `P(Y | X)`:** How probable the observed evidence `Y` would be if `X` held.
- **Posterior `P(X | Y)`:** The updated belief about `X` after observing `Y`.
- **Evidence (marginal likelihood) `P(Y)`:** The normalizing denominator, obtained by summing the numerator over every value of the unknown: `P(Y) = P(X|Y)P(Y) + P(X|not Y)P(not Y)` in the binary case, or `sum_{i in S} P(X | Y = y_i) P(Y = y_i)` in general.

#### Extension

- **Conditioned Bayes' rule:** Bayes' rule still holds inside a fixed context `Z`: `P(Y | X, Z) = P(X | Y, Z) P(Y, Z) / P(X, Z)`.

### Mean, variance, covariance, correlation

#### Expectation and moments

- **Expectation `E_X[g(X)]`:** The mean value, centre of mass, or first moment: `E_X[g(X)] = integral g(x) p_X(x) dx`. For a discrete variable the integral becomes a sum.
- **Mean `mu`:** Expectation of the variable itself, `E_X[X] = integral x p_X(x) dx`.
- **N-th moment:** `E[g(X)]` with `g(x) = x^n`.
- **N-th central moment:** `E[g(X)]` with `g(x) = (x - mu)^n` — the moment taken about the mean rather than about zero.
- **Linearity of expectation:** `E[aX] = a E[X]`, `E[a + X] = a + E[X]`, and `E[X + Y] = E[X] + E[Y]`. The last holds whether or not `X` and `Y` are independent.

#### Spread of one variable

- **Variance:** The second central moment, `Var(X) = E_X[(X - E_X[X])^2] = E_X[X^2] - E_X[X]^2`. It measures spread about the mean.
- **Variance under transformation:** `Var(aX) = a^2 Var(X)` and `Var(a + X) = Var(X)` — shifting a variable does not change its spread, scaling it changes the spread quadratically.
- **Standard deviation `sigma`:** The square root of the variance, back in the units of the original variable.

#### Two variables together

- **Covariance:** `cov(X, Y) = E[(X - E[X])(Y - E[Y])] = E[XY] - E[X]E[Y]`. Positive when the two tend to move together, negative when they move oppositely, zero when there is no linear relationship. Its magnitude depends on the units of both variables.
- **Variance of a sum:** `Var(X + Y) = Var(X) + 2 cov(X, Y) + Var(Y)`. The cross term vanishes only when the variables are uncorrelated.
- **Correlation:** Covariance normalized by both standard deviations, `corr(X, Y) = cov(X, Y) / (sigma_X sigma_Y)`, giving a unit-free number in `[-1, 1]`. Same information as covariance, on a comparable scale.
- **Uncorrelated:** `cov(X, Y) = 0`. It rules out a *linear* relationship only.
- **Uncorrelated vs independent:** Independence implies uncorrelated; **the converse is false in general** — a nonlinear dependence (e.g. `Y = X^2` with `X` symmetric about 0) has zero covariance yet total dependence. For **jointly Gaussian** variables the two do coincide. This is the same trap as the linear-algebra deck's "uncorrelated iff orthogonal?" question — see [Linear Algebra](02-linear-algebra.md).
- **Covariance matrix `Sigma`:** For a random vector, `Sigma = Cov(X) = E[(X - mu)(X - mu)^T]` — variances on the diagonal, pairwise covariances off it. Always symmetric and positive semidefinite.

### Gaussians in more than one dimension

#### The distribution

- **Multivariate Gaussian:** `p(x | mu, Sigma) = 1/((2 pi)^(n/2) |Sigma|^(1/2)) * exp(-1/2 (x - mu)^T Sigma^-1 (x - mu))`, for `x` in `R^n`.
- **Moment parameterization:** Describing that Gaussian by its first two moments, `mu = E(X)` and `Sigma = Cov(X)`. They are all the distribution has.
- **Mahalanobis distance:** `Delta^2 = (x - mu)^T Sigma^-1 (x - mu)` — the squared distance from the mean, rescaled by the covariance so that spread-out directions count for less. It is the exponent of the multivariate Gaussian, so level sets of the density are level sets of this distance: ellipsoids whose axes are the eigenvectors of `Sigma`.

#### Closure properties

- **Linear transform property:** A linear transform of a Gaussian is Gaussian. `E(AX + b) = A E(X) + b` and `Cov(AX + b) = A Cov(X) A^T` hold for *any* distribution; for a Gaussian this gives `X ~ N(mu, Sigma)` implies `AX + b ~ N(A mu + b, A Sigma A^T)`.
- **Sum property:** The sum of two **independent** Gaussians is Gaussian, with `mu_y = mu_1 + mu_2` and `Sigma_y = Sigma_1 + Sigma_2`.
- **Product property:** The product of two Gaussian functions is another Gaussian function, though **no longer normalized**: `N(a, A) N(b, B) prop N(c, C)` with `C = (A^-1 + B^-1)^-1` and `c = C A^-1 a + C B^-1 b`.

#### Why Gaussians are everywhere

- **Central limit theorem (CLT):** The distribution of the sample mean of `n` i.i.d. draws tends to a normal distribution as `n` grows, **regardless of the shape of the original distribution**. The deck's illustration: repeated size-4 samples from a biased dice PMF have means that pile up into a bell curve.

### Probability vs likelihood, and MLE

#### Two readings of one expression

- **Probability:** With the parameters fixed, the chance of the data — `p(data | theta)` read as a function of the data. The area under a PDF over an interval.
- **Likelihood:** With the data fixed, the same expression `L(theta | X)` read as a function of the **parameters**. It is not a probability distribution over `theta` and does not integrate to 1.

#### Maximum likelihood

- **i.i.d. (independent and identically distributed):** The main assumption behind MLE — each observation is drawn from the same distribution and is independent of the others. It licenses turning the joint likelihood into a product: `L(theta | X) = prod_{i=1..n} P(x^{i} | theta)`.
- **Maximum likelihood estimation (MLE):** Choosing the parameter value that makes the observed data most probable: `theta_hat = argmax_theta L(theta | X)`.
- **Log-likelihood `l(theta | X)`:** `log L(theta | X)`. Taking the log turns the product into a sum, which is easier to differentiate; since `log` is monotonic, the maximizer is unchanged. This is *the trick* the deck names explicitly.
- **The Bernoulli MLE (the deck's worked case):** With `P(x^{i} | theta) = theta^(x^{i}) (1 - theta)^(1 - x^{i})`, the likelihood collapses to `theta^(sum x^{i}) (1 - theta)^(sum (1 - x^{i}))`. Its log is `log(theta) sum x^{i} + log(1 - theta) sum (1 - x^{i})`; setting the derivative to zero gives `sum x^{i} / theta - sum (1 - x^{i}) / (1 - theta) = 0`, hence **`theta_hat = (1/n) sum_i x^{i}`** — the observed fraction of heads.
- **Objective function:** The quantity being optimized during training. Here it is the (log-)likelihood, maximized; in later topics it is usually a loss, minimized.

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L5 — Prob and Stats | W3 (Sep 7-11) | [04-probability.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/04-probability.pdf) | [04-probability-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/04-probability-note.pdf) |
| L6 — Prob and Stats (contd) | W3 (Sep 7-11) | [04-probability.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/04-probability.pdf) | [04-probability-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/04-probability-note.pdf) |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Both went live between Sep 6 and Sep 13, 2026; re-check anything else with `../scripts/check-slides.sh`.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [Data, Information and Knowledge — the differences (archived)](https://web.archive.org/web/20210107132902/http://www.infogineering.net/data-information-knowledge.htm) — *W3*
- [Correlation vs covariance (CrossValidated)](https://stats.stackexchange.com/questions/18082/how-would-you-explain-the-difference-between-correlation-and-covariance) — *W2*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Pattern Recognition and Machine Learning — Bishop
- The Elements of Statistical Learning — Hastie, Tibshirani & Friedman

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] Bayes' rule stated in prior / likelihood / posterior / evidence terms — and what each is in a concrete ML setting.
- [ ] MLE vs MAP: what changes, and when do they coincide?
- [ ] Multivariate Gaussian: what does the covariance matrix do to the shape of the level sets? (Feeds GMM.)
- [ ] Independence vs conditional independence vs uncorrelated — which implies which?

## Notes on this topic

The deck and the professor's annotated `04-probability-note.pdf` are both live as of Sep 13, 2026. The annotated notes fill in what the plain deck leaves blank — see below.

Andrew Moore's probability tutorial is listed in the schedule but the CMU page is dead (404), so it's omitted here.

### Deck outline

The professor's own outline, repeated on every section divider slide:

Probability Distributions → Joint and Conditional Probability Distributions → Bayes' Rule → Mean and Variance → Properties of Gaussian Distribution → Maximum Likelihood Estimation

### What the professor filled in live

Six slides in the plain deck are blank apart from their title — "Mean and average", "Variance and average", "Covariance", "Correlation" (slides 26-29), and two of the three "Prob vs Likelihood" slides. His annotated notes derive all of them; the keyword definitions above already reflect the standard versions, and here's specifically what he added:

- **Joint probability is on his "do not like" list.** His annotation on the dice/coin joint-count example literally reads "add joint probability to your DO NOT LIKE list" — he treats it as the thing that's easy to compute from counts but easy to misuse, and prefers reasoning through conditionals and the product/sum rules instead.
- **Mean vs average — they coincide only when the sample matches the pmf's weights.** Worked example: `X = [1, 2, 3]` with `p(X) = [1/6, 2/6, 3/6]` gives `E[g(X)] = sum p(x) g(x) = 14/6`, which is *not* the plain average `(1+2+3)/3 = 2`. But re-writing the sample as `X = [1, 2, 2, 3, 3, 3]` (each value repeated in proportion to its probability) makes the plain average equal `14/6` too — `avg(X) = E[g(X)]` only once the sample's empirical frequencies match the distribution's probabilities.
- **Variance and covariance, as data-matrix products.** For a centered data matrix `X̄` (each column mean-subtracted), `Var = (1/N) X̄ᵀ X̄` for a single feature and `Cov = (1/N) X̄ᵀ X̄` (a `d × d` matrix) for `d` features — variances on the diagonal, cross terms off it, always symmetric (`σ_hw = σ_wh`) with `-∞ < σ_hw < +∞`. This is the matrix form of the covariance-matrix definition above, worked through on a concrete two-column example (`h`, `w` with means `[2, 5]`).
- **Correlation is covariance after standardizing.** Standardize each centered column by its own std dev (`h* = h̄/σ_h`, `w* = w̄/σ_w`), then `COR = (1/N) X*ᵀ X*` — same construction as `Cov`, but every diagonal entry is forced to 1 and every off-diagonal entry lands in `[-1, 1]` (his worked example gets `corr(h, w) = 0.7`).
- **Uncorrelated but dependent — his own instance of the trap.** Let `X = Z` be a standard Gaussian, `Y = Z²` (chi-squared, clearly a deterministic function of `X`, hence maximally dependent), and `h = Z³`. He shows `cov(X, Y) = E[XY] - E[X]E[Y] = E[Z³] - E[Z]E[Z²] = 0 - 0 = 0`: zero covariance despite total dependence, because `Z³` is an odd function and averages to 0 for a symmetric-about-0 variable. His arrow diagram: `Independent ⇒ uncorrelated ⇒ linear independent` — one-directional, not reversible.
- **Probability vs. likelihood, worked with two Gaussians.** Fixed data `x^(1), ..., x^(n)`; two candidate parameter settings, `(a=2, b=1)` and `(a=1, b=1)`, are each plugged into the *same* fixed data to get a likelihood value `L(θ|X) = prod f(x^(i)|a,b)` — whichever `(a, b)` makes the observed data sit under the taller part of its density wins. This is the concrete version of "probability fixes θ and varies the data; likelihood fixes the data and varies θ."
- **The log trick, spelled out geometrically.** He justifies replacing "maximize `L`" with "maximize `log L`" two ways: `log(a·b) = log a + log b` turns the product into a sum, and taking a monotonic transform (log) of a concave objective doesn't move the maximizer — contrasted against `f(x) = x²` (convex, minimized at 0) vs `f(x) = -x²` (concave, maximized at 0) as a reminder of which direction the optimization goes.
- **Gaussian MLE closed form.** Solving `∂l(a,b|X)/∂a = 0` and `∂l(a,b|X)/∂b = 0` gives `a = (1/N) sum x^(i) = mu` and `b = (1/N) sum (x^(i) - mu)^2 = sigma^2` — MLE recovers the sample mean and the (biased, `/N` not `/(N-1)`) sample variance.
- **Bernoulli MLE, numeric.** For the sequence `H, H, H, T`, encoding `H -> 1`, `T -> 0` gives `theta_hat = (1+1+1+0)/4 = 3/4` — the worked instance of `theta_hat = (1/n) sum x^(i)` from the keyword definitions above.

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
