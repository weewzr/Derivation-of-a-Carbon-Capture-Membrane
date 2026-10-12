# 04 - Permeance, Selectivity, and Pressure-Ratio Sensitivity

## Status
Derived for the candidate steady, ideal, binary, constant-pressure cross-flow model. Not independently reviewed and not calibrated to CN4119.

## 1. Two independent membrane transport parameters
Let Pi_C and Pi_N denote CO2 and N2 permeances [mol/(m2 s Pa)].

Define ideal permeance selectivity alpha=Pi_C/Pi_N.

Then Pi_N=Pi_C/alpha. Specifying Pi_C and alpha is equivalent to specifying both permeances, provided all values refer to the same material, membrane architecture and test conditions.

Do not confuse permeability [mol/(m s Pa)] with permeance [mol/(m2 s Pa)] or membrane-material ideal selectivity with measured mixed-gas selectivity.

## 2. Flux law
J_C=Pi_C P_f(x-r y)
J_N=(Pi_C/alpha)P_f[(1-x)-r(1-y)]
where r=P_p/P_f.

## 3. Local permeate-composition equation
For locally withdrawn cross-flow permeate:
y=J_C/(J_C+J_N).

Hence:
y/(1-y)=alpha(x-r y)/[(1-x)-r(1-y)].

For r=0:
y=alpha x/(alpha x+1-x).

This describes local permeate composition, not overall collected permeate purity.

## 4. Exact common permeance scaling
Multiply both permeances by k>0 while keeping alpha, pressures and all other assumptions fixed.

The algebraic closure for y is unchanged because it depends on the ratio alpha, not the common permeance scale.

The component-flow equations are:
dF_i/dA=-Pi_i P_f (driving-force fraction).

Under the new permeances k Pi_i:
dF_i/dA=-k Pi_i P_f (driving-force fraction).

Define B=kA. Then dF_i/dB equals the original ODE. Thus the same outlet state is reached at:
A_new=A_old/k.

This scaling holds only for the ideal constant-property, constant-pressure model without geometry-dependent pressure drop, polarization or other scale effects.

## 5. Dimensionless area
Define:
a=(Pi_C P_f/F_0) A.

Let f_C=F_C/F_0, f_N=F_N/F_0, x=f_C/(f_C+f_N).

Then:
df_C/da=-(x-r y),
df_N/da=-(1/alpha)[(1-x)-r(1-y)].

The dimensionless model depends on inlet CO2 fraction z, alpha, pressure ratio r and dimensionless area a.

The actual area scale is:
A=(F_0/(Pi_C P_f)) a.

This shows why feed throughput, absolute permeance and feed pressure determine membrane sizing, while selectivity and pressure ratio determine the dimensionless separation behavior.

## 6. Analytical selectivity behavior at r=0
y=alpha x/(alpha x+1-x).

For fixed 0<x<1:
dy/dalpha=x(1-x)/[alpha x+1-x]^2 > 0.

Thus higher selectivity increases local permeate CO2 fraction in this ideal zero-permeate-pressure limit.

At alpha=1, y=x.
As alpha approaches infinity, y approaches 1 for any fixed x>0.

These are mathematical limits, not claims about achievable industrial membrane materials.

## 7. Pressure-ratio limitation
For a CO2-enriched permeate with y>x and positive CO2 flux, the condition x-r y>0 implies:
r<x/y.

Consequently, high permeate pressure relative to feed pressure can suppress CO2 flux even for a selective membrane.

Reducing r may improve driving force but increases vacuum/compression energy requirements. Pressure-ratio optimisation is an integrated engineering/economic problem, not a free mathematical improvement.

## 8. Example: illustrative parameters only
If z=0.10 and alpha=30, at r=0 the local permeate composition at the inlet is:
y=3/(3+0.9)=0.76923.

This 76.9% is a local ideal limiting composition. It is NOT a predicted CN4119 product purity, overall module permeate composition or practical zero-pressure operating case.

## 9. Verification requirements
- compare two membranes with equal alpha and permeances scaled by k: outlet curves collapse when plotted against dimensionless area a;
- check alpha=1 and r=0 limiting cases;
- check positivity and component conservation;
- test the high-r driving-force limitation;
- ensure no result is interpreted as cost or physical validation without literature data.

## 10. Next
Derive a numerically explicit, solver-ready nondimensional cross-flow specification with stable local root selection, stopping criteria and test tolerances. Then request independent mathematical review.
