# Canonical Equation Register

This is the single authoritative equation ID register for the membrane derivation. Equation IDs are stable and should not be recycled.

| ID | Description | Equation/document | Class | Units checked? | Independent check | Status | Dependencies / use |
|---|---|---|---|---|---|---|---|
| MEM-GOV-001 | General species conservation | 01 transport derivation | CONSERVATION | YES | Control-volume balance | VERIFIED FOR GENERAL BALANCE | Constitutive model |
| MEM-GOV-002 | Steady nonreactive membrane continuity | 01 transport derivation | DERIVED | YES | Steady local balance | CANDIDATE | Flux derivation |
| MEM-CON-001 | Fickian membrane transport | 01 transport derivation | CONSTITUTIVE | YES | Sign/dimensions | ASSUMPTION-DEPENDENT | Surface concentrations |
| MEM-CON-002 | Linear sorption | 01 transport derivation | CONSTITUTIVE | YES | Material-model evidence | ASSUMPTION-DEPENDENT | Partial pressure |
| MEM-FLX-001 | Solution-diffusion flux relation | 01 transport derivation | DERIVED UNDER ASSUMPTIONS | YES | Zero driving-force limit | CANDIDATE | Module balances |
| MEM-FLX-002 | Ideal-gas partial-pressure form | 01 transport derivation | DERIVED UNDER ASSUMPTIONS | YES | Mole-fraction/pressure check | CANDIDATE | Module balances |
| MEM-BIN-001 | CO2 feed-side component balance | 02 binary cross-flow model | CONSERVATION | YES | Integral balance | CANDIDATE | ODE model |
| MEM-BIN-002 | N2 feed-side component balance | 02 binary cross-flow model | CONSERVATION | YES | Integral balance | CANDIDATE | ODE model |
| MEM-BIN-003 | Local cross-flow permeate closure | 02 binary cross-flow model | MODEL CLOSURE | YES | Architecture check | CANDIDATE / REVIEW REQUIRED | ODE model |
| MEM-PERF-001 | CO2 recovery definition | 02 binary cross-flow model | DEFINITION | YES | Bounds | CANDIDATE | Result reporting |
| MEM-PERF-002 | CO2 enrichment factor | 02 binary cross-flow model | DEFINITION | YES | Composition check | CANDIDATE | Result reporting |
| MEM-PERF-003 | Stage cut | 02 binary cross-flow model | DEFINITION | YES | Total balance | CANDIDATE | Result reporting |

## Register rules
1. The register is canonical; use IDs rather than inventing alternate IDs.
2. If a derivation changes, preserve the old status/history and record the change.
3. Each equation must state symbols, units, domain and assumptions in its source document.
4. "Verified" names the exact scope/benchmark; it never means all possible membranes or operating conditions.
5. External source equations should have a citation and must be distinguished from equations derived in this project.
6. Add each new equation when it is created, not retrospectively at manuscript time.

## Review 01 reconciliation additions (candidate, not independently verified)

| ID | Description | Source | Class | Status |
|---|---|---|---|---|
| MEM-SOL-001 | Retentate CO2 composition | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-002 | Dimensionless CO2 driving force | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-003 | Dimensionless N2 driving force | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-004 | Local permeate composition closure | docs/05 and docs/06 | IDEALISED COLLECTOR BALANCE | REVIEW PENDING |
| MEM-SOL-005 | Dimensionless CO2 retentate ODE | docs/05 | CONSERVATION + CONSTITUTIVE | REVIEW PENDING |
| MEM-SOL-006 | Dimensionless N2 retentate ODE | docs/05 | CONSERVATION + CONSTITUTIVE | REVIEW PENDING |
| MEM-SOL-007 | Feed-inlet initial conditions | docs/05 | DESIGN/INPUT | CANDIDATE |
| MEM-SOL-008 | Canonical closure residual H | docs/05 and docs/06 | DERIVED | REVIEW PENDING |
| MEM-SOL-009 | Admissible root interval | docs/05 and docs/06 | DERIVED UNDER ONE-WAY FLUX | REVIEW PENDING |
| MEM-SOL-010 | Stage cut | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-011 | CO2 recovery | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-012 | Collected permeate CO2 fraction | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-013 | Retentate CO2 fraction | docs/05 | DEFINITION | CANDIDATE |
| MEM-SOL-014 | Physical area recovery | docs/05 | DIMENSIONAL IDENTITY | CANDIDATE |

The main-research corrections in docs/06, docs/07 and verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md remain subject to independent review. Earlier VERIFIED labels in the pre-review register should not be interpreted as Review 01 closure.
