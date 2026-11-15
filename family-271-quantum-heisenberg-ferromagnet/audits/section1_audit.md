# Section 1 Audit: Spin Slots, Loops, and Pins (`01-loops.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation

### What This Section Does (Big Picture)

Section 1 is the **Rosetta Stone** of the entire paper. It translates the quantum spin problem into a classical probability problem. Specifically, it establishes three things:

1. **The slot decomposition:** Replace each spin-$S$ at site $x$ with $\ell = 2S$ spin-$\frac{1}{2}$ "slots" projected onto the symmetric subspace.
2. **The loop representation:** The thermal partition function $Z = \text{Tr}\, e^{-\beta H}$ becomes an expectation over random Poisson exchange pictures, weighted by $2^{c(\omega)}$ where $c(\omega)$ is the number of spacetime loops.
3. **Pin laws:** A family of re-weighted probability measures where loops touching "pinned" spacetime points lose their factor of 2, with controlled perturbation bounds.

Once this section is validated, the rest of the paper works purely in the probabilistic loop language.

---

### A1. The Slot Set and Symmetric Subspace (Lines 22–70)

**Physical setup:** Each site $x \in \Lambda$ with spin $S$ is replaced by $\ell = 2S$ distinguishable spin-$\frac{1}{2}$ particles (called "slots"). The full slot Hilbert space is:

$$\widehat{\mathcal{H}}_\Lambda = \bigotimes_{i \in V_\Lambda} \mathbb{C}^2, \qquad V_\Lambda = \Lambda \times \{1, \ldots, \ell\}$$

The physical spin operators are recovered by:

$$\widehat{S}_x^a = \sum_{j=1}^{\ell} s_{(x,j)}^a$$

restricted to the symmetric subspace $\text{Sym}^\ell(\mathbb{C}^2)$ at each site. The projector onto this subspace is:

$$\mathcal{S}_x = \frac{1}{\ell!} \sum_{\kappa \in \mathfrak{S}_\ell} \mathcal{U}_{\kappa, x}$$

> [!NOTE]
> **Physics meaning:** This is the standard Schwinger construction. A spin-$S$ irreducible representation of $SU(2)$ is isomorphic to $\text{Sym}^{2S}(\mathbb{C}^2)$ — the symmetric part of $2S$ copies of the fundamental (spin-1/2) representation. The projector $\mathcal{S}_x$ symmetrizes by averaging over all $\ell!$ permutations of the slots at site $x$.

**The critical identity** (Equation 2.4, Line 64):

$$\widehat{H}_\Lambda = -\frac{1}{2} \sum_{\{i,j\} \in \mathcal{E}_\Lambda} \mathcal{U}_{(ij)} + \frac{q_\Lambda}{4} I$$

This says the Heisenberg Hamiltonian in the slot picture is (up to a constant) just **minus one-half times the sum of all inter-site transpositions**. Each transposition $\mathcal{U}_{(ij)}$ swaps the quantum states of slots $i$ and $j$.

### A2. Proof of Lemma 2.1 — Line-by-Line Verification (Lines 72–109)

**Step 1 (Lines 73–89): Showing the spin matrices match.**

The symmetric basis vectors $\psi_k$ are normalized sums of all elementary tensors with exactly $k$ up-spins out of $\ell$ slots. Then:

$$\widehat{S}^z \psi_k = (k - \ell/2)\psi_k$$

Under $m = k - S = k - \ell/2$, this gives $\widehat{S}^z |m\rangle = m|m\rangle$. ✅

For $\widehat{S}^+$: each of the $\ell$ raising operators $s_j^+$ acts on an elementary tensor by flipping one down-spin to up. Among the $\binom{\ell}{k}$ basis tensors in $\psi_k$, each has $\ell - k$ down-spins available to flip. But many flips produce the same $k+1$-up tensor, so the counting is:

$$\widehat{S}^+ \psi_k = (k+1)\sqrt{\frac{\binom{\ell}{k+1}}{\binom{\ell}{k}}} \psi_{k+1} = \sqrt{(\ell-k)(k+1)}\, \psi_{k+1}$$

**Verification of the coefficient:** We need $\sqrt{(\ell - k)(k+1)} = \sqrt{S(S+1) - m(m+1)}$ under $m = k - S$, $\ell = 2S$.

$$S(S+1) - m(m+1) = S(S+1) - (k-S)(k-S+1) = S^2 + S - k^2 + 2kS - S^2 + k - S = 2kS + k - k^2$$

$$= k(2S + 1 - k) = k(\ell + 1 - k)$$

Wait — the paper gives $\sqrt{(\ell-k)(k+1)}$. Let me check: $(\ell - k)(k+1) = (2S - k)(k+1)$.

And $S(S+1) - m(m+1)$ with $m = k - S$:

$$= S^2 + S - (k-S)^2 - (k-S) = S^2 + S - k^2 + 2kS - S^2 - k + S = 2S + 2kS - k^2 - k$$

$$= (2S - k)(1 + k) = (\ell - k)(k+1) \quad \checkmark$$

✅ **The coefficient is correct.**

**Step 2 (Lines 91–99): Projector and commutativity.**

The claim that the symmetrizer $\mathcal{S}_x$ is self-adjoint, idempotent, and projects onto the symmetric subspace is standard representation theory.

The claim that $\widehat{H}_\Lambda$ and $\widehat{M}_\Lambda$ commute with within-site permutations: $\widehat{S}_x^a = \sum_j s_{(x,j)}^a$ is symmetric in the slot labels at site $x$, so conjugation by a within-site permutation just reorders the summands. ✅

**Step 3 (Lines 101–108): The transposition identity.**

For two spin-1/2 factors, the claim is:

$$\sum_{a=x,y,z} s_i^a s_j^a = \frac{1}{2}\mathcal{U}_{(ij)} - \frac{1}{4}I$$

**Direct verification:** In the standard basis $\{|\!\uparrow\uparrow\rangle, |\!\uparrow\downarrow\rangle, |\!\downarrow\uparrow\rangle, |\!\downarrow\downarrow\rangle\}$:

- $s^z \otimes s^z$ is diagonal: $\text{diag}(1/4, -1/4, -1/4, 1/4)$
- $s^x \otimes s^x + s^y \otimes s^y = \frac{1}{2}(s^+ \otimes s^- + s^- \otimes s^+)$, which gives $1/2$ on the off-diagonal $|\!\uparrow\downarrow\rangle \leftrightarrow |\!\downarrow\uparrow\rangle$ block.
- Total $\mathbf{s}_i \cdot \mathbf{s}_j = \text{diag}(1/4, -1/4, -1/4, 1/4) + \frac{1}{2}\begin{pmatrix} 0 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0\end{pmatrix}$

The swap operator $\mathcal{U}_{(ij)}$ has matrix $\text{diag}(1,0,0,1) + \text{off-diag}(|\!\uparrow\downarrow\rangle\leftrightarrow|\!\downarrow\uparrow\rangle)$, i.e., $\text{diag}(1,0,0,1)$ plus the same off-diagonal block with coefficient 1. So:

$$\frac{1}{2}\mathcal{U}_{(ij)} - \frac{1}{4}I = \frac{1}{2}\begin{pmatrix}1&0&0&0\\0&0&1&0\\0&1&0&0\\0&0&0&1\end{pmatrix} - \frac{1}{4}\begin{pmatrix}1&0&0&0\\0&1&0&0\\0&0&1&0\\0&0&0&1\end{pmatrix} = \begin{pmatrix}1/4&0&0&0\\0&-1/4&1/2&0\\0&1/2&-1/4&0\\0&0&0&1/4\end{pmatrix}$$

This matches $\mathbf{s}_i \cdot \mathbf{s}_j$ exactly. ✅

---

### A3. The Loop Representation (Proposition 2.2, Lines 111–208)

**The base exchange law $\mathbb{P}_{\text{b}}$:**

1. On each slot edge $\{i, j\} \in \mathcal{E}_\Lambda$, place an independent Poisson process of rate $1/2$ on time interval $[0, \beta)$.
2. At each Poisson mark, swap the two slot lines.
3. At time $\beta$, apply an independent uniform permutation of the $\ell$ slots at each site, then wrap time $\beta \to 0$.

Following slot lines through this spacetime picture creates closed **cycles**. The number of cycles is $c(\omega)$.

**Main claim (Equation 2.5):**

$$Z_\Lambda(\beta) = \text{Tr}\, e^{-\beta H_\Lambda} = e^{\beta q_\Lambda / 4}\, \mathbb{E}_{\text{b}}\, 2^{c(\omega)}$$

**Physics meaning:** The quantum partition function equals a classical expectation of $2^{c(\omega)}$ over random exchange pictures — each cycle carries a weight of 2 because it can independently be colored "up" or "down."

**Verification of the proof:**

**Step 1 (Lines 157–167):** The expected permutation operator factorizes:

$$\mathbb{E}_{\text{b}}\, \mathcal{U}_{\varphi_\beta} = \exp\left\{\frac{\beta}{2}\sum_{\{i,j\} \in \mathcal{E}_\Lambda}(\mathcal{U}_{(ij)} - I)\right\} = e^{-\beta q_\Lambda/4} e^{-\beta \widehat{H}_\Lambda}$$

This uses the matrix exponential for independent Poisson-driven transpositions. The generator of each edge's Poisson process is $\frac{1}{2}(\mathcal{U}_{(ij)} - I)$ (rate 1/2 jumps from $I$ to $\mathcal{U}_{(ij)}$). Since different edges act on different tensor factors, they commute, and the full generator is the sum. The resulting exponential is exactly $e^{-\beta q_\Lambda/4} e^{-\beta \widehat{H}_\Lambda}$ by Equation (2.4). ✅

**Step 2 (Lines 171–177):** Averaging independent endpoint permutations at each site gives the symmetrizer $\mathcal{S}_\Lambda$:

$$\mathbb{E}_{\text{b}}\, \mathcal{U}_{\pi_\omega} = e^{-\beta q_\Lambda / 4}\, \mathcal{S}_\Lambda\, e^{-\beta \widehat{H}_\Lambda}$$

This uses: (i) $\widehat{H}_\Lambda$ commutes with within-site permutations (proved in Lemma 2.1), so the endpoint symmetrizer can be pulled to the left; (ii) averaging uniform within-site permutations gives $\mathcal{S}_\Lambda$. ✅

**Step 3 (Lines 191–207):** Computing the trace over the elementary tensor basis $\eta \in \{-1, +1\}^{V_\Lambda}$:

The permutation operator $\mathcal{U}_{\pi_\omega}$ has diagonal entry 1 at $\eta$ if and only if $\eta$ is constant on every cycle of $\pi_\omega$ (because the permutation moves each factor to its image under $\pi_\omega$, and the matrix element is nonzero only if each slot's spin agrees with its image's spin — i.e., all slots in a cycle share the same spin). The eigenvalue of $\widehat{M}_\Lambda = \sum_i s_i^z$ on such an $\eta$ is $\frac{1}{2}\sum_C \varepsilon_C a_C$. ✅

The spectral law formula (Equation 2.6) follows immediately by tracing with $\Phi(M_\Lambda)$. ✅

---

### A4. Pin Laws (Lines 210–302)

**Definition:** For a pin set $D$ of spacetime points, cycles touching $D$ lose their weight-2 factor:

$$w_D(\omega) = 2^{n_D(\omega)}, \qquad n_D(\omega) = \#\{\text{cycles missing } D\}$$

**Physics meaning:** Pinning a cycle to "up" halves its weight (from 2 to 1). Cycles that avoid the pins retain their full weight. The pin law $\mathbb{P}_D$ re-weights the base measure accordingly.

**Dense boundary pins (Lemma 2.3, Lines 252–302):**

The continuous boundary pin set $D_0 = \partial\Lambda \times \{1,\ldots,\ell\} \times (\mathbb{R}/\beta\mathbb{Z})$ pins every boundary slot at every time. The lemma says this can be approximated by finite time grids $\mathcal{C}_n$:

- Almost surely, only finitely many cycles exist, each visiting the boundary for a positive-length time interval.
- A dense time grid eventually detects every such visit.
- So $w_{D_n}(\omega) \to w_D(\omega)$ and $\mathcal{B}_{D_n}(\omega) \to \mathcal{B}_D(\omega)$ eventually.
- Total-variation convergence of the pin laws follows by dominated convergence.

**Verification:** The key physical fact is that a cycle visiting a boundary site occupies it for a **positive-length time interval** (not just an instant), because (a) inter-site exchange marks are isolated Poisson points, so between consecutive marks a slot line stays at the same site for a positive duration, and (b) endpoint permutations preserve the site. Any positive-length visit to the boundary is detected by a dense time grid. This argument is correct. ✅

> [!NOTE]
> The monotonicity $w_{D_n} \downarrow w_D$ (Line 289) deserves a check: adding more pin times to the boundary can only *increase* the pin set, which can only *decrease* the number of cycles missing it, hence $n_{D_n} \le n_{D_{n-1}}$ eventually, giving $w_{D_n} \ge w_{D_{n+1}}$ eventually... 
>
> Actually wait — more pins means more cycles are "caught," so $n_{D_n}$ (cycles missing $D_n$) **decreases** as $n$ grows, meaning $w_{D_n} = 2^{n_{D_n}}$ **decreases**. The notation $w_{D_n} \downarrow w_D$ means decreasing to $w_D$. ✅

---

### A5. Factorial Domination (Lemma 2.4, Lines 304–398)

**Claim:** Under any pin law, ordered $n$-tuples of distinct exchange marks satisfy:

$$\mathbb{E}_D \sum_{(u_1,\ldots,u_n) \in (\omega_{\text{m}})^n_{\ne}} F(u_1,\ldots,u_n) \le 2^n \int F \prod_j \mu(du_j)$$

**Physics meaning:** Even though the pin law $\mathbb{P}_D$ distorts the Poisson process, the factorial moment measure of the marks is bounded by $2^n$ times the product measure. This is a "marks don't pile up too much under re-weighting" estimate.

**Verification of the proof:**

**Step 1: The insertion bound (Lines 334–349, Equation 2.11).**

Inserting a transposition at spacetime point $u$ into picture $\omega$:
- Cuts two directed strands and reconnects them with crossed outgoing portions
- If strands are on **different** cycles: two cycles merge into one → $c$ decreases by 1 → $n_D$ can decrease by at most 1
- If strands are on the **same** cycle: one cycle splits into two → $c$ increases by 1 → $n_D$ increases by at most 1

For the weight: each insertion can increase $n_D$ by at most 1 (in the splitting case, a cycle missing $D$ splits into two cycles both missing $D$), so $w_D$ can at most double per insertion:

$$w_D\!\left(\omega + \sum_{j=1}^n \delta_{u_j}\right) \le 2^n\, w_D(\omega)$$

**Is this tight?** The worst case is $n$ insertions all splitting $D$-avoiding cycles. Each split at most doubles the weight. So $2^n$ is correct. ✅

**Step 2: The Mecke formula (Lines 352–380).**

The Mecke formula for Poisson processes is a standard result: for a Poisson process with intensity $\mu$,

$$\mathbb{E}\left[\sum_{(u_1,\ldots,u_n) \in \omega^n_{\ne}} F(u_1,\ldots,u_n)\right] = \int F(u_1,\ldots,u_n) \prod_j \mu(du_j) \cdot \mathbb{E}[\text{rest}]$$

The paper derives this directly from the Poisson expansion (Lines 356–364). The factorial term $k!/(k-n)!$ counts the number of ways to choose the $n$ distinguished marks from $k$ total. After relabeling and resumming, the identity on Lines 366–376 follows. ✅

Combining with the insertion bound gives the final inequality. Division by $Z_D$ completes the proof. ✅

**Step 3: Mixed lists (Lines 383–392).**

The extension to mixed lists of actual marks and fresh (independent) Poisson marks: the actual marks contribute $2\mu$ each, the fresh marks contribute $\mu$ each. This follows from independence and the factorial domination on the actual marks. ✅

---

## Part B: Issue-by-Issue Audit

### Issue 1: Poisson rate 1/2 per slot edge (Line 113)

The base exchange law places rate-$1/2$ Poisson processes on each **slot edge** $\{i,j\} \in \mathcal{E}_\Lambda$. Each lattice edge $\{x,y\}$ generates $\ell^2$ slot edges (all pairs of slots from the two sites). So the total exchange rate across one lattice edge is $\ell^2 / 2 = 2S^2$.

From Equation (2.4): $\widehat{H}_\Lambda = -\frac{1}{2}\sum_{\{i,j\} \in \mathcal{E}_\Lambda} \mathcal{U}_{(ij)} + \frac{q_\Lambda}{4}I$, and the Poisson generator is $\frac{1}{2}\sum(\mathcal{U}_{(ij)} - I)$. The factor $-1/2$ in the Hamiltonian matches the rate $+1/2$ in the Poisson generator (with the sign flip from $e^{-\beta H}$). ✅

### Issue 2: Endpoint permutations and time-seam convention (Lines 114–130)

The convention: at time $\beta$, apply an independent uniform permutation at each site, then identify $\beta \equiv 0$. "Time 0 is understood just after the within-site endpoint permutations and the wrapping of time." This means the one-period slot permutation $\pi_\omega$ is the composition of the inter-site exchanges followed by the endpoint permutations. Cycles of $\pi_\omega$ correspond to cycles of the spacetime picture.

This convention is consistent with Equation (2.8): averaging the endpoint permutations gives the symmetrizer $\mathcal{S}_\Lambda$, which projects onto the physical Hilbert space. ✅

### Issue 3: Claim "$c(\omega) \le |V_\Lambda|$" (Line 123)

The number of cycles is at most the number of slots, since cycles partition the slots. Each slot belongs to exactly one cycle. ✅

### Issue 4: Equation (2.8) — operator ordering (Lines 173–177)

$$\mathbb{E}_{\text{b}}\, \mathcal{U}_{\pi_\omega} = e^{-\beta q_\Lambda/4}\, \mathcal{S}_\Lambda\, e^{-\beta \widehat{H}_\Lambda}$$

The operator ordering matters: $\mathcal{S}_\Lambda$ is on the left. Since $[\widehat{H}_\Lambda, \mathcal{S}_\Lambda] = 0$ (proved in Lemma 2.1), we actually have $\mathcal{S}_\Lambda e^{-\beta\widehat{H}_\Lambda} = e^{-\beta\widehat{H}_\Lambda} \mathcal{S}_\Lambda$, so the ordering doesn't matter. ✅

### Issue 5: Trace identity (Lines 183–189)

$$\text{Tr}_{\mathcal{H}_\Lambda}(e^{-\beta H_\Lambda}\Phi(M_\Lambda)) = e^{\beta q_\Lambda/4}\, \mathbb{E}_{\text{b}}\, \text{Tr}_{\widehat{\mathcal{H}}_\Lambda}(\mathcal{U}_{\pi_\omega} \Phi(\widehat{M}_\Lambda))$$

This uses: the trace over the physical Hilbert space $\mathcal{H}_\Lambda$ equals the trace over $\text{ran}(\mathcal{S}_\Lambda) \subset \widehat{\mathcal{H}}_\Lambda$ (since they are unitarily equivalent), and $\text{Tr}(\mathcal{S}_\Lambda A) = \text{Tr}_{\text{ran}(\mathcal{S}_\Lambda)}(A)$ when $A$ commutes with $\mathcal{S}_\Lambda$ (since $\mathcal{S}_\Lambda$ is a projector). ✅

### Issue 6: The "spin component letters" in the Hamiltonian (Lines 29–30)

> "In its inner sum the letters $a = x, y, z$ designate spin components."

This is a **notational collision**: $x$ and $y$ are used both as lattice sites and as spin-component labels. However, the context makes the meaning clear — in the outer sum $\{x, y\}$ is a pair of sites, while in the inner sum $a \in \{x, y, z\}$ labels spin directions. The paper inherits this standard (if slightly unfortunate) convention from physics tradition.

**Verdict:** This is not an error, but a **minor presentation issue** worth noting.

### Issue 7: Dominated convergence in Lemma 2.3 (Lines 289–301)

The dominating function for dominated convergence is $2^{|V_\Lambda|}$, which bounds $w_{D_n}$ uniformly. Since $|V_\Lambda|$ is fixed (finite volume), this is finite. The paper correctly notes on Lines 300–301 that "the dominating constant here depends on the fixed volume; no uniform-in-volume bound on the total loop weight is asserted." ✅

### Issue 8: Pin-insertion splitting analysis (Lines 339–342)

> "On splitting, it increases by at most one: a cycle missing $D$ gives two such cycles, while a cycle meeting $D$ has at least one descendant still meeting $D$."

**Careful check:** If a cycle $C$ with $C \cap D = \emptyset$ splits into $C_1, C_2$, both descendants avoid $D$ (since their union of strands equals $C$'s strands), so $n_D$ increases by exactly 1. If $C$ meets $D$, then at least one descendant must contain the strand that passes through the pin, so $n_D$ increases by at most 1 (the other descendant might miss $D$).

Wait — actually re-reading: "a cycle meeting $D$ has at least one descendant still meeting $D$." The pin is a spacetime point on a strand. After splitting, the strand containing that pin goes to exactly one of the two descendants. So one descendant meets $D$, and the other might not — meaning $n_D$ could increase by 1. But the paper says "increases by at most one" in total. ✅

For the joining case: two cycles merge. If both missed $D$, now one misses $D$ → $n_D$ decreases by 1. If one or both met $D$, the merged cycle meets $D$ → $n_D$ decreases by 0 or 1. So $n_D$ cannot increase. ✅

**Combining over $n$ insertions:** Each insertion changes $n_D$ by at most +1, so after $n$ insertions $n_D$ increases by at most $n$, giving $w_D \le 2^n w_D(\omega)$. ✅

---

## Part C: Summary of Section 1 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 1** |

All four results (Lemma 2.1, Proposition 2.2, Lemma 2.3, Lemma 2.4) are **correct**. The slot decomposition algebra, the loop partition function identity, the pin-law convergence, and the factorial domination bound all check out under careful verification.

> [!NOTE]
> **Key items verified and resolved:**
> - ✅ Slot decomposition algebra (tracked from Section 0, Item 2)
> - ✅ Cycle weight = 2 identity (tracked from Section 0, Item 3)
>
> **Items still to track:**
> 1. Lieb–Robinson / NOS2006 hypotheses → Section 7
> 2. Stable-polynomial pin test (Borcea–Brändén–Liggett) → Section 2
> 3. Exterior-moment determinant identity → Section 3
> 4. Nash inequality + flow construction → Sections 4–5
> 5. Induction closure $\varepsilon(p) = o(p)$ → Section 6
