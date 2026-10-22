# Hemelas

**A paired single-cell multi-omics atlas and regulatory modeling framework for human hematopoiesis.**

[Explore the website](https://hemelas.aigenomicsyulab.com/) · [Website manual](https://hemelas.aigenomicsyulab.com/#user-guide-preview) · [Data downloads](#data-downloads) · [Analysis notebooks](#analysis-notebooks)

## About the study

This repository accompanies our forthcoming preprint:

> **AI-driven single-cell multi-omic modeling reveals the regulation of human hematopoiesis and pathogenic rewiring.**

Hemelas brings together paired gene expression and chromatin accessibility profiles from human peripheral blood, bone marrow, and fetal liver across developmental stages and healthy and disease contexts. The study combines harmonized data processing, consensus cell annotation, multi-omics integration benchmarking, and metacell aggregation to provide a reference for investigating hematopoietic cell states.

| Atlas component | Scale |
| --- | ---: |
| Paired single cells after quality control | 1,641,866 |
| Samples | 201 |
| Datasets | 32 |
| Genes in the integrated expression matrix | 36,601 |
| Harmonized ATAC peak regions | 527,459 |
| Major cell types | 14 |
| Fine-grained cell states | 42 |
| Paired SEACell metacells | 21,795 |

Building on this resource, **HemeGET** adapts the [General Expression Transformer (GET)](https://github.com/GET-Foundation/get_model) to paired hematopoietic metacell profiles. It models the relationship between chromatin accessibility and gene expression and supports the inference of cell-state-aware regulatory programs and candidate transcription factor (TF) interactions. The study combines these predictions with protein structure modeling, ClinVar annotations, biochemical validation, and patient-derived transcriptomic analyses to investigate how coding variants may perturb TF partnerships.

The resulting networks represent model-inferred regulatory associations. Predicted TF interaction interfaces and variant overlaps support hypothesis generation and prioritization; they do not establish physical binding or pathogenic mechanisms for every predicted interaction.

## Using the Hemelas website

Open **[hemelas.aigenomicsyulab.com](https://hemelas.aigenomicsyulab.com/)** and use the four navigation cards at the top of the page. Browser exploration does not require installing this repository.

| Module | What you can explore | How to start |
| --- | --- | --- |
| **Single cell omics** | RNA expression, chromatin-derived gene activity, cell annotations, and genomic tracks | Choose a modality and annotation label, enter a gene symbol, select an autocomplete suggestion, and click **Query**. |
| **Motif-centered Network** | Cell-type-resolved motif regulatory networks | Choose a cell type, adjust the edge count and weight range, and select a motif to focus the network. |
| **Variant mechanism** | Predicted TF complex structures and associated ClinVar variant sites | In **Common** mode, select a TF pair and click a residue link in the ClinVar table to highlight it in the structure viewer. |
| **Data Download** | Single-cell data, SEACells, model checkpoints, regulatory associations, structures, and variant tables | Select a resource or use **View & Download** to choose a file from a grouped resource. |

### Example explorations

- **Gene expression and accessibility:** query `CD79A` in **Single cell omics**, inspect the UMAP, and use the box plot tool to compare cell groups. Open the IGV track tool to inspect genomic signal around the queried gene.
- **Motif networks:** select a cell type in **Motif-centered Network** and query `AHR`. Inspect the edge weights and their signs in the selected cellular context.
- **Structure and variants:** select `ATF2` and `CREB5` in **Variant mechanism** and inspect the available residue links and clinical annotations alongside the predicted structure.

For illustrated instructions, open **Manual** in the website footer or visit the [website manual](https://hemelas.aigenomicsyulab.com/#user-guide-preview).

## Data downloads

Visit the **Data Download** module on the [Hemelas website](https://hemelas.aigenomicsyulab.com/) to access:

- **Single-cell data:** RNA expression, ATAC gene activity, peak matrices, and ATAC fragment archives.
- **SEACell data:** paired metacell RNA profiles, ATAC peak matrices, and gene accessibility scores.
- **Fine-tuned HemeGET models:** checkpoints trained on the full SEACell collection and the HSPC subset.
- **Regulatory associations:** cell-type-resolved motif–motif association tables.
- **Predicted structures and interfaces:** AlphaFold 3 structures and interface-site tables for common and cell-type-specific TF interactions.
- **Variant annotations:** TF variants from ClinVar and their associations with common and cell-type-specific TF interaction interfaces.

These resources are hosted on the website and are not bundled in this code repository.

## Using this code repository

The `notebooks/` directory contains the study's analysis notebooks, from source-data processing through regulatory and variant analysis. The numbering describes the broad analysis stages; it is not a single executable pipeline.

### Get the notebooks

```bash
git clone https://github.com/Yu-Lab-Genomics/Hemelas_code.git
cd Hemelas_code
```

### Prepare the analysis environment and inputs

1. **Choose an analysis stage** from the notebook index below. Read its imports and input/output paths before running any cells.
2. **Download the required data** from the portal and obtain any additional source-study files, reference genomes, annotations, or model assets required by that stage. The download catalogue does not guarantee a one-to-one match with every historical intermediate filename.
3. **Set up the relevant tools.** Python analyses use packages such as Scanpy, AnnData, SnapATAC2, CellTypist, CellHint, SEACells, CellRank, scVelo, PyTorch, and GET, depending on the notebook. R sections use tools such as Seurat and Signac. Peak calling and structure prediction additionally require MACS2 and AlphaFold 3, respectively. Install the dependencies for your selected stage using the corresponding projects' instructions.
4. **Configure paths.** Replace every relevant `/path/to/...` placeholder with your own data, reference, model, or executable location. Set the kernel working directory to the data/project directory expected by each analysis before running it; relative data paths are resolved from that directory, not from the repository layout. Create output directories as needed.
5. **Run selected sections in the appropriate interpreter.** Open Python sections in Jupyter with the intended environment. Run R and Bash sections in R and a shell, respectively, or explicitly configure an interpreter bridge.

For a Python analysis environment with JupyterLab installed, start the notebook interface with:

```bash
jupyter lab notebooks/
```

Use a separate output directory for derived results and retain cell/feature identifiers when aligning data across modalities. Model checkpoints require the matching GET architecture and configuration; the [GET implementation](https://github.com/GET-Foundation/get_model) provides the upstream model code.

### Analysis notebooks

| Notebook | Analysis stage |
| --- | --- |
| [0_Visual.ipynb](notebooks/0_Visual.ipynb) | Atlas overview and visualization |
| [1_ATAC_modality_and_cCREs.ipynb](notebooks/1_ATAC_modality_and_cCREs.ipynb) | ATAC processing and candidate cis-regulatory regions |
| [2_Matrix_from two_modality.ipynb](notebooks/2_Matrix_from%20two_modality.ipynb) | Assembly of RNA and ATAC matrices |
| [3_Cell_annotation_from_paper.ipynb](notebooks/3_Cell_annotation_from_paper.ipynb) | Collection and harmonization of source-study cell annotations |
| [4_Preprocess_celltypist_cellhint.ipynb](notebooks/4_Preprocess_celltypist_cellhint.ipynb) | Preprocessing and reference-based annotation |
| [5_Cell_annotation_from_majority_voting.ipynb](notebooks/5_Cell_annotation_from_majority_voting.ipynb) | Consensus annotation by majority voting |
| [6_Integrate_using_snapatac2_and_wnn.ipynb](notebooks/6_Integrate_using_snapatac2_and_wnn.ipynb) | Spectral and multimodal integration analyses |
| [7_Integrate_using_multiple_algorithms.ipynb](notebooks/7_Integrate_using_multiple_algorithms.ipynb) | Comparison of additional integration methods |
| [8_New_data_and_delete_share-seq_data.ipynb](notebooks/8_New_data_and_delete_share-seq_data.ipynb) | Dataset updates and atlas assembly |
| [9_Hemelas_cell_annotation.ipynb](notebooks/9_Hemelas_cell_annotation.ipynb) | Harmonized Hemelas cell annotation |
| [10_Hemelas_Integrate_benchmark.ipynb](notebooks/10_Hemelas_Integrate_benchmark.ipynb) | Integration benchmarking |
| [11_Subcluster_analysis.ipynb](notebooks/11_Subcluster_analysis.ipynb) | Fine-grained cell-state annotation and visualization |
| [12_SEACells_analysis.ipynb](notebooks/12_SEACells_analysis.ipynb) | Metacell aggregation and downstream analyses |
| [13_GET_fine_tuning.ipynb](notebooks/13_GET_fine_tuning.ipynb) | GET adaptation and regulatory interpretation |
| [14_Common_and_specific_TF_interaction.ipynb](notebooks/14_Common_and_specific_TF_interaction.ipynb) | Common and cell-type-specific candidate TF networks |
| [15_Variants_affect_TF_interaction.ipynb](notebooks/15_Variants_affect_TF_interaction.ipynb) | Structure-based interface and variant analyses |

## Citation and support

The accompanying paper will be released as a preprint:

> *AI-driven single-cell multi-omic modeling reveals the regulation of human hematopoiesis and pathogenic rewiring.*

The preprint link and complete citation will be added once it is posted. When using Hemelas, please cite the preprint when available and acknowledge the original datasets and analysis tools relevant to your work.

For code questions or reproducibility issues, [open a GitHub issue](https://github.com/Yu-Lab-Genomics/Hemelas_code/issues). For website and data enquiries, use **Contact us** in the [portal](https://hemelas.aigenomicsyulab.com/) footer.

## License

This repository's code is released under the [MIT License](LICENSE), copyright © 2026 Hemelas contributors. Third-party datasets, software, and model weights remain subject to their respective licenses and terms; this code license does not relicense those resources.
