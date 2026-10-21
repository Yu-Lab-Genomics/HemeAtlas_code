# Hemelas analysis code

This repository contains historical analysis notebooks for the Hemelas project,
covering ATAC peak processing, cell annotation, integration, SEACells, GET model
fine-tuning, TF interactions, and variant analysis.

## Configure paths before use

Machine-specific data, reference, model, and executable paths have been removed.
Paths beginning with `/path/to/` are placeholders and must be replaced with your
own locations. The placeholder roots distinguish the Hemelas project, annotation
project, SEACells project, GET project, reference data, ClinVar data, AlphaFold 3
project, and HMMER binaries.

Relative input/output paths and resource filenames are retained to document the
relationships between processing stages. These files are not bundled with this
repository. Set the working directory for each section and provide the required
inputs before running it. A placeholder is not a working default configuration.

Run `macs2` and the AlphaFold 3 `python` command from the appropriate activated
environment. Package environments have not yet been pinned for these notebooks.

## Notebook status

The notebooks are historical analysis records, not an end-to-end executable
pipeline. Several combine Python, R, or Bash snippets despite declaring a Python
kernel. Run those sections in the appropriate interpreter; do not use Run All
without first resolving the issues in [CODE_REVIEW.md](CODE_REVIEW.md).

Comments, display labels, and console messages are in English. Stored execution
outputs, execution counts, and nonessential execution/UI metadata were cleared
to remove stale logs and embedded machine paths. Scientific parameters and
analysis operations were preserved; no scientific analysis was rerun during
this cleanup. Original notebook outputs remain in the repository history.

