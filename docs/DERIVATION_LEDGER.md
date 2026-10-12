# First-Principles Derivation Ledger

Use this file to record each derivation step and its status. It is not a place to mark equations complete merely because they look familiar.

| ID | Result to derive | Starting principle | Assumptions needed | Independent check | Status |
|---|---|---|---|---|---|
| DER-001 | Chemical-potential driving force | Thermodynamics | State equation/fugacity choice | Units and equilibrium limit | PLANNED |
| DER-002 | Sorption at membrane surfaces | Constitutive/interface relation | Linear or chosen sorption model | Interface limit | PLANNED |
| DER-003 | Diffusive transport through selective layer | Fick/chemical-potential transport | Homogeneous layer, steady or specified transient | Dimensions and sign | PLANNED |
| DER-004 | Permeability = diffusivity x solubility | Solution-diffusion constitutive model | Linear sorption and constant properties | Unit consistency | PLANNED |
| DER-005 | Partial-pressure flux law | Previous steps | Ideal gas/linear permeability and stated thickness | Zero driving force | PLANNED |
| DER-006 | Feed-side differential component balance | Conservation of species | Steady module; sign/area convention | Integrated mass balance | PLANNED |
| DER-007 | Total flow and composition equations | Definitions (F=\sum_iF_i, x_i=F_i/F) | Defined stream path | Mole fractions sum to one | PLANNED |
| DER-008 | Permeate closure for selected module arrangement | Component conservation | Chosen flow arrangement | Whole-module species balance | PLANNED |
| DER-009 | Recovery, purity, enrichment, stage cut | Definitions | Explicit reference streams | Bounds and consistency | PLANNED |
| DER-010 | Area sizing/design equation | Flux + balances | Target/known design variable | Analytical limiting case | PLANNED |

## Required derivation format

For every equation:
1. physical purpose;
2. starting principle;
3. algebraic derivation;
4. symbols and SI units;
5. assumptions/domain;
6. numerical inputs/provenance if evaluated;
7. dimensional check;
8. limiting-case check;
9. status and independent review.
