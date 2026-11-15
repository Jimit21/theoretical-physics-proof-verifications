# Section 2 Audit: A Simultaneous Pin Test (`02-pin-test.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation

### What This Section Does (Big Picture)

Section 2 is the paper's **most original algebraic contribution**. It proves:

> **Proposition 3.1 (Simultaneous pin test):** If $T$ is a set of $m$ slot-time points and $E$ is an existing pin set, then
> $$\mathbb{P}_E(T \subseteq \mathcal{B}_E) \le (2r)^m$$
> where $r$ is the mean return fraction — the average probability (under the larger pin law $\mathbb{P}_P$, $P = E \cup T$) that a random line starting from a point in $T$ reaches $T$ again before reaching $E$.

**Physics meaning in plain English:** Suppose we pin all boundary slots (plus possibly some interior points) and ask: "What is the probability that $m$ prescribed interior slot-time points all belong to cycles that completely avoid the pins?" The answer is exponentially small in $m$, bounded by $(2r)^m$, where $r$ measures how "self-returning" the test set $T$ is within the exchange dynamics. If $r < 1/2$, this probability decays exponentially.

This is the linchpin that converts the percolation/ordering problem into a **random walk return-probability estimate** — a much more tractable analytic quantity.

### The Key Idea: Negative Dependence via Stable Polynomials

The proof strategy is:

1. **Encode** the exchange-picture permutation as a multiaffine polynomial $\prod_i(x_i + y_{\pi(i)})$
2. **Show** this polynomial is **stable** (no zeros when all variables have positive imaginary part)
3. **Splice out** non-pin points to get a generating polynomial for $\sigma(T)$ — the image of $T$ under the next-pin map
4. **Use stability** to prove **negative dependence**: the events "$j \in \sigma(T)$" for different $j$ are negatively correlated
5. **Conclude** that the probability of all of $T$ landing in $\sigma(T)$ is at most the product of marginals $\le r^m$
6. **Compare** the $\mathbb{P}_E$ and $\mathbb{P}_P$ laws, paying a factor $2^m$

---

## Part B: Line-by-Line Verification

### B1. Setup and the Next-Pin Map $\sigma$ (Lines 7–59)

**Definition (Lines 11–18):** For $i \in T$, follow the directed cycle from $i$ forward in time. The event $\mathcal{R}_i(E, T)$ occurs if the line returns to some point of $T$ before it reaches any point of $E$. The return fraction is:

$$r = \frac{1}{m}\sum_{i \in T} \mathbb{P}_P(\mathcal{R}_i(E, T))$$

**The key equivalence (Equation 3.3, Lines 37–44):**

$$\{T \subseteq \mathcal{B}_E\} = \{\sigma(T) = T\} = \{T \subseteq \sigma(T)\}$$

where $\sigma$ maps each pin to the next pin on its directed cycle.

**Verification:** If every cycle through $T$ avoids $E$, then following from any $t \in T$, the next pin encountered is in $T$ (since no $E$-pin is hit). So $\sigma(T) \subseteq T$. But $\sigma$ is a bijection on $P$, so $|\sigma(T)| = |T|$, forcing $\sigma(T) = T$. Conversely, $\sigma(T) = T$ means iterating $\sigma$ from any $t \in T$ stays in $T$ forever, so the cycle through $t$ never hits $E$. The last equality $\{\sigma(T) = T\} = \{T \subseteq \sigma(T)\}$ uses $|\sigma(T)| = |T| = m$: if $T \subseteq \sigma(T)$ and both have size $m$, they're equal. ✅

**Return-fraction identity (Equation 3.4, Lines 47–49):**

$$mr = \mathbb{E}_P|T \cap \sigma(T)| = \sum_{j \in T}\mathbb{P}_P(j \in \sigma(T))$$

This uses: $j \in \sigma(T)$ iff some $i \in T$ has $\sigma(i) = j$, i.e., the line from $i$ reaches $j$ (which is in $T$) before reaching $E$. Since $\sigma$ is a bijection, $|T \cap \sigma(T)| = \sum_{j \in T}\mathbf{1}_{j \in \sigma(T)}$. Taking $\mathbb{P}_P$-expectations gives $mr$, where $r$ is the average over $i \in T$ of the probability that $\sigma(i) \in T$, which is equivalent to $\mathcal{R}_i(E, T)$ occurring. ✅

---

### B2. Stable Polynomials — Closure Operations (Lemma 3.1, Lines 63–114)

**Definition (Lines 63–67):** A polynomial is **stable** if it has no zero in $\mathbb{H}^n$ (all variables in the open upper half-plane). It is **multiaffine** if degree $\le 1$ in each variable.

**Claimed closure properties:**
1. Coefficientwise limits with bounded degree → stable (unless zero)
2. Specialization of a variable to a real number → stable (or zero)
3. Partial differentiation → stable (or zero)
4. Identification of two variables → stable

**Verification of the proofs:**

**(1) Limits (Lines 80–90):** Uses Hurwitz's theorem / Rouché's theorem. If the limit $F$ vanished at some $\mathbf{z} \in \mathbb{H}^n$, restrict to a complex line through $\mathbf{z}$ where $F$ is not identically zero. On a small disk, $F_n \to F$ uniformly (polynomial convergence on compacts), and the argument principle forces $F_n$ to also have a zero nearby — contradicting stability of $F_n$. The existence of a non-trivial line direction follows from the Taylor expansion. ✅

**(2) Specialization (Lines 92–93):** Setting $z_k = a \in \mathbb{R}$ is the limit of $z_k = a + i/n$. By (1), the limit is stable unless zero. ✅

**(3) Differentiation (Lines 96–113):** Fix all variables except $t$ in $\mathbb{H}$. The resulting univariate polynomial has all roots in $\overline{\mathbb{H}^-}$ (closed lower half-plane), i.e., roots $\zeta_j$ with $\text{Im}\, \zeta_j \le 0$. The logarithmic derivative is:

$$\frac{\partial_t F}{F} = \sum_{j=1}^k \frac{1}{t - \zeta_j}$$

For $t \in \mathbb{H}$, each $t - \zeta_j$ has $\text{Im}(t - \zeta_j) > 0$, so $1/(t - \zeta_j)$ has $\text{Im} < 0$, hence the sum has $\text{Im} < 0$. Therefore $\partial_t F/F \ne 0$, so $\partial_t F(t) \ne 0$ for $t \in \mathbb{H}$. ✅

**(4) Identification (Line 94):** If $F(z_1, \ldots, z_n)$ is stable, then $F(z, z, z_3, \ldots, z_n)$ has no zero when $z, z_3, \ldots \in \mathbb{H}$. Trivially true from the definition. ✅

---

### B3. Partial Symmetrization (Lemma 3.2, Lines 123–161)

**Claim:** If $F$ is stable multiaffine and $\tau$ swaps two variables, then $(1-u)F + u\tau F$ is stable for $0 \le u \le 1$.

**Verification:** Fix all other variables in $\mathbb{H}$ and write the two-variable section as $q(z,w) = a + bz + cw + ezw$. Stability gives:

$$N(z) := \text{Im}\left((a + bz)\overline{(c + ez)}\right) \ge 0 \quad \text{for } z \in \mathbb{H}$$

(because if $c + ez \ne 0$, the root $w = -(a+bz)/(c+ez)$ must lie outside $\mathbb{H}$, so $\text{Im}(w) \le 0$, which means $N(z) \ge 0$).

The swapped polynomial satisfies $N^\tau(z) \ge 0$ similarly. For the mixture:

$$\text{Im}\left((a + b_u z)\overline{(c_u + ez)}\right) = (1-u)N(z) + uN^\tau(z) + u(1-u)|b-c|^2 \text{Im}\, z$$

**I need to verify this identity.** Let $b_u = (1-u)b + uc$ and $c_u = (1-u)c + ub$. Expand:

$(a + b_u z)\overline{(c_u + ez)} = a\bar{c}_u + a\bar{e}\bar{z} + b_u z \bar{c}_u + b_u z \bar{e}\bar{z}$

$(a + bz)\overline{(c + ez)} = a\bar{c} + a\bar{e}\bar{z} + bz\bar{c} + bz\bar{e}\bar{z}$

$(a + cz)\overline{(b + ez)} = a\bar{b} + a\bar{e}\bar{z} + cz\bar{b} + cz\bar{e}\bar{z}$

The mixture $(1-u) \cdot \text{first} + u \cdot \text{second}$:

The $a\bar{e}\bar{z}$ and $z\bar{e}\bar{z}$ terms: $(1-u)(a\bar{e}\bar{z} + bz\bar{e}\bar{z}) + u(a\bar{e}\bar{z} + cz\bar{e}\bar{z}) = a\bar{e}\bar{z} + b_u z\bar{e}\bar{z}$ ✅ (matches)

The remaining terms: $(1-u)(a\bar{c} + bz\bar{c}) + u(a\bar{b} + cz\bar{b}) = a\bar{c}_u + z((1-u)b\bar{c} + uc\bar{b})$

versus the target: $a\bar{c}_u + b_u z \bar{c}_u = a\bar{c}_u + z((1-u)b + uc)(\overline{(1-u)c + ub})$

Expand: $b_u \bar{c}_u = ((1-u)b + uc)(\overline{(1-u)c + ub}) = (1-u)^2 b\bar{c} + u^2 c\bar{b} + u(1-u)(b\bar{b} + c\bar{c})$

versus: $(1-u)b\bar{c} + uc\bar{b}$

The difference is: $(1-u)^2 b\bar{c} + u^2 c\bar{b} + u(1-u)(|b|^2 + |c|^2) - (1-u)b\bar{c} - uc\bar{b}$

$= -(1-u)u \cdot b\bar{c} - u(1-u)c\bar{b} + u(1-u)(|b|^2 + |c|^2)$

$= u(1-u)(|b|^2 + |c|^2 - b\bar{c} - c\bar{b}) = u(1-u)|b - c|^2$

So $\text{Im}((a + b_u z)\overline{(c_u + ez)}) = (1-u)N(z) + uN^\tau(z) + u(1-u)|b-c|^2 \cdot \text{Im}(z)$, where the last term comes from $z \cdot u(1-u)|b-c|^2$ contributing $u(1-u)|b-c|^2 \text{Im}(z)$ to the imaginary part.

For $z \in \mathbb{H}$, all three terms are $\ge 0$. ✅ **The identity checks out exactly.**

---

### B4. Exchange Symbols (Lemma 3.3, Lines 172–226)

**Claim:** For permutations built from independent Bernoulli transpositions, $\mathbb{E}[F_\pi(\mathbf{x}, \mathbf{y})]$ is stable.

**Verification:** The base case (identity permutation) gives $\prod_i(x_i + y_i)$ — a product of sums of distinct variables, each nonzero in $\mathbb{H}^{2|V|}$. ✅

Composing with a transposition $(j\,k)$ replaces $y_{\pi(j)} \leftrightarrow y_{\pi(k)}$, which is just swapping two $y$-variables. Averaging a Bernoulli transposition is then the partial symmetrization of Lemma 3.2. ✅

The Poisson-process approximation (Lines 197–206): approximate rate-$\lambda$ Poisson by thin Bernoulli slices (at most one mark per slice). The probability of disagreement is $O(\lambda^2 \delta) \to 0$. This is the standard Poisson-Bernoulli coupling. ✅

The uniform-permutation approximation (Lines 208–225): running Poisson transpositions on all pairs within a subset $A$ generates a continuous-time random walk on $\mathfrak{S}_A$ that converges to uniform (by irreducibility + positive entries after unit time + uniform is the invariant measure for random group multiplication). The convergence rate bound $1 - M\eta$ per step is crude but sufficient. ✅

---

### B5. Layered Symbol and Splicing (Lines 228–305)

**Construction (Lines 228–248):** Cut the time circle at every pin time. The interval permutations are independent, and their $x/y$ variable sets are disjoint across intervals. The product of their stable symbols is therefore stable (product of stable polynomials with disjoint variable sets is stable). ✅

**Splicing Lemma 3.4 (Lines 254–305):**

Eliminating a non-pin point $q$ by setting $x_q = y_q = t$ and taking the $t$-coefficient:

- If $q$ is not a fixed point: factors $(x_i + t)(t + y_j)$ have $t$-coefficient $x_i + y_j$, which splices the path $i \to q \to j$ into $i \to j$. ✅
- If $q$ is a fixed point: factor $(x_q + y_q) = 2t$, coefficient is $2$. This is the cycle-weight factor! ✅
- A cycle missing all pins eventually reduces to a single fixed point, contributing one factor of $2$.

So the result is $\mathbb{E}_{\text{b}}[2^{n_P(\pi)} \prod_{i \in P}(x_i + y_{\sigma(i)})]$. ✅

**The generating polynomial (Equation 3.8, Lines 263–274):**

Differentiating in $x_i$ for $i \in P \setminus T$ picks the $x_i$ factor from each such term. Setting all remaining $x$-variables (including those in $T$) to zero picks the $y_{\sigma(i)}$ factor from the $T$-indexed terms. This gives $\prod_{i \in T} y_{\sigma(i)}$ — the generating polynomial of the random subset $\sigma(T)$.

After dividing by $Z_P$, this is a stable multiaffine probability generating polynomial. ✅

---

### B6. Negative Dependence from Stability (Lemma 3.5, Lines 316–366)

**Claim:** If $G(\mathbf{y}) = \mathbb{E}\prod_{j \in A} y_j$ is stable, then $\Pr(J \subseteq A) \le \prod_{j \in J}\Pr(j \in A)$.

**Verification:** For two variables, write $G(z,w) = a + bz + cw + ezw$ with $a,b,c,e \ge 0$, $a+b+c+e = 1$. The stability condition with real coefficients gives:

$$0 \le \text{Im}((a + bz)\overline{(c + ez)}) = (bc - ae)\text{Im}\, z$$

For $z \in \mathbb{H}$, $\text{Im}\, z > 0$, so $bc \ge ae$. The covariance of the two presence indicators is:

$$\text{Cov}(X_1, X_2) = e - (b+e)(c+e)$$

where $\Pr(X_1 = 1, X_2 = 1) = e$, $\Pr(X_1 = 1) = b + e$, $\Pr(X_2 = 1) = c + e$.

$$e - (b+e)(c+e) = e - bc - be - ce - e^2 = e(1 - b - c - e) - bc = ea - bc \le 0$$

since $bc \ge ae$. ✅ **Negative covariance confirmed.**

The induction over elements of $J$ (Lines 354–365): condition on $j_1 \in A$, which gives a new stable generating polynomial (by differentiation + specialization). Then the conditional probability of $j_2 \in A$ given $j_1 \in A$ is $\le \Pr(j_2 \in A)$. Iterate. ✅

---

### B7. Main Proof of Proposition 3.1 (Lines 368–443)

**Step 1 — Finite pins (Lines 369–401):**

By Lemmas 3.4 and 3.5: $\mathbb{P}_P(T \subseteq \sigma(T)) \le \prod_{j \in T}\mathbb{P}_P(j \in \sigma(T))$.

By AM-GM: $\prod_{j \in T}\mathbb{P}_P(j \in \sigma(T)) \le \left(\frac{1}{m}\sum_j \mathbb{P}_P(j \in \sigma(T))\right)^m = r^m$. ✅

**Step 2 — Law comparison (Lines 385–401):**

Deleting the $m$ pins in $T$ from $P$ to get $E$: each cycle that met $T$ but missed $E$ becomes unpinned, contributing at most one extra factor of 2. At most $m$ such cycles, so $w_E \le 2^m w_P$. Also $w_P \le w_E$ trivially (more pins = fewer unpinned cycles). Hence:

$$\mathbb{P}_E(H) = \frac{\mathbb{E}_{\text{b}}[\mathbf{1}_H w_E]}{Z_E} \le \frac{2^m \mathbb{E}_{\text{b}}[\mathbf{1}_H w_P]}{Z_E} = \frac{2^m Z_P}{Z_E}\mathbb{P}_P(H) \le 2^m r^m$$

where $Z_E \ge Z_P$ (since $w_E \ge w_P$). ✅

**Step 3 — Dense-boundary limit (Lines 403–443):**

The passage from finite boundary cuts to continuous boundary pins uses the same dominated-convergence argument as Lemma 2.3. The crucial observation for the return test (Lines 421–436): a line starting from $i \in T$ either meets $F$ first (all tests fail), meets the boundary for a positive-duration visit first (detected by any sufficiently fine grid), or meets neither (all tests succeed). The convergence of $\mathbf{1}_{\mathcal{R}_i(E_n, T)} \to \mathbf{1}_{\mathcal{R}_i(E, T)}$ is pointwise a.s. ✅

The statement on Line 430 — "Since $T$ is disjoint from $D_0$, a boundary visit cannot first occur only at the return point" — is needed to ensure that the return to $T$ doesn't coincide with a boundary visit at the same instant. Since $T$ is a single-time set of interior slots and $D_0$ involves boundary slots, $T \cap D_0 = \emptyset$, so the return point in $T$ is not a boundary point. ✅

---

## Part C: Physics Interpretation and Significance

### Why This Result Matters for the Physics

The pin test converts a **many-body quantum correlation question** into a **single-particle random-walk question**:

- **Input:** "Are $m$ interior spins on cycles that avoid the magnetized boundary?" (a collective property of the loop ensemble)
- **Output:** Bounded by $(2r)^m$, where $r$ depends only on the first-return probability of a **single** random walk on the loop structure

This is a dramatic simplification. The negative-dependence result (from stable polynomials) is what makes it work: it says the events "spin $j$ avoids the boundary" for different $j$ are **negatively correlated** — knowing that one spin avoids the boundary makes it *less* likely that another does too. This is physically intuitive: cycles that avoid the boundary must thread through the interior, and they compete for the available spacetime paths.

### Connection to the Borcea–Brändén–Liggett Theory

The stable polynomial framework originates in:
- **Borcea & Brändén (2008–2009):** Classification of linear operators preserving stability
- **Borcea, Brändén & Liggett (2009):** "Negative dependence and the geometry of polynomials" — showed that strongly Rayleigh measures (whose generating polynomials are stable) satisfy the strongest negative dependence properties

The paper's application is novel: it applies the BBL theory not to a static combinatorial object (like a determinantal measure), but to the **dynamical exchange-path permutation** of the loop representation. The construction of the layered exchange symbol (product of interval symbols) and the splicing operation are original contributions.

---

## Part D: Summary of Section 2 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 2** |

All five lemmas and the main proposition are **correct**. The stable-polynomial machinery is applied rigorously, the splicing construction correctly reduces to the next-pin map, and the dense-boundary limit is handled properly.

> [!NOTE]
> **Items verified and resolved:**
> - ✅ Stable-polynomial pin test (Borcea–Brändén–Liggett) — tracked from Section 0, Item 4
>
> **Items still to track:**
> 1. Lieb–Robinson / NOS2006 hypotheses → Section 7
> 2. Exterior-moment determinant identity → Section 3
> 3. Nash inequality + flow construction → Sections 4–5
> 4. Induction closure $\varepsilon(p) = o(p)$ → Section 6
