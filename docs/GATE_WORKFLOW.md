# Derivation Gate Workflow

## Gate A - Physical problem and assumptions
Deliverable: scope, membrane mechanism, geometry/flow arrangement candidate, symbol/unit dictionary, open questions.
Exit criterion: all variables and physical boundaries are explicit, or unresolved items are clearly marked and the derivation is restricted accordingly.

## Gate B - Continuous transport and module mathematics
Deliverable: derivation from species conservation and constitutive transport to a closed module model with boundary conditions.
Exit criterion: equations/unknowns/conditions are well-posed for the declared module arrangement.

## Gate C - Analytical and limiting references
Deliverable: units, zero driving force, zero-area, no-separation/nonselective and constant-driving-force reference checks.
Exit criterion: equations are algebraically consistent and limiting outcomes match physical expectations.

## Gate D - Numerical specification
Deliverable: state vector, solver type, algebraic closures, residuals, admissibility conditions, tolerances, convergence plan, invalid-input behaviour.
Exit criterion: an independent programmer can implement without guessing scientific choices.

## Gate E - Independent audit
Deliverable: immutable review; finding-by-finding resolution record.
Exit criterion: all blockers closed or explicitly accepted as non-blocking with bounded claim scope.

## Gate F - MATLAB implementation
Deliverable: equation-to-code map, tests, benchmark output, mesh/step convergence, reproduction instructions.
Exit criterion: code reproduces the accepted mathematical contract; deviations are reported rather than hidden.

## Gate G - Literature benchmark and uncertainty
Deliverable: property register, matched literature/reference comparison, sensitivity and uncertainty, model-validity range.
Exit criterion: parameters have provenance and core conclusions are robust enough for the intended use.

## Gate H - HYSYS/DWSIM integration and economics
Deliverable: consistent stream contract, matched baseline, energy/cost/carbon comparison.
Exit criterion: cost per useful CO2 benefit is calculated with a declared boundary and uncertainties.

Stop after each gate.
