# STATUS

## Current state
The membrane repository now explicitly follows a staged derivation workflow adapted from the TRISO mathematical project. A candidate transport derivation and generic binary cross-flow model exist, but both remain subject to the mathematical gate and independent review process.

## Current gate
Gate A / early Gate B: physical problem definition and candidate continuous derivation.

## Workflow authority
- `docs/DERIVATION_WORKFLOW_TRISO_STYLE.md`
- `docs/GATE_WORKFLOW.md`
- `docs/CANONICAL_EQUATION_REGISTER.md`
- `docs/DERIVATION_LEDGER.md`

## Current mathematical documents
- `docs/01_FIRST_PRINCIPLES_TRANSPORT_DERIVATION.md`
- `docs/02_GENERIC_BINARY_CROSSFLOW_MODEL.md`
- `docs/INITIAL_CONDITIONS_AND_BOUNDARIES.md`
- `docs/MATHEMATICAL_DERIVATION_PLAN.md`
- `docs/MATLAB_HANDOFF_SPECIFICATION.md`

## Current scientific position
The dense-polymer solution-diffusion law and idealised binary cross-flow closure are candidates under explicit assumptions; they are not yet promoted to a final project-specific verified model. The local permeate closure in cross-flow must be reviewed against the exact geometric interpretation before relying on it numerically.

## Open blockers
- Confirm module architecture/flow arrangement and permeate-side physical closure.
- Independently audit the generic binary equations, especially the algebraic local permeate-composition equation and admissible-flux domain.
- Receive actual CN4119 feed conditions and membrane-property evidence.
- Complete an analytical limiting benchmark.
- Verify the mathematical equation register against the canonical derivation documents.

## Next bounded action
Perform a derivation audit of the generic binary cross-flow model and close any mathematical errors before extending the equations.

## Stop condition
Do not proceed to MATLAB/DWSIM implementation, parameter optimisation, or project economics until the continuous mathematical model is closed and the relevant limiting checks pass.
