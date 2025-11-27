facsforge — FlowJo-compatible FACS analysis as code
facsforge is a command-line toolkit for reproducible Flow Cytometry (FACS) analysis driven by configuration files rather than GUIs.

It enables users to:

Convert FlowJo workspaces (.wsp) into a declarative YAML gating format
Reproduce FlowJo-style gating outside the GUI
Batch process large FCS collections on HPC systems
Export gated populations as CSV
Generate publication-ready plots
Overlay index-sorting metadata (e.g. well positions)
Apply FlowJo-like biexponential (logicle) scaling without proprietary software
The project is designed for high-performance environments where FlowJo is not suitable or available, such as:

HPC clusters
Containerized workflows
Automated pipelines
Reproducible analysis reports
Unlike GUI tools, facsforge treats gating as code.
This makes cytometry analysis:

versionable
reviewable
testable
reproducible
FlowJo compatibility

facsforge supports:

FlowJo .wsp → YAML conversion
Polygon gates
Hierarchical gating
Subpopulation extraction
Index sorting overlays
Logicle scaling for fluorescence channels
Linear scaling for FSC / SSC
Multi-gate CSV export
Batch plotting
The goal is not to replace FlowJo interactively —
but to make FlowJo analyses portable, automatable, and defensible.

On HPC: one command, full analysis

When installed as a Singularity / Apptainer image and exposed via Lmod:

ml FlowUtils

facsforge analyze-facs \
    -o results/analysis \
    sample.fcs \
    index.csv \
    gates.yaml
No GUI.
No licenses.
No manual clicks.
Fully reproducible.

Philosophy

facsforge follows three principles:

Declare gating, don’t click it
Automate everything repeatable
Never hide biology in a GUI
The result is cytometry that behaves like code —
and code that behaves like your experiment.
