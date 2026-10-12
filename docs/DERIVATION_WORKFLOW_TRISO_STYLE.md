# Mathematical Derivation Workflow - Adapted from TRISO Project

## Purpose
Use the proven workflow discipline of the TRISO mathematical project while adapting the mathematics to gas-membrane transport. This is a process contract; it does not imply the physical models or equations are the same.

## Core sequence

**raw starting material -> canonical physical problem -> conservation -> constitutive law -> governing equations -> boundary/interface conditions -> continuous/module solution -> numerical formulation -> implementation handoff -> verification -> independent review**

For this membrane project, the derivation stages are:

### M0 - Preserve sources and establish the physical problem
- Keep supplied assignment/specifications and original notes as raw evidence.
- Record source, version/date, units and any ambiguity.
- Define the membrane/module physical question and intended output.
- Maintain an assumption register; mark unknowns as unknown rather than choosing silently.

### M1 - Define variables, units and sign conventions
Freeze symbol definitions and units before derivation. Define feed-side/permeate-side, component flux direction, area coordinate, partial-pressure notation, total/component molar flows, composition definitions and membrane thickness/permeance notation.

### M2 - Derive component conservation from a differential control volume
Begin with species accumulation = inflow - outflow + transfer/source.
Derive the feed-side/retentate component balance over an element dA. Derive the permeate balance appropriate to the selected module architecture. Do not jump straight to a familiar ODE.

### M3 - Derive the constitutive transport relation
Start from chemical potential as the thermodynamic driving force. State the chosen membrane transport mechanism. For dense polymer solution-diffusion, derive the linear partial-pressure relation from sorption and diffusion assumptions. Distinguish:
- diffusivity in the membrane;
- solubility/sorption coefficient;
- permeability;
- selective-layer thickness;
- permeance.

If non-linear sorption, facilitated transport, defects, support resistance, concentration polarisation or non-ideal fugacity is relevant, record it as a justified extension rather than silently mixing models.

### M4 - Derive gas-mixture closure
Derive ideal partial pressures or use fugacity where needed. Derive mole fractions from component flow rates. Do not hold composition or total flow constant when the balances say they change.

### M5 - Specify module architecture and close the system
Choose cross-flow, co-current, counter-current or well-mixed permeate plenum. Define how permeate composition at each location is determined. State unknowns, equations and boundary conditions and show that the system is neither under- nor over-specified.

### M6 - Derive performance observables
Derive total flows, component balances, permeate/retentate compositions, CO2 recovery, purity, enrichment, stage cut, and loss fractions. Do not call enrichment capture or avoided emissions.

### M7 - Derive the analytical/limiting reference
Before complex numerical implementation, solve one simple case analytically (e.g. constant driving force and constant permeance) and specify limiting cases. This becomes a mathematical reference.

### M8 - Derive the numerical representation
Only after the continuous model is explicit, convert it into a discretised ODE/BVP/algebraic formulation. State sign conventions, solver variables, step/mesh controls, convergence criteria and invalid-domain handling.

### M9 - Map equations to implementation
Create an equation-to-code table for MATLAB first, then DWSIM custom-unit mapping if used. Implementation must not redefine the physics silently.

### M10 - Verify and reconcile
Verify units, zero driving force, zero area, species/total balance, admissibility, limiting cases, analytical reference and numerical convergence. Preserve the raw test evidence.

### M11 - Independent mathematical review
A reviewer reads the frozen derivation and equation register independently, then records immutable findings. Main research resolves only evidence-backed findings and preserves the audit/reconciliation.

### M12 - Literature calibration and application
Only after the mathematical model and verification tests are in place, promote literature parameter sets and actual CN4119 conditions. Compare matched literature benchmarks, quantify sensitivity/uncertainty and proceed to integrated economics.

## Canonical derivation document rule
There should be one continuous canonical derivation path. Preserve original materials as raw inputs; do not overwrite them. Give every displayed governing, boundary, constitutive, numerical and result equation a stable ID. Maintain a canonical equation register mapping equation ID to derivation section, status, assumptions, units and downstream use.

## Equation status labels
Use:
- EXACT/IDENTITY: follows by algebra/definition under stated domain;
- CONSERVATION: follows from a control-volume balance;
- CONSTITUTIVE: selected physical transport/property law;
- ASSUMPTION: simplification chosen for this model;
- DERIVED: mathematical result from listed equations;
- LITERATURE INPUT: source-supplied parameter;
- UNVERIFIED: no adequate independent check yet;
- VERIFIED FOR [specific scope]: evidence exists for the stated benchmark only;
- OPEN: incomplete derivation or evidence.

Do not use VERIFIED without a named scope.

## Review gates
- Gate A: physical definition/assumptions frozen.
- Gate B: continuous derivation complete through a closed module model.
- Gate C: analytical and limiting references pass.
- Gate D: numerical mathematical specification complete.
- Gate E: independent mathematical audit reconciled.
- Gate F: MATLAB implementation verified against the mathematical contract.
- Gate G: matched literature case and sensitivity evidence accepted.
- Gate H: DWSIM/HYSYS coupling and economic interpretation.

## End-of-phase report
GATE:
STARTING COMMIT:
FILES CHANGED:
EQUATION IDs ADDED/CHANGED:
DERIVATIONS COMPLETED:
ASSUMPTIONS CHANGED?:
PARAMETERS PROMOTED?:
INDEPENDENT CHECKS:
OPEN FINDINGS:
NEXT SINGLE ACTION:
STOPPED: YES

## Scope rule
Do not automatically begin the next gate. Derive only as far as needed to make the selected mathematical object unambiguous, verify it, record state, and stop.
