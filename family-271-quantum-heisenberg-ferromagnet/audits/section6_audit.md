# Section 6 Audit: Heat-Flow Leakage and the Pin Bootstrap (`06-leakage.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation (Colleague-Level)

### What This Section Achieves
Section 6 is the **grand mathematical synthesis** of the paper. It combines:
1. The **Dirichlet dissipation principle** from Section 3 ($m(1-r) \ge \mathbb{E}_P \langle f, (I-U)f \rangle$),
2. The **local Nash inequality** from Section 4 ($\|v\|_2^{2+4/d} \le C \mathcal{D}(v)\|v\|_1^{4/d}$), and
3. The **decaying finite-energy flows** from Section 5 ($|\langle \mu, g \rangle| \le \sqrt{C m R^\alpha \mathcal{D}(g)}$),

to prove that over a time interval of duration $2s = 2p^{-11/10}$, the continuous-time quantum diffusion dissipates nearly all its initial kinetic energy:
$$\mathbb{E}_P \langle f, (I-U)f \rangle \ge m[1 - \varepsilon(p)]$$
with the critical scaling:
$$\varepsilon(p) = o(p) \quad \text{as } p \downarrow 0$$

Because $\varepsilon(p)$ vanishes faster than $p$, choosing $p$ sufficiently small guarantees:
$$2\varepsilon(p) \le p$$
Applying Proposition 2.1 (the simultaneous pin test from Section 2) yields:
$$\mathbb{P}_E(T \subseteq \mathcal{B}_E) \le (2r)^m \le (2\varepsilon(p))^m \le p^m = p^{|T|}$$
This **closes the downward induction** $\mathsf{I}_p(E)$!

**The physical triumph:** For a single interior slot $j$ at time zero, with only boundary pins $D_0$:
$$\mathbb{P}_{D_0}(j \in \mathcal{B}_{D_0}) \le p_* < \frac{1}{4}$$
That is, the probability that an interior spin avoids the boundary is strictly less than $1/4$. Consequently, with probability at least $3/4$, **interior spins belong to macroscopic exchange loops touching the boundary**, establishing long-range ferromagnetic order in the finite box!

---

## Part B: Step-by-Step Mathematical & Physical Audit

### B1. Two-Ended Propagation and Exact Loss (Lemma 7.1, Lines 84–221)

**Two-ended operator factorization:**
- Let $C_{2s}$ be initial forward propagation of duration $2s$, and $C_{2s}^{\rm rev}$ be the adjoint of the ending propagation of duration $2s$.
- Factoring $U = B M A$ with $A = C_{2s}$, $B^* = C_{2s}^{\rm rev}$, and $M$ the intervening contraction:
  $$\langle v, U v \rangle = \langle B^* v, M A v \rangle \le \|B^* v\|_2 \|A v\|_2 \le \frac{1}{2}\left( \|C_{2s} v\|_2^2 + \|C_{2s}^{\rm rev} v\|_2^2 \right)$$
- Subtracting from $\|v\|_2^2$ yields the two-ended loss bound:
  $$\langle v, (I-U)v \rangle \ge \frac{1}{2}\left( [\|v\|_2^2 - \|C_{2s} v\|_2^2] + [\|v\|_2^2 - \|C_{2s}^{\rm rev} v\|_2^2] \right)$$
✅ **Exact and standard.**

**The exact loss identity (Lines 205–218):**
Let $\mathcal{L}(u) = \|f\|_2^2 - \|C_u f\|_2^2$. With $f = \eta + g$, $\eta = \mathbf{1}_T$, $\langle \eta, g \rangle = 0$:
- Between jumps, the continuous Dirichlet generator gives $\frac{d}{du}\|g_u\|_2^2 = -2\mathcal{D}_{t(u)}(g_u)$.
- Instantaneous jumps and completions produce non-negative norm contractions $\Delta_g(v) \ge 0$.
- Integrating and expanding the square $\|\eta_u + g_u\|_2^2$:
  $$\mathcal{L}(u) \ge m - \|\eta_u\|_2^2 - 2\langle \eta_u, g_u \rangle + 2\int_0^u \mathcal{D}_{t(v)}(g_v) dv$$
✅ **Exact lower bound.**

---

### B2. Mass Localization via Mixed Factorial Domination (Lemma 7.2, Lines 224–300)

**The claim:** The localized mass $\zeta_u = \sum_{i \in T} \eta_{i,u}$ (killed upon exiting $B_R(x_i)$) satisfies:
$$\mathbb{E}_P \|\eta_u - \zeta_u\|_1 \le C m e^{-cs} \qquad (0 \le u \le 2s)$$
with $R = \lceil C_* s \rceil$.

**Audit of the proof:**
- A particle can escape $B_R(x_i)$ by time $u \le 2s$ only if it executes at least $R$ nearest-neighbor steps.
- Any sequence of $R$ steps uses $k$ actual Poisson marks and $R-k$ fresh marks.
- By mixed factorial domination (Lemma 2.4), the joint measure on ordered times $0 < t_1 < \cdots < t_R < u$ is bounded by $2^k (1/2)^{R-k} dt_1 \cdots dt_R = dt_1 \cdots dt_R$.
- The simplex volume is $u^R / R! \le (2s)^R / R!$.
- Number of choices of adjacent slot edges at each step is at most $2d\ell^2$.
- Summing over all combinations:
  $$\text{Expected escape paths} \le (2d\ell^2)^R \frac{(2s)^R}{R!} \le \frac{(2Ks)^R}{R!}, \qquad K = 3d\ell^2$$
- Since $R = \lceil C_* s \rceil$, Stirling's bound $R! \ge (R/e)^R$ gives:
  $$\frac{(2Ks)^R}{R!} \le \left(\frac{2eKs}{R}\right)^R \le \left(\frac{2eK}{C_*}\right)^R$$
- Choosing $C_* > 4eK$ makes the ratio $\le 1/2$, so the bound is $\le 2^{-R} \le e^{-cs}$.
- Summing over $m$ anchors gives $C m e^{-cs}$. ✅ **Watertight.**

---

### B3. Local Nash Decay During Regular Times (Lemma 7.3, Lines 332–395)

**The claim:** For $s \le u \le 2s$:
$$\mathbb{E}_P \|\eta_u\|_2^2 \le C m \left[ e^{-cs} + R^\alpha (s^{-d/2} + \delta) \right]$$

**Audit of the proof:**
- Let $q_i(u) = \|\eta_{i,u}\|_2^2$.
- At regular times, the local Nash inequality (Proposition 4.6) gives:
  $$q_i'(u) = -2\mathcal{D}_{t(u)}(\eta_{i,u}) \le -c q_i(u)^{1+2/d}$$
- Integrating:
  $$\frac{d}{du}\left( q_i(u)^{-2/d} \right) \ge \frac{2c}{d} > 0$$
- If the regular time in $[0, s]$ is at least $s/2$, then $q_i(s)^{-2/d} \ge \text{const} \cdot s \implies q_i(u) \le C s^{-d/2}$.
- By Proposition 4.4, the probability of nonregular time is $\delta = C R^d p^{2d} + C e^{-c R^\xi}$.
- The expected irregular time in $[0, s]$ is $\le s\delta$. By Markov's inequality, the probability that irregular time exceeds $s/2$ is at most $\frac{s\delta}{s/2} = 2\delta$.
- Thus $\mathbb{E}_P \|\eta_{i,u}\|_2^2 \le C(s^{-d/2} + \delta)$.
- For the full sum $\zeta_u$: at any site $z$, sparsity (Equation 6.1) limits the number of contributing anchors to $L(1+R)^\alpha \le C R^\alpha$.
- By Cauchy–Schwarz:
  $$\|\zeta_u\|_2^2 \le C R^\alpha \sum_{i \in T} q_i(u) \implies \mathbb{E}_P \|\zeta_u\|_2^2 \le C m R^\alpha(s^{-d/2} + \delta)$$
- Adding the localization error $2\|\eta_u - \zeta_u\|_1 \le C m e^{-cs}$ gives the asserted decay. ✅ **Rigorous and complete.**

---

### B4. Absorbing the Cross-Term via Weighted Young's Inequality (Proposition 7.4, Lines 403–507)

**The claim:** $\mathbb{E}_P \mathcal{L}(2s) \ge m [1 - \varepsilon(p)]$.

**Audit of the weighted integration:**
- Decompose $\eta_u = \mu_u + (\eta_u - \mu_u)$, where $\mu_u = \sum_{i \text{ regular}} \eta_{i,u}$.
- Discarded mass pairing: $\mathbb{E}_P \langle \eta_u - \mu_u, g_u \rangle \le C m (e^{-cs} + \delta)$.
- For regular anchors, Section 5 (Proposition 5.4) provides:
  $$|\langle \mu_u, g_u \rangle| \le \sqrt{A \mathcal{D}_{t(u)}(g_u)}, \qquad A = C m R^\alpha$$
- Now integrate over $u \in [s, 2s]$ with probability density $w(u) = \frac{2(2s-u)}{s^2}$.
- Cumulative tail weight: $W(u) = \int_u^{2s} w(v) dv = \frac{(2s-u)^2}{s^2}$.
- By Fubini / Tonelli:
  $$\int_s^{2s} w(u) \left( 2\int_0^u \mathcal{D}_v(g_v) dv \right) du \ge 2\int_s^{2s} W(u) \mathcal{D}_u(g_u) du$$
- Applying **weighted Young's inequality** at each instant $u$:
  $$2 w(u) \sqrt{A \mathcal{D}_u(g_u)} \le 2 W(u) \mathcal{D}_u(g_u) + \frac{A w(u)^2}{2 W(u)}$$
  The cross-term is completely absorbed by the positive dissipated energy $2 W(u) \mathcal{D}_u(g_u)$!
- **Evaluating the remainder integral (Lines 488–493):**
  $$\frac{w(u)^2}{W(u)} = \frac{\frac{4(2s-u)^2}{s^4}}{\frac{(2s-u)^2}{s^2}} = \frac{4}{s^2} \quad (\text{strictly constant on } [s, 2s)!)$$
  $$\int_s^{2s} \frac{w(u)^2}{W(u)} du = \frac{4}{s^2} \cdot s = \frac{4}{s}$$
  Thus the total remainder is:
  $$\int_s^{2s} \frac{A w(u)^2}{2 W(u)} du = \frac{2A}{s} = \frac{C m R^\alpha}{s}$$
- Collecting all error terms:
  $$\mathbb{E}_P \mathcal{L}(2s) \ge m \left[ 1 - C\left( e^{-cs} + R^\alpha(s^{-d/2} + \delta + s^{-1}) \right) \right]$$
✅ **Ingenious and mathematically exact.**

---

### B5. Exponent Calculations and Induction Closure (Theorem 7.5, Lines 509–613)

**Checking the exponents:**
Recall $s = p^{-a}$ with $a = 11/10 = 1.1$, $R \approx s = p^{-1.1}$, and $\alpha = 1/100 = 0.01$.

1. **Term $R^\alpha / s$:**
   $$p^{a(1-\alpha)} = p^{1.1 \times 0.99} = p^{1.089}$$
   Exponent is $1.089 > 1$. ✅
2. **Term $R^\alpha s^{-d/2}$:**
   For $d \ge 3$: $d/2 - \alpha \ge 1.5 - 0.01 = 1.49$.
   $$p^{a(d/2-\alpha)} \le p^{1.1 \times 1.49} = p^{1.639}$$
   Exponent is $1.639 > 1$. ✅
3. **Term $R^{\alpha+d} p^{2d}$ (from $\delta$):**
   For $d \ge 3$:
   $$2d - a(d+\alpha) \ge 6 - 1.1 \times (3 + 0.01) = 6 - 3.311 = 2.689$$
   Exponent is $2.689 > 1$. ✅
4. **Exponential terms $e^{-cs}$ and $e^{-c R^\xi}$:**
   Decay faster than any power of $p$.

**Conclusion:** Every single error term decays as $O(p^{1.089})$.
Therefore:
$$\varepsilon(p) = o(p) \quad \text{as } p \downarrow 0$$

Choosing $p_* > 0$ such that $2\varepsilon(p) \le p$ for all $p \le p_*$ yields:
$$\mathbb{P}_E(T \subseteq \mathcal{B}_E) \le (2r)^m \le (2\varepsilon(p))^m \le p^m$$
This closes the induction.

For a single slot $j$ at time zero with boundary pins $E = D_0$:
$$\mathbb{P}_{D_0}(j \in \mathcal{B}_{D_0}) \le p_* < \frac{1}{4}$$
✅ **The low-temperature loop percolation bound is proven!**

---

## Part C: Summary of Section 6 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 6** |

Every derivation, differential inequality, weighted Young integral, and exponent bound in Section 6 is completely rigorous and correct.

> [!NOTE]
> **Tracked items status:**
> - ✅ Induction closure with $\varepsilon(p) = o(p)$ (tracked from Section 0, Item 7) — **Verified and closed.**
>
> **Final remaining item to track:**
> 1. Lieb–Robinson / NOS2006 hypotheses & KMS state construction → Section 7
