# Project Brief

## Working title
First-Principles 1-D CO2 Membrane Pretreatment / Pre-Concentration Model

## Course / context
CN4119.

## Primary research question
Can a literature-grounded CO2-selective membrane pretreatment step increase the useful CO2 concentration entering downstream capture enough to reduce the integrated system's cost per tonne of CO2 avoided/captured, after accounting for CO2 losses, membrane area and pressure-related energy?

## Intended split of responsibilities
- Research/derivation: establish physical assumptions, derive governing equations, collect literature inputs, define mathematical boundary conditions and verification cases.
- MATLAB implementation: friend implements the signed-off equations and returns reproducible results and test evidence.
- Process integration: use DWSIM for the custom membrane block if practical, and Aspen HYSYS for upstream/downstream plant simulation. Initial exchange can be offline stream-data transfer rather than real-time coupling.

## Initial process concept
Flue gas near 80 degC -> direct-contact cooling to approximately 40 degC -> blower / pressure conditioning -> membrane pretreatment -> CO2-enriched and CO2-depleted streams -> downstream capture boundary.

This is provisional pending the uploaded CN4119 specifications.

## Main deliverables
1. First-principles derivation.
2. Literature/source and parameter registers.
3. A mathematically complete MATLAB handoff specification.
4. Verification plan and reference cases.
5. Separation metrics: composition, recovery, enrichment and stage cut.
6. Membrane sizing: area and flux.
7. Energy: blower/compression/vacuum penalties as applicable.
8. Incremental economics relative to a consistent no-membrane baseline.
9. Sensitivity and uncertainty analysis.
10. Transferable DWSIM custom-unit-operation requirements.

## Explicit falsification requirements
The membrane option may be rejected if:
- the selected membrane's wet-flue-gas performance is inadequate;
- CO2 losses to the wrong outlet erase the benefit;
- required area/capital is excessive;
- pressure/vacuum work offsets the capture benefit;
- the downstream capture process does not achieve a real cost/performance improvement;
- credible uncertainty ranges reverse the preferred decision.

## Initial modelling constraint
Begin with a steady-state, isothermal, one-dimensional module model only if the selected membrane and expected operating window justify it. Add stages, non-isothermal behaviour, wet competitive sorption, pressure drops or polarisation only when evidence shows they are consequential.

## Current unknowns
Exact feed composition/flow, operating pressure, membrane chemistry and architecture, layer thickness/permeance basis, downstream capture boundary, equipment costs, power prices and annual operating basis remain to be confirmed from project specifications and literature.
