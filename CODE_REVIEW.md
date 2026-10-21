# Initial code review and publication cleanup

Reviewed baseline: `8751048b0249e0db1b3988d7eb622963606c910c` (2026-10-21).
Scope: static inspection of all 16 notebooks, path cleanup, and English text.
Cell numbers below are one-based and include Markdown cells.

## Completed in this change

- Replaced 72 machine-specific path occurrences with descriptive `/path/to/`
  placeholders or executable names resolved through the active environment.
- Translated 164 source lines containing Chinese comments, plot text, or messages.
- Replaced the SimHei plot font with Matplotlib's DejaVu Sans for English labels.
- Removed 927 stored output blocks, reset execution counts, and removed
  nonessential execution/UI metadata. Historical results remain in Git history.
- Retained relative workflow paths, dataset identifiers, resource filenames,
  scientific parameters, and analysis operations.

## Existing issues requiring a separate implementation pass

| Priority | Location | Finding and implication |
| --- | --- | --- |
| High | `6_Integrate_using_snapatac2_and_wnn.ipynb`, cell 257 | `rna.obsm['joint_spectral_multi_harmony'] = embedding'` contains a trailing quote and raises a Python syntax error. |
| High | `11_Subcluster_analysis.ipynb`, cell 7 | The entire cell is indented at top level without an enclosing block, causing `IndentationError`. |
| High | `1_ATAC_modality_and_cCREs.ipynb`, `2_Matrix_from two_modality.ipynb`, `3_Cell_annotation_from_paper.ipynb`, `10_Hemelas_Integrate_benchmark.ipynb`, and `15_Variants_affect_TF_interaction.ipynb` | Python-kernel notebooks contain R or Bash source without an interpreter bridge. A Python kernel cannot execute these sections as written. Some R expressions can even parse as Python but have different semantics. |
| Medium | `15_Variants_affect_TF_interaction.ipynb`, cell 7 | The AlphaFold command lacks a continuation before the final `2>&1` / `tee` line, so that line does not capture the AlphaFold command's output as intended. GPU index 7 is also hardcoded. |
| High: verify data alignment | `8_New_data_and_delete_share-seq_data.ipynb`, cells 9, 55, and 82; `6_Integrate_using_snapatac2_and_wnn.ipynb`, cell 257 | Metadata, feature names, or embeddings are assigned positionally using `.tolist()` or `.to_numpy()`. Correctness depends on identical upstream row/column order; these assignment sites do not assert identity. Validate identifiers and align by key before changing the workflow. This is a risk, not evidence that the historical results are misaligned. |
| High: verify modality | `2_Matrix_from two_modality.ipynb`, cell 21 | Selects files matching `atac.rds` but writes `data_rna/rna_16_17.mtx` and later uses gene-oriented labels. It also selects file positions 1, 17, and 6 and hardcodes matrix dimensions. Confirm the intended input modality and file manifest before correcting names or rerunning. |
| Medium: verify definition | `14_Common_and_specific_TF_interaction.ipynb`, cells 20 and 26 | The variable named `non_zero_counts` uses `> 0`, which counts positive values rather than all nonzero values. The two definitions coincide only for nonnegative input. Confirm the upstream value range and manuscript definition before changing this condition. |
| Medium | Repository-wide | No dependency/environment specification, input manifest, or execution-order documentation was present at baseline. Relative paths point to external intermediates. Removing host paths alone does not establish reproducibility. |

IPython commands such as `%matplotlib inline`, `%%time`, and `?function` are
not ordinary Python syntax; they were not treated as defects solely because
`ast.parse` rejects them.

## Validation and limits

Validation passed for all 16 JSON documents, unchanged cell counts/types/order,
absence of Chinese text and original host/user path remnants, cleared outputs,
and `git diff --check`. All 1,715 previously parseable Python cells preserve
their AST structure after normalizing text constants. Another 53 existing
R/Bash/IPython or syntax-error cells were excluded from the AST comparison.
The available interpreters lack `nbformat`, so full notebook schema validation
was not performed. Existing syntax problems are
reported above rather than silently repaired in this text/path cleanup.

No notebook was executed against scientific inputs. R/Bash sections and runtime
dependencies were not validated by running their analyses. This is an initial
static review, not a full numerical or scientific audit. The change removes
paths from the current files; it does not rewrite Git history.
