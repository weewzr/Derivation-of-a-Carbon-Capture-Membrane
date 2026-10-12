# Review 01 Remediation: Numerical Acceptance and Verification Contract

Status: candidate implementation-independent requirements, pending independent re-review. Addresses IMR01-M02, IMR01-D01, IMR01-D02. Values below are proposed verification tolerances for dimensionless synthetic benchmarks, NOT physical accuracy guarantees.

## 1. Domain
Dimensionless state f_C,f_N with f_C(0)=z, f_N(0)=1-z, 0<z<1, alpha>0, 0<=r<1. Let f=f_C+f_N, x=f_C/f.

Use f_min=1e-10 as a default synthetic benchmark depletion cutoff. End integration before f<=f_min; this is a numerical guard, not a physically calibrated residual flow.

Component negativity tolerance eps_neg=1e-12 (normalized by F0). Values below -eps_neg fail; values in [-eps_neg,0] may be treated as roundoff only for diagnostics and not propagated into an invalid state.

## 2. Local root
For r=0 use exact y=alpha*x/(alpha*x+1-x).
For 0<r<1 compute [L,U] as defined in docs/06, then solve H(y)=0 with a bracketed method.

Acceptance: |H(y)| <= 1e-11*max(1,alpha) for synthetic verification cases, with 0<=y<=1 and q_C,q_N>=-1e-12. Require tighter residual in convergence study if this criterion dominates output error.

## 3. ODE controls
Proposed starting tolerances: relative 1e-9, absolute 1e-12 for dimensionless f_C,f_N. These are initial implementation targets, not evidence of accuracy.

Stop with explicit status:
- TARGET_AREA_REACHED;
- TARGET_RECOVERY_REACHED;
- RETENTATE_DEPLETED;
- TARGET_UNREACHABLE_WITHIN_BOUNDS;
- INVALID_INPUT;
- NUMERICAL_FAILURE.

An adaptive integrator may evaluate trial states outside the physical domain. Reject trial states/steps that exceed admissibility tolerances; do not evaluate x=f_C/f at f<=0. An implementation must use a solver strategy capable of preserving this domain or report failure.

## 4. Recovery-target search
Set a maximum dimensionless area a_max as a required user input, rather than silently expanding without bound. If the requested R_target is outside [0,1], reject it. Evaluate the solution at a=0 and a_max, terminating earlier at depletion/invalid domain. If the target is not bracketed by an attainable solution on [0,a_max], return TARGET_UNREACHABLE_WITHIN_BOUNDS. Otherwise use a bracketed scalar search on area; stop when |R(a)-R_target|<=1e-7 and the area bracket is within 1e-7*max(1,a_max), or report NUMERICAL_FAILURE after a declared maximum iteration count (suggest 100).

## 5. Synthetic test cases
TEST-A: z=0.10, alpha=1, r=0.2, a_T=0.25. Exact f_total=1-(1-r)a_T=0.8, x=0.10, f_C=0.08, f_N=0.72. Acceptance absolute 1e-8 for these dimensionless outputs.

TEST-B: z=0.10, alpha=30, r=0, a_T=0.10. Verify invariant f_C/z=(f_N/(1-z))^30, relative residual <=1e-7 for nonzero quantities; test mass conservation and local root residual. This case has no asserted exact outlet values until separately computed and reviewed.

TEST-C: zero area a_T=0. Exact f_C=z, f_N=1-z, theta=0. Overall collected permeate composition is undefined (not zero).

TEST-D: equal-permeance total-flow benchmark at two nonzero a_T values, both below exhaustion; compare with 1-(1-r)a_T.

TEST-E: fixed z,alpha,r,a_T and common permeance scaling k=4. Dimensionless outlets unchanged; physical area for same dimensionless target decreases by factor four.

TEST-F: halve ODE tolerances and repeat until changes in f_C,f_N,R_C,theta are <=1e-7 absolute; document actual observed differences.

## 6. Constant-driving-force reference
For a single species with constant prescribed partial-pressure difference delta_p>0, constant permeance Pi and fixed area A:
J=Pi*delta_p, F_out=F_in-Pi*delta_p*A.
This is a separately prescribed-driving-force analytical reference. It is NOT the full coupled binary module with changing composition, and is used only to check units, sign and area integration.

## 7. Evidence distinction
The test specifications above have not been executed. Passing them would establish numerical implementation correctness only within the idealised model and specified cases. They do not establish experimental membrane validity.
