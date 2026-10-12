# First-Principles Derivation Ledger

This ledger tracks *main-research derivation status*, not independent-review closure. The original independent Review 01 remains FAIL pending re-review.

| ID | Mathematical object | Canonical evidence | Assumption / dependency | Main research status | Independent status |
|---|---|---|---|---|---|
| DER-001 | Chemical-potential driving force | docs/07 | isothermal chemical potentials, mobility law | DERIVED CONDITIONALLY | RE-REVIEW PENDING |
| DER-002 | Membrane-interface sorption | docs/01, docs/07 | local equilibrium, Henry-linear sorption | DERIVED CONDITIONALLY | RE-REVIEW PENDING |
| DER-003 | Through-layer diffusion | docs/01, docs/07 | steady, homogeneous constant D | DERIVED CONDITIONALLY | REVIEW 01 ACCEPTED ALGEBRA |
| DER-004 | Permeability and permeance | docs/01 | P=DS, Pi=P/ell | DERIVED CONDITIONALLY | REVIEW 01 ACCEPTED ALGEBRA |
| DER-005 | Gas partial-pressure flux law | docs/01, docs/07 | ideal gas and linear sorption | DERIVED CONDITIONALLY | RE-REVIEW PENDING |
| DER-006 | Retentate component balances | docs/02 | steady local area control volume | DERIVED | REVIEW 01 ACCEPTED ALGEBRA |
| DER-007 | Total-flow/composition identities | docs/02, docs/05 | F>0 | DERIVED | REVIEW 01 ACCEPTED ALGEBRA |
| DER-008 | Local permeate collector closure | docs/06 | ideal local withdrawal, no axial permeate mixing | DERIVED FOR IDEALISED GEOMETRY | BLOCKER RE-REVIEW PENDING |
| DER-009 | Purity, recovery, enrichment, stage cut | docs/02, docs/05 | nonzero denominator where required | DERIVED | REVIEW 01 ACCEPTED DEFINITIONS |
| DER-010 | Area scaling and sizing | docs/04, docs/05 | fixed pressure, constant permeance | DERIVED CONDITIONALLY | REVIEW 01 ACCEPTED SCALING |
| DER-011 | Local admissible root and uniqueness | docs/06 | 0<x<1, 0<=r<1, alpha>0 | REVISED PROOF | MAJOR RE-REVIEW PENDING |
| DER-012 | Analytical limiting cases | docs/03, verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md | r=0 or alpha=1 | DERIVED, TESTS NOT EXECUTED | REVIEW 01 ACCEPTED IDENTITIES |
| DER-013 | Solver stopping and target recovery | verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md | chosen numerical tolerances/area cap | SPECIFIED, NOT EXECUTED | MAJOR RE-REVIEW PENDING |
| DER-014 | Numerical convergence | verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md | solver implementation needed | PLANNED | NOT TESTED |
| DER-015 | Literature-calibrated model | literature/LITERATURE_AND_PARAMETER_REGISTER.md | actual CN4119 data/material | OPEN | NOT REVIEWED |

## Equation documentation rule
For each consequential equation state physical purpose, starting principle, algebra, symbols/SI units, assumptions, dimensional and limiting checks, and review status.

## Source-of-truth precedence
The consolidated correction contract (docs/06 and docs/07 plus verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md) takes precedence over superseded proof/solver wording in docs/01-05 until those documents are revised. This does not mean independent acceptance.
