# STATUS

## Current state
Repository initialized for a first-principles, implementation-independent CO2 membrane pretreatment model. The mathematical plan, boundary-condition contract, derivation ledger, literature register, economic metrics and MATLAB handoff specification exist.

## Current gate
G0-G1: recover actual CN4119 specifications and complete the evidence/property basis.

## Canonical files
- `PROJECT_BRIEF.md`
- `RESEARCH_FRAMING.md`
- `docs/MATHEMATICAL_DERIVATION_PLAN.md`
- `docs/INITIAL_CONDITIONS_AND_BOUNDARIES.md`
- `docs/DERIVATION_LEDGER.md`
- `docs/MATLAB_HANDOFF_SPECIFICATION.md`
- `docs/ECONOMIC_METRICS.md`
- `docs/LITERATURE_FINDINGS_2026-10.md`
- `literature/LITERATURE_AND_PARAMETER_REGISTER.md`

## Current scientific position
A dense-polymer solution-diffusion membrane is the candidate starting model, conditional on confirming membrane type and operating conditions. The commonly used partial-pressure flux law is valid only under stated constitutive and gas-phase assumptions. It is not yet a final project equation set because the module flow arrangement and boundary conditions must be selected.

## Open blockers
- Actual CN4119 feed composition, flow, temperature, pressure and wet/dry basis.
- Membrane material/class and selective-layer/module architecture.
- Membrane permeance/selectivity data measured under sufficiently relevant conditions.
- Module arrangement and permeate-side boundary closure.
- Downstream HYSYS capture performance interface and economic comparison boundary.

## Next action
Upload source specifications to `attachments/`. Then inventory the inputs, verify literature data from primary sources, choose a matched benchmark, and finish the equation derivation before writing implementation code.

## Stop condition
Do not optimise or claim a preferred design until the feed basis, membrane class, module equations and baseline are frozen and verified.
