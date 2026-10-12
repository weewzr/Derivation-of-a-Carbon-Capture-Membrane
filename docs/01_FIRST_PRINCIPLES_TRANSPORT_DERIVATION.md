> **Review 01 reconciliation:** This derivation is valid conditionally under Fickian membrane transport and linear sorption. It does not by itself derive the mobility law from conservation. For the separate chemical-potential/constitutive argument and its limitations, see [07_CHEMICAL_POTENTIAL_TRANSPORT_SCOPE.md](07_CHEMICAL_POTENTIAL_TRANSPORT_SCOPE.md). Independent acceptance is pending.

# 01 - First-Principles Membrane Transport Derivation

## Status
CANDIDATE DERIVATION - not yet independently reviewed; membrane material and CN4119 feed basis not frozen.

## 1. Physical problem
A dense nonporous selective layer separates a flue-gas feed from a lower-partial-pressure permeate side. Species i sorbs at the feed interface, diffuses through a selective layer of thickness l, and desorbs at the permeate interface.

Let x be distance through the selective layer, increasing from feed (x=0) to permeate (x=l).

## 2. Conservation
For species concentration c_i(x,t) within the membrane [mol/m^3] and flux J_i [mol/(m^2 s)]:

d(c_i)/dt + div(J_i) = R_i.

For one-dimensional, steady, nonreactive transport:

dJ_i/dx = 0.

Thus J_i is constant across the selective layer under the stated assumptions.

## 3. Constitutive transport law
Assume Fickian transport in the membrane:

J_i = -D_i dc_i/dx,

where D_i [m^2/s] is the membrane-phase diffusivity, not the gas diffusivity.

With constant D_i:

integral from x=0 to l of J_i dx = -D_i integral from c_i,f^m to c_i,p^m of dc_i.

Therefore:

J_i l = D_i (c_i,f^m - c_i,p^m)

and

J_i = (D_i/l)(c_i,f^m - c_i,p^m).

## 4. Membrane-surface sorption
For linear sorption at each interface:

c_i,f^m = S_i p_i,f
c_i,p^m = S_i p_i,p

where S_i [mol/(m^3 Pa)] is the membrane-phase solubility coefficient and p_i [Pa] is the gas-phase component partial pressure at the membrane surface.

Substitute:

J_i = (D_i S_i/l)(p_i,f - p_i,p).

Define permeability:

P_i = D_i S_i [mol/(m s Pa)]

and permeance:

Pi_i = P_i/l [mol/(m^2 s Pa)].

Hence:

**J_i = Pi_i (p_i,f - p_i,p).**

## 5. Ideal gas contacting phases
Under ideal gas mixture assumptions:

p_i,f = x_i,f P_f
p_i,p = y_i,p P_p

where x_i,f and y_i,p are local feed-side and permeate-side mole fractions. Thus:

**J_i = Pi_i (P_f x_i,f - P_p y_i,p).**

The local permeate composition must be determined from a defined module flow arrangement. It is not automatically equal to the feed composition or the overall collected permeate composition.

## 6. Dimensional check
[Pi_i] [delta p_i] = mol/(m^2 s Pa) * Pa = mol/(m^2 s), matching J_i.

## 7. Limiting checks
- Zero partial-pressure difference implies zero component flux.
- If l doubles while permeability and surface partial pressures remain unchanged, flux halves.
- For positive permeance and p_i,f > p_i,p, flux is positive feed-to-permeate.

## 8. Assumptions and limitations
- Dense nonporous membrane and solution-diffusion mechanism.
- Steady one-dimensional transport through the selective layer.
- Constant membrane diffusivity and linear sorption in the studied range.
- Negligible additional support, interfacial and concentration-polarization resistance.
- No membrane-phase reaction or facilitated transport.
- Isothermal layer for this derivation.
- Ideal gas contacting phases only for the final partial-pressure/mole-fraction substitution.
- Wet flue gas may alter sorption, permeance, selectivity and phase behavior.
- Permeability/permeance must be sourced for the chosen material and test conditions.

## 9. Next mathematical step
Derive differential retentate and permeate component balances for a specific module flow arrangement. Do not finalize module ODEs until cross-flow, co-current, counter-current or mixed-permeate closure is chosen.

## 10. Verification status
Algebraic and dimensional checks: documented.
Independent mathematical review: pending.
Literature parameter validation: pending.
Project-specific numerical substitution: pending.
