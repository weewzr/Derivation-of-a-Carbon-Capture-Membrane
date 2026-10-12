> **Review 01 reconciliation:** The local permeate composition is an explicit **ideal local-collector geometry assumption**, derived from a differential permeate collector balance in [06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md](06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md). This model does not represent a generic co-/counter-current permeate channel. The revised admissible root and proof in document 06 supersede informal proof wording here. Numerical stopping criteria are in [REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md](../verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md).

# 02 - Generic Binary CO2/N2 Cross-Flow Membrane Model

## Status
CANDIDATE mathematical model. Independent review and parameter selection pending. This is a cross-flow model with locally removed permeate, not a co-current/counter-current permeate-channel model.

## 1. Scope and conventions
Steady, isothermal, ideal-gas CO2/N2 feed at constant feed pressure P_f and constant permeate pressure P_p. The dense membrane has constant species permeances Pi_C and Pi_N. No pressure drop, concentration polarization, sweep gas, backmixing of permeate into the feed, or water.

A is cumulative membrane area [m2] from feed inlet A=0. F_C(A) and F_N(A) are feed/retentate-side component molar flow rates [mol/s]. F=F_C+F_N. x=F_C/F is local retentate CO2 mole fraction. The permeate removed at each area element dA has instantaneous CO2 mole fraction y(A). Flux J_i [mol/(m2 s)] is positive feed-to-permeate.

## 2. Constitutive transport
J_C=Pi_C(P_f x-P_p y).
J_N=Pi_N(P_f(1-x)-P_p(1-y)).
Pi_i [mol/(m2 s Pa)].

Assume the local cross-flow permeate has no tangential accumulation or axial mixing. Its composition is therefore the ratio of instantaneous component transfer rates:
y=J_C/(J_C+J_N), provided J_C+J_N>0.

This is an algebraic local closure, NOT the overall collected permeate composition.

Define r=P_p/P_f and alpha=Pi_C/Pi_N. If J_N>0 and J_C>0, the closure is equivalently:
y/[1-y] = alpha (x-r y)/[(1-x)-r(1-y)].

This relation must be solved on the physically admissible branch: 0<=y<=1, x-r y>=0 and (1-x)-r(1-y)>=0. In parameter regions where these inequalities cannot hold, the positive one-way-flux cross-flow assumption is invalid; report that explicitly instead of forcing a root.

## 3. Species conservation on dA
For steady operation, retentate inflow minus outflow equals component transfer through the membrane:
dF_C/dA=-J_C,
dF_N/dA=-J_N.

Thus:
dF/dA=-(J_C+J_N).

Since x=F_C/F:
dx/dA=[-J_C+x(J_C+J_N)]/F
      =[(x-1)J_C+x J_N]/F.

These are alternative representations, not independent additional constraints. Integrate either the two component-flow ODEs or the (F,x) ODEs.

## 4. Initial condition
At A=0:
F_C(0)=F_0 z,
F_N(0)=F_0(1-z),
with F_0>0 and 0<z<1.

The model is an initial-value ODE with an algebraic permeate-composition closure.

## 5. Collected permeate and conservation
At total area A_T:
F_C,p=F_0 z-F_C(A_T),
F_N,p=F_0(1-z)-F_N(A_T),
F_p=F_C,p+F_N,p,
F_r=F_C(A_T)+F_N(A_T).

Overall permeate composition Y_C,p=F_C,p/F_p when F_p>0. This is generally different from local y(A).

Verify for each component:
F_i,0=F_i,r+F_i,p.

## 6. Metrics
Stage cut theta=F_p/F_0.
CO2 recovery R_C=F_C,p/(F_0 z).
CO2 enrichment E_C=Y_C,p/z.
Retentate CO2 mole fraction x_r=F_C(A_T)/F_r.

Report both permeate and retentate streams; pre-concentration is not synonymous with total CO2 avoided.

## 7. Area sizing
For fixed A_T, solve the ODE to obtain performance. For target recovery R_target, solve for the smallest physically admissible A_T that achieves it, if reachable under the selected pressure and permeance assumptions. Do not prescribe both area and recovery as independent fixed constraints.

## 8. Dimensional and limiting checks
- [Pi_i]*[pressure]=mol/(m2 s).
- [dF_i/dA]=mol/(s m2).
- A_T=0: retentate equals feed and permeate flow is zero.
- P_f x_i=P_p y_i: corresponding component flux is zero.
- Integrated component balance closes exactly at continuum level.
- Pi_C=Pi_N gives no intrinsic material selectivity, although pressure-driven separation and finite stage cut still require careful interpretation.
- If pressure ratio is too high to allow positive component fluxes, the assumed one-way cross-flow model has no admissible solution.
- Grid/step refinement must be tested before numerical results are accepted.

## 9. Handoff algorithm
For each ODE evaluation:
1. obtain F_C,F_N and compute F,x;
2. solve the local nonlinear equation for y using a bracketed method on the admissible interval;
3. calculate J_C,J_N;
4. return [-J_C,-J_N].
Terminate or report invalid when F<=0, admissible y does not exist, or a physical/solver domain condition fails.

## 10. Known limitations and next steps
No water/O2, pressure drop, support resistance, nonideal thermodynamics, permeance dependence on temperature/composition/humidity, multistage recycle or real module hydrodynamics. Membrane material and parameters remain to be sourced from literature. This is an initial generic mathematical benchmark, not a calibrated CN4119 design.

## 11. References
Derivation uses conservation and the solution-diffusion constitutive assumptions in docs/01_FIRST_PRINCIPLES_TRANSPORT_DERIVATION.md. Primary literature/property verification is still required.
