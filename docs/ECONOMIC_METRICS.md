# Economic Metrics and System Boundary

## Objective
Evaluate whether membrane pretreatment lowers integrated capture cost or improves useful CO2 capture under a consistent baseline and operating basis.

## Separation metrics
[
R_{CO2}=F_{CO2,p}/F_{CO2,f},\quad
E_{CO2}=y_{CO2,p}/x_{CO2,f},\quad
\theta=F_p/F_f.
]
These are different metrics. Enrichment is not capture, recovery is not purity, and separated CO2 is not automatically avoided CO2.

## Baseline
Define a no-membrane reference with the same:
- flue-gas source and production rate;
- downstream capture product specification;
- annual operating hours;
- emissions boundary;
- power/cost year and currency;
- CO2 compression/transport boundary where relevant.

## Annual cost
Use a consistent annual cost function:
[
C_{annual}=C_{capital,annualized}+C_{replacement}+C_{electricity}
+C_{maintenance}+C_{other}.
]
Avoid double-counting power or capture duties already included in HYSYS.

## Cost per tonne
An incremental abatement metric can be written as:
[
C_{inc}=
\frac{C_{annual,membrane case}-C_{annual,baseline}}
{E_{avoided,membrane case}-E_{avoided,baseline}}.
]
The denominator must be defined. If it is zero or negative, the metric is not a meaningful positive-cost-per-abatement value; report the result and interpretation rather than hiding it.

Where the membrane changes cost but not avoided emissions, report incremental annual cost and the downstream process benefit separately.

## Important caution
If the membrane just pre-concentrates CO2 before the same absorber and does not change capture rate, energy or size, enrichment alone may create no avoided-emissions benefit. Its benefit must come from an evidenced change in downstream process performance or a different capture route.

## Components potentially needed
- membrane selective-layer/module capital;
- replacement/aging;
- blower/compressor/vacuum electricity;
- pressure drop;
- downstream absorber/solvent-regeneration change;
- CO2 compression;
- maintenance;
- cost-year, currency and annualization assumptions.

Do not assign unsupported costs before source collection.
