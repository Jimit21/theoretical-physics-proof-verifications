# Section 4 Audit: Sparse Obstacles and Local Diffusion (`04-sparse-geometry.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation (Colleague-Level)

### What This Section Achieves
In Section 3, the return fraction was converted to Dirichlet dissipation:
$$m(1-r) \ge \mathbb{E}_P \langle f, (I-U)f \rangle$$
For the dissipation to be large ($\ge m(1-\varepsilon)$), mass initially localized on the test set $T$ must disperse across the lattice under the one-period quantum diffusion $U$.

**The physical obstacle:** The diffusion takes place only through the unexposed "holes." If all $2S$ slots at a site are occupied by exposed background cycles, that site is an impenetrable **obstacle** ($\mathcal{O}_t$). If obstacles were to cluster into a closed perimeter around a test point, the diffusing spin would be trapped in a finite cage, bouncing repeatedly back to $T$ ($r \approx 1$).

**Section 4 establishes that such cages do not exist:**
1. **Subcritical obstacle percolation (§4.1–§4.2):** Under the downward induction hypothesis $\mathsf{I}_p(P)$, the density of blocked sites is bounded by a small parameter $p \ll 1$. Using a multiscale **binary witness tree**, the authors prove that obstacle clusters have exponentially decaying tails:
   $$\mathbb{P}_P(z \in \mathcal{O}_t, \operatorname{rad}_z \mathcal{C}_t(z) \ge h) \le C \exp(-c h^\gamma)$$
2. **Regular Anchors (§4.3):** Around almost every test point $x \in T$ ("anchor"), the local neighborhood contains fewer than $2d$ obstacles in any radius-$M_*$ ball, and all distant obstacles have sublinear radii $\le (1 + |z-x|_\infty)^\nu$. The probability of anchor irregularity is bounded by:
   $$\delta = C R^d p^{2d} + C \exp(-c R^\xi)$$
3. **Local Nash Inequality (§4.4):** In dimension $d \ge 3$, removing fewer than $2d$ sites cannot disconnect the lattice (since each finite component would require at least $2d$ boundary exits along the coordinate axes). Transferring the Dirichlet form via Diaconis–Saloff-Coste path comparison yields the **Local Nash inequality**:
   $$\|v\|_2^{2 + 4/d} \le C \mathcal{D}_t(v) \|v\|_1^{4/d}$$
   This guarantees that localized wavepackets dissipate energy and disperse rapidly into the bulk.

---

## Part B: Step-by-Step Mathematical & Physical Audit

### B1. Sparse Scaling and Deterministic-Time Blocking (Lemma 5.1, Lines 16–142)

**Definitions:**
- Exponents: $\alpha = 1/100$, $\nu = 1/(100d)$, $a = 11/10$.
- Sparse set condition: $\#\{i \in A : x_i \in B_h(z)\} \le L(1+h)^\alpha$, with $L \ge \max\{2d, \ell, 4\}$.
- Scales: $s = p^{-11/10}$, $R = \lceil C_* s \rceil$, $\beta \ge 5s$, time grid $\mathcal{G}$ with gaps $\le p^{4d}$.
- Induction hypothesis $\mathsf{I}_p(P)$: $\mathbb{P}_P(A \subseteq \mathcal{B}_P) \le p^{|A|}$ for every sparse $A$ at a single grid time.

**Audit of Lemma 5.1 (Lines 90–142):**
- Let $t$ be an arbitrary deterministic time and $q$ the preceding grid time, so interval $I = (q, t]$ has length $|I| \le p^{4d}$.
- A site blocked at $t$ was either blocked at $q$ or experienced an inter-site Poisson exchange during $I$.
- By factorial domination (Lemma 2.4), the expected number of marks in a site’s edge star during $I$ is at most $2d \ell^2 |I| \le C p^{4d}$.
- For a small set of $|A| = 2d$ sites:
  $$\mathbb{P}_P(A \subseteq \mathcal{O}_t) \le p^{2d} + 2d \cdot C p^{4d} \le C_0 p^{2d}$$
- For a sparse set of $n$ sites: either $\ge \lceil n/2 \rceil$ sites were blocked at $q$ (probability $\le 2^n p^{\lceil n/2 \rceil}$), or $\ge \lceil n/2 \rceil$ sites had incident marks.
  By bipartite lattice parity, at least $k = \lceil n/4 \rceil$ sites of the same parity have marks. Since their edge stars are disjoint, the factorial bound gives $\le (C p^{4d})^k$.
  Since $4d \lceil n/4 \rceil \ge dn \ge n/2$, both terms are bounded by $(C_0 \sqrt{p})^n$. ✅ **Valid.**

---

### B2. Multiscale Binary Witness Trees & Component Tails (Lemma 5.2, Lines 144–261)

**Adjacency:** Two blocked sites are adjacent if $|u - v|_\infty \le 8$.
- Scale sequence: $h_j = 16 b^j$, with $b > 100$ chosen so that $b^\alpha > 4$.
- An admissible witness is an assignment of sites to the vertices of a rooted binary tree of depth $j$ such that at each scale $h_k$, the left and right child clusters satisfy:
  $$\operatorname{dist}_\infty(\mathcal{L}_{w0}, \mathcal{L}_{w1}) \ge h_k / 4$$
- *Sparsity of leaves check:* Any ball of diameter $< h_k/4$ meets at most one child branch at scale $h_k$, containing at most $2^{k-1}$ leaves. For $h_{k-1}/8 \le h < h_k/8$:
  $$L(1+h)^\alpha \ge L(2 b^{k-1})^\alpha \ge 2^{k-1}$$
  Thus the leaves of any admissible tree are guaranteed to be sparse!
- *Tree count overcounting bound:* $A_j \le (C_d h_j)^d A_{j-1}^2 \implies A_j \le C_b^{2^j}$.
- *Probability bound:* By Lemma 5.1, the probability that all $2^j$ leaves are blocked is $\le (C_0 \sqrt{p})^{2^j}$.
- Choosing $p_0$ small enough that $C_b C_0 \sqrt{p_0} \le e^{-2}$ gives:
  $$\mathbb{P}_P(z \in \mathcal{O}_t, \operatorname{rad}_z \mathcal{C}_t(z) \ge h_j) \le \exp(-2 \cdot 2^j)$$
  Interpolating for $h \ge 16$ gives the sub-exponential tail:
  $$\mathbb{P}_P(z \in \mathcal{O}_t, \operatorname{rad}_z \mathcal{C}_t(z) \ge h) \le C \exp(-c h^\gamma), \qquad \gamma = \log_b 2 > 0$$
✅ **Rigorous and uniform in $p \le p_0$.**

---

### B3. Regular Anchors (Definition 5.3 & Proposition 5.4, Lines 263–323)

An anchor $x \in \mathbb{Z}^d$ is regular at scale $R$ if:
1. Near: every $z \in B_{11R}(x)$ has $\#(\mathcal{O}_t \cap B_{M_*}(z)) < 2d$.
2. Far: every $z \in \mathcal{O}_t \setminus B_{10R}(x)$ has $\operatorname{rad}_z \mathcal{C}_t(z) \le (1 + |z-x|_\infty)^\nu$.

**Failure probability bound:**
- Number of centers in $B_{11R}(x)$ is $\le C R^d$. Failure of (1) is bounded by $C R^d p^{2d}$ via Lemma 5.1.
- Failure of (2) is a tail sum:
  $$\sum_{z : |z-x|_\infty > 10R} C \exp\left(-c (1+|z-x|_\infty)^{\nu \gamma}\right) \le C \exp(-c' R^{\nu \gamma})$$
- Setting $\xi = \nu \gamma > 0$ yields:
  $$\mathbb{P}_P(t \text{ not regular for } x) \le \delta := C R^d p^{2d} + C \exp(-c R^\xi)$$
✅ **Valid.**

---

### B4. Uniform Local Connectivity (Lemma 5.5, Lines 341–379)

**Theorem:** If $d \ge 2$, $K \ge 1$, and $F \subset \mathbb{Z}^d$ with $\#(F \cap B_\rho(u)) < 2d$, then any two unblocked sites $u, v \in B_K(u)$ can be connected by an unblocked path of length $\le (2\rho + 1)^d$ inside $B_\rho(u)$.

**Physics / Topology Verification:**
- Why can fewer than $2d$ deleted sites never disconnect $\mathbb{Z}^d$?
  Suppose $\mathbb{Z}^d \setminus F$ had a finite connected component $\mathcal{K}$.
  From any vertex in $\mathcal{K}$, moving along each of the $2d$ coordinate rays ($\pm e_1, \ldots, \pm e_d$) must eventually leave $\mathcal{K}$.
  The first point on each ray lying outside $\mathcal{K}$ must belong to the boundary of $\mathcal{K}$, which is contained in $F$.
  Because rays in distinct coordinate directions from a common origin are disjoint except at the origin, these $2d$ exit points are all distinct!
  Therefore, $|F| \ge 2d$, contradicting $|F| < 2d$.
  Hence $\mathbb{Z}^d \setminus F$ has **no finite components**.
- The complement of a bounding box for $F$ is connected for $d \ge 2$. Thus $\mathbb{Z}^d \setminus F$ is connected.
- Compactness / subsequence argument yields the uniform radius $\rho(d, K)$ and length bound. ✅ **Brilliant classical argument.**

---

### B5. Local Nash Inequality (Proposition 5.6, Lines 401–486)

**The setup:**
- Nonnegative function $v$ supported on available slots above $B_R(x)$.
- Energy: $\mathcal{D}_t(v) = \frac{1}{2}\sum_{\{i,j\} \in E(\mathcal{H}_t)} (v_i - v_j)^2$.

**Transfer to lattice function $w$:**
- For unblocked $z$, let $V(z) = \max_j v_{(z,j)}$.
- For blocked $z \in B_{R+3}(x)$, choose an unblocked nearest neighbor $\phi(z)$ (exists because $B_{M_*}(z)$ has $< 2d$ blocked sites).
- Set $w(z) = V(z)$ if unblocked, $V(\phi(z))$ if blocked in $B_{R+3}$, 0 outside.
- Norm comparison:
  $$\|v\|_2^2 \le \ell \|w\|_2^2, \qquad \|w\|_1 \le (2d+1)\|v\|_1$$
- Energy comparison via path lifting:
  Neighbors $z, z'$ lift to maximizing slots $u, u'$ with $|u - u'|_\infty \le 3$.
  Lemma 5.5 connects $u$ and $u'$ by an unblocked path of length $\le \text{const}$.
  By Cauchy–Schwarz on path differences:
  $$(w(z) - w(z'))^2 \le C \sum_{\text{path}} (v_i - v_j)^2 \implies \mathcal{E}_{\mathbb{Z}^d}(w) \le C \mathcal{D}_t(v)$$

**Proof of the standard Nash inequality on $\mathbb{Z}^d$ (Lines 459–483):**
- Block averaging operator $A_k w$:
  $$\|w - A_k w\|_2^2 \le C_d k^2 \mathcal{E}_{\mathbb{Z}^d}(w)$$
  $$\|A_k w\|_2^2 \le k^{-d} \|w\|_1^2$$
- Summing:
  $$\|w\|_2^2 \le C_d k^2 \mathcal{E}_{\mathbb{Z}^d}(w) + 2 k^{-d} \|w\|_1^2$$
- Optimizing $k = \lceil (4 \|w\|_1^2 / \|w\|_2^2)^{1/d} \rceil$ balances the two terms and yields:
  $$\|w\|_2^{2 + 4/d} \le C_d \mathcal{E}_{\mathbb{Z}^d}(w) \|w\|_1^{4/d}$$
- Combining with norm and energy transfers gives:
  $$\|v\|_2^{2 + 4/d} \le C \mathcal{D}_t(v) \|v\|_1^{4/d}$$
✅ **Complete, airtight, and textbook-perfect.**

---

## Part C: Summary of Section 4 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 4** |

All definitions, exponents, multiscale witness trees, component tails, connectivity theorems, and the local Nash inequality are mathematically rigorous and physically sound.

> [!NOTE]
> **Tracked items status:**
> - ✅ Nash inequality + sparse geometry (tracked from Section 0, Item 6) — **Verified and closed.**
>
> **Remaining items to track:**
> 1. Decaying finite-energy flows → Section 5
> 2. Induction closure $\varepsilon(p) = o(p)$ → Section 6
> 3. Lieb–Robinson / NOS2006 hypotheses & KMS state construction → Section 7
