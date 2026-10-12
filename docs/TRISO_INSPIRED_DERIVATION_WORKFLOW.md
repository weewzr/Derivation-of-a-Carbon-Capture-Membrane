# TRISO-Inspired Mathematical Derivation Workflow

## Authority and adaptation

This workflow adapts the verified structure of `weewzr/Derivation-of-TRISO-Source-Term-Modelling`, especially:
- `docs/triso/00_consolidated_mathematical_foundation.md`;
- `docs/triso/13_canonical_equation_register.md`;
- `docs/triso/23_active_method_scope.md`;
- independent continuous-mathematics and discrete-mathematics audits.

Copy the rigor and verification gates, not the TRISO spherical PDE, eigenproblem, stochastic WOS machinery or needless complexity.

## Phase C0 - Physical problem and benchmark freeze
Define membrane class, species, transport mechanism, system boundary, geometry, coordinate, feed/permeate flow arrangement, and known versus unresolved conditions. Record a minimal generic binary benchmark separately from the future CN4119 design case.

## Phase C1 - Fundamental definitions and conservation
Begin with a finite control volume and explicitly derive:
- species inventory and accumulation;
- flux into/out of the control volume;
- local membrane-phase conservation;
- differential feed-side and permeate-side module balances.

Define all symbols, units and sign conventions.

## Phase C2 - Constitutive and thermodynamic derivation
Derive the transport chain:
chemical potential / fugacity -> membrane interface equilibrium/sorption -> diffusion through membrane -> permeability -> permeance -> component flux.

Separate conservation identities from constitutive assumptions. Never present linear sorption, constant diffusivity, ideal gas, or constant permeance as exact universal laws.

## Phase C3 - Geometry and boundary/closure derivation
State module coordinate and flow arrangement. Derive the relevant boundary conditions and local permeate closure, including the mathematical domain of admissible solutions.

The cross-flow local-permeate model is the first candidate. Co-current and counter-current arrangements are separate mathematical problems.

## Phase C4 - Continuous solution and analytical limiting cases
Before discretisation:
- derive exact zero-area and zero-driving-force limits;
- derive constant-driving-force area/flux relation;
- establish overall species balance;
- derive admissible bounds on compositions and recovery;
- investigate nonselective and pressure-ratio limits;
- identify whether a closed-form solution exists for the full coupled binary model or whether an implicit/numerical solution is required.

Do not invent a closed-form solution where none has been established.

## Phase C5 - Canonical equation register
Assign stable IDs to every consequential equation:
- MEM-GOV: conservation;
- MEM-THM: thermodynamics;
- MEM-CON: constitutive transport;
- MEM-BC: boundaries/closure;
- MEM-ANA: analytical/limiting results;
- MEM-DIS: numerical formulation;
- MEM-VER: verification;
- MEM-ECO: economic coupling.

Each record must include derivation source, assumptions, units, status, and downstream dependencies.

## Gate R1 - Independent continuous-mathematics review
A fresh reviewer checks C0-C5 without editing the author's derivation. Record findings and a separate resolution file.

Possible outcome: PASS FOR DISCRETISATION / CONDITIONAL PASS / FAIL.

Do not call the mathematical foundation independently verified before the review is actually completed.

## Phase C6 - Discrete mathematics, before code
Define unknowns, spatial/area grid, discrete component balances, nonlinear local-permeate root, admissible root interval, boundary treatment, numerical scheme, stopping conditions, and conservation residuals.

Derive the discrete scheme explicitly from the continuous equations. Do not jump straight into MATLAB code.

## Gate R2 - Independent discrete-mathematics review
Audit discretisation consistency, positivity, conservation, root uniqueness/selection, conditioning and error claims.

## Phase C7 - Verification and convergence specification
Create a hierarchy:
1. algebra and units;
2. exact limiting cases;
3. conservation;
4. admissibility/positivity;
5. analytical benchmark;
6. area-grid/step refinement;
7. literature benchmark with matched assumptions.

Code execution is not itself validation.

## Phase C8 - MATLAB / DWSIM implementation handover
Freeze:
- mathematical contract;
- parameter register;
- input/output schema;
- solver algorithm;
- acceptance tests;
- invalid-input behavior;
- example benchmark.

Friend implements independently. Record any deviations as explicit change requests.

## Phase C9 - Literature-calibrated project application
Only after verified generic math:
- insert CN4119 feed and membrane literature parameters;
- quantify enrichment, recovery, area, energy and losses;
- integrate with HYSYS downstream model;
- compare baseline and membrane cases on the same boundary;
- compute cost per useful CO2 captured/avoided with correct denominators.

## Bounded execution rule
At each phase:
1. read STATUS and canonical files;
2. perform exactly one phase;
3. update equation register and evidence;
4. record what is verified vs conditional;
5. update STATUS;
6. commit;
7. STOP.

## Derivation writing standard
For each equation:
physical purpose -> fundamental law -> intermediate algebra -> final equation -> symbols and SI units -> assumptions -> dimensional check -> limiting case -> dependency.

## Stop condition
Do not start C6 until R1 passes. Do not call C8 ready until R2 and the verification specification are complete.
