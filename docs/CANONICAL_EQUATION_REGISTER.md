# Canonical Equation Register

This is the single authoritative equation ID register for the membrane derivation. Equation IDs are stable and should not be recycled.

| ID | Description | Equation/document | Class | Units checked? | Independent check | Status | Dependencies / use |
|---|---|---|---|---|---|---|---|
| MEM-GOV-001 | General species conservation | 01 transport derivation | CONSERVATION | YES | Control-volume balance | VERIFIED FOR GENERAL BALANCE | Constitutive model |
| MEM-GOV-002 | Steady nonreactive membrane continuity | 01 transport derivation | DERIVED | YES | Steady local balance | CANDIDATE | Flux derivation |
| MEM-CON-001 | Fickian membrane transport | 01 transport derivation | CONSTITUTIVE | YES | Sign/dimensions | ASSUMPTION-DEPENDENT | Surface concentrations |
| MEM-CON-002 | Linear sorption | 01 transport derivation | CONSTITUTIVE | YES | Material-model evidence | ASSUMPTION-DEPENDENT | Partial pressure |
| MEM-FLX-001 | Solution-diffusion flux relation | 01 transport derivation | DERIVED UNDER ASSUMPTIONS | YES | Zero driving-force limit | CANDIDATE | Module balances |
| MEM-FLX-002 | Ideal-gas partial-pressure form | 01 transport derivation | DERIVED UNDER ASSUMPTIONS | YES | Mole-fraction/pressure check | CANDIDATE | Module balances |
| MEM-BIN-001 | CO2 feed-side component balance | 02 binary cross-flow model | CONSERVATION | YES | Integral balance | CANDIDATE | ODE model |
| MEM-BIN-002 | N2 feed-side component balance | 02 binary cross-flow model | CONSERVATION | YES | Integral balance | CANDIDATE | ODE model |
| MEM-BIN-003 | Local cross-flow permeate closure | 02 binary cross-flow model | MODEL CLOSURE | YES | Architecture check | CANDIDATE / REVIEW REQUIRED | ODE model |
| MEM-PERF-001 | CO2 recovery definition | 02 binary cross-flow model | DEFINITION | YES | Bounds | CANDIDATE | Result reporting |
| MEM-PERF-002 | CO2 enrichment factor | 02 binary cross-flow model | DEFINITION | YES | Composition check | CANDIDATE | Result reporting |
| MEM-PERF-003 | Stage cut | 02 binary cross-flow model | DEFINITION | YES | Total balance | CANDIDATE | Result reporting |

## Register rules
1. The register is canonical; use IDs rather than inventing alternate IDs.
2. If a derivation changes, preserve the old status/history and record the change.
3. Each equation must state symbols, units, domain and assumptions in its source document.
4. "Verified" names the exact scope/benchmark; it never means all possible membranes or operating conditions.
5. External source equations should have a citation and must be distinguished from equations derived in this project.
6. Add each new equation when it is created, not retrospectively at manuscript time.

## MEM-SOL register (re-review 01 completion)

| ID | Description | Source docs | Class | Assumptions/domain | Units | Check evidence | Status | Downstream dependency |
|---|---|---|---|---|---|---|---|---|
| MEM-SOL-001 | Retentate CO2 composition | docs/05 | definition | f_C+f_N>0 | 1 | ratio identity | Independently checked symbolically for restricted model; numerical execution pending | feeds closure |
| MEM-SOL-002 | Dimensionless CO2 driving force | docs/05 | definition | ideal gas; fixed r; 0<=y<=1 | 1 | flux law substitution | Independently checked symbolically for restricted model; numerical execution pending | CO2 ODE |
| MEM-SOL-003 | Dimensionless N2 driving force | docs/05 | definition | ideal gas; fixed r; 0<=y<=1 | 1 | flux law substitution | Independently checked symbolically for restricted model; numerical execution pending | N2 ODE |
| MEM-SOL-004 | Local permeate composition | docs/06 | ideal collector balance | no axial mixing/sweep/hold-up; positive total flux | 1 | local component control-volume; re-review 01 | Independently checked symbolically for restricted model; numerical execution pending | closure root |
| MEM-SOL-005 | Dimensionless CO2 ODE | docs/05 | conservation plus constitutive | steady feed; fixed Pi_C,P_f; f>0 | 1 | area rescaling; re-review 01 | Independently checked symbolically for restricted model; numerical execution pending | solver |
| MEM-SOL-006 | Dimensionless N2 ODE | docs/05 | conservation plus constitutive | steady feed; fixed Pi_N,P_f; f>0 | 1 | area rescaling; re-review 01 | Independently checked symbolically for restricted model; numerical execution pending | solver |
| MEM-SOL-007 | Inlet state | docs/05 | boundary/input | 0<z<1; F0>0 | 1 | normalization identity | Independently checked symbolically for restricted model; numerical execution pending | IVP |
| MEM-SOL-008 | Canonical closure residual H | docs/06 | derived | 0<x<1; 0<=r<1; alpha>0 | 1 | bracket signs and derivative; re-review 01 | Independently checked symbolically for restricted model; numerical execution pending | root solver |
| MEM-SOL-009 | Admissible root interval | docs/06 | derived | 0<r<1; nonnegative component fluxes | 1 | q_C>=0,q_N>=0; re-review 01 | Independently checked symbolically for restricted model; numerical execution pending | root solver |
| MEM-SOL-010 | Stage cut | docs/05 | definition | normalized feed F0>0 | 1 | overall flow balance | Independently checked symbolically for restricted model; numerical execution pending | output |
| MEM-SOL-011 | CO2 recovery | docs/05 | definition | z>0 | 1 | component balance | Independently checked symbolically for restricted model; numerical execution pending | output |
| MEM-SOL-012 | Collected permeate CO2 fraction | docs/05 | definition | theta>0 | 1 | component balance | Independently checked symbolically for restricted model; numerical execution pending | output |
| MEM-SOL-013 | Retentate CO2 fraction | docs/05 | definition | f_C+f_N>0 | 1 | mole-fraction identity | Independently checked symbolically for restricted model; numerical execution pending | output |
| MEM-SOL-014 | Physical area conversion | docs/04/05 | dimensional identity | Pi_C>0; P_f>0; F0>0 | m2 | unit check and scaling; re-review 01 | Independently checked symbolically for restricted model; numerical execution pending | sizing |

This register reflects independent re-review 01's **restricted** mathematical acceptance only. It does not claim executed MATLAB/DWSIM verification, empirical validation, or suitability of a commercial module. Original review reports remain immutable.


## MEM-ANA register (document 08 mathematical completion)

| ID | Description | Source | Class | Assumptions/domain | Units | Check evidence | Status | Dependencies / use |
|---|---|---|---|---|---|---|---|---|
| MEM-ANA-001 | Identity $q_C+q_N=1-r$ | docs/08 | ALGEBRAIC IDENTITY | Ideal binary local-collector model; $0\le r<1$ | 1 | Direct substitution | Symbolically derived; numerical execution not required for identity | Total-flow bounds |
| MEM-ANA-002 | Monotonic stage cut and component recoveries | docs/08 | DERIVED | Admissible branch; $0<x<1$, $z\in(0,1)$, $\alpha>0$, $r<1$ | 1 per dimensionless area | Differentiate definitions and ODEs | Symbolically derived; numerical behavior not executed | Target design search |
| MEM-ANA-003 | Exact parametric solution at $r=0$ | docs/08 | ANALYTICAL LIMIT | $z\in(0,1)$, $\alpha>0$, $u\in(0,1]$ | Dimensionless | Integrate component-ODE ratio and area relation | Symbolically derived; numerical benchmark pending | Verification TEST-B |
| MEM-ANA-004 | Exact solution at $\alpha=1$ | docs/08 | ANALYTICAL LIMIT | $0\le r<1$, $0\le a<1/(1-r)$ | Dimensionless | Closure $y=x$; integrate total-flow ODE | Symbolically derived; numerical benchmark pending | Verification TEST-A/TEST-D |
| MEM-ANA-005 | Constant-driving-force single-component reference | docs/08 and verification contract | ANALYTICAL REFERENCE | Constant $\Pi$, constant $\Delta p>0$ | $F$ in mol/s, $A$ in m$^2$ | Integrate $dF/dA=-\Pi\Delta p$ | Symbolically derived; numerical execution pending | Sign and dimensional test |

These analytical entries complete the generic symbolic reference set for the restricted model. They do not imply that TEST-A through TEST-F have been executed or that the intended commercial module has been confirmed.
