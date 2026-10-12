> **Review 01 reconciliation:** The earlier informal monotonicity proof in section 3 is **superseded** by the explicit derivative and bracket-sign proof in [06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md](06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md). Polynomial coefficients should be called c2, c1 and c0; the symbol a is reserved for dimensionless area. The benchmark identities below remain candidate analytical references, not executed numerical evidence.

# 03 - Binary Cross-Flow Closure Audit and Analytical Benchmarks

## Status
MAIN RESEARCH MATHEMATICAL CHECK - independent review pending. This document audits the candidate cross-flow closure under the exact idealised model assumptions, without promoting literature inputs or claiming experimental validation.

## 1. Assumptions
Binary CO2/N2, isothermal, steady, ideal-gas contacting phases, positive constant permeances Pi_C and Pi_N, constant P_f>P_p>=0, locally withdrawn cross-flow permeate without axial mixing. No pressure drop, sweep gas or membrane-side reactions.

Define x=retentate CO2 mole fraction, y=local permeate CO2 mole fraction, r=P_p/P_f, alpha=Pi_C/Pi_N>0. The physically useful parameter domain is 0<x<1, 0<=r<1, alpha>0.

## 2. Closure derivation
Component fluxes:
J_C=Pi_C P_f(x-r y).
J_N=Pi_N P_f[(1-x)-r(1-y)].

For local cross-flow withdrawal:
y=J_C/(J_C+J_N).

Therefore:
y/(1-y)=alpha (x-r y)/[(1-x)-r(1-y)].

Cross multiplication:
y[(1-x)-r+r y]=alpha(1-y)(x-r y).

Expanding:
r(1-alpha)y^2 + [1-x-r+alpha(x+r)]y - alpha x = 0.

Define:
a=r(1-alpha),
b=1-x-r+alpha(x+r),
c=-alpha x.

The equation is a y^2+b y+c=0. Avoid numerically unstable quadratic roots where alpha or r is close to a degenerate limit; a bracketed scalar root finder is a safe general approach.

## 3. Existence and admissibility for P_f>P_p
Let total local flux J_T(y)=J_C(y)+J_N(y).

At y=0:
J_C=Pi_C P_f x>0.
At y=1:
J_N=Pi_N P_f(1-x)>0.

Define h(y)=J_C(y)-y J_T(y).

Then h(0)=Pi_C P_f x>0 and h(1)=-Pi_N P_f(1-x)<0, so at least one root exists in (0,1).

A more direct uniqueness proof uses g(y)=J_C/(J_C+J_N) only where J_T>0; the two fluxes decrease/increase with y respectively, but the total derivative need not have fixed sign. Instead use the polynomial or flux ratio on the admissible interval.

At any closure root, y=J_C/J_T. Because P_f>P_p, the total flux cannot be zero if both component fluxes are nonnegative. A root with negative component fluxes is not automatically an admissible cross-flow solution. The physically admissible interval is:
max(0,1-(1-x)/r) <= y <= min(1,x/r) for r>0.
For r=0 the interval is [0,1].

The admissible interval is nonempty when r<=1, and for 0<r<1 and 0<x<1 its interior is nonempty. At the lower bound J_N=0 if that bound is active, while at the upper bound J_C=0 if active; evaluating the local flux-ratio residual across the admissible interval establishes a physical root. A unique root follows because J_C decreases with y and J_N increases with y; the ratio J_C/(J_C+J_N) strictly decreases on the positive-flux interval while y strictly increases.

Thus for 0<x<1, 0<=r<1 and Pi_i>0 there is one physical local cross-flow closure solution. For r>=1, this argument no longer applies and the one-way-flow assumption must be reassessed.

## 4. Limiting benchmark: zero permeate pressure
For r=0:
J_C=Pi_C P_f x,
J_N=Pi_N P_f(1-x).

Local permeate fraction:
y=alpha x/[alpha x+(1-x)].

For alpha=1, y=x. For alpha>1 and 0<x<1, y>x.

The retentate component ODEs become decoupled:
dF_C/dA=-Pi_C P_f F_C/(F_C+F_N),
dF_N/dA=-Pi_N P_f F_N/(F_C+F_N).

Taking their ratio:
dF_C/dF_N=(Pi_C/Pi_N)(F_C/F_N)=alpha F_C/F_N.

Integrating:
ln(F_C/F_C0)=alpha ln(F_N/F_N0).

Therefore the analytical invariant is:
**F_C/F_C0 = (F_N/F_N0)^alpha**.

This is a strong numerical benchmark for the coupled ODE implementation at r=0.

## 5. Limiting benchmark: equal permeances
If alpha=1, closure gives y=x for 0<=r<1.

Then:
J_C=Pi P_f x(1-r),
J_N=Pi P_f(1-x)(1-r).

Thus:
dF/dA=-Pi(P_f-P_p)
and
dx/dA=0.

Hence:
**F(A)=F_0-Pi(P_f-P_p)A**,
**x(A)=z**,

valid only until the total retentate flow remains positive. This is a second analytical benchmark.

## 6. Global mass conservation
For each component i:
dF_i/dA=-J_i.
Integrating 0 to A_T:
F_i,r(A_T)=F_i,0-integral_0^A_T J_i dA.

Define F_i,p=integral_0^A_T J_i dA. Then:
**F_i,0=F_i,r+F_i,p**.

This conservation identity is independent of selectivity and must be satisfied numerically within declared tolerance.

## 7. Numerical implementation tests
- closure root residual near solver tolerance;
- closure y in [0,1] and J_C,J_N>=0 within tolerance;
- r=0 invariant over area;
- alpha=1 exact total-flow and composition reference;
- zero area returns unchanged feed;
- positive component flows and 0<=x<=1;
- integrated component conservation;
- step/mesh refinement;
- detect retentate exhaustion before nonphysical negative flows.

## 8. Scope and caveats
The r=0 limit is an ideal analytical benchmark, not a realistic claim that vacuum at zero pressure is physically achievable or energetically free.
The equal-permeance benchmark tests mathematical behavior, not CO2 enrichment.
These results verify only the idealised cross-flow model; they do not validate real membrane modules or wet flue-gas performance.

## 9. Next gate
Independent mathematical review of the closure, uniqueness argument and analytical benchmarks. Then freeze the MATLAB/DWSIM implementation contract.
