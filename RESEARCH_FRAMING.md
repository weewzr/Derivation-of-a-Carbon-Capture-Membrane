# Research Framing

## 1. Main objective
Develop the mathematical model before code implementation. The immediate deliverable is a precise equation-level specification suitable for independent MATLAB implementation.

## 2. Competing hypotheses
- H1: partial membrane pretreatment increases downstream CO2 partial pressure enough to improve capture economics.
- H2: membrane area and pressure-work costs exceed downstream savings.
- H3: partial flue-gas split / moderate recovery is economically better than processing the full feed.
- H4: wet-gas effects or realistic membrane-property variation make dry-gas literature performance overly optimistic.
- H5: the best decision is no membrane pretreatment.

## 3. Primary membrane model candidate
For a dense, nonporous polymer membrane, start with solution-diffusion:
1. chemical potential drives species transport;
2. gas sorbs into the membrane at the feed interface;
3. species diffuse through the selective layer;
4. species desorb on the permeate side;
5. permeability is the product of diffusivity and solubility under the linear model;
6. a partial-pressure driving-force law follows under the stated assumptions.

A common ideal-gas form is
[
J_i = \Pi_i(p_{i,f}-p_{i,p})
=\Pi_i(P_f x_{i,f}-P_p y_{i,p}),
]
where (\Pi_i=P_i/l) is permeance, not permeability. This is not universally valid: nonideal fugacity, concentration-dependent sorption, support resistance, defects, polarisation, and wet-gas effects may require extensions.

## 4. First-principles module balances
For a differential membrane area (dA), with feed/retentate flow moving in the increasing coordinate and permeate leaving the feed side,
[
\frac{dF_{i,r}}{dA}=-J_i.
]
The permeate-side composition and pressure must be closed consistently with a selected module arrangement (e.g. cross-flow/local permeate composition, counter-current, co-current, or well-mixed permeate plenum). The module geometry is part of the mathematical boundary-value problem and cannot be omitted.

For a local permeate stream with differential accumulation,
[
dF_{i,p}=J_i,dA
]
is a component transfer balance, but how transferred material is routed/mixed depends on the module model. Do not set (y_{i,p}) equal to a constant unless a well-mixed permeate assumption is explicitly chosen.

## 5. Performance definitions
Given feed CO2 molar flow (F_{mathrm{CO2},f}), permeate CO2 flow (F_{mathrm{CO2},p}), and total permeate flow (F_p):
- recovery (R_{mathrm{CO2}}=F_{mathrm{CO2},p}/F_{mathrm{CO2},f});
- enrichment (E_{mathrm{CO2}}=y_{mathrm{CO2},p}/x_{mathrm{CO2},f});
- stage cut (\theta=F_p/F_f);
- permeate purity (y_{mathrm{CO2},p}=F_{mathrm{CO2},p}/F_p).

Recovery, purity, enrichment and stage cut are different quantities.

## 6. Physical boundary and integration
The membrane model's outlet streams go to a broader downstream capture comparison. Cost benefit must compare the baseline and membrane cases under the same system boundary and product/abatement objective.

## 7. Verification before implementation handoff
At minimum:
- unit/dimensional checks;
- zero driving force gives zero flux;
- zero membrane area gives unchanged feed;
- component balance closes;
- nonselective membrane limit behaves consistently;
- single-species constant-driving-force solution;
- grid/refinement sensitivity for discretised module equations;
- comparison with one literature benchmark using matched assumptions.

## 8. Literature protocol
All numerical membrane inputs must record material, test mixture, humidity, temperature, feed/permeate pressure, thickness, permeance/permeability basis, selectivity definition, conditioning/aging, and uncertainty if reported.

The 2020 Dong et al. hybrid study is a candidate systems benchmark, not a universal source of membrane properties. Exact values must be checked against the paper and its stated modelling basis before promotion into the canonical register.

## 9. Open decisions
- exact CN4119 conditions and actual flue gas basis;
- membrane material/type;
- module flow arrangement;
- feed/permeate pressures and pressure-drop assumptions;
- water phase and wet/dry basis;
- downstream capture performance link;
- cost basis and economic objective.

