<!-- solve-problem:fda91485-d92b-4e75-a080-2c4bfee6c937 -->
# Fourier min-entropy–influence conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/fda91485-d92b-4e75-a080-2c4bfee6c937).

## What is the problem?

Let \(f:\{-1,1\}^n\to\{-1,1\}\) be a Boolean function with Fourier expansion \(f = \sum_{S\subseteq[n]}\widehat f(S)\chi_S\), where \(\chi_S(x)=\prod_{i\in S}x_i\) and \(\widehat f(S)=\mathbb{E}[f\chi_S]\). The **total influence** is \(\mathrm{Inf}(f)=\sum_{i=1}^n \mathrm{Inf}_i(f)\), with \(\mathrm{Inf}_i(f)=\Pr[f(x)\ne f(x^{\oplus i})]\); equivalently \(\mathrm{Inf}(f)=\sum_S |S|\widehat f(S)^2\). The **Fourier min-entropy** is \(-\log_2\max_S \widehat f(S)^2\).

**Conjecture (FMI):** There exists a universal constant \(C\) such that for every Boolean \(f\),
\[
-\log_2 \max_S \widehat f(S)^2 \;\le\; C\cdot \mathrm{Inf}(f).
\]
Equivalently, \(f\) has some coefficient with \(\widehat f(S)^2 \ge 2^{-C\,\mathrm{Inf}(f)}\). This is the min-entropy (single-coefficient) weakening of the Fourier Entropy–Influence (FEI) conjecture, which asserts \(\sum_S \widehat f(S)^2\log_2(1/\widehat f(S)^2)\le C'\,\mathrm{Inf}(f)\). Since min-entropy ≤ entropy, FEI implies FMI. Note the trivial direction: the max coefficient is at least \(2^{-H}\) where \(H\) is Fourier entropy, so FMI is strictly weaker.

## Why does it matters?

FMI says any low-influence function must have a "large" Fourier coefficient — spectral concentration of a strong, dimension-free form. This is exactly what weak-learning algorithms (e.g., the KM/low-degree algorithm in learning theory, Jackson's harmonic-sieve) need: a significant coefficient can be found by sampling. It is the natural first target toward the FEI conjecture, which is itself connected toBounds on formula complexity, seed elongation in pseudorandomness, and stability results in Boolean analysis. Its resolution would clarify the fundamental relationship between sensitivity structure and spectral structure of Boolean functions.

## What's already known?

- FMI holds for standard function families: characters, dictators, majority, tribes, read-once decision trees, symmetric functions — with modest constants.
- O'Donnell (2003?) conjectured FMI as a step toward FEI; the general case is open even for bounded-depth DNFs/CNFs (though there are partial results for restricted classes — verify current status for read-once DNFs and bounded-read branching programs).
- Mansour's conjecture (for DNFs) implies FMI for DNFs; it remains open in general.
- A 2025 paper (DOI: 10.1016/j.dam.2024.12.011, authors to be verified) establishes **lower bounds on the constant \(C\)**, i.e., constructions of functions forcing \(C\) to exceed some explicit value — showing FMI, if true, cannot hold with an arbitrarily small constant. It does not prove the inequality.
- Trivial general bound: \(\max_S\widehat f(S)^2 \ge 1/2^n\), useless since influence can be \(O(1)\) (e.g., tribes) while \(n\) grows.
- Hypercontractivity gives \(\max_S \widehat f(S)^2 \ge \mathrm{poly}(1/\mathrm{Inf})\)-type lower bounds, but these decay polynomially rather than exponentially in \(\mathrm{Inf}\) — hypercontractivity alone cannot give FMI.

## What would count as solving it?

- **Full solution:** A proof that \( -\log_2\max_S \widehat f(S)^2 \le C\,\mathrm{Inf}(f)\) for all Boolean \(f\) with an explicit universal \(C\).
- **Refutation:** An explicit family of functions with \(\mathrm{Inf}(f)=O(1)\) but \(\max_S\widehat f(S)^2\to 0\) (this would refute FMI and show FEI's min-entropy weakening is false).
- **Partial results a referee would value:** the inequality for broad classes (all DNFs, all bounded-depth circuits, symmetric noise-stable functions); or improved lower bounds on the optimal constant \(C^\*=\sup_f \frac{-\log_2\max_S\widehat f(S)^2}{\mathrm{Inf}(f)}\), narrowing the gap toward the conjectured \(O(1)\) value.

## How to start

1. Read O'Donnell's *Analysis of Boolean Functions* (2014), Chapter on the FEI conjecture and entropy-influence connections, to get the standard toolkit (hypercontractivity, randomness extraction from small spectra).
2. Study the 2025 lower-bound paper (DOI above) to understand which functions are extremal candidates — constants near the supremum typically come from tribes-like or recursive constructions; refuting/confirming these as extremal is the crux.
3. Try induction on noise-operator smoothing: apply \(T_\rho\) to reduce entropy, relate the smoothed max coefficient to the original via level-1 inequalities. Main obstacle: smoothing can destroy the max coefficient much faster than it reduces influence.
4. Restrict first to DNFs: attempt FMI via Mansour-style spectral arguments; success there is a publishable partial result.

## Key references

- Ryan O'Donnell, *Analysis of Boolean Functions*, Cambridge University Press, 2014. Comprehensive textbook; covers Fourier analysis, influence, hypercontractivity, and states FEI/FMI with surrounding context. https://dl.acm.org/doi/book/10.5555/2689462
- *A Lower Bound on the Constant in the Fourier Min-Entropy/Influence Conjecture*, Discrete Applied Mathematics, 2025, DOI: 10.1016/j.dam.2024.12.011. Constructs functions showing the universal constant \(C\) must be at least some explicit value (authors and exact bound: verify).
- Gopalan, Meka, Reingold, "DNF sparsification and a faster deterministic counting algorithm," Computational Complexity (2013). Mansour's conjecture-related spectral work for DNFs, the main known route to FMI for DNFs. (verify)
- Friedgut, Kalai, Naor (2002) and Kahn–Kalai–Linial (1988) results on Fourier concentration and influences; foundational inequalities any attack will build on. (verify exact statements needed)

## Warnings

- The census record's key work is a 2025 paper known only by DOI; authors and exact content should be verified before relying on it — I could not independently confirm details.
- Do not confuse FMI with FEI: FEI ⇒ FMI, but partial FEI results for restricted classes do not automatically transfer.
- The inequality is scale-sensitive: the constant \(C\) matters, and naive approaches (e.g., Parseval plus hypercontractivity) give only polynomial dependence on \(1/\mathrm{Inf}\), exponentially off.
- Extremal examples like tribes suggest \(\mathrm{Inf}\approx \ln 2\)-type regimes are where constants bite; test any proof against tribes and recursive AND-OR constructions.
- Beware the common error of assuming monotone or transitive-symmetric structure in the general statement — it must hold for *all* Boolean functions.

---
*`ALGO-000228` · unverified*

## Acceptance guidance

- **Full solution:** A proof that \( -\log_2\max_S \widehat f(S)^2 \le C\,\mathrm{Inf}(f)\) for all Boolean \(f\) with an explicit universal \(C\).
- **Refutation:** An explicit family of functions with \(\mathrm{Inf}(f)=O(1)\) but \(\max_S\widehat f(S)^2\to 0\) (this would refute FMI and show FEI's min-entropy weakening is false).
- **Partial results a referee would value:** the inequality for broad classes (all DNFs, all bounded-depth circuits, symmetric noise-stable functions); or improved lower bounds on the optimal constant \(C^\*=\sup_f \frac{-\log_2\max_S\widehat f(S)^2}{\mathrm{Inf}(f)}\), narrowing the gap toward the conjectured \(O(1)\) value.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/fda91485-d92b-4e75-a080-2c4bfee6c937?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000228.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000228)
