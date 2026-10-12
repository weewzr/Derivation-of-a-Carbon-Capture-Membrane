# STATUS

## Current state
The repository contains a candidate steady, isothermal, ideal-gas binary CO2/N2 solution-diffusion cross-flow model. An independent continuous-mathematics review has now been completed and committed. Its conclusion is **FAIL - REMEDIATION REQUIRED**. The derivation documents themselves have not been modified by the reviewer.

## Current gate
- Gate B: candidate continuous model exists, but the physical module architecture/local permeate closure remains conditional.
- Gate C: analytical identities have been independently rederived symbolically; reproducible numerical acceptance evidence is still incomplete.
- Gate E (independent audit): review completed with open findings; gate does not pass.
- MATLAB/DWSIM implementation: **not cleared by this review**.

## Workflow authority
- `docs/DERIVATION_WORKFLOW_TRISO_STYLE.md`
- `docs/GATE_WORKFLOW.md`
- `docs/CANONICAL_EQUATION_REGISTER.md`
- `docs/DERIVATION_LEDGER.md`

## Current mathematical documents
- `docs/01_FIRST_PRINCIPLES_TRANSPORT_DERIVATION.md`
- `docs/02_GENERIC_BINARY_CROSSFLOW_MODEL.md`
- `docs/03_BINARY_CROSSFLOW_CLOSURE_AUDIT.md`
- `docs/04_PERMEANCE_SELECTIVITY_SCALING.md`
- `docs/05_SOLVER_READY_BINARY_CONTRACT.md`
- `docs/INITIAL_CONDITIONS_AND_BOUNDARIES.md`
- `docs/MATLAB_HANDOFF_SPECIFICATION.md`

## Independent review
- Review: `reviews/INDEPENDENT_CONTINUOUS_MATHEMATICS_REVIEW_01.md`
- Decision: **FAIL - REMEDIATION REQUIRED**
- Findings: 1 BLOCKER, 5 MAJOR, 3 MODERATE, 2 MINOR, 1 NOTE.
- Finding IDs: IMR01-B01, IMR01-M01 through IMR01-M05, IMR01-D01 through IMR01-D03, IMR01-N01 through IMR01-N03.
- All findings remain **OPEN** for the Main Research workflow. This status file does not declare any finding resolved or accepted.
- The review is an audit record, not an instruction to modify the derivation in this commit.

## Independently checked mathematical points
- Steady nonreactive membrane-phase conservation and constant flux through the layer.
- Fickian diffusion plus linear-sorption solution-diffusion flux law, conditional on those constitutive assumptions.
- Retentate component balances and CO2 mole-fraction derivative.
- Binary cross-flow closure polynomial expansion and physical-flux interval.
- Dimensionless area scaling and common-permeance scaling.
- The symbolic `r=0` invariant and the equal-permeance (`alpha=1`) limiting solution.

These symbolic checks do not amount to empirical validation or numerical implementation verification.

## Open blockers
- IMR01-B01: specify and justify the physical/geometric scope of the idealized local cross-flow closure.
- IMR01-M01: replace the closure uniqueness/existence discussion with one consistently defined residual, explicit derivative and endpoint-sign proof.
- IMR01-M02: define operational solver admissibility, depletion, event handling, and target-recovery stopping rules.
- IMR01-M03: reconcile the canonical equation register and derivation ledger with the solver contract and review states.
- IMR01-M04: either narrow the solution-diffusion claim to its stated constitutive assumptions or derive the advertised chemical-potential/fugacity chain.
- IMR01-M05: identify the supported module geometry and explain/elaborate the eliminated permeate-side state.
- IMR01-D01 through IMR01-D03 and IMR01-N01 through IMR01-N02 remain open as detailed in the review.
- Actual CN4119 feed conditions and sourced membrane-property evidence are still outstanding (IMR01-N03).

## Next bounded action
The Main Research chat should reconcile the findings independently in a separate remediation pass, preserving this review unchanged and recording evidence for each finding. After that, request a new review only against the updated commit.

## Stop condition
Do not proceed to MATLAB/DWSIM implementation, parameter optimisation, or project economics until the open blocker(s) are addressed, the continuous model is closed for a confirmed architecture, and the required analytical/numerical acceptance checks are recorded.
