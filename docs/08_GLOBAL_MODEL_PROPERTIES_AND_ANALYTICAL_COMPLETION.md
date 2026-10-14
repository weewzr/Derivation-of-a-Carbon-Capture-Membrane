# 08 - Global Properties and Analytical Completion of the Ideal Binary Model

**Status:** Supplementary continuous-mathematics derivation. Symbolically checked; numerical tests are specified but not executed. This note does not assert suitability for a commercial module or calibrate the model to CN4119.

## 1. Scope and variables

Use the ideal local-collector model defined in docs/06_REVIEW01_CROSSFLOW_CLOSURE_REMEDIATION.md, with the constitutive assumptions and limitations in docs/07_CHEMICAL_POTENTIAL_TRANSPORT_SCOPE.md.

Assume:
- Binary ideal-gas feed, CO2 fraction $z\in(0,1)$.
- Constant $P_f>P_p\ge0$, $r=P_p/P_f\in[0,1)$.
- Constant positive permeances, $\alpha=\Pi_C/\Pi_N>0$.
- No permeate axial mixing, sweep gas, pressure drop, or other omitted effects in the stated ideal local-collector arrangement.

Dimensionless flows and area are
$$
f_C=F_C/F_0,\quad f_N=F_N/F_0,\quad f=f_C+f_N,\quad x=f_C/f,\quad
a=(\Pi_C P_f/F_0)A.
$$
Let
$$
q_C=x-r y,\qquad q_N=(1-x)-r(1-y).
$$
The governing equations are
$$
\frac{df_C}{da}=-q_C,\qquad
\frac{df_N}{da}=-\frac{q_N}{\alpha},\qquad
f_C(0)=z,\quad f_N(0)=1-z.
$$
The local closure is the unique admissible root of $H(y)=\alpha(1-y)q_C-yq_N=0$ on the interval derived in document 06.

## 2. Exact identity for the sum of dimensionless driving forces

Directly from the definitions,
$$
q_C+q_N=(x-r y)+(1-x-r(1-y))=1-r.
$$
This identity is independent of local composition and local permeate composition. It does **not** say that total molar flux is spatially constant; the actual permeance-weighted dimensionless total-flow removal is $q_C+q_N/\alpha$, which depends on composition when $\alpha\ne1$.

## 3. Monotonicity and admissible output metrics

From the component balances,
$$
\frac{df}{da}=-\left(q_C+\frac{q_N}{\alpha}\right).
$$
On the admissible branch, $q_C,q_N\ge0$, and $q_C+q_N=1-r>0$. Therefore, while the retentate state is physical,
$$
\min(1,1/\alpha)(1-r)
\le q_C+q_N/\alpha
\le\max(1,1/\alpha)(1-r).
$$
Thus total retentate flow decreases strictly for $r<1$. The mathematical depletion-area bound, extending the model continuously to the zero-flow limit, is
$$
\frac{1}{\max(1,1/\alpha)(1-r)}
\le a_{\mathrm{dep}}\le
\frac{1}{\min(1,1/\alpha)(1-r)}.
$$
This bound is for the ideal mathematical model; a numerical implementation must stop at its declared positive depletion cutoff before evaluating $x=f_C/f$ at $f=0$.

Define stage cut, CO2 recovery, and overall collected permeate CO2 fraction as
$$
\theta=1-f,\qquad R_C=\frac{z-f_C}{z},\qquad
Y_{C,p}=\frac{z-f_C}{\theta}\quad(\theta>0).
$$
Their derivatives along the model are
$$
\frac{d\theta}{da}=q_C+\frac{q_N}{\alpha}>0,\qquad
\frac{dR_C}{da}=\frac{q_C}{z}\ge0.
$$
For an interior composition $0<x<1$, the unique closure root is interior to the admissible interval, so $q_C,q_N>0$; hence CO2 recovery is strictly increasing before the model reaches its endpoint. The N2 recovery $R_N=((1-z)-f_N)/(1-z)$ obeys
$$
\frac{dR_N}{da}=\frac{q_N}{\alpha(1-z)}\ge0.
$$
These properties justify a bracketed target-recovery search over a bounded area interval, provided the target is bracketed before the prescribed numerical depletion cutoff. They do not justify an unbounded search or guarantee that an arbitrary target is reachable before the chosen cutoff.

The permeate composition and enrichment can also be written
$$
Y_{C,p}=\frac{zR_C}{\theta},\qquad
E_C=\frac{Y_{C,p}}{z}=\frac{R_C}{\theta},
\quad \theta>0.
$$
These expressions are identities, not additional governing equations. At $a=0$, $\theta=0$, so bulk collected permeate composition and enrichment are undefined.

## 4. Exact analytical family I: zero permeate pressure

For $r=0$, the flux fractions are $q_C=x$ and $q_N=1-x$. The ODEs are
$$
\frac{df_C}{da}=-\frac{f_C}{f_C+f_N},\qquad
\frac{df_N}{da}=-\frac{f_N}{\alpha(f_C+f_N)}.
$$
Dividing one equation by the other gives
$$
\frac{df_C}{df_N}=\alpha\frac{f_C}{f_N}.
$$
Integration from the feed inlet yields
$$
\frac{f_C}{z}=\left(\frac{f_N}{1-z}\right)^\alpha.
$$
Set $u=f_N/(1-z)\in(0,1]$. Then
$$
f_N=(1-z)u,\qquad f_C=zu^\alpha.
$$
Substitution into the N2 ODE gives
$$
\frac{du}{da}=-\frac{1}{\alpha(zu^{\alpha-1}+1-z)}.
$$
Integrating from $u=1$ at $a=0$ to the current $u$ gives the exact parametric area relation
$$
\boxed{a=z(1-u^\alpha)+\alpha(1-z)(1-u)}.
$$
For every $\alpha>0$, the right-hand side increases strictly as $u$ decreases from 1 to 0. This supplies an exact reference for both normalized component flows and dimensionless area in the $r=0$ mathematical limit:
$$
(f_C,f_N,a)=
\left(zu^\alpha,(1-z)u,\ z(1-u^\alpha)+\alpha(1-z)(1-u)\right).
$$
At complete mathematical depletion, $a_{\mathrm{dep}}=z+\alpha(1-z)$. This is a mathematical limiting case, not a claim that zero absolute permeate pressure is physically attainable or energetically free.

## 5. Exact analytical family II: equal permeances

For $\alpha=1$, the closure residual simplifies to $H(y)=x-y$, so the unique root is $y=x$ for any $0\le r<1$. Then
$$
q_C=(1-r)x,\qquad q_N=(1-r)(1-x).
$$
Consequently
$$
\frac{df_C}{da}=-(1-r)x,\qquad
\frac{df_N}{da}=-(1-r)(1-x),\qquad
\frac{df}{da}=-(1-r),\quad \frac{dx}{da}=0.
$$
With the inlet conditions,
$$
\boxed{f(a)=1-(1-r)a},
$$
$$
\boxed{f_C(a)=z[1-(1-r)a]},
$$
$$
\boxed{f_N(a)=(1-z)[1-(1-r)a]},\qquad
0\le a<\frac{1}{1-r}.
$$
This exact family includes numerical case TEST-A and checks composition invariance, component balances, sign convention, and depletion endpoint handling.

## 6. Constant-driving-force reference

For one component with a prescribed constant partial-pressure difference $\Delta p>0$, constant permeance $\Pi$, and fixed area coordinate,
$$
J=\Pi\Delta p,\qquad \frac{dF}{dA}=-\Pi\Delta p.
$$
Integration yields
$$
\boxed{F(A)=F(0)-\Pi\Delta p\,A}.
$$
Units: $[\Pi\Delta p]=\mathrm{mol\,m^{-2}\,s^{-1}}$, and multiplying by area gives $\mathrm{mol\,s^{-1}}$. This is a separate single-component reference with externally prescribed driving force, not an analytical solution of the full coupled binary model.

## 7. Mathematical completion statement and remaining non-mathematical dependencies

For fixed $z,\alpha,r$ in the declared domain, the restricted ideal model is a closed continuous system: an algebraic local root with a unique admissible value at each interior state, coupled to the two dimensionless component-flow ODEs and feed-inlet conditions. The generic case need not have an elementary closed-form $f_C(a),f_N(a)$ solution to be mathematically specified; numerical integration is a legitimate solution method once the contract is implemented and verified.

The following are not missing symbolic derivations and cannot be established by algebra alone:
- Whether the intended commercial module is adequately represented by the ideal independent local collectors.
- Actual CN4119 feed conditions and source-matched mixed-gas membrane properties.
- Executed numerical test evidence.
- Experimental validity, equipment energy, economics, or avoided-emissions performance.

**Status:** Supplementary continuous mathematical properties derived. The model is mathematically specified for the restricted ideal local-collector assumptions. Numerical verification and physical applicability remain open.
