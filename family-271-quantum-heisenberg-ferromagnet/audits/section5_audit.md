# Section 5 Audit: Flows Around the Blocked Components (`05-flows.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation (Colleague-Level)

### What This Section Achieves
In Section 3, the Dirichlet dissipation lower bound for $f = \mathbf{1}_T + g$ required controlling the cross-term:
$$\langle \text{spread mass from } T, \, g \rangle$$
where $g = f - \mathbf{1}_T$ is the future-hitting probability (satisfying $g = 0$ on $T$ and on the boundary).

**The physical method:** The authors employ **Gauss's Divergence Theorem / Thomson's Principle** from classical electrostatics:
- If a mass distribution $\mu = \sum_{i \in I} \mu_i$ is represented as the divergence of a vector field (flow) $J$ ($\operatorname{div} J = \mu$), then by summation by parts:
  $$\langle \mu, g \rangle = \sum_{e = (u,v)} J(e) (g(u) - g(v))$$
- Applying the **Cauchy–Schwarz inequality**:
  $$|\langle \mu, g \rangle| \le \sqrt{\mathcal{E}(J)} \cdot \sqrt{2\mathcal{D}(g)}$$
  where $\mathcal{E}(J) = \sum_e J(e)^2$ is the **energy of the flow**, and $\mathcal{D}(g) = \frac{1}{2}\sum_e (g(u) - g(v))^2$ is the **Dirichlet kinetic energy**.

**The challenge and solution in Section 5:**
On a random landscape with obstacles $\mathcal{O}_t$, current cannot flow along straight lines. The authors construct an explicit, unblocked, divergence-free unit flow $J_a$ draining to infinity from every regular slot $a$ such that:
1. **Clearance & Topology (§5.1):** Blocked components are thickened by radius 4 and their finite interior pockets filled, creating laminar **hulls** $H_C$. The exterior boundary $S_C$ is proven connected via an elementary plaquette argument, providing guaranteed unblocked detour routes.
2. **Decay of Routed Flow (§5.2):** Starting from an explicit full-lattice orthant flow decaying like $(1+h)^{1-d}$, the edges are replaced by unblocked detour routes. The sublinear obstacle radius bound from Section 4 ($\operatorname{rad} \mathcal{C} \le (1+h)^\nu$) ensures that detour congestion at distance $h$ is at most $C(1+h)^{d\nu}$. The routed flow decays like:
   $$|J_a(e)| \le C (1 + \operatorname{dist}(e, y))^{-k}, \qquad k = d - 1 - d\nu$$
   In $d \ge 3$, $2k > d$, so the single-flow energy $\sum_e J_a(e)^2 < \infty$ is finite!
3. **Mutual Overlap & Total Energy (§5.3):** Due to the geometric sparsity of $T$, the mutual overlap of flows from different anchors $x_i, x_j \in T$ decays like $(1 + |x_i - x_j|)^{-(2k-d)}$ and is summable across the lattice. The total energy of a superposition of $m$ unit flows is bounded by:
   $$\mathcal{E}(J) \le C m R^\alpha$$
   yielding the fundamental Dirichlet pairing bound:
   $$\left|\left\langle \sum_{i \in I} \mu_i, g \right\rangle\right| \le \sqrt{C m R^\alpha \mathcal{D}(g)}$$

---

## Part B: Step-by-Step Mathematical & Physical Audit

### B1. Hull Topology and Clearance (Lemma 6.1, Lines 33–127)

**The construction:**
- For each blocked component $C$ (step size $\le 8$), let $A_C = \{z : \operatorname{dist}(z, C) \le 4\}$.
- $H_C = \mathbb{Z}^d \setminus U_C$, where $U_C$ is the unique infinite component of $\mathbb{Z}^d \setminus A_C$.
- Exterior vertex boundary: $S_C = \{v \notin H_C : \exists u \in H_C, |u-v|_1 = 1\}$.

**Audit of Lemma 6.1:**
- *Disjointness & Laminarity (Lines 82–98):* Because distinct components have separation $\ge 9$, their radius-4 thickenings $A_C$ are disjoint. If $A_{C'}$ lies in a finite pocket of $\mathbb{Z}^d \setminus A_C$, then $H_{C'} \subset H_C$. Otherwise, they lie in each other's infinite components, making $H_C \cap H_{C'} = \emptyset$. Thus, hulls are strictly laminar (nested or disjoint).
- *Clearance (Lines 70–73 & 116–120):* For any cut edge $\{u, v\}$ with $u \in H_C, v \notin H_C$:
  - $u \in A_C \implies \operatorname{dist}(u, C) = 4$ (if it were inside a pocket, $v$ could not belong to the infinite component).
  - $v \notin A_C$ and $|u-v|_1 = 1 \implies \operatorname{dist}(v, C) = 5$.
  - Both $u$ and $v$ have distance $\ge 4$ from $C$ and $\ge 4$ from all other components $C'$. Both are strictly unblocked!
- *Boundary Connectivity via Plaquettes (Lines 100–115):*
  Let $\mathcal{E}_C$ be the cut edges between $H_C$ and $U_C$. Every 2-dimensional lattice plaquette (elementary square) has boundary cycle length 4, so it intersects the cut an even number of times ($0, 2,$ or $4$).
  Modulo 2, any closed loop is a sum of plaquettes.
  If the cut had $\ge 2$ connected components, taking one edge from each and closing them via paths in $H_C$ and $U_C$ creates a closed loop intersecting each component once, giving an odd intersection number (1), which is impossible!
  Therefore, the cut edges are connected through plaquettes, meaning the outer endpoints $S_C$ are connected by steps of sup-norm $\le 1$.
  Interpolating coordinate changes one by one stays at distance $\ge 4$ from $C$ and $\ge 3$ from all other components, so all intermediate sites survive! ✅ **Flawless discrete topology.**

---

### B2. The Once-Only Rerouting Map (Lines 129–163)

- Keep only inclusion-maximal hulls $\mathfrak{H}$ (pairwise disjoint).
- Pick representative $r_H \in S_C$ for each $H \in \mathfrak{H}$.
- Define $\rho(z) = r_H$ if $z \in H$, and $z$ if $z \notin \bigcup H$.
- Edge rerouting $(u, v)$:
  - Both in same hull: empty path.
  - Neither in hull: edge itself.
  - One in hull ($u \in H$): boundary path $r_H \to v$.
  - Distinct hulls ($u \in H, v \in H'$): route is $r_H \to v \to u \to r_{H'}$. Both $u$ and $v$ are unblocked, and $v \to u$ traverses the edge in reverse!
  - Loop-erasing gives a simple path on unblocked sites. ✅ **Valid.**

---

### B3. Decaying Routed Unit Flow (Proposition 6.2, Lines 171–308)

**Base orthant flow $F_y$ on $\mathbb{Z}^d$ (Lines 243–261):**
At site $y+n$ with $n \in \mathbb{Z}_{\ge 0}^d$ and level $N = |n|_1$:
- Mass assigned: $a_N = \binom{N+d-1}{d-1}^{-1} = \frac{(d-1)! N!}{(N+d-1)!} \sim N^{1-d}$.
- Outgoing along coordinate direction $e_j$: fraction $\frac{n_j+1}{N+d}$.
- Conservation check:
  Incoming mass at level $N \ge 1$:
  $$\sum_{j : n_j \ge 1} a_{N-1} \frac{n_j}{N+d-1} = a_{N-1} \frac{\sum n_j}{N+d-1} = a_{N-1} \frac{N}{N+d-1} = a_N$$
  which matches outgoing mass! At level $0$, outgoing mass is $a_0 = 1$.
  Thus $\operatorname{div} F_y = \mathbf{1}_{\{y\}}$, and $|F_y(e)| \le C (1 + \operatorname{dist}(e, y))^{1-d}$.

**Rerouting and congestion bound (Lines 263–285):**
- By Section 4's remote regularity, any obstacle cluster at distance $b_C$ has diameter $\le 2(1+b_C)^\nu + 8$.
- Displacement of route of edge $e$ is at most $C(1 + \operatorname{dist}(e, y))^\nu$.
- If target edge $f$ is at distance $h = \operatorname{dist}(f, y)$, any original edge $e$ routed through $f$ has distance $t = \operatorname{dist}(e, y)$ satisfying $|h - t| \le C(1+t)^\nu + C \implies 1+t \asymp 1+h$.
- All such original edges $e$ lie within distance $C(1+h)^\nu$ of $f$.
- The number of such edges (congestion) is at most $C(1+h)^{d\nu}$.
- Multiplying the base flow by the congestion:
  $$|J_a^0(f)| \le C (1+h)^{1-d+d\nu} = C (1+h)^{-k}, \qquad k = d - 1 - d\nu$$
- For $\nu = 1/(100d)$, $d\nu = 1/100$, so $k = d - 1 - 0.01$.
- For $d \ge 3$: $2k = 2d - 2.02 \ge 6 - 2.02 = 3.98 > d = 3$.
  Thus the energy integral $\sum_h h^{d-1} h^{-2k} = \sum_h h^{d-1-2k} < \infty$ converges!
- Adding the short connector $Q_a$ gives $\operatorname{div} J_a = \mathbf{1}_{\{a\}}$. ✅ **Verified.**

---

### B4. Flow Overlap and Dirichlet Pairing Bound (Lemma 6.3 & Proposition 6.4, Lines 315–413)

**Lemma 6.3 (Overlap of two decaying flows):**
For two flows with decay $k \in (d/2, d)$:
$$\sum_e |J(e) J'(e)| \le C (1 + |y - y'|_\infty)^{-(2k-d)}$$
- *Proof:* In ball of radius $H/3$ around $y$: $|J'| \le C H^{-k}$, while $\sum_{\text{near } y} |J| \le C H^{d-k}$. Product is $C H^{d-2k}$.
- In dyadic annuli outside: $\sum_{j \ge 0} (2^j H)^{d-2k} \le C H^{d-2k}$ since $2k > d$. ✅ **Exact.**

**Proposition 6.4 (Energy of superposition of sparse flows):**
- Let $I \subseteq T$ be regular anchors, and $\mu_i$ a sub-probability mass supported in $B_R(x_i)$.
- Flow $J = \sum_{i \in I} \sum_a \mu_i(a) J_{i,a}$ has $\operatorname{div} J = \sum_{i \in I} \mu_i$.
- Overlap exponent:
  $$q = 2k - d = d - 2 - 2d\nu = d - 2 - 0.02 \ge 1 - 0.02 = 0.98$$
  Notice $q = 0.98 \gg \alpha = 0.01$!
- Summing mutual overlaps:
  $$\sum_e J(e)^2 \le C \sum_{i \in I} \left[ \#\{j \in I : |x_j - x_i|_\infty \le 4R\} + \sum_{j : |x_j - x_i|_\infty > 4R} (1 + |x_j - x_i|_\infty)^{-q} \right]$$
  - The first term is bounded by the sparsity condition: $\#\{j \in T : |x_j - x_i|_\infty \le 4R\} \le L(1+4R)^\alpha \le C R^\alpha$.
  - The second term is broken into dyadic annuli:
    $$\sum_{j \ge 0} \#\{j : |x_j - x_i|_\infty \in [2^j 4R, 2^{j+1} 4R)\} \cdot (2^j R)^{-q} \le C \sum_{j \ge 0} (2^j R)^\alpha (2^j R)^{-q} = C R^{\alpha - q} \sum_{j \ge 0} 2^{j(\alpha - q)} \le C$$
    because $q > \alpha$!
- Therefore:
  $$\sum_e J(e)^2 \le C |I| R^\alpha \le C m R^\alpha$$
- Green's identity summation by parts:
  $$\left\langle \sum_{i \in I} \mu_i, g \right\rangle = \sum_e J(e) (g(e^-) - g(e^+))$$
- Applying Cauchy–Schwarz gives:
  $$\left|\left\langle \sum_{i \in I} \mu_i, g \right\rangle\right| \le \left( \sum_e J(e)^2 \right)^{1/2} \left( \sum_e (g(e^-) - g(e^+))^2 \right)^{1/2} \le \left( C m R^\alpha \mathcal{D}(g) \right)^{1/2}$$
✅ **Complete, rigorous, and beautifully executed.**

---

## Part C: Summary of Section 5 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 5** |

All geometric rerouting constructions, clearance arguments, decay exponent calculations, dyadic overlap summations, and Cauchy–Schwarz Dirichlet pairing bounds are mathematically sound.

> [!NOTE]
> **Tracked items status:**
> - ✅ Decaying finite-energy flows (tracked from Section 0, Item 6) — **Verified and closed.**
>
> **Remaining items to track:**
> 1. Induction closure with $\varepsilon(p) = o(p)$ → Section 6
> 2. Lieb–Robinson / NOS2006 hypotheses & KMS state construction → Section 7
