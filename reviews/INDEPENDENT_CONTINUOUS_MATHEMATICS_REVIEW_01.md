# Independent Continuous Mathematics Review 01

**Repository:** `weewzr/Derivation-of-a-Carbon-Capture-Membrane`  
**Review date:** 2026-10-12  
**Scope:** Current main-branch generic binary CO2/N2 steady, isothermal, ideal-gas, constant-pressure cross-flow model in documents 01-05.  
**Role:** Independent mathematical audit only. No derivation documents have been edited by this review.  
**Decision:** **FAIL - REMEDIATION REQUIRED**

## 1. Executive finding

The general membrane-phase species balance, constant-property Fick/linear-sorption solution-diffusion flux law, retentate component balances, dimensionless area scaling, and two stated limiting benchmarks are consistent within their declared assumptions.

The model is not yet suitable for an unqualified independent MATLAB/DWSIM implementation. The admissible-interval uniqueness proof uses an incomplete monotonicity argument; the local cross-flow closure is an architecture assumption rather than a consequence of feed-side balances alone; the solver stopping/admissibility contract lacks concrete numerical tolerances and precise depletion handling; and the canonical equation register does not include the latest MEM-SOL equations or consistently record verification status. The model remains an idealised candidate, not a validated physical module model.

This review does not conclude that the local closure is necessarily wrong. It concludes that the current proof and implementation contract do not establish all claims needed to pass the mathematical gate.

## 2. Findings summary

| ID | Severity | Finding |
|---|---|---|
| IMR01-B01 | BLOCKER | Local cross-flow closure is not derived from a fully specified geometric control volume; it is an explicit idealisation that needs a bounded physical definition before being treated as the implementation contract. |
| IMR01-M01 | MAJOR | The closure uniqueness proof in documents 03 and 05 contains incomplete monotonicity justification and boundary-sign arguments that should be replaced by a verified proof. |
| IMR01-M02 | MAJOR | The stopping/depletion contract is not precise enough to guarantee ODE integration only on its valid state domain or robust termination of target-area/recovery searches. |
| IMR01-M03 | MAJOR | The equation register and verification status are not synchronized with the latest MEM-SOL-001 through MEM-SOL-014 contract. |
| IMR01-M04 | MAJOR | The derivation workflow promises a chemical-potential/fugacity-first transport chain, but document 01 starts from Fick's law and linear sorption; this is conditional constitutive modelling, not the advertised full thermodynamic derivation. |
| IMR01-M05 | MAJOR | The local permeate closure applies only to a specific differential cross-flow idealisation and does not independently derive permeate-side transport/accumulation for a physical module. |
| IMR01-D01 | MODERATE | Numerical admissibility, residual tolerances, convergence acceptance criteria, and robust root evaluation are not specified numerically. |
| IMR01-D02 | MODERATE | The r=0 invariant and equal-permeance analytical case are correct, but a constant-driving-force area/flux benchmark and concrete test tolerances are not supplied. |
| IMR01-D03 | MODERATE | The feed initial conditions are clear, but the absence of a separate permeate-side boundary condition should be explicitly tied to the chosen algebraic closure in the implementation handoff. |
| IMR01-N01 | MINOR | Notation reuses a for a polynomial coefficient in document 03 and dimensionless area in document 05. |
| IMR01-N02 | MINOR | Strictly positive-flux equations and zero-component-flux endpoints are not consistently distinguished in the closure narrative. |
| IMR01-N03 | NOTE | No project-specific permeance values or CN4119 data are supplied; this is disclosed and does not invalidate the generic symbolic derivation. |

## 3. Independent rederivation

### 3.1 Membrane transport under the selected constitutive assumptions

For species i, local membrane-phase conservation is

    partial(c_i)/partial(t) + div(J_i) = R_i.

For steady, one-dimensional, nonreactive transport through a homogeneous layer, this reduces to dJ_i/dxi = 0, hence J_i is constant across the selective layer.

With Fickian membrane-phase transport J_i = -D_i dc_i/dxi, constant D_i, and linear interfacial sorption c_i,f^m = S_i p_i,f, c_i,p^m = S_i p_i,p, integration gives

    J_i = (D_i S_i / ell)(p_i,f - p_i,p) = Pi_i(p_i,f - p_i,p),
    Pi_i = D_i S_i / ell.

The dimensions are [D_i S_i / ell] = mol m^-2 s^-1 Pa^-1, and multiplying by pressure gives flux mol m^-2 s^-1. With ideal-gas contacting phases as an additional assumption, p_i,f = P_f x_i and p_i,p = P_p y_i.

The algebra is correct under these explicit constitutive assumptions. Fick's law plus linear sorption is a selected transport model, not a universal consequence of conservation or a complete derivation from chemical potential. Either narrow the scope to this assumed model over a stated validity range, or add the separate thermodynamic derivation required to support the broader claim.

### 3.2 Retentate component balances

For a differential area strip dA, transfer is J_i dA from the retentate side under the declared sign convention. The steady balance is

    F_i(A) - F_i(A+dA) = J_i dA, so dF_i/dA = -J_i.

Summing gives dF/dA = -(J_C+J_N). For x=F_C/F,

    dx/dA = [F(dF_C/dA) - F_C(dF/dA)]/F^2
          = [-J_C + x(J_C+J_N)]/F.

These equations and inlet conditions F_C(0)=F_0 z, F_N(0)=F_0(1-z) are consistent. The two component-flow ODEs are preferable as the numerical state because they make conservation and nonnegative-state constraints direct.

### 3.3 Algebraic closure

With r=P_p/P_f, alpha=Pi_C/Pi_N, and P_f>0,

    J_C = Pi_C P_f (x-r y),
    J_N = Pi_N P_f ((1-x)-r(1-y)).

If the local differential permeate stream is defined to have the instantaneous transfer composition and total transfer is positive, then y=J_C/(J_C+J_N). Substitution yields

    h(y) = alpha(1-y)(x-r y) - y((1-x)-r(1-y)) = 0,

or

    r(1-alpha)y^2 + [1-x-r+alpha(x+r)]y - alpha x = 0.

The polynomial expansion is correct.

For one-way nonnegative component transfer, the driving-force inequalities imply

    L = max(0, 1-(1-x)/r), U = min(1, x/r)

for r>0, and y in [0,1] for r=0. For 0<x<1 and 0<r<1, the interval is nonempty. A root in [0,1] alone is not sufficient evidence of physical admissibility.

The stated proof that J_C decreases and J_N increases and therefore J_C/(J_C+J_N) decreases is not justified solely by those facts because the denominator also varies. On the positive-flux interval define q_C=x-r y, q_N=1-x-r+r y, D(y)=alpha q_C+q_N, and g(y)=alpha q_C/D(y). Differentiation gives

    g'(y) = [-alpha r D(y) - alpha q_C r(1-alpha)]/D(y)^2
          = -alpha r(1-r)/D(y)^2 < 0 for 0<r<1,

because D(y)+q_C(1-alpha)=1-r. For r=0, g is constant and y=alpha*x/(alpha*x+1-x). Existence still needs a consistently scaled residual and an endpoint sign proof that handles endpoints with one zero component flux without dividing by that flux. The derivation documents should present one residual and prove the bracket signs for that exact residual.

### 3.4 Dimensionless scaling

Set f_i=F_i/F_0 and a=(Pi_C P_f/F_0)A. Then

    df_C/da = -(x-r y),
    df_N/da = -[(1-x)-r(1-y)]/alpha.

All terms are dimensionless. [Pi_C P_f/F_0] = m^-2, so a is dimensionless and A=(F_0/(Pi_C P_f))a has units m^2. Multiplying both permeances by k>0 leaves alpha, r, and y(x) unchanged and scales the physical area needed for the same dimensionless outlet state by 1/k within this constant-property model. This is consistent.

### 3.5 Performance outputs and conservation

For prescribed endpoint a_T, theta=1-(f_C+f_N) is total stage cut, R_C=(z-f_C)/z is CO2 recovery, and Y_C,p=(z-f_C)/theta is overall collected permeate CO2 fraction only for theta>0. At zero area, theta=0 and bulk permeate composition is undefined, as the contract correctly states. Component outlet identities follow from integrating dF_i/dA=-J_i, provided the ODE stays in its physical domain.

## 4. Findings and required corrections

### IMR01-B01 — BLOCKER: physical scope of the local cross-flow closure

**Location:** `docs/02_GENERIC_BINARY_CROSSFLOW_MODEL.md` §§1-2; `docs/03_BINARY_CROSSFLOW_CLOSURE_AUDIT.md` §3; `docs/05_SOLVER_READY_BINARY_CONTRACT.md` physical assumptions and MEM-SOL-004.

**Justification:** Feed-side conservation gives dF_i/dA=-J_i; it does not alone imply y=J_C/(J_C+J_N). That equality defines an idealized differential cross-flow element whose locally withdrawn permeate has the instantaneous transfer composition and no tangential permeate accumulation or mixing. A real module may instead have a permeate channel/plenum, pressure drop, sweep flow, or spatial mixing, for which a permeate-side balance and appropriate closure are needed.

**Required correction:** State the physical/geometric definition of the idealized cross-flow element and label the closure as a model assumption, not a universal membrane equation. Document configurations for which it is and is not a reasonable approximation. Keep implementation conditional on confirming that architecture.

### IMR01-M01 — MAJOR: closure uniqueness proof needs a consistently defined residual

**Location:** `docs/03_BINARY_CROSSFLOW_CLOSURE_AUDIT.md` §3 and `docs/05_SOLVER_READY_BINARY_CONTRACT.md` admissible interval proof.

**Justification:** Monotonicity of the individual fluxes alone does not prove monotonicity of their ratio. The explicit derivative above establishes strict decrease on the positive-flux interval for 0<r<1. Existence requires a separate endpoint proof for the chosen residual, including edge cases where one flux vanishes.

**Required correction:** Replace the informal statement with the full derivative calculation and a sign-consistent endpoint proof for the exact residual used by the solver. Show the root is on the nonnegative-flux interval, not merely in [0,1].

### IMR01-M02 — MAJOR: integration and recovery stopping conditions are underspecified

**Location:** `docs/05_SOLVER_READY_BINARY_CONTRACT.md` “Solver contract” and “Stopping and output”.

**Justification:** x=f_C/(f_C+f_N) is undefined at zero total retentate. Adaptive ODE solvers can take trial steps outside f_i>=0, even when the exact trajectory approaches the domain boundary. “Declared nonphysical/depleted threshold” does not specify a threshold or event. Recovery-target area search needs a bracket, reachability test, and finite stopping rule.

**Required correction:** Specify a positive cutoff f_C+f_N<=epsilon_F, component admissibility tolerance, event/rejected-step handling, and target-recovery search rules: bracket expansion or maximum dimensionless area, reachability decision, convergence tolerances, and an explicit target-unreachable result. Test the rules rather than leaving them to the implementer.

### IMR01-M03 — MAJOR: equation register and verification status are not synchronized

**Location:** `docs/CANONICAL_EQUATION_REGISTER.md`, `STATUS.md`, `docs/05_SOLVER_READY_BINARY_CONTRACT.md`.

**Justification:** The solver contract introduces MEM-SOL-001 through MEM-SOL-014, but the canonical register ends with earlier MEM-GOV/MEM-CON/MEM-FLX/MEM-BIN/MEM-PERF entries. The ledger still labels core derivations PLANNED, while some register entries say VERIFIED without a complete review record connecting that label to the current contract and verification evidence.

**Required correction:** Reconcile the register and ledger after mathematical revisions. Add entries for active solver-contract equations with source, assumptions, units/domain, dependencies, and review status. Do not mark closure uniqueness or analytical benchmarks independently verified until findings are reconciled and reproducible checks are recorded. Keep open findings open in STATUS.md.

### IMR01-M04 — MAJOR: advertised thermodynamic derivation is incomplete

**Location:** `docs/DERIVATION_WORKFLOW_TRISO_STYLE.md` M3; `docs/TRISO_INSPIRED_DERIVATION_WORKFLOW.md` C2; `docs/01_FIRST_PRINCIPLES_TRANSPORT_DERIVATION.md` §§3-5.

**Justification:** The derivation assumes Fick's law, applies linear sorption c_i^m=S_i p_i, and combines them to obtain D_i S_i/ell. It does not derive the transport driving force from chemical potential or establish partial pressure as the thermodynamic potential over a broad validity range. This is not an algebraic error, but the workflow's promised thermodynamic chain has not been demonstrated.

**Required correction:** Either narrow the claim and handoff to “Fickian diffusion plus linear sorption over a specified validity range”, or add the separate thermodynamic/constitutive derivation needed for chemical-potential/fugacity claims. Do not present the current sequence as a universal first-principles consequence.

### IMR01-M05 — MAJOR: permeate-side model is eliminated by assumption

**Location:** `docs/02_GENERIC_BINARY_CROSSFLOW_MODEL.md` §§1-2; `docs/INITIAL_CONDITIONS_AND_BOUNDARIES.md`; `docs/MATLAB_HANDOFF_SPECIFICATION.md`.

**Justification:** The feed-side ODEs form a closed IVP only after y(x) is imposed algebraically. There is no independent permeate-side state or material balance. This is valid for the stipulated local-withdrawal abstraction but is not equivalent to a general cross-flow module with a permeate channel. The handoff requires an arrangement diagram but none is supplied in the reviewed mathematical contract.

**Required correction:** Add the geometry/arrangement schematic and explain why the instantaneous local permeate composition equals the transfer ratio under the idealization; otherwise derive the appropriate permeate-channel/plenum model. Identify the exact supported configuration in the MATLAB/DWSIM handoff.

### IMR01-D01 — MODERATE: numerical acceptance criteria are not operational

**Location:** `docs/05_SOLVER_READY_BINARY_CONTRACT.md`; `docs/MATLAB_HANDOFF_SPECIFICATION.md`.

**Justification:** “Near solver tolerance”, “within numerical tolerance”, “stabilize”, and “materially negative” are qualitative and cannot provide reproducible pass/fail results across implementations.

**Required correction:** Specify absolute/relative tolerances for closure residuals, component-flow positivity, mass-balance residuals, ODE error control, endpoint metrics, and grid/tolerance refinement. Include a small benchmark input set and expected tolerances, separate from literature calibration.

### IMR01-D02 — MODERATE: analytical checks need a complete acceptance contract

**Location:** `docs/03_BINARY_CROSSFLOW_CLOSURE_AUDIT.md` §§4-5; `docs/05_SOLVER_READY_BINARY_CONTRACT.md` verification cases.

**Justification:** The r=0 invariant is correct: F_C/F_C0=(F_N/F_N0)^alpha. The alpha=1 benchmark is also correct: y=x, dF/dA=-Pi(P_f-P_p), and x=z until retentate exhaustion. No explicit finite test values or tolerances are attached, and the planned constant-driving-force area/flux reference is absent.

**Required correction:** Provide a constant-driving-force reference or formally mark it out of scope, and specify numeric inputs plus pass tolerances for the r=0 and alpha=1 cases. Distinguish algebraic identities from executed numerical test evidence.

### IMR01-D03 — MODERATE: distinguish feed initial conditions from permeate boundaries

**Location:** `docs/INITIAL_CONDITIONS_AND_BOUNDARIES.md`; `docs/05_SOLVER_READY_BINARY_CONTRACT.md`.

**Justification:** The state is (f_C,f_N) with feed-inlet initial data; no independent permeate boundary value exists because the algebraic closure removes that state. This is consistent for this IVP, but the generic boundary note covers other architectures and could lead implementers to assume that the current model includes them.

**Required correction:** Explicitly state that no separate permeate boundary condition is used in the current local-closure model. Identify how conditions change for co-current, counter-current, or mixed-plenum architectures.

### IMR01-N01 — MINOR: notation collision for a

**Location:** `docs/03_BINARY_CROSSFLOW_CLOSURE_AUDIT.md` §2; `docs/05_SOLVER_READY_BINARY_CONTRACT.md`.

**Justification:** Document 03 uses a for the coefficient r(1-alpha); document 05 uses a for dimensionless area. These project-wide symbols are easy to confuse when implementing.

**Required correction:** Use distinct labels such as c2, c1, c0 for polynomial coefficients and reserve a for dimensionless area.

### IMR01-N02 — MINOR: distinguish positive-flux interior from zero-transfer endpoints

**Location:** `docs/02_GENERIC_BINARY_CROSSFLOW_MODEL.md` §2; `docs/05_SOLVER_READY_BINARY_CONTRACT.md` MEM-SOL-004/009.

**Justification:** A root at an admissible interval endpoint can have J_C=0 or J_N=0. The ratio y/(1-y) or a flux ratio involving a zero component is not defined there, even if the polynomial residual is well-defined. The solver should rely on a canonical residual and handle endpoints directly.

**Required correction:** Define the residual as the canonical root function and limit ratio rearrangements to the strict interior. Handle zero-component-flux endpoints without division by that component flux.

### IMR01-N03 — NOTE: project-specific inputs are absent

**Location:** README.md, STATUS.md, parameter register.

**Justification:** Feed specifications and membrane/permeance data are not supplied. The current model supports generic symbolic mathematics and benchmarks only; it cannot support quantitative CN4119 predictions or sizing/economics claims.

**Required correction:** None to the derivation. Preserve the scope limitation and do not promote illustrative parameters to project predictions.

## 5. Boundary, dimensional, and initial-condition review

- Feed IVP: f_C(0)=z, f_N(0)=1-z, with F_0>0, 0<z<1: consistent.
- Flux sign: positive feed-to-permeate and dF_i/dA=-J_i: consistent.
- Permeance units: mol m^-2 s^-1 Pa^-1: consistent.
- Dimensionless area: a=(Pi_C P_f/F_0)A is dimensionless: consistent.
- Y_C,p is undefined at zero stage cut; correctly qualified in the contract.
- This is a steady-state module ODE, so its feed-inlet condition is an independent-variable initial condition, not a transient time initial condition.
- Wet gas, support resistance, nonideal fugacity, pressure drop, and real module geometry are outside the proved model.

## 6. Conclusion

**FAIL - REMEDIATION REQUIRED**

The core transport algebra and component balances are a suitable candidate foundation under stated assumptions. Dimensionless scaling and the two analytical limiting identities also check out. However, architecture-specific closure, proof presentation, numerical boundary/stopping rules, and equation-register/verification bookkeeping must be made implementation-grade before the handoff can be called independently reviewed and ready.

No mathematical derivation has been modified by this review. All findings remain open for the Main Research chat to address independently.
