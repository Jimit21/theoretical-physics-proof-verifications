# Section 3 Audit: Exposed Paths and a One-Particle Return Identity (`03-exposure.tex`)
## Family 271 — *Spontaneous magnetization in the quantum Heisenberg ferromagnet*

---

## Part A: Physics Translation (Colleague-Level)

### What This Section Achieves
In Section 2, the authors proved that the probability of $m$ interior spins avoiding the boundary pins is bounded by $(2r)^m$, where:
$$r = \frac{1}{m}\sum_{i \in T} \mathbb{P}_P(\text{next pin after } i \text{ belongs to } T)$$
To close the downward induction and establish spontaneous magnetization, one must prove $r \le p/2 \ll 1$.

However, in the full quantum loop soup:
- Cycles wind around each other and compete for Poisson exchange marks.
- Conditioning on pins introduces complicated, non-local many-body correlations.

**Section 3 solves this by an exact mathematical reduction:**
1. **Exposure conditioning (§3.1):** Reveal and freeze all cycles that miss $P = E \cup T$. On the remaining space, all cycles must hit $P$.
2. **Determinantal duality (§3.2):** Using an exterior-algebra / rank-one minor identity, the *first moment* of the next-pin arrival matrix under the multi-cycle conditioning matches the transition probabilities of a **single classical Markov random walk** with independent noise on each pass!
3. **Dirichlet energy dissipation (§3.3–§3.4):** The return fraction $r$ is bounded by the dissipation of Dirichlet energy of a test function $f$ under the one-period diffusion kernel $U$:
   $$m(1-r) \ge \mathbb{E}_P \langle f, (I-U)f \rangle$$
   This transforms the problem of bounding loop correlations into a classical kinetic / diffusion problem: if the initial mass on $T$ diffuses and dissipates energy, $r$ must be small.

---

## Part B: Step-by-Step Mathematical & Physical Audit

### B1. Exposure Disintegration (Proposition 4.1, Lines 27–184)

**The construction:**
- Labels on cycles avoiding $P$ are exposed along with their spacetime trajectories over one period $[0, \beta)$ and endpoint permutations.
- Unoccupied slots at time $t$ are called **holes** $H_t(\mathbf{a})$. All pins are holes at their designated times; boundary slots are holes throughout the period.
- The conditional law on the remaining picture, $\mathbb{Q}_{\mathbf{a}}$, places rate-$1/2$ Poisson exchanges on slot edges whose endpoints are both holes, transports holes when an exposed label jumps, and completes endpoints by uniform bijections on remaining slots.
- $G_P$ is the event that every remaining cycle meets $P$.

**Verification of the Poisson splitting (Lines 108–127):**
- Let $b$ be the number of slot edges. Two clocks $N_e^{(1)}, N_e^{(2)}$ per edge: $N_e^{(1)}$ accepted if at least one endpoint is an exposed label; $N_e^{(2)}$ accepted if neither is an exposed label.
- Total superposed rate is $b$. Next mark chooses an edge uniformly with probability $1/(2b)$ and is accepted with probability $1/2$. By Poisson thinning and splitting, this reproduces independent rate-$1/2$ Poisson processes on every edge.
- Independence of endpoint completions follows because each site’s permutation is conditioned only on the pre-completion positions of exposed labels at that site.

**The partition of unity (Equation 4.5, Lines 165–170):**
$$2^{n_P} = \sum_{A \subseteq V_\Lambda} \mathbf{1}_{F_A} 2^{c_A} \mathbf{1}_{G_P}$$
- For any picture, there is a unique set of initial labels $A$ whose cycles miss $P$.
- $c_A$ is the number of cycles formed by $A$, each carrying weight 2.
- The remaining cycles all meet $P$, each carrying weight 1 (since $\mathbf{1}_{G_P} = 1$).
- Thus $2^{n_P}$ matches the sum over $A$ on the right-hand side.
- Dividing by $Z_P = \mathbb{E}_{\mathrm{b}} 2^{n_P}$ gives the disintegration formula (Equation 4.4). ✅ **Valid.**

---

### B2. Exterior Powers & Determinantal Duality (Lemma 4.2 & Proposition 4.3, Lines 193–398)

This is the mathematical core of the reduction.

**Lemma 4.2 (Rank-one perturbation of exterior powers, Lines 209–278):**
Let $T_{ij}$ be the transposition swapping coordinates $i$ and $j$.
$$T_{ij} - I = -(e_i - e_j)(e_i - e_j)^*$$
*Check:*
- For $e_i$: $-(e_i - e_j)(e_i - e_j)^* e_i = -(e_i - e_j)(1) = e_j - e_i = (T_{ij} - I)e_i$.
- For $e_j$: $-(e_i - e_j)(e_i - e_j)^* e_j = -(e_i - e_j)(-1) = e_i - e_j = (T_{ij} - I)e_j$.
- For $e_k$ ($k \ne i, j$): $(e_i - e_j)^* e_k = 0 \implies (T_{ij} - I)e_k = 0$.

This shows $T_{ij} - I$ is strictly **rank one**.
Consequently, in the matrix $I + u(T_{ij} - I)$, any minor expanded by multilinearity in columns has at most one column from the rank-one perturbation (two or more columns chosen from a rank-one matrix yield determinant zero).
Therefore, every minor is strictly affine in $u$:
$$\bigwedge\nolimits^k ((1-u)I + u T_{ij}) = (1-u)\bigwedge\nolimits^k I + u \bigwedge\nolimits^k T_{ij}$$
By independence of successive factors:
$$\mathbb{E}\left[\bigwedge\nolimits^k \Pi\right] = \bigwedge\nolimits^k \mathbb{E}\Pi = \bigwedge\nolimits^k K$$
✅ **Remarkable and completely rigorous.**

**Proposition 4.3 (Conditional next-pin first moment, Lines 289–398):**
Let $V = J \sqcup Q$ with $J = P$. Let $\Pi$ be a permutation matrix on $V$ satisfying the exterior-moment identity, and let $G_J$ be the event that every cycle of $\Pi$ visits $J$.

Let $D = \begin{pmatrix} W & 0 \\ 0 & I_Q \end{pmatrix}$.
By minor expansion:
$$\mathbb{E}\det(I - D\Pi) = \det(I - DK)$$

- If $\Pi$ has a cycle contained entirely in $Q$, let $v$ be its indicator vector on $Q$ (extended by 0 on $J$). Then $\Pi v = v$, and $D\Pi v = I_Q \Pi_{QQ} v = v$, which means $(I - D\Pi)v = 0$. Hence $\det(I - D\Pi) = 0$!
- If $\Pi \in G_J$, then $\Pi_{QQ}$ has no cycles, so $\Pi_{QQ}$ is nilpotent.
  Applying Schur block elimination to $\begin{pmatrix} I - W\Pi_{JJ} & -W\Pi_{JQ} \\ -\Pi_{QJ} & I - \Pi_{QQ} \end{pmatrix}$:
  $$\det(I - D\Pi) = \det(I - \Pi_{QQ}) \det\left(I - W[\Pi_{JJ} + \Pi_{JQ}(I - \Pi_{QQ})^{-1}\Pi_{QJ}]\right)$$
  Since $\Pi_{QQ}$ is nilpotent, $\det(I - \Pi_{QQ}) = 1$.
  The term $\Sigma = \Pi_{JJ} + \Pi_{JQ}(I - \Pi_{QQ})^{-1}\Pi_{QJ}$ is precisely the **first-return / next-visit matrix to $J$**!

Therefore:
$$\mathbb{E}[\mathbf{1}_{G_J} \det(I - W\Sigma)] = \det \begin{pmatrix} I - WK_{JJ} & -WK_{JQ} \\ -K_{QJ} & I - K_{QQ} \end{pmatrix}$$
- Setting $W = 0$ immediately yields:
  $$\mathbb{P}(G_J) = \det(I - K_{QQ})$$
- Dividing by $\mathbb{P}(G_J)$ and applying the Schur complement to the block matrix gives:
  $$\mathbb{E}[\det(I - W\Sigma) \mid G_J] = \det(I - WH)$$
  where $H = K_{JJ} + K_{JQ}(I - K_{QQ})^{-1}K_{QJ}$.
- Taking the linear term in $W$ extracts the entrywise expectation:
  $$\mathbb{E}[\Sigma \mid G_J] = H$$
  where $H$ is the hitting distribution of a Markov chain with transition matrix $K$! ✅ **Watertight and elegant.**

---

### B3. Fresh Turns & Continuous Boundary Limit (Lemma 4.4, Lines 412–518)

- Approximates continuous boundary pinning $D_0$ by dense time grids $D_{0,n}$.
- Because Poisson jumps occur at isolated times, each boundary visit has strictly positive time duration.
- A dense set of cuts detects every boundary visit.
- Thus $\mathbf{1}_{G_n} \uparrow \mathbf{1}_{G_P}$ and $\mathbf{1}_{A_n} \downarrow \mathbf{1}_A$ almost surely.
- The conditional expectation under $\mathbb{P}_P$ matches the fresh-turn walk:
  $$\mathbb{P}_P(\text{next pin after } i \text{ lies in } T \mid \mathcal{H}) = \mathbb{P}_{\mathbf{a}}^{\text{walk}}(\tau_T^+ < \tau_E)$$
✅ **Verified.**

---

### B4. Minimal Hitting Function & Dirichlet Dissipation (Lemma 4.5, Lines 520–645)

**The setup:**
- Ignore pins in $E \setminus D_0$ (this only increases the probability of reaching $T$ before being killed).
- Let $U$ be the one-period transition matrix with boundary killing on $D_0$.
- $U$ is substochastic: $\|U v\|_2 \le \|v\|_2$.
- Define $f$ as the minimal solution to:
  $$f = 1 \text{ on } T, \qquad U^* f = f \text{ off } T$$
  Physically, $f(x)$ is the probability that a random walk starting at $x$ ever hits $T$ before hitting the boundary $D_0$.

**The quadratic form identity (Lines 616–623):**
$$\langle f, (I-U)f \rangle = \langle (I - U^*)f, f \rangle$$
- For $x \notin T$: $(I - U^*)f(x) = f(x) - (U^* f)(x) = 0$.
- For $x \in T$: $f(x) = 1$, so $((I - U^*)f)(x) = 1 - (U^* f)_x$.
Thus:
$$\langle f, (I-U)f \rangle = \sum_{i \in T} (1 - (U^* f)_i)$$

**The return fraction bound:**
Since ignoring $E \setminus D_0$ can only increase return probabilities:
$$q_i(\mathbf{a}) \le (U^* f)_i \implies 1 - q_i(\mathbf{a}) \ge 1 - (U^* f)_i$$
Summing over $i \in T$ and taking expectations under $\mathbb{P}_P$:
$$m(1-r) = \mathbb{E}_P \sum_{i \in T}(1 - q_i(\mathbf{a})) \ge \mathbb{E}_P \langle f, (I-U)f \rangle$$
Writing $f = \eta + g$ with $\eta = \mathbf{1}_T$ and $\langle \eta, g \rangle = 0$:
$$\mathbb{E}_P \langle f, (I-U)f \rangle \ge m(1 - \varepsilon) \implies r \le \varepsilon$$
✅ **Completely sound and rigorous.**

---

## Part C: Summary of Section 3 Findings

| # | Location | Severity | Finding |
|---|----------|----------|---------|
| — | — | — | **No mathematical errors or gaps found in Section 3** |

Every derivation in Section 3 is exact. The exterior-power minor identity, the Schur-complement hitting formula, the dense boundary limit, and the Dirichlet energy dissipation inequality hold without flaw.

> [!NOTE]
> **Tracked items status:**
> - ✅ Exterior-moment determinant identity (tracked from Section 0, Item 5) — **Verified and closed.**
>
> **Remaining items to track:**
> 1. Nash inequality + sparse geometry → Section 4
> 2. Decaying finite-energy flows → Section 5
> 3. Induction closure $\varepsilon(p) = o(p)$ → Section 6
> 4. Lieb–Robinson / NOS2006 hypotheses & KMS state construction → Section 7
