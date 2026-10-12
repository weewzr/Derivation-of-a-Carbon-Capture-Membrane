# STATUS

## Current state
Repository initialized for a first-principles, implementation-independent membrane model. Mathematical contract and MATLAB handoff documents are in place. Initial membrane-transport and DWSIM implementation sources have been recorded.

## Current gate
G0-G1: recover actual CN4119 specifications and complete the literature/property register.

## Canonical current files
- `PROJECT_BRIEF.md`
- `RESEARCH_FRAMING.md`
- `docs/MATHEMATICAL_DERIVATION_PLAN.md`
- `docs/DERIVATION_LEDGER.md`
- `docs/INITIAL_CONDITIONS_AND_BOUNDARIES.md`
- `docs/MATLAB_HANDOFF_SPECIFICATION.md`
- `docs/ECONOMIC_METRICS.md`
- `literature/LITERATURE_AND_PARAMETER_REGISTER.md`
- `docs/LITERATURE_FINDINGS_2026-10.md`

## Current scientific position
A dense-polymer solution-diffusion membrane is the candidate starting model, conditional on confirming material type and realistic operating conditions. The idealised partial-pressure flux relation is literature-standard under stated assumptions, but the module configuration and property basis are not yet frozen.

## Open blockers
- Actual CN4119 feed composition, flow, temperature, pressure and wet/dry basis.
- Membrane material/class and selective-layer/module architecture.
- Membrane permeance/selectivity data with matching test conditions.
- Module arrangement and permeate-side boundary model.
- Downstream HYSYS capture performance interface and economic boundary.

## Next action
Upload source specifications to `attachments/`. Then produce the parameter register and select a matched membrane benchmark before the complete derivation is promoted to canonical.

## Stop condition
No optimisation or final base-case result until the feed, membrane class and module boundary conditions are frozen.
