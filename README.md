# First-Principles CO2 Membrane Pretreatment

This repository develops the mathematical model for a CO2-selective membrane used as a flue-gas pretreatment / pre-concentration step upstream of downstream capture.

## Primary deliverable

A rigorous, readable derivation and implementation-independent mathematical specification that can be handed to a friend for MATLAB implementation and later represented as a DWSIM custom unit operation.

The scientific question is not merely whether the membrane concentrates CO2. It is whether it improves the integrated capture system and lowers total cost per tonne of CO2 avoided or usefully captured.

## Workflow

1. Recover the actual CN4119 specifications from `attachments/`.
2. Build a sourced membrane-property and operating-condition register.
3. Freeze the membrane class and the physical/system boundary.
4. Derive transport and module conservation from first principles.
5. Specify numerical unknowns, boundary conditions, outputs and solver requirements.
6. Verify the equations with limiting and analytical cases.
7. Hand the frozen mathematical specification to the MATLAB implementer.
8. Compare model results against literature/reference calculations.
9. Integrate membrane outlet streams with the larger HYSYS process.
10. Evaluate recovery, enrichment, energy, equipment sizing and incremental cost.

## Scope control

First target: steady-state, isothermal, 1-D dense polymeric solution-diffusion membrane module, subject to confirmation that the selected material and project conditions support this model.

Do not start with CFD. Do not treat a component-split block as a physical membrane model. Do not optimize before the model, literature inputs and baseline are defined.

## Derivation workflow

The derivation follows `docs/DERIVATION_WORKFLOW_TRISO_STYLE.md`, adapted from the TRISO project's verified-first-principles workflow. The canonical equation register is `docs/CANONICAL_EQUATION_REGISTER.md`; phase/gate exits are controlled by `docs/GATE_WORKFLOW.md`. Preserve raw evidence, derive continuously, assign stable equation IDs, verify limiting cases, conduct independent review, then freeze the MATLAB handoff.

## Main files

- `PROJECT_BRIEF.md` - project charter
- `RESEARCH_FRAMING.md` - scientific questions and model path
- `STATUS.md` - canonical current state
- `docs/MATHEMATICAL_DERIVATION_PLAN.md` - staged derivation plan
- `docs/MATLAB_HANDOFF_SPECIFICATION.md` - expected deliverable for implementation
- `literature/LITERATURE_AND_PARAMETER_REGISTER.md` - sources and parameter provenance
- `docs/ECONOMIC_METRICS.md` - system-level metrics
- `attachments/README.md` - place specifications here

## Scientific honesty

The initial governing equations can be derived from conservation laws and the selected constitutive model. Membrane permeance, selectivity, price, module cost, and real-gas/property data are empirical or literature-derived inputs, not first-principles outputs.
