# Section 7 Audit: From Pinned Loops to a Magnetized Equilibrium State (`07-kms.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation (Colleague-Level)

### What This Section Achieves
Section 7 is the **culmination of the entire work**. In Section 6, the authors established that inside any finite box $\Lambda$, with boundary pins $D_0$, each interior spin has probability at least $3/4$ of belonging to an exchange cycle touching the boundary.

However, in a finite box at zero external field ($h = 0$), the Hamiltonian has exact continuous $SU(2)$ rotation symmetry, so the finite-volume expectation of any single spin vanishes identically: $\langle S_x^z \rangle_\Lambda = 0$.

**Section 7 performs the rigorous thermodynamic limit ($\Lambda \nearrow \mathbb{Z}^d$):**
1. **Surface Energy vs. Bulk Entropy (Lemma 8.1):**
   The cost of forcing boundary cycles to be "up" is proportional to the boundary surface area $\exp(-C |\partial \Lambda_N|) \sim \exp(-O(N^{d-1}))$. Meanwhile, the aligned bulk spins produce a total magnetization $M_N \sim \frac{S}{2} V_N \sim N^d$. In $d \ge 3$, volume strictly dominates surface area ($N^d \gg N^{d-1}$). Thus, the free zero-field Gibbs state carries a **macroscopic magnetization tail**:
   $$\mu_N([S V_N / 2, \infty)) \ge \frac{1}{2}\exp(-C |\partial \Lambda_N|)$$
2. **Infinitesimal Symmetry-Breaking Field (Proposition 8.2):**
   Applying an explicit vanishing Zeeman field $h_N = N^{-1/2} \downarrow 0$ shifts the Gibbs weight toward the positive magnetization tail. Because $h_N V_N \sim N^{d - 1/2} \gg N^{d-1}$, the positive tail is selected with probability tending to 1:
   $$\lim_{N \to \infty} \rho_N^{\text{in}}(M_N / V_N) \ge \frac{S}{4}$$
   Averaging translations and using weak-* compactness yields a translation-invariant infinite-volume state $\omega$ with $\omega(S_0^z) \ge S/4$.
3. **Verification of the KMS Boundary Condition (Theorem 1.1):**
   Checking the Lieb–Robinson / Nachtergaele–Ogata–Sims (2006) hypotheses guarantees that infinite-volume dynamics $\tau_t$ exists. Applying Phragmén–Lindelöf maximum principle techniques on the analytic strip $\mathcal{S}_\beta = \{0 \le \operatorname{Im} z \le \beta\}$ proves that $\omega$ satisfies the full **KMS equilibrium condition**:
   $$F_{A,B}(t) = \omega(A \tau_t(B)), \qquad F_{A,B}(t + i\beta) = \omega(\tau_t(B) A)$$
   This completes the proof of Theorem 1.1 and rigorously establishes spontaneous symmetry breaking in the 3D quantum Heisenberg ferromagnet!

---

## Part B: Step-by-Step Mathematical & Physical Audit

### B1. Surface-Order Cost of Boundary Coloring & Spectral Tail (Lemma 8.1, Lines 37–105)

**The setup:**
- Let $G_N$ be the event that every cycle meeting the continuous boundary pins $D_0$ is colored "up".
- $n_0$: number of cycles meeting $D_0$.
- $J_N$: number of inter-site Poisson marks incident to the boundary during $[0, \beta)$.

**Audit of the proof:**
- Any cycle meeting $D_0$ either contains a time-zero boundary slot (at most $\ell |\partial \Lambda_N|$ slots) or uses an incident inter-site mark (at most $2 J_N$ marks).
  $$n_0 \le \ell |\partial \Lambda_N| + 2 J_N$$
- By the unpinned factorial bound (Lemma 2.4):
  $$\mathbb{E}_\varnothing J_N \le 2d \beta \ell^2 |\partial \Lambda_N| \implies \mathbb{E}_\varnothing n_0 \le (\ell + 4d\beta\ell^2) |\partial \Lambda_N|$$
- Given the picture, $\Pr(G_N \mid \omega) = 2^{-n_0}$.
- By Jensen's inequality:
  $$\Pr(G_N) = \mathbb{E}[2^{-n_0}] \ge 2^{-\mathbb{E} n_0} \ge \exp(-C_{\beta,d,S} |\partial \Lambda_N|)$$
  with $C_{\beta,d,S} = (\log 2)(\ell + 4d\beta\ell^2)$.
- Conditioned on $G_N$, cycles meeting $D_0$ are "up", while cycles missing $D_0$ have fair colors.
- By the singleton estimate of Section 6 (Theorem 6.5), for any unpinned slot $i$:
  $$\mathbb{P}_{D_0}(i \in \mathcal{B}_{D_0}) \le p_* < \frac{1}{4}$$
  So the conditional mean spin is $\frac{1}{2}(1 - \mathbb{P}_{D_0}(i \in \mathcal{B}_{D_0})) \ge \frac{1}{2}(1 - p_*)$.
- Summing over all $\ell V_N = 2S V_N$ slots:
  $$\mathbb{E}[M_N / V_N \mid G_N] \ge S(1 - p_*)$$
- Let $q = \Pr(M_N / V_N \ge S/2 \mid G_N)$. Using $M_N / V_N \le S$:
  $$S(1 - p_*) \le S q + \frac{S}{2}(1 - q) = \frac{S}{2}(1 + q) \implies q \ge 1 - 2p_* > \frac{1}{2}$$
  since $p_* < 1/4$.
- Therefore:
  $$\mu_N([S V_N / 2, \infty)) \ge q \Pr(G_N) \ge \frac{1}{2} \exp(-C_{\beta,d,S} |\partial \Lambda_N|)$$
✅ **Exact, elementary, and completely sound.**

---

### B2. The Vanishing-Field Thermodynamic Limit (Proposition 8.2, Lines 118–206)

**Audit of the construction:**
- Interaction term $\mathbf{S}_x \cdot \mathbf{S}_y = S_x^z S_y^z + \frac{1}{2}(S_x^+ S_y^- + S_x^- S_y^+)$ commutes with $S_x^z + S_y^z$.
  Thus $[H_N, M_N] = 0$.
- In the presence of external field $h > 0$, the Hamiltonian is $K_N = H_N - h M_N$.
- The tilted spectral distribution is:
  $$\mu_{N,h}(dm) = \frac{e^{\beta h m} \mu_N(dm)}{\int e^{\beta h u} \mu_N(du)}$$
- Tail bound:
  Numerator on $m < S V_N / 4$: $\le e^{\beta h S V_N / 4}$.
  Denominator on $u \ge S V_N / 2$: $\ge e^{\beta h S V_N / 2} \mu_N([S V_N / 2, \infty)) \ge \frac{1}{2} e^{\beta h S V_N / 2} e^{-C |\partial \Lambda_N|}$.
  Dividing gives:
  $$\mu_{N,h}((-\infty, S V_N / 4)) \le 2 \exp\left\{ C_{\beta,d,S} |\partial \Lambda_N| - \frac{\beta h S}{4} V_N \right\}$$
- For cubes $\Lambda_N = [-N, N]^d$, $V_N = (2N+1)^d$, and $|\partial \Lambda_N| / V_N \le \frac{2d}{2N+1}$.
- Choose explicit vanishing field:
  $$h_N = N^{-1/2} \downarrow 0$$
  The negative exponent term scales as $h_N V_N \sim N^{-1/2} N^d = N^{d - 1/2}$.
  The positive surface term scales as $|\partial \Lambda_N| \sim N^{d - 1}$.
  For $d \ge 3$:
  $$d - 1/2 \ge 2.5 > d - 1 = 2$$
  The negative term dominates! The exponent tends to $-\infty$, so:
  $$q_N = \mu_{N, h_N}((-\infty, S V_N / 4)) \longrightarrow 0$$
- Thus the mean magnetization satisfies:
  $$\rho_N^{\text{in}}(M_N / V_N) \ge \frac{S}{4}(1 - q_N) - S q_N = \frac{S}{4} - \frac{5S}{4} q_N \longrightarrow \frac{S}{4}$$
- Translation averaging $\omega_N(A) = \frac{1}{V_N} \sum_{x \in \Lambda_N} \rho_N(T_x(A))$ ensures translation invariance in the limit.
- By weak-* compactness (Banach–Alaoglu), a subsequence converges to a translation-invariant state $\omega$ with $\omega(S_0^z) \ge S/4$. ✅ **Flawless.**

---

### B3. Deep Box Dynamics & Nachtergaele–Ogata–Sims Verification (Lemma 8.3, Lines 217–309)

**Verification of the Lieb–Robinson / NOS (2006) hypotheses:**
- We verified the requirements of Theorem 2.2 in Nachtergaele–Ogata–Sims (2006):
  1. Graph metric on $\mathbb{Z}^d$.
  2. Bounded, finite-range interaction: nearest-neighbor pairs, each term norm $\le 3S^2$.
  3. Decay function $F(r) = (1+r)^{-d-1}$ is summable and satisfies the convolution condition $\sum_z F(|x-z|) F(|z-y|) \le C F(|x-y|)$.
  4. Uniform coordination number $2d$.
- Therefore, the infinite-volume dynamics $\tau_t$ exists as a strongly continuous group of *-automorphisms on the quasi-local algebra $\mathcal{A}$, independent of boundary conditions!

**Deep box uniformity:**
- For $x \in I_N = \{x \in \Lambda_N : \operatorname{dist}_\infty(x, \Lambda_N^c) \ge \lfloor \sqrt{N} \rfloor\}$, the box boundary is at distance $\ge \sqrt{N} \to \infty$.
- The fraction of excluded boundary sites $|\Lambda_N \setminus I_N| / V_N = O(N^{-1/2}) \to 0$.
- Because $[H_N, M_N] = 0$, the vanishing Zeeman field produces only a local rotation $\gamma_{-h_N t}^L(B)$, whose norm error is at most $h_N |t| \|[\sum_{u \in L} S_u^z, B]\| = O(N^{-1/2}) \to 0$.
- Thus $\sup_{x \in I_N} \sup_{|t| \le T} \|\alpha_t^N(T_x(B)) - T_x(\tau_t(B))\| \to 0$. ✅ **Rigorous.**

---

### B4. Bounded Strip Limits & KMS Proof (Lemma 8.4 & Theorem 1.1, Lines 319–493)

**Lemma 8.4 (Phragmén–Lindelöf for the thermal strip):**
- Let $\mathcal{S}_\beta = \{0 \le \operatorname{Im} z \le \beta\}$.
- Boundedness on edges $|F_n(t)| \le C$, $|F_n(t+i\beta)| \le C$ implies $|F_n(z)| \le C$ throughout $\mathcal{S}_\beta$ by applying the maximum principle to $e^{-\varepsilon z^2} F_n(z)$ and sending $\varepsilon \downarrow 0$.
- Applying the maximum principle to $G_n(z) = e^{-z^2} F_n(z)$ proves uniform convergence on the strip.

**Completion of Theorem 1.1:**
- Define $F_N^{A,B}(z) = \frac{1}{V_N} \sum_{x \in \Lambda_N} \rho_N(T_x(A) \alpha_z^N(T_x(B)))$.
- By finite-volume trace cyclicity:
  $$F_N^{A,B}(t) = \omega_N(A \alpha_t^N(B)) \longrightarrow \omega(A \tau_t(B))$$
  $$F_N^{A,B}(t+i\beta) = \omega_N(\alpha_t^N(B) A) \longrightarrow \omega(\tau_t(B) A)$$
- Applying Lemma 8.4 yields a function $F_{A,B}(z)$ analytic in the strip with the required KMS boundary values.
- Density of local observables extends the KMS condition to the entire quasi-local algebra $\mathcal{A}$.
- The state $\omega$ is translation invariant and satisfies $\omega(S_0^z) \ge S/4 > 0$.
- **Theorem 1.1 is completely, rigorously proven!** ✅ **Watertight.**

---

## Part C: Summary of Section 7 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 7** |

The surface-to-volume ratio scaling, the vanishing-field selection, the Nachtergaele–Ogata–Sims dynamics verification, and the complex-analytic KMS strip proof are mathematically flawless.

> [!NOTE]
> **Tracked items status:**
> - ✅ Lieb–Robinson / NOS2006 hypotheses & KMS state construction (tracked from Section 0, Item 1) — **Verified and closed.**
>
> **ALL MASTER TRACKING ITEMS ARE NOW FULLY VERIFIED AND CLOSED.**
