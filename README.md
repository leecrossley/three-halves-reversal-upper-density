# How rare is a reversal in the three-halves prime window?

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24410815.svg)](https://doi.org/10.5281/zenodo.24410815)

This result is now maintained in [prime-window-all-widths](https://github.com/leecrossley/prime-window-all-widths/tree/main/results/three-halves-reversal-upper-density). This repository is archived and keeps its releases and DOI.

At dilation $b=3/2$, a reversal is a scale $y$ where the weighted sum of primes between $y$ and $2.25y$ overshoots its predicted size. Assuming the Riemann hypothesis (RH), this repository shows that reversals are extraordinarily rare: in the long run they occupy less than $10^{-232}$ of the logarithmic scale.

The bound needs RH alone, with no independence assumption on the zeta zeros, and it rests on a finite calculation with the first 500 zeros. It limits how often reversals can happen without saying whether one ever does. Whether any reversal occurs under RH alone remains open here, and the bound gives no location for the first one.

## Statement

Assuming the Riemann hypothesis, the upper logarithmic density of reversals is less than $10^{-232}$.

Fix $b=3/2$. Give each ordinary prime $p$ weight $(\log p)W_b(p/y)$, where

$$
W_b(t)=\begin{cases}
 b(1-1/t)&1 < t\le b,\\
 b^2/t-1&b < t < b^2,\\
 0&\text{otherwise}.
\end{cases}
$$

Write $D_b(y)=b(b-1)y\log b-\sum_p(\log p)W_b(p/y)$. A reversal means $D_b(y)<0$. Its frequency up to $X>1$ is

$$
d(X)=\frac{1}{\log X}\int_1^X {\bf1}_{D_b(y)<0}\thinspace\frac{dy}{y}.
$$

All logarithms are natural.

## How the proof goes

1. Under RH the normalised deficit $D_b(y)/\sqrt y$ is $-\Delta$ plus a sum of non-negative terms $a_\tau[1+\cos(\tau\log(by))]$ over the zeta zeros, up to $o(1)$. Here the $a_\tau>0$ are explicit summable coefficients with sum $L$, and $\Delta=L-2\sqrt b(\sqrt b-1)^2$. [PROOF.md](PROOF.md) gives the formulas. At $b=3/2$, $0<\Delta<0.00163$.
2. For every $\varepsilon>0$, a reversal at sufficiently large $y$ therefore forces the terms from the first 500 zeros to add up to at most $\Delta+\varepsilon$, since the rest are non-negative. An exponential bound with $\lambda=150000$ turns this into $e^{\lambda(\Delta+\varepsilon)}$ times the time average of a product of 500 factors.
3. Each factor is bounded by a trigonometric polynomial of degree $500000$. Best and Trudgian's computation shows that the first 500 ordinates satisfy no nonzero integer relation with coefficients that small, so the average of the product is the product of the constant terms.
4. Each constant term is at most $e^{-u_j}I_0(u_j)$, a Bessel function value, where $u_j=\tfrac d2(1-e^{-2\lambda a_{\tau_j}/d})$ for the $j$-th positive ordinate $\tau_j$ and $d=500000$. Letting $\varepsilon\downarrow0$, the upper logarithmic density is at most $e^{\lambda\Delta}\prod_{j=1}^{500}e^{-u_j}I_0(u_j)$, and the programs certify that this bound is below $10^{-232}$.

The full argument is in [PROOF.md](PROOF.md).

## Verification

The first program encloses 500 zero ordinates and evaluates the scaled Bessel function in ball arithmetic. The second verifies a sign change of the completed zeta function in 500 disjoint intervals and checks the zero count above them. It computes $L$ from the original ramp and an enclosed positive tail. It bounds each scaled Bessel factor by its positive power series with a geometric remainder. Both programs use FLINT. Best and Trudgian's lattice computation is an input from the cited paper. [Best and Trudgian, Appendix A, Table 2](https://arxiv.org/pdf/1209.3843#page=13)

```sh
python -m pip install -r requirements.txt
python verify.py
python independent.py
```

[Recorded runs](evidence/check.txt), [checksums](SHA256SUMS)

## Prior work

Rubinstein and Sarnak developed the distribution theory of prime races. Fiorilli obtained races with biases arbitrarily close to one, and Zhao studied integrals of Mertens errors related to this weighted sum. An earlier calculation for this exact window gives arbitrarily late reversals under an additional independence hypothesis. The estimate here concerns the specific $3/2$ window under RH alone. The literature checked yielded no earlier value for this bound. [Rubinstein and Sarnak](https://www.math.uwaterloo.ca/~mrubinst/publications/Chebyshev.pdf), [Fiorilli](https://arxiv.org/abs/1210.6946), [Zhao](https://arxiv.org/html/2411.18903v2), [Earlier oscillation statement](https://github.com/leecrossley/prime-band-three-halves-oscillation/tree/v1.0.1)
