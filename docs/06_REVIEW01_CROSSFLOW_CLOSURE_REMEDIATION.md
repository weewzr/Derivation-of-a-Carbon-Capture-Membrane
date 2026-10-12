# Review 01 Remediation: Physical Cross-Flow Closure and Mathematical Proof

Status: Main Research correction, pending independent re-review. Addresses IMR01-B01, IMR01-M01, IMR01-M05, IMR01-D03, IMR01-N01 and IMR01-N02 in a bounded pass.

## 1. Idealised module geometry (IMR01-B01, M05)

Consider a feed/retentate channel partitioned into differential membrane strips of area dA. Feed flows tangentially along increasing A. Each strip transfers J_C dA and J_N dA into a local permeate collector, which immediately withdraws those gases at uniform prescribed pressure P_p. There is no sweep gas, tangential permeate flow, axial permeate mixing, permeate hold-up, or membrane-to-collector pressure drop.

Schematic (each downward outlet is a *different* local permeate stream):

feed inlet -> [feed strip dA_1] -> [feed strip dA_2] -> ... -> retentate outlet
                    |                    |
                    v                    v
             local collector 1    local collector 2
                    |                    |
                    +---- collected permeate header (downstream only) ---->

The common collected header is downstream of the transfer interface. It does not remix gas back into any local membrane-surface collector, so its bulk composition is not used in the local flux law.

Steady component balance on the infinitesimal local collector:
0 = J_i dA - dF_i,p,local.
Summing:
dF_p,local=(J_C+J_N)dA.
Thus local withdrawn permeate mole fraction is:
y=dF_C,p,local/dF_p,local=J_C/(J_C+J_N), provided total transfer is positive.

This closure is a *specific idealised collector architecture*, not a general consequence of feed-side conservation. It is appropriate for an initial reduced-order benchmark when local permeate withdrawal and uniform P_p are reasonable approximations. It does NOT represent a co-current/counter-current permeate channel, an axially mixed permeate plenum at the membrane interface, significant permeate-side pressure drop, or backmixing from a shared header. Those require separate permeate-side state equations and boundary conditions.

The present model is a feed-inlet initial-value problem with an algebraic local collector closure; no independent permeate-channel boundary condition is needed. Feed initial conditions are f_C(0)=z and f_N(0)=1-z. The prescribed permeate *pressure* P_p is a parameter, not an independently specified permeate *composition*.

## 2. Canonical local root equation (IMR01-M01, N01, N02)

Define 0<x<1, 0<=r=P_p/P_f<1, alpha=Pi_C/Pi_N>0, q_C=x-r y, q_N=(1-x)-r(1-y).

The local collector equation is:
H(y)=alpha(1-y)q_C-y q_N=0.

For r>0 restrict y to:
L=max(0,1-(1-x)/r), U=min(1,x/r).
For r=0 use [0,1].

On [L,U], q_C>=0 and q_N>=0. Since r<1, both cannot be zero simultaneously: q_C+q_N=1-r>0. Therefore D(y)=alpha q_C+q_N>0 and g(y)=alpha q_C/D(y) is defined.

H(y)=D(y)[g(y)-y], so root selection can use H without dividing by any component flux.

At y=L: if L=0, H(L)=alpha q_C>=0; if L>0, q_N(L)=0 and H(L)=alpha(1-L)q_C>=0.
At y=U: if U=1, H(U)=-q_N<=0; if U<1, q_C(U)=0 and H(U)=-U q_N<=0.

For interior x in (0,1), r in (0,1), endpoint inequalities are strict. Thus continuity guarantees a root.

Compute derivatives: q_C'=-r, q_N'=r, D'=r(1-alpha).
g'=alpha[q_C' D-q_C D']/D^2
  =-alpha*r[D+(1-alpha)q_C]/D^2
  =-alpha*r(q_C+q_N)/D^2
  =-alpha*r(1-r)/D^2 < 0.

Therefore g-y is strictly decreasing, so the root is unique. For r=0, g is constant and y=g gives the unique root.

The polynomial is:
c2*y^2+c1*y+c0=0
c2=r(1-alpha)
c1=1-x-r+alpha(x+r)
c0=-alpha*x.

Reserve a for dimensionless membrane area; do not use it for a polynomial coefficient.

Zero-component-flux endpoints are allowed in the admissible set, but ratio formulas y/(1-y) or J_C/J_N must only be used where their denominators are nonzero. Use H for root finding.

## 3. Scope
This is a mathematical proof for the idealised local-withdrawal model only. It is not evidence that a commercial membrane module has the stipulated collector geometry, uniform P_p or negligible axial permeate mixing.

## 4. Verification status
- Local collector control-volume closure: derived under stated idealisation.
- Existence/uniqueness on admissible interval: algebraically derived.
- Independent reviewer acceptance: pending.
- CN4119 module suitability: unresolved.
