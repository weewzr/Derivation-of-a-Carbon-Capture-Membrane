# Initial Literature Findings (2026-10)

## Dense-polymer transport formulation

A 2023 review of gas-separation membrane module modelling describes the solution-diffusion model as the usual transport model for dense, nonporous polymers: sorption at the high-pressure surface, diffusion through the membrane and desorption at the low-pressure surface. For ideal-gas contacting phases it gives a flux proportional to the difference in component partial pressures. It also frames chemical potential as the thermodynamic driving force.

Source: https://www.mdpi.com/2077-0375/13/7/639

## Permeability versus permeance

For a dense selective layer, a common idealised relation is:

J_i = (P_i / l) (p_i,f - p_i,p) = Pi_i (p_i,f - p_i,p)

where:
- J_i: molar flux [mol m^-2 s^-1];
- P_i: permeability [mol m / (m^2 s Pa)] under this SI convention;
- l: selective-layer thickness [m];
- Pi_i = P_i/l: permeance [mol m^-2 s^-1 Pa^-1];
- p_i,f and p_i,p: feed- and permeate-side partial pressures [Pa].

The formula assumes a suitable linear constitutive approximation and negligible extra resistance. Thin-film composite supports, defects, non-linear sorption, concentration polarisation and non-ideal conditions may require added resistance or a different constitutive model.

Review: https://www.mdpi.com/2077-0375/13/7/639
Fundamentals review: https://pubs.acs.org/doi/10.1021/acs.macromol.7b01718

## DWSIM feasibility

DWSIM documents a Python Script Unit Operation (IronPython or Python.NET), with material and energy ports and script variables. This makes a custom membrane block plausible, subject to a prototype proving that component flows/compositions, pressure, enthalpy and solver iteration can be handled robustly.

Official API: https://dwsim.org/help/api/custom/python-script-uo.html
Scripting guide: https://dwsim.org/help/main/54-python-scripting.html

## Additional candidate membrane material evidence (not yet selected)

A 2020 paper on PIM-1@MOF thin-film composite membranes reports CO2 permeance and CO2/N2 selectivity under specified laboratory and aging conditions. It is a candidate for understanding the high-permeance/selectivity trade-off, but is not automatically transferable to the project's wet flue gas or module design.

Candidate paper details visible from publisher indexing:
Liu et al. (2020), “High-throughput CO2 capture using PIM-1@MOF based thin film composite membranes”, Chemical Engineering Journal 396, 125328.
https://doi.org/10.1016/j.cej.2020.125328

## Promotion status

These sources support the candidate physical framework only. The project has NOT yet selected a membrane material/property dataset or promoted any numerical permeability/permeance into a canonical design basis.

## Next literature actions
1. Obtain and check the original Dong et al. hybrid paper directly.
2. Confirm exact units and meanings for any 1500 GPU / selectivity 30 values previously noted.
3. Collect at least two primary membrane-material sources with test gas, RH, T, pressure, material architecture, thickness, aging and uncertainty context.
4. Determine whether data are for pure gas, mixed gas, wet gas, selective layer or whole composite membrane.
5. Preserve conflicting datasets if testing conditions differ rather than averaging them.
