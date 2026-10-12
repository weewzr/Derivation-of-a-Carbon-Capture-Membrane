# Review 01 Main Research Resolution Record

Independent review: reviews/INDEPENDENT_CONTINUOUS_MATHEMATICS_REVIEW_01.md
Original decision: FAIL - REMEDIATION REQUIRED.
This resolution is authored by Main Research and does not change the original immutable review.

| Finding | Main Research action | Evidence | Status |
|---|---|---|---|
| IMR01-B01 | Defined local collectors and derived local composition by differential control volume | docs/06 | REMEDIATED - REVIEW PENDING |
| IMR01-M01 | Derived explicit g'=-alpha*r*(1-r)/D^2 and bracket endpoint proof | docs/06 | REMEDIATED - REVIEW PENDING |
| IMR01-M02 | Added depletion, positivity, bounded target search and stop statuses | verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md | REMEDIATED - REVIEW PENDING |
| IMR01-M03 | Registered MEM-SOL-001 to 014 | docs/CANONICAL_EQUATION_REGISTER.md | REMEDIATED - LEDGER SYNCHRONIZED; REVIEW PENDING |
| IMR01-M04 | Added chemical-potential, constitutive mobility and Henry sorption chain | docs/07 | REMEDIATED - REVIEW PENDING |
| IMR01-M05 | Explained why no independent permeate-channel state exists for local collectors | docs/06 | REMEDIATED - REVIEW PENDING |
| IMR01-D01 | Added proposed numerical tolerances and acceptance cases | verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md | REMEDIATED - NOT EXECUTED |
| IMR01-D02 | Added synthetic tests and separately prescribed constant-driving-force reference | verification/REVIEW01_NUMERICAL_ACCEPTANCE_CONTRACT.md | REMEDIATED - NOT EXECUTED |
| IMR01-D03 | Explicit feed IVP and prescribed permeate pressure, no permeate composition BC | docs/06 | REMEDIATED - REVIEW PENDING |
| IMR01-N01 | Polynomial c2/c1/c0 notation | docs/06 | REMEDIATED - REVIEW PENDING |
| IMR01-N02 | Canonical H residual avoids zero-flux divisions | docs/06 | REMEDIATED - REVIEW PENDING |
| IMR01-N03 | No project data yet | STATUS.md | OPEN AS INPUT DEPENDENCY |

## Remaining work
1. Derivation ledger and docs/01-05 now cross-reference corrective evidence; the older proof remains visible but explicitly superseded.
2. Obtain independent re-review of the corrected mathematical contract.
3. Execute numerical tests during implementation. Specified tolerances are not evidence of passing tests.
4. Select realistic membrane module and literature properties before project-specific claims.

## Gate
No PASS FOR IMPLEMENTATION is claimed yet. All independent findings remain open until independent reviewer acceptance.
