> **Review 01 reconciliation:** This document is a historical candidate specification, **not a frozen implementation handoff**. For the authoritative corrected local-collector architecture and proof see [06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md](06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md); for numerical tolerances, events and target search see [REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md](../verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md). The corrections await independent re-review. Do not use this document alone to implement the model.

# 05 - Solver-Ready Continuous Binary Cross-Flow Contract

Status: MAIN RESEARCH CANDIDATE. Independent mathematical review pending. No CN4119 parameter calibration.

## Physical and constitutive assumptions
Steady, isothermal, ideal-gas, binary CO2 (C) and N2 (N), dense solution-diffusion selective layer, constant positive permeances, fixed P_f>P_p>=0, locally withdrawn cross-flow permeate without axial permeate mixing. Ignore pressure losses, polarization, water and membrane aging for this benchmark.

Let F_0>0 [mol/s], z in (0,1), x=F_C/(F_C+F_N), y=local permeate CO2 mole fraction, alpha=Pi_C/Pi_N>0, r=P_p/P_f in [0,1), a=(Pi_C P_f/F_0)A>=0. Let f_C=F_C/F_0 and f_N=F_N/F_0.

## Governing equations
MEM-SOL-001: x=f_C/(f_C+f_N).
MEM-SOL-002: q_C=x-r*y.
MEM-SOL-003: q_N=(1-x)-r*(1-y).
MEM-SOL-004: y=q_C/(q_C+q_N/alpha), assuming nonnegative component fluxes and positive total flux.
MEM-SOL-005: df_C/da=-q_C.
MEM-SOL-006: df_N/da=-q_N/alpha.
MEM-SOL-007: f_C(0)=z; f_N(0)=1-z.

The local closure equivalently satisfies:
MEM-SOL-008: h(y)=(1-y)*alpha*(x-r*y)-y*((1-x)-r*(1-y))=0.
It is quadratic with coefficients r(1-alpha), 1-x-r+alpha*(x+r), -alpha*x.

## Admissible local algebraic interval
For r=0, use y=alpha*x/(alpha*x+1-x).
For 0<r<1:
MEM-SOL-009: L=max(0,1-(1-x)/r); U=min(1,x/r).
Solve h(y)=0 on [L,U].

Proof of existence and uniqueness on this interval:
q_C>=0 and q_N>=0 there. At L, either L=0 and h(L)=alpha*q_C>0, or q_N(L)=0 and h(L)=(1-L)*alpha*q_C>0 for 0<x<1, r<1. At U, either U=1 and h(U)=-q_N<0, or q_C(U)=0 and h(U)=-U*q_N<0. Thus a root exists. The flux fraction g(y)=alpha*q_C/(alpha*q_C+q_N) is nonincreasing (strictly decreasing for r>0) on [L,U], since q_C decreases and q_N increases as y increases. Hence y=g(y) has a unique root. At r=0, g is constant, also giving a unique root.

Do not use an unconstrained quadratic root that may select an unphysical branch.

## Solver contract
At each ODE evaluation:
1. reject f_C<0 or f_N<0 beyond numerical tolerance, or f_C+f_N<=0;
2. calculate x;
3. determine y using analytic r=0 case or bracketed scalar root on [L,U];
4. compute q_C and q_N and reject materially negative values;
5. return [-q_C,-q_N/alpha].
Use an adaptive ODE integrator or a conservative area discretisation. Refine integration tolerances/area grid until outputs stabilize.

## Stopping and output
For prescribed a_T, integrate until a_T or until the retentate reaches a declared nonphysical/depleted threshold. For target recovery, solve for the smallest a_T satisfying the target if reachable before termination. A recovery target is not automatically attainable.

MEM-SOL-010: theta=1-(f_C+f_N).
MEM-SOL-011: R_C=(z-f_C)/z.
MEM-SOL-012: Y_C,p=(z-f_C)/theta, only for theta>0.
MEM-SOL-013: x_r=f_C/(f_C+f_N), only while retentate exists.
MEM-SOL-014: A=(F_0/(Pi_C*P_f))*a_T [m2].

At a_T=0 the permeate flow is zero and permeate bulk composition is undefined, although local y at the inlet is well-defined.

## Verification cases
V1: a_T=0 gives f_C=z and f_N=1-z.
V2: r=0 yields f_C/z=(f_N/(1-z))^alpha.
V3: alpha=1 yields x=z and f_C+f_N=1-(1-r)*a while positive.
V4: f_C+f_N+theta=1 and each component feed equals retentate plus permeate.
V5: y within [L,U] and closure residual tends to zero under tighter root tolerance.
V6: physical outlet observables converge under tighter ODE tolerance/area refinement.
V7: changing Pi_C and Pi_N by common factor k at fixed physical inputs yields identical dimensionless results and physical required area scaled by 1/k.

## Limits
No empirical validation, no pressure work or economics, no wet-gas transport, no mixed-gas property calibration, no multistage operation. r=0 is a mathematical limit, not feasible zero-absolute-pressure equipment. The module model is an idealized cross-flow representation, not a detailed fiber geometry.

## Next
Request independent mathematical audit of documents 01-05, reconcile findings, and then freeze the implementation handoff. Actual literature parameters and CN4119 feed conditions are separate inputs.
