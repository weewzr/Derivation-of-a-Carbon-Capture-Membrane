# Literature and Parameter Register

## Rules
Every numerical value should identify source, material/configuration, test conditions, units, whether measured/modelled, and how it is used. No paper's "optimum" transfers automatically to CN4119.

## Candidate systems-level benchmark
Dong et al. (2020), "Novel membrane-absorption hybrid process for CO2 capture from flue gas", Atmospheric Pollution Research, open PDF: https://aaqr.org/articles/aaqr-20-07-oa-0374.pdf

Role: candidate benchmark for flowsheet/economic framing and a membrane-absorption hybrid. Before promotion, extract exact assumptions, definitions, model equations, pressure ratio, flow split, membrane-area model, equipment costs, power assumptions and comparison boundary.

Candidate conditions mentioned in project notes, not yet independently frozen:
- gas temperature 40 C;
- 4.20 vol% CO2;
- 5.00 vol% O2;
- 81.77 vol% N2;
- 7.03 vol% H2O;
- 1.06 bar;
- CO2 permeance/permeability basis stated in project notes as 1500 GPU;
- CO2/N2 selectivity stated as 30;
- feed-to-permeate pressure ratio 10:1;
- recovery cases around 5-30%.

These are PROVISIONAL reported-study values and must be checked against the original paper before being used in a canonical benchmark. In particular verify whether the paper says permeability or permeance, and whether GPU units are correctly attributed.

## Parameter register

| ID | Parameter | Value | Unit | Provenance class | Material/test gas | T | Feed/p permeances | Humidity | Source / page/equation | Use/status |
|---|---|---:|---|---|---|---|---|---|---|---|
| PAR-001 | CO2 permeance | TBD | GPU or mol m^-2 s^-1 Pa^-1 | UNRESOLVED | TBD | TBD | TBD | TBD | TBD | OPEN |
| PAR-002 | N2 permeance | TBD | GPU or mol m^-2 s^-1 Pa^-1 | UNRESOLVED | TBD | TBD | TBD | TBD | TBD | OPEN |
| PAR-003 | CO2/N2 selectivity | TBD | dimensionless | UNRESOLVED | TBD | TBD | TBD | TBD | TBD | OPEN |
| PAR-004 | feed CO2 fraction | TBD | mol/mol | PROJECT SPECIFICATION | flue gas | TBD | n/a | wet/dry TBD | attachment | OPEN |
| PAR-005 | feed total molar flow | TBD | mol/s | PROJECT SPECIFICATION | flue gas | TBD | n/a | n/a | attachment | OPEN |
| PAR-006 | feed pressure | TBD | Pa | PROJECT SPECIFICATION | flue gas | TBD | n/a | n/a | attachment | OPEN |
| PAR-007 | permeate pressure | TBD | Pa | DESIGN BASIS | membrane | TBD | n/a | n/a | TBD | OPEN |

## Needed source extraction
1. Find primary membrane-material data for CO2 and N2 under relevant wet-gas conditions.
2. Check permeance vs permeability and selective-layer thickness.
3. Capture pressure, temperature, humidity, aging and test-mixture context.
4. Record uncertainty and evidence quality.
5. Retain contradictory sources instead of silently averaging incompatible data.
