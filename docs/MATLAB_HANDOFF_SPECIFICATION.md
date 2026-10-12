# MATLAB Handoff Specification

## Purpose
This document defines what must be delivered before MATLAB coding is considered ready. It is not a code specification until the physical configuration and equations are frozen.

## Required sections
1. Mathematical model purpose and domain.
2. Diagram of module flow arrangement.
3. Species list and component ordering.
4. Assumption register with rationale and validity range.
5. Governing equations and derivation references.
6. State/unknown vector and coordinate.
7. Flux sign convention.
8. Initial and boundary conditions.
9. Parameter table: symbol, meaning, unit, value, class, source.
10. Solver formulation (ODE, BVP, algebraic/ODE coupling) and numerical method.
11. Output definitions and units.
12. Failure/invalid-input behavior.
13. Verification tests with expected limiting behaviours.
14. One matched literature/reference case.
15. Reproduction command/environment/versioning.

## Required outputs
- component molar flow rates along the module;
- total feed/retentate/permeate flows;
- local compositions and partial pressures/fugacities;
- component fluxes;
- CO2 recovery, purity, enrichment and stage cut;
- membrane area / area required for a declared target;
- component balance residuals;
- error/convergence evidence;
- assumptions and unsupported domains.

## Minimum tests
- zero transmembrane driving force -> zero component flux;
- zero membrane area -> outlet equals inlet within numerical tolerance;
- integrated component transfer matches feed/permeate balance;
- no negative component flows;
- mole fractions remain in [0,1] and sum to one;
- non-selective limit does not spuriously create selectivity;
- analytical limiting case agrees to declared tolerance;
- results converge under mesh refinement.

Do not hand over the model until these are defined, even if implementation can begin on a separate prototype branch.
