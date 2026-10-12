# Mathematical Derivation Plan

## M0 - Freeze the intended physical model
Confirm gas components, membrane type, selective-layer model, feed/permeate pressure arrangement, module geometry, thermal assumption, stage cut, and whether feed-side pressure drop is modelled.

## M1 - Species transport from first principles
For dense polymer solution-diffusion:
1. chemical potential: (\mu_i=\mu_i^\circ+RT\ln f_i);
2. sorption equilibrium at membrane surfaces;
3. chemical-potential gradient drives transport;
4. derive an appropriate flux expression from the constitutive law;
5. under suitable ideal-gas, linear-sorption and constant-property assumptions, obtain (J_i=\Pi_i(f_{i,f}-f_{i,p})\) or its partial-pressure approximation;
6. make clear (P_i\) is permeability and (\Pi_i=P_i/l\) is permeance.

The exact derivation and notation must be made internally consistent; don't mix permeability and permeance.

## M2 - Differential module conservation
Choose coordinate and module arrangement explicitly. Apply conservation to a differential membrane element:
[
\text{accumulation} = \text{in} - \text{out} + \text{transfer}.
]
For the feed/retentate side with area coordinate (A):
[
dF_{i,r}/dA=-J_i.
]
Derive corresponding total-flow and composition relations from (F_r=\sum_iF_{i,r}), (x_i=F_i/F_r), rather than assuming total flow or composition constant.

Close the permeate composition using the chosen module arrangement. Counter-current modelling may require a boundary-value problem; cross-flow or well-mixed assumptions yield different equations. State exactly which one is used.

## M3 - Gas mixture and pressure relations
Define:
[
p_i=y_iP
]
for ideal gas, or fugacity (f_i=\phi_i y_iP) if a nonideal model is justified. State wet/dry basis and water treatment. Add pressure-drop equations only when parameters/correlations are available.

## M4 - Boundary conditions
Specify inlet feed component flows, feed pressure and temperature; permeate boundary/plenum pressure or outlet condition; module length/area; and any stage-cut/design condition. Avoid over-specifying an ODE or leaving a boundary-value problem under-specified.

## M5 - Performance equations
Derive flow, composition, recovery, purity, enrichment, stage cut, CO2 losses and component-balance closure.

## M6 - Area sizing
Integrate local flux over area or solve the coupled differential model for the area that achieves a specified design target. State the target and don't confuse a specified area with a computed area.

## M7 - Energy and economics interfaces
Calculate pressure-system duties from a declared compression/vacuum architecture. Develop cost comparison after material/energy balance closes.

## M8 - Verification cases
- dimensions;
- zero driving force;
- zero area;
- component and total balance;
- limiting nonselective/selective cases;
- constant-flux or constant-driving-force analytical case;
- mesh/refinement tests;
- literature benchmark.

## Handoff rule
The MATLAB specification freezes equations, signs, coordinates, unknowns, boundary conditions, parameter units, numerical scheme and acceptance tests. Implementation must report where it deviates.
