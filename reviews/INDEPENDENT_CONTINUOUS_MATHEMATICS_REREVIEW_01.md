# Independent Continuous Mathematics Re-Review 01

**Review date:** 2026-10-12  
**Repository:** `weewzr/Derivation-of-a-Carbon-Capture-Membrane`  
**Reviewed branch:** `main` at tree `889d9dc0b2388791108533e18af332d7816c5cbb`  
**Original audit:** `reviews/INDEPENDENT_CONTINUOUS_MATHEMATICS_REVIEW_01.md`  
**Remediation record:** `reviews/INDEPENDENT_CONTINUOUS_MATHEMATICS_REVIEW_01_RESOLUTION.md`  
**Reviewer constraint:** The original review and derivation documents were not edited during this re-review.

## 1. Overall decision

**ACCEPTABLE ONLY UNDER RESTRICTED ASSUMPTIONS.**

Main Research has corrected the local closure specification, supplied a mathematically sound existence/uniqueness argument for the selected closure, bounded the proposed numerical acceptance rules, and explicitly narrowed the solution-diffusion transport derivation to conditional constitutive assumptions. Independent algebraic checks support those changes.

This is **not** an unrestricted pass for a real membrane module, not empirical validation, and not evidence that numerical tests have been executed. The current continuous model is suitable as a prototype implementation contract only if the implemented system is exactly the idealized local-collector model described in document 06, with constant positive permeances, constant pressures, ideal binary gas, and all other stated assumptions. The intended physical module has not yet been confirmed against that architecture.

One original finding remains open as an input dependency (project data), and two findings are only partially resolved, especially the equation-register metadata. Numerical acceptance criteria have been specified but not executed. The Main Research resolution table is a useful ledger; its “remediated” labels are not adopted automatically as independent closure.

## 2. Disposition summary

| Original finding | Severity | Independent status | Reason in brief |
|---|---|---|---|
| IMR01-B01 | BLOCKER | **PARTIALLY RESOLVED** | The ideal local-collector geometry and differential balance are now explicit; suitability of this architecture for the intended real module remains unconfirmed. |
| IMR01-M01 | MAJOR | **CLOSED** | The derivative and endpoint signs in document 06 establish one admissible root under the specified parameter domain. |
| IMR01-M02 | MAJOR | **CLOSED** | The acceptance contract gives a depletion cutoff, negativity tolerance, solver tolerances, stop statuses, and bounded recovery-target search. This closes the specification finding, not implementation testing. |
| IMR01-M03 | MAJOR | **PARTIALLY RESOLVED** | The MEM-SOL entries exist and the ledger is clearer, but the equation-register additions omit per-equation assumptions, units/domain, and dependencies requested by the review. |
| IMR01-M04 | MAJOR | **CLOSED** | Document 07 separates thermodynamic driving force from assumed mobility, membrane ideality, Henry sorption, and the resulting conditional flux law. |
| IMR01-M05 | MAJOR | **CLOSED** | Document 06 defines the supported ideal local-withdrawal configuration and makes clear that it is not a generic permeate-channel model. |
| IMR01-D01 | MODERATE | **CLOSED** | Quantitative proposed tolerances and numerical acceptance criteria are now present; their execution remains pending. |
| IMR01-D02 | MODERATE | **CLOSED** | The r=0 and equal-permeance tests have concrete input cases and acceptance rules, and a separate constant-driving-force benchmark is specified. Tests are not yet executed. |
| IMR01-D03 | MODERATE | **CLOSED** | The model is explicitly a feed-inlet IVP with prescribed permeate pressure and no independent permeate-composition boundary condition under its local-collector closure. |
| IMR01-N01 | MINOR | **CLOSED** | Document 06 uses c2/c1/c0 for closure-polynomial coefficients and reserves a for dimensionless area. |
| IMR01-N02 | MINOR | **CLOSED** | H(y) is the canonical residual; endpoint zero-component-flux cases are described without dividing by the zero component flux. |
| IMR01-N03 | NOTE | **OPEN** | Actual CN4119 conditions and selected membrane-property evidence remain absent, so project-specific performance and sizing claims are unsupported. |

## 3. Independent mathematical re-checks

### 3.1 Local collector balance and physical closure

Document 06 now identifies a specific idealization: each differential membrane strip transfers (J_i,dA) into its own local collector, which immediately withdraws the gas at prescribed uniform (P_p), without tangential permeate flow, hold-up, axial mixing, sweep gas, or a pressure drop between membrane and collector.

The local collector component balance is
[
0=J_i,dA-dF_{i,p,local},
]
so (dF_{i,p,local}=J_i,dA). Summing species,
[
dF_{p,local}=(J_C+J_N),dA.
]
Where (J_C+J_N>0),
[
y=\frac{dF_{C,p,local}}{dF_{p,local}}
=\frac{J_C}{J_C+J_N}.
]
This derivation is valid for the stated local-collector idealization. It does not establish that a commercial hollow-fibre, spiral-wound, or other membrane module behaves this way. The architecture-dependent portion of IMR01-B01 therefore remains conditional on choosing a compatible physical system.

### 3.2 Closure residual, admissible interval, existence, and uniqueness

For
[
q_C=x-r y,\quad q_N=(1-x)-r(1-y),
]
with (0<x<1), (alpha>0), and (0\le r<1), document 06 uses
[
H(y)=\alpha(1-y)q_C-yq_N.
]
The root equation is equivalent to (y=\alpha q_C/(\alpha q_C+q_N)) whenever the total denominator is positive, but (H) itself remains defined when one component flux is zero.

For (0<r<1), the nonnegative-flux interval is
[
L=\max(0,1-(1-x)/r),\quad U=\min(1,x/r).
]
Throughout that interval, (q_C,q_N\ge0) and
[
q_C+q_N=1-r>0,quad
D=\alpha q_C+q_N>0.
]
The endpoint residual signs are correctly derived:
- at (y=L=0), (H=\alpha x>0);
- at an active lower bound (q_N=0) with (L>0), (H=\alpha(1-L)q_C>0);
- at (y=U=1), (H=-q_N=-(1-x)<0);
- at an active upper bound (q_C=0) with (U<1), (H=-Uq_N<0), where (q_N=1-r>0).

The strict signs for (0<x<1) and (0<r<1), together with continuity, give at least one root in the bracket.

For uniqueness, define
[
g(y)=\frac{\alpha q_C}{D},\quad D=\alpha q_C+q_N.
]
Since (q_C'=-r), (q_N'=r), and (D'=r(1-\alpha)),
[
g'(y)=\frac{-\alpha r[D+(1-\alpha)q_C]}{D^2}
=-\frac{\alpha r(q_C+q_N)}{D^2}
=-\frac{\alpha r(1-r)}{D^2}<0.
]
Thus (g(y)-y) is strictly decreasing; it can have at most one root. Combined with the endpoint signs, exactly one admissible root exists. For (r=0), (H(y)=\alpha x-y[\alpha x+(1-x)]) is linear, with the unique root
[
y=\frac{\alpha x}{\alpha x+1-x}.
]
This closes IMR01-M01 for the declared domain. The result does not extend by this proof to (r\ge1), (x\in\{0,1}), or non-positive permeances; those states must remain outside the claimed domain or be separately treated.

### 3.3 Transport derivation and scope

Document 07 states
[
\mu_i=\mu_i^\circ+RT\ln(f_i/f^\circ),
\qquad d\mu_i=RT\,d\ln f_i
]
at fixed temperature; assumes a linear nonequilibrium mobility law
[
J_i=-\frac{D_i c_i}{RT}\frac{d\mu_i^m}{d\xi};
]
and, for an ideal membrane phase with (d\mu_i^m=RT,d\ln c_i), reduces this to Fickian transport. Interface equilibrium plus the Henry-linear relation (c_i^m=S_i f_i), with ideal-gas (f_i=p_i), gives
[
J_i=\frac{D_iS_i}{\ell}(p_{i,f}-p_{i,p})=\Pi_i(p_{i,f}-p_{i,p}).
]
This is internally coherent when the mobility law, ideal membrane-phase relation, local interface equilibrium, constant (D_i), and linear sorption are explicitly treated as assumptions. The document does that. It appropriately does not claim that conservation laws alone determine (D_i), (S_i), permeability, or selectivity. IMR01-M04 is closed conditionally; material calibration and validation remain open inputs.

### 3.4 Numerical contract and analytic reference cases

The numerical contract now provides:
- (f_{min}=10^{-10}) as a default synthetic depletion cutoff;
- component negativity tolerance (10^{-12}) in normalized flow;
- closure residual criterion ( |H(y)|\le10^{-11}\max(1,\alpha));
- initial ODE tolerances (rtol=10^{-9}), (atol=10^{-12});
- explicit terminal statuses;
- a user-supplied maximum dimensionless area, bracketed target recovery search and explicit target-unreachable/failure outcomes;
- synthetic test inputs, expected outcomes and tolerances;
- a constant-driving-force single-species reference, explicitly distinguished from the coupled binary model.

TEST-A is mathematically consistent: for (alpha=1), (y=x), so (df/da=-(1-r)). At (r=0.2), (a_T=0.25), the total normalized retentate flow is (1-(1-r)a_T=0.8); with (z=0.1), (f_C=0.08) and (f_N=0.72), matching the listed values.

For (r=0), the stated invariant is correct:
[
\frac{f_C}{z}=\left(\frac{f_N}{1-z}\right)^\alpha.
]
It follows by dividing the two component ODEs, (df_C/da=-x) and (df_N/da=-(1-x)/\alpha), to obtain (d f_C/d f_N=\alpha f_C/f_N), then integrating over the positive-flow domain.

These are **specifications and analytic checks, not executed test results**. The contract correctly labels them as proposed tolerances and states that the values do not guarantee physical accuracy. Accordingly, IMR01-M02, D01, and D02 are closed at the specification level only; numerical implementation acceptance still requires execution and evidence.

### 3.5 Register and status reconciliation

The canonical register now contains MEM-SOL-001 through MEM-SOL-014 and labels new closure equations as review pending. The derivation ledger also distinguishes main-research derivation status from independent review status. This materially improves traceability.

However, the new MEM-SOL table columns contain only ID, description, source, class, and status. They do not, on a per-equation basis, include the assumptions/domain, units, check evidence, and dependencies required by the canonical register rules and by IMR01-M03's correction request. Some of these can be inferred from the source documents or DER entries, but the register's purpose is to provide a canonical trace without such inference. IMR01-M03 remains partially resolved until the per-equation records are complete. This documentation defect does not change the independently checked algebra but should be corrected before calling the register a complete implementation handoff.

## 4. Required residual work

1. **Architecture/input closure:** Identify whether the intended membrane module can reasonably be represented by the local independent collectors and uniform permeate pressure in document 06. Until then, claims must be restricted to the idealized collector model.
2. **Equation-register completeness:** Add per-equation assumptions/domain, units, independent-check evidence/status, and dependencies for MEM-SOL entries, without retroactively implying unperformed numerical verification.
3. **Run the tests:** Execute TEST-A through TEST-F in the chosen implementation and retain outputs, conservation residuals, root residuals, positivity/admissibility results, and convergence changes. Do not equate a defined acceptance contract with a passed test.
4. **Project calibration:** Obtain actual CN4119 feed conditions and a sourced, applicability-matched membrane property set before any project performance, area, capture-benefit, or economics claim.

## 5. Gate recommendation

The idealized continuous equations are mathematically defensible **under the restricted assumptions stated in documents 06 and 07**. A prototype numerical implementation may proceed only if it is explicitly scoped to that ideal local-collector model and implements the numerical acceptance contract. Do not describe that step as validation for the intended physical membrane module or as clearance for CN4119 predictions.

The independent mathematical review is therefore:

**ACCEPTABLE ONLY UNDER RESTRICTED ASSUMPTIONS**

Original finding dispositions remain as tabulated above. The original Review 01 and the mathematical derivations have not been changed by this re-review.
