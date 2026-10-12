# Project Agent Instructions

## Recover current state before work
Read:
1. `STATUS.md`
2. `PROJECT_BRIEF.md`
3. `RESEARCH_FRAMING.md`
4. `docs/MATHEMATICAL_DERIVATION_PLAN.md`
5. `docs/DERIVATION_LEDGER.md`
6. `literature/LITERATURE_AND_PARAMETER_REGISTER.md`
7. attached specifications and unresolved decisions.

## Scientific objective
Derive a model the user can independently hand off to MATLAB/DWSIM implementation. Do not jump directly to code or generic simulation.

## Hard rules
- The equations must follow from stated principles and assumptions.
- The membrane constitutive relation and module architecture must be justified.
- Distinguish permeability from permeance, recovery from purity, concentration from recovery, and separated CO2 from avoided CO2.
- Never treat provisional literature values as final project values.
- Never invent CN4119 conditions not present in source files.
- Preserve contradictory literature and uncertainty.
- Do not optimise before a frozen base model exists.
- Do not start CFD unless a later evidence-based requirement justifies it.
- Work one bounded gate at a time, update STATUS, then STOP.

## Phase output
Report:
GATE:
STARTING COMMIT:
FILES CHANGED:
DERIVATIONS COMPLETED:
PARAMETERS PROMOTED:
VERIFICATION:
OPEN ISSUES:
NEXT SINGLE ACTION:
STOPPED: YES
