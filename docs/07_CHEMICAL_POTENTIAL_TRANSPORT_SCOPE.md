# Chemical Potential and Solution-Diffusion: Thermodynamic Scope

Status: derivation supplement, pending independent review. Addresses IMR01-M04. The thermodynamic driving-force argument is distinguished from the constitutive mobility and sorption assumptions.

## 1. Chemical potential
For species i at temperature T, chemical potential is mu_i=mu_i^standard+RT ln(f_i/f^standard). At fixed T, dmu_i=RT d ln f_i. For an ideal gas, f_i=p_i.

## 2. Transport in membrane
Under an isothermal local-equilibrium, linear nonequilibrium transport approximation, a species flux relative to a stationary membrane matrix can be represented as:
J_i=-(D_i c_i/(RT)) dmu_i^m/dxi,
where xi is the membrane thickness coordinate and D_i is a constitutive mobility-related diffusion coefficient. This relation is an assumption of a specific transport law, not a consequence of conservation alone.

If the membrane phase is locally ideal in the relevant concentration range:
dmu_i^m=RT d ln c_i,
and hence:
J_i=-D_i dc_i/dxi.

Nonideal sorption/activity and concentration-dependent D_i require a generalized formulation; this simplified reduction is not universal.

## 3. Interface equilibrium
At each gas/membrane interface, local thermodynamic equilibrium gives mu_i^gas=mu_i^membrane. A material-specific sorption isotherm then relates membrane concentration to contacting gas fugacity. In the Henry-linear limit:
c_i^m=S_i f_i.
For ideal gas, f_i=p_i. The coefficient S_i is empirical and must be measured or sourced.

## 4. Integration
Assume steady one-dimensional membrane transport, no reaction, constant D_i, uniform layer thickness ell, and identical linear sorption coefficient S_i at the two faces.

Conservation gives dJ_i/dxi=0.
Using J_i=-D_i dc_i/dxi:
J_i=(D_i/ell)(c_i,f^m-c_i,p^m)
   =(D_i*S_i/ell)(f_i,f-f_i,p).

Define permeability P_i=D_i S_i and permeance Pi_i=P_i/ell:
J_i=Pi_i(f_i,f-f_i,p).

For ideal gas:
J_i=Pi_i(P_f x_i-P_p y_i).

## 5. Units
[mu]=J/mol; [RT]=J/mol; [D_i c_i/(RT) * dmu/dxi]=m2/s * mol/m3 / (J/mol) * (J/mol)/m = mol/(m2 s).
[S_i]=mol/(m3 Pa); [Pi_i]=mol/(m2 s Pa).

## 6. Important limitations
- A chemical-potential gradient is a thermodynamic driving force, but the linear mobility law and ideal membrane activity relation are constitutive assumptions.
- Membrane-phase ideality and linear sorption are not universal for CO2/polymer systems.
- Mixture coupling, facilitated transport, plasticization, humidity, support resistance and concentration polarization are omitted.
- No claim is made that the membrane permeability or selectivity is calculable from conservation laws alone.
- The fugacity form requires consistent gas/membrane equilibrium and material calibration; simply substituting fugacity into a dry-gas permeance law may not be valid without supporting evidence.
