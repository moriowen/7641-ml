# Linear Algebra

> **Foundations** · L3, L4 · Week 2  
> **Quiz:** Q1 — L3, L4 · plus the Syllabus Quiz

## Keyword definitions

### Notation and matrix basics

- **`R` and `C`:** `R` denotes the real numbers, while `C` denotes the complex numbers.
- **"If and only if" (`iff`):** Both statements imply each other, so they are logically equivalent.
- **Scalar:** A single number, such as `3` or `-1.5`.
- **Vector:** An ordered list of numbers, usually written as a column. A vector in `R^d` has `d` real-valued entries.
- **Zero vector:** A vector whose entries are all zero.
- **Matrix:** A rectangular array of numbers. `A in R^{n x d}` means that `A` has `n` rows and `d` columns. ML/data-matrix convention: rows are data points/instances, columns are dimensions/features.
- **Entry:** One value in a vector or matrix. `A_ij` is the entry in row `i`, column `j` of `A`.
- **Dimension:** The number of components or features in a vector. In these notes, `d` usually denotes the number of features.
- **Instance (data point):** One observation in a dataset. In a data matrix, each of the `n` rows usually represents one instance.
- **Square matrix:** A matrix with the same number of rows and columns.
- **Tall matrix:** A matrix with more rows than columns, so `n > d`.
- **Wide matrix:** A matrix with more columns than rows, so `d > n`.
- **Transpose:** The matrix formed by swapping rows and columns. Its entries satisfy `(A^T)_ij = A_ji`.
- **Conjugate transpose:** The transpose of a complex matrix with every entry also replaced by its complex conjugate. It is written `A*` or `A^H`.
- **Symmetric matrix:** A square matrix that equals its transpose, so `A = A^T`.
- **Anti-symmetric (skew-symmetric) matrix:** A square matrix satisfying `A = -A^T`. Every diagonal entry must be zero.
- **Symmetric and anti-symmetric decomposition:** The identity `A = (A + A^T)/2 + (A - A^T)/2`, which writes any square matrix as the sum of a symmetric matrix and a skew-symmetric matrix.
- **Identity matrix:** A square matrix with `1` on the main diagonal and `0` elsewhere. It satisfies `AI = IA = A`.
- **Diagonal matrix:** A matrix whose off-diagonal entries are all zero.

### Norms and geometry

- **Norm:** A function that measures the size or length of a vector and satisfies non-negativity, definiteness, homogeneity, and the triangle inequality.
- **Non-negativity:** A norm cannot be negative: `||x|| >= 0`.
- **Definiteness:** `||x|| = 0` exactly when `x` is the zero vector.
- **Homogeneity:** Scaling a vector scales its norm by the absolute value of the scalar: `||tx|| = |t| ||x||`.
- **Triangle inequality:** The length of a sum cannot exceed the sum of the lengths: `||x + y|| <= ||x|| + ||y||`.
- **l1 norm (Manhattan norm):** The sum of the absolute values of a vector's entries: `||x||_1 = sum_i |x_i|`.
- **l2 norm (Euclidean norm):** The ordinary straight-line length of a vector: `||x||_2 = sqrt(sum_i x_i^2)`.
- **l-infinity norm (maximum norm):** The largest absolute entry in a vector: `||x||_inf = max_i |x_i|`.
- **lp norm:** The family `||x||_p = (sum_i |x_i|^p)^(1/p)` for `p >= 1`.
- **Frobenius norm:** The square root of the sum of the squared entries of a matrix: `||A||_F = sqrt(sum_i sum_j A_ij^2)`.
- **Orthogonal vectors:** Vectors whose dot product is zero. Nonzero orthogonal vectors meet at a 90-degree angle.
- **Unit vector:** A vector whose norm is `1`.
- **Orthonormal vectors:** Vectors that are mutually orthogonal and each have norm `1`.
- **Normalized vector:** A vector rescaled to have norm `1`, usually by dividing it by its original norm.
- **Orthogonal matrix:** A real square matrix with orthonormal columns, so `Q^TQ = QQ^T = I` and `Q^-1 = Q^T`.
- **Unitary matrix:** The complex-number analogue of an orthogonal matrix. It satisfies `U*U = UU* = I`, where `U*` is the conjugate transpose. For real matrices, this reduces to the orthogonal-matrix definition.
- **Projection:** The component of one vector in the direction of another. The scalar projection of `x` onto `y` is `x . (y/||y||)`; the vector projection is `((x . y)/(y . y))y`.

### Products, dependence, and rank

- **Matrix product:** For `A in R^{n x d}` and `B in R^{d x p}`, the product `AB` is an `n x p` matrix with entries `(AB)_ij = sum_k A_ik B_kj`.
- **Inner product (dot product):** A scalar computed as `x^T y = sum_i x_i y_i`. It measures how strongly two vectors point in the same direction after accounting for their lengths.
- **Outer product:** The matrix `xy^T`, whose `(i,j)` entry is `x_i y_j`.
- **Linear combination:** A weighted sum of vectors, such as `a_1x_1 + ... + a_kx_k`.
- **Basis:** A linearly independent set of vectors that spans a vector space. Every vector in that space has a unique representation in the basis.
- **Linearly dependent:** A set of vectors is dependent if at least one vector can be written as a linear combination of the others. Equivalently, some nonzero coefficients produce the zero vector.
- **Linearly independent:** A set of vectors is independent if the only linear combination equal to zero uses all zero coefficients.
- **Span:** The set of every vector obtainable as a linear combination of a given collection of vectors.
- **Column space:** The span of a matrix's columns.
- **Row space:** The span of a matrix's rows.
- **Null space:** The set of all vectors `x` satisfying `Ax = 0`.
- **Column rank:** The number of linearly independent columns in a matrix.
- **Row rank:** The number of linearly independent rows in a matrix. Row rank always equals column rank.
- **Rank:** The common row rank and column rank. It is the dimension of the column space or row space.
- **Full rank:** A matrix with the largest rank its shape permits: `rank(A) = min(n,d)`.
- **Rank-deficient matrix:** A matrix whose rank is less than `min(n,d)`.

### Inverses, trace, and determinant

- **Inverse:** For a square matrix `A`, the matrix `A^-1` satisfying `A^-1A = AA^-1 = I`.
- **Invertible (non-singular) matrix:** A square matrix that has an inverse.
- **Singular matrix:** A square matrix that has no inverse. Its determinant is zero, and it is not full rank.
- **Pseudo-inverse:** The Moore-Penrose inverse `A+`, which is defined for every matrix and acts as a best-fit replacement when an ordinary inverse does not exist. If `A` has full column rank, `A+ = (A^T A)^-1A^T`.
- **Trace:** The sum of a square matrix's diagonal entries: `tr(A) = sum_i A_ii`.
- **Cyclic property of trace:** Factors inside a trace may be cyclically rotated without changing the value, such as `tr(ABC) = tr(BCA) = tr(CAB)`, when the products are defined.
- **Determinant:** A scalar associated with a square matrix. Its magnitude gives the factor by which the matrix scales volume, and its sign records orientation.
- **Minor:** The determinant left after deleting one selected row and column from a matrix.
- **Cofactor:** The signed minor `(-1)^(i+j)M_ij` used in determinant expansion.
- **Cofactor expansion:** A way to compute a determinant by multiplying entries from one row or column by their cofactors and summing the results.

### Eigenvalues, covariance, and SVD

- **Eigenvector:** A nonzero vector `x` whose direction is unchanged by a square matrix `A`, meaning `Ax = lambda x`.
- **Eigenvalue:** The scalar `lambda` that tells how an eigenvector is scaled in `Ax = lambda x`.
- **Characteristic equation:** The equation `det(A - lambda I) = 0`; its solutions are the eigenvalues of `A`.
- **Characteristic polynomial:** The polynomial `det(A - lambda I)` in the variable `lambda`.
- **Eigenspace:** For an eigenvalue `lambda`, the set of all vectors satisfying `(A - lambda I)x = 0`. It includes the zero vector, although the zero vector is not itself an eigenvector.
- **Eigendecomposition:** A factorization `A = X Lambda X^-1`, where the columns of `X` are linearly independent eigenvectors and `Lambda` contains their eigenvalues on its diagonal. This form exists only when `A` is diagonalizable.
- **Diagonalizable matrix:** A square matrix with enough linearly independent eigenvectors to form a basis, allowing an eigendecomposition.
- **Positive semidefinite (PSD) matrix:** A symmetric matrix `A` for which `x^T A x >= 0` for every vector `x`. Equivalently, all of its eigenvalues are nonnegative.
- **Centered data matrix:** A data matrix produced by subtracting each feature's mean from that feature's values.
- **Covariance:** A measure of how two centered variables vary together. Positive covariance means they tend to move in the same direction; negative covariance means they tend to move in opposite directions.
- **Covariance matrix:** A square matrix containing the pairwise covariances of a dataset's features. With the convention used in these notes, `C = X_bar^T X_bar / n`.
- **Correlation:** A normalized version of covariance that measures the strength and direction of a linear relationship, usually on a scale from `-1` to `1`.
- **Singular value decomposition (SVD):** A factorization `A = U Sigma V^T` that exists for every real matrix.
- **Singular values:** The nonnegative diagonal entries of `Sigma`, conventionally arranged from largest to smallest. Their squares are the eigenvalues of `A^T A`.
- **Left singular vectors:** The columns of `U`. They are orthonormal eigenvectors of `AA^T`.
- **Right singular vectors:** The columns of `V`. They are orthonormal eigenvectors of `A^T A`.
- **Full SVD:** The form with square `U` and `V`, including complete orthonormal bases for both spaces.
- **Thin (reduced) SVD:** An exact, smaller form of the SVD that removes dimensions not needed by the shape of the original matrix.
- **Compact SVD:** An exact SVD that keeps only the singular vectors associated with nonzero singular values.
- **Truncated SVD:** An approximation that keeps only the largest `k` singular values and their singular vectors.
- **Principal component analysis (PCA):** A dimensionality-reduction method that projects centered data onto the eigenvectors of its covariance matrix with the largest eigenvalues.
- **Matrix calculus:** Rules for differentiating expressions involving vectors and matrices.
- **Kernel:** A function that measures similarity between two inputs and can often be interpreted as an inner product in another feature space. A valid kernel produces a positive semidefinite Gram matrix.
- **Gram matrix:** A matrix of pairwise inner products. For data points `x_1, ..., x_n`, its entries are `G_ij = x_i^T x_j`, or `G_ij = k(x_i,x_j)` when using a kernel.

## Slides & professor's annotated notes

| Lecture | Week | Deck | Professor's annotated notes |
|---|---|---|---|
| L3 — Linear Algebra | W2 (Aug 31-Sep 4) | [03-linear-algebra.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/03-linear-algebra.pdf) | **[03-linear-algebra-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/03-linear-algebra-note.pdf)** |
| L4 — Linear Algebra (contd) | W2 (Aug 31-Sep 4) | [03-linear-algebra.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/03-linear-algebra.pdf) | **[03-linear-algebra-note.pdf](https://mahdi-roozbahani.github.io/CS46417641-fall2026/course/max/03-linear-algebra-note.pdf)** |

The **annotated notes** are the professor's own in-lecture markup of the deck — that's the version to study from. Anything marked *not posted yet* 404s as of Sep 6, 2026; re-check with `../scripts/check-slides.sh`.

## Reading

No textbook is required for this course, but the professor strongly encourages the readings listed per class. Week tags show where each item appears on the schedule.

- [Linear Algebra Review — Zico Kolter (CS229)](http://cs229.stanford.edu/section/cs229-linalg.pdf) — *W2*
- [Correlation vs covariance (CrossValidated)](https://stats.stackexchange.com/questions/18082/how-would-you-explain-the-difference-between-correlation-and-covariance) — *W2*

Recommended books that cover this topic (from the course's optional book list — chapter choice is mine, not assigned):

- Pattern Recognition and Machine Learning — Bishop (appendix on linear algebra)
- The Elements of Statistical Learning — Hastie, Tibshirani & Friedman

## Prep questions

Answer these before lecture; they're the ones that tend to decide whether the lecture lands.

- [ ] Eigen-decomposition: what do eigenvectors of a covariance matrix mean geometrically? (This comes back in PCA.)
- [ ] Positive semi-definiteness — how do I check it, and why does it matter for covariance matrices and kernels?
- [ ] Matrix calculus: derivative of x'Ax and of ||Ax - b||^2 w.r.t. x. Needed for linear regression.
- [ ] Rank, null space, and when a linear system has no / one / infinitely many solutions.

## Notes on this topic

Both L3 and L4 use the **same deck and same annotated PDF** — the professor continues through it, so the notes file is cumulative. Re-download it after L4 rather than assuming the L3 copy is current.

Correlation vs covariance was assigned in Week 2 but is really probability material — cross-referenced in [Probability & Statistics](03-probability-and-statistics.md).

### Deck outline

The professor's own outline, repeated on every section divider slide:

Basics → Norms → Multiplications → Matrix Inversion → Trace & Determinant → Eigenvalues/Eigenvectors → SVD

Slide 4 also lists **Matrix Calculus**, but it is dropped from every later outline slide and from the summary slide. It is **not covered** in this deck. Two of the Prep questions above (matrix calculus, positive semi-definiteness / null space) are therefore not answered by these slides — they come from the Kolter CS229 review, not from lecture.

### 1. Basics and notation

Linear algebra compactly represents systems of linear equations: `4x1 - 5x2 = -13`, `-2x1 + 3x2 = 9` becomes `Ax = b` with `A = [[4,-5],[-2,3]]`, `b = [-13, 9]`.

- **Matrix** `A in R^{n x d}` — n rows, d columns. ML convention used throughout the course: **n = instances (data points), d = dimensions (features)**. Rows are data points `x^(i)`, columns are features `x_j`.
- **Vector** `x in R^d` — default a **column** vector (d rows, 1 column), though context can make it 1 x d. Scalar is `R^{1x1}`.
- **Transpose** `A^T in R^{d x n}`, elementwise `(A^T)_ij = A_ji`. Properties: `(A^T)^T = A`, `(AB)^T = B^T A^T`, `(A+B)^T = A^T + B^T`. Extension he uses later in the SVD derivation: `(ABC)^T = C^T B^T A^T`.
- **Symmetric**: `A = A^T`. **Anti-symmetric (skew)**: `A = -A^T`. Both require square.
- **Symmetric + anti-symmetric decomposition** — worked on the board (slide 7):
  `A = 1/2 (A + A^T) + 1/2 (A - A^T)`, with `H = A + A^T` satisfying `H = H^T`, and `G = A - A^T` satisfying `G = -G^T`.
- **Tall vs wide** (his annotation): `n >> d` is a *tall* matrix (many points, few features — the usual ML case); `d > n` is *wide*.

### 2. Norms

A norm is any function `f : R^d -> R` satisfying all four:

1. **Non-negativity** — `f(x) >= 0` for all x
2. **Definiteness** — `f(x) = 0` **iff** `x = 0`
3. **Homogeneity** — `f(tx) = |t| f(x)` for scalar t
4. **Triangle inequality** — `f(x+y) <= f(x) + f(y)`

Informally: the "length" of a vector.

| Norm | Formula | On `x = [1, 2, -3]` |
|---|---|---|
| l2 (Euclidean) | `‖x‖_2 = sqrt(sum_i x_i^2)` | `sqrt(14)` |
| l1 (Manhattan) | `‖x‖_1 = sum_i abs(x_i)` | 6 |
| l-inf (max) | `‖x‖_inf = max_i abs(x_i)` | 3 |
| l_p family | `‖x‖_p = (sum_i abs(x_i)^p)^(1/p)`, `p >= 1` | — |
| Frobenius (matrix) | `‖A‖_F = sqrt(sum_i sum_j A_ij^2) = sqrt(tr(A^T A))` | — |

`‖x‖_2^2 = sum x_i^2` (squared, no root) is the form that shows up in loss functions.

His annotations tie this straight to optimization — he wrote **"optimization = training"** — and sketched `f(x) = x^2` (smooth, `f'(x) = 2x = 0 => x = 0`) against `f(x) = |x|` (kink at 0, not differentiable there). That is the l2-vs-l1 regularization story arriving early; it returns in [Regularized Regression](12-regularized-regression.md).

### 3. Special matrices

- **Identity** `I in R^{d x d}` — 1s on the diagonal, 0s elsewhere.
- **Diagonal** `D = diag(d_1, ..., d_d)` — all *off-diagonal* elements are 0. He wrote out `D^T D = D^2 = diag(a^2, b^2, c^2)` and `D^-1 = diag(1/a, 1/b, 1/c)`.
- **Orthogonal vectors**: `x . y = 0`.
- **Orthonormal / unitary matrix** `U in R^{d x d}` — columns mutually orthogonal **and** each of unit norm. He wrote **"orthonormal = unitary"** explicitly.
  - `U^T U = I = U U^T`, therefore **`U^T = U^-1`**. This is his answer to the slide's own question "Is the inverse of a unitary matrix equal to its transpose?" — **yes**.
  - `‖Ux‖_2 = ‖x‖_2` — unitary transforms preserve length (rotation, no stretching).
  - `I` itself is unitary.

### 4. Multiplications

- **Matrix product**: `A in R^{n x d}`, `B in R^{d x p}` gives `C in R^{n x p}` with `C_ij = sum_{k=1..d} A_ik B_kj`. Inner dimensions must match.
- **Inner / dot product** — (1 x d)(d x 1) → a **scalar**, `sum_i x_i y_i`. Dot product **is** a linear operation (he wrote "Yes" on the slide).
- **Outer product** `x (x) y` — (d x 1)(1 x n) → an **n x d matrix**, entry (i,j) = `x_i y_j`.

> **Source conflict — slide 15 vs slide 16.** Slide 15's printed text labels `x y^T` the *inner* product and `x^T y` the *outer* product. That is swapped relative to standard convention, and swapped relative to slide 16, where he **hand-corrected** the outer product to `x (x) y = x y^T`. The slide-15 label was left uncorrected. Resolve by **shape, not label**: row x column = scalar = inner; column x row = matrix = outer. If a quiz question names the product, decide from the resulting dimensions.

- **Geometric form**: `x . y = ‖x‖ ‖y‖ cos(theta)`. Uses: testing orthogonality, computing the Euclidean norm (`x . x = ‖x‖_2^2`), and scalar projection. His annotation: the projection of x onto y is `x . (y / ‖y‖)`, i.e. dot with the *unit* vector `y_hat = y / ‖y‖`.

**Inner product properties** (three slides, all making the same claim): the inner product measures **correlation** between two vectors, scaled by their norms.

- `u . v > 0` → `theta < 90` → positively correlated / same general direction
- `u . v < 0` → `theta > 90` → negatively correlated
- `u . v = 0` → `theta = 90` → **orthogonal**

Slide 19 poses, and deliberately leaves unanswered: *"If two variables are uncorrelated they are orthogonal, and if two variables are orthogonal they are uncorrelated. Can I really say that?"* Left open on purpose — see Quiz prep below.

### 5. Linear independence and rank

- **Linearly dependent**: some vector is a linear combination of the others, `x_d = sum_{i=1..d-1} alpha_i x_i` for scalars `alpha_i`. Otherwise **linearly independent**.
- **Column rank**: size of the largest linearly independent subset of columns. **Row rank**: same for rows. They are always equal — that common value is *the* rank.
- **Full rank**: `rank = min{n, d}`, the maximum possible.

His worked examples:

- `A = [[1,2,3],[2,4,6]]` → `x2 = 2*x1`, `x3 = 3*x1`, so **rank 1**
- `B = [[1,0,2],[2,1,0],[3,2,1]]` → **full rank = 3**
- Identity → **rank d** (full)
- `X = [[1,4],[2,5],[3,6]]` (3 x 2) → rank 2 = `min{3,2}`, full rank. The *columns* satisfy `x2 = x1 + 3`, which is **not** a linear combination (adding a constant is not scaling), so they stay independent. The *rows* are dependent: `x^(2) = 1/2 x^(1) + 1/2 x^(3)`.

### 6. Matrix inverse

- **Inverse** of square `A in R^{d x d}`: the unique `A^-1` with `A^-1 A = I = A A^-1`.
- If `A^-1` does not exist, A is **singular / non-invertible**. **A is invertible iff A is full rank iff `|A| != 0`.**
- **Pseudo-inverse** for non-square `A in R^{n x d}`: `A+ = (A^T A)^-1 A^T in R^{d x n}`.
  - `A+ A = I` (d x d) — the left-inverse works
  - `A A+ != I` in general (n x n; he labelled it "= C") — the other side does not collapse to identity
  - His intuition on the board: `(A^T A)^-1 A^T` is roughly "`A^T` divided by `A^T A`". This is the normal-equations formula that returns in [Linear Regression](11-linear-regression.md).

### 7. Trace

`tr(A) = sum_{i=1..d} A_ii` — sum of the diagonal elements. Square matrices only.

- `tr(A) = tr(A^T)`
- `tr(A + B) = tr(A) + tr(B)`
- `tr(tA) = t * tr(A)`
- **Cyclic property**: `tr(ABC) = tr(BCA) = tr(CAB)` whenever the product is square. Cyclic rotation only — not arbitrary reordering.

Connects to norms (`‖A‖_F = sqrt(tr(A^T A))`) and to eigenvalues (`tr(A) = sum lambda_i`).

### 8. Determinant

`det(A) = sum_{j=1..d} (-1)^(i+j) a_ij M_ij` — cofactor expansion, where `M_ij` is the determinant of A with row i and column j deleted (the minor).

For 2 x 2 `A = [[a,b],[c,d]]`: **`|A| = ad - bc`**.

Properties:

- `|A| = |A^T|`
- `|AB| = |A| |B|`
- **`|A| = 0` iff A is not invertible**
- `|A^-1| = 1 / |A|`

**Geometric meaning** (from his sketch): the determinant is the signed volume of the parallelepiped spanned by the columns. If `x2 = alpha * x1` the columns are collinear, the parallelogram has zero area, so `det = 0`, so singular, so rank-deficient. Determinant, rank, and invertibility are one idea in three costumes.

### 9. Eigenvalues and eigenvectors

For square `A in R^{d x d}`, `lambda in C` is an **eigenvalue** and `x in C^d` an **eigenvector** if

```
Ax = lambda x,    x != 0
```

The `x != 0` is part of the definition — `x = 0` satisfies the equation trivially and is excluded.

Meaning: A acting on x returns the same direction, scaled by `lambda`. Geometrically, a change into a basis where A only stretches.

**How to compute:**

1. `Ax = lambda x` gives `(A - lambda I) x = 0` with `x != 0`
2. A nonzero solution exists only if `(A - lambda I)` is **singular**, i.e. **`|A - lambda I| = 0`** — the characteristic equation. His board argument: if `(A - lambda I)` were invertible, multiply both sides by its inverse to get `Ix = 0`, so `x = 0`, contradiction.
3. That determinant is a **degree-d polynomial** in `lambda`; its d roots are the d eigenvalues.
4. For each `lambda`, solve `(A - lambda I) x = 0` for the eigenvector.

**Worked example (slide 34).** `A = [[1,2],[3,-4]]`: `(1 - lambda)(-4 - lambda) - 6 = 0` gives `lambda_1 = -5`, `lambda_2 = 2`.

- `lambda_1 = -5`: `6x1 + 2x2 = 0` → `x = [1, -3]`, normalized `[-0.3162, 0.9487]`
- `lambda_2 = 2`: `-x1 + 2x2 = 0` → `x = [2, 1]`, normalized `[0.8944, 0.4472]`

Eigenvectors are determined only up to scale — `[1, -3]` and its normalized form are the same eigenvector.

**Eigendecomposition.** Stack the eigenvectors as **columns** of X and the eigenvalues on the diagonal of `Lambda`:

```
AX = X Lambda        and if X is invertible,  A = X Lambda X^-1
```

Convention: `lambda_1 >= lambda_2 >= ...`, descending.

**Properties:**

- `tr(A) = sum_i lambda_i`
- `|A| = prod_i lambda_i`
- **rank(A) = number of non-zero eigenvalues**
- If A is non-singular, the eigenvalues of `A^-1` are `1 / lambda_i`
- The eigenvalues of a **diagonal matrix are its diagonal entries**

**His three in-lecture questions and the answers he wrote (slide 36):**

- *Can a matrix have repeated eigenvalues?* — **Yes.** `I_{3x3}` has `lambda = 1, 1, 1`.
- *Are the eigenvectors of a matrix orthogonal to each other?* — **Not in general. YES if A is symmetric.** He crossed out the unconditional claim and wrote "If A is symmetric, then YES" across the slide.
- *Does linear independence imply orthogonality?* — **No.** `[[1,4],[2,5],[3,6]]` has independent columns that are not orthogonal; `[[1,0],[0,1]]` has both. Orthogonality implies independence, not the reverse.

### 10. Singular Value Decomposition

For a **centered** data matrix `X_bar in R^{n x d}` (n instances, d dimensions):

```
X_bar = U Sigma V^T
```

- `U in R^{n x n}` — unitary, `U U^T = I`. Left singular vectors.
- `Sigma in R^{n x d}` — diagonal, non-negative **singular values**, descending.
- `V in R^{d x d}` — unitary, `V V^T = I`. Right singular vectors.

Works for **any** matrix, square or not — unlike eigendecomposition. Truncated/thin form (his annotation): U is `n x k`, Sigma is `k x k`, `V^T` is `k x d`, keeping the top k singular values. He noted the numpy call: `np.linalg.svd(X)` returns `U, Sigma, V^T`.

**The SVD-to-covariance link (slides 39-40) — the punchline of the lecture.**

Covariance matrix `C = X_bar^T X_bar / n in R^{d x d}`. Substituting the SVD and using `(ABC)^T = C^T B^T A^T` and `U^T U = I`:

```
C = (V Sigma^T U^T)(U Sigma V^T) / n = V Sigma^2 V^T / n = V (Sigma^2 / n) V^T
```

Right-multiply by V and use `V^T V = I`:

```
CV = V (Sigma^2 / n)        compare with        AX = X Lambda
```

So **V holds the eigenvectors of the covariance matrix**, and

```
lambda_i = Sigma_i^2 / n
```

where `lambda_i` is an eigenvalue of C and `Sigma_i` a singular value of `X_bar`. The covariance eigenvalues come straight out of the SVD of X, without ever forming C. This is exactly the machinery behind [PCA](10-dimensionality-reduction-pca.md).

**Geometric meaning of SVD:** any linear map A decomposes into **rotate (`V^T`) → scale along axes (`Sigma`) → rotate (`U`)**. The unit circle becomes an ellipse with semi-axes `sigma_1 u_1`, `sigma_2 u_2`.


## My notes

### Before lecture


### During lecture


### After lecture — what I still don't get



## Quiz prep

- [ ] Re-read the professor's annotated notes
- [ ] Redo any worked example from the deck without looking
- [ ] Write my own one-paragraph summary of the topic

Things he flagged, asked, or deliberately left open in lecture — the likeliest quiz material:

- [ ] Write A as a sum of symmetric and anti-symmetric parts, and prove each half has the claimed property (he worked this on the board, slide 7)
- [ ] "If two variables are uncorrelated they are orthogonal, and vice versa — can I really say that?" (slide 19; he left it unanswered on purpose)
- [ ] Is the inverse of a unitary matrix equal to its transpose? (slide 12 — yes)
- [ ] Are the eigenvectors of a matrix orthogonal to each other? (slide 36 — only if A is symmetric)
- [ ] Does linear independence imply orthogonality? (slide 36 — no; the converse does hold)
- [ ] Can a matrix have repeated eigenvalues? (slide 36 — yes)
- [ ] Given `rank(A) = 0` or a rank-deficient A, state its eigenvalues, determinant, and invertibility
- [ ] Derive `lambda_i = Sigma_i^2 / n` starting from `X_bar = U Sigma V^T` (slides 39-40)
- [ ] Ranks of `[[1,2,3],[2,4,6]]`, `[[1,0,2],[2,1,0],[3,2,1]]`, and the identity (slide 24)
- [ ] Full eigenvalue/eigenvector computation for `[[1,2],[3,-4]]` (slide 34)
- [ ] Compute l1, l2, l-inf norms of a given vector, and the Frobenius norm of a matrix two ways


---

[Schedule](https://mahdi-roozbahani.github.io/CS46417641-fall2026/docs/course-info/course-schedule-mahdi/) · [All topics](README.md)
