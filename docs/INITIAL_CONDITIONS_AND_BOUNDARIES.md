# Initial Conditions, Boundary Conditions, and Coordinate Contract

This note prevents an under-specified membrane module problem.

## Required decisions before solving

- module arrangement: cross-flow, co-current, counter-current, or a well-mixed permeate plenum;
- area coordinate orientation;
- which stream is retentate/feed-side and which is permeate-side;
- feed and permeate pressure profiles;
- whether feed-side/permeate-side pressure drops are neglected or modelled;
- isothermal vs non-isothermal;
- ideal partial pressure vs fugacity driving force;
- module geometry / area distribution;
- design specification: fixed area, fixed stage cut, target recovery, or target permeate composition.

## Feed boundary
At the feed inlet, specify every component molar flow (F_{i,f,0}), temperature, pressure, and wet/dry composition basis. Total flow and mole fractions should be checked for consistency.

## Permeate boundary
Do not invent a single permeate composition boundary for a distributed module without defining the arrangement. Counter-current systems generally require a coupled boundary-value treatment; co-current and cross-flow use different local balances; a perfectly mixed permeate plenum is a separate idealization.

## Outer-area endpoint
A model may prescribe membrane area and compute outlet states, or prescribe a performance target and solve for the area. Do not prescribe both independently unless they are consistent.

## Sign convention
Define (J_i>0) as component (i) moving from feed side to permeate side. With area (A) increasing along the feed/retentate direction:
[
\frac{dF_{i,r}}{dA}=-J_i.
]
Every equation, output and test must follow this convention.

## Pressure and fugacity
For ideal gas, (p_i=y_iP). For nonideal gases use (f_i=\phi_i y_iP) where justified. The driving force is feed-interface minus permeate-interface partial pressure/fugacity. State the selected form and domain.

