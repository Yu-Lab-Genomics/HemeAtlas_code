# Hemelas

**A paired single-cell multi-omics atlas and regulatory modeling framework for human hematopoiesis.**

[Explore the website](https://hemelas.aigenomicsyulab.com/) · [Website manual](https://hemelas.aigenomicsyulab.com/#user-guide-preview) · [Data downloads](#data-downloads) · [Analysis notebooks](#analysis-notebooks) · [MIT License](LICENSE)

## About the study

This repository accompanies **“AI-driven single-cell multi-omic modeling reveals the regulation of human hematopoiesis and pathogenic rewiring.”**

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

The **Data Download** module is the central catalogue for the resources below. The direct links use the same download endpoints as the website buttons. File sizes are approximate values displayed by the portal and may change as resources are updated.

### Single-cell and metacell data

| Resource | Download | Approximate size |
| --- | --- | ---: |
| Single-cell RNA, full data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=rna_all) | 6.5 GB |
| Single-cell RNA, web data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=rna_web) | 1.4 GB |
| Single-cell ATAC, full gene activity data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=atac_full_activity) | 15.8 GB |
| Single-cell ATAC, web gene activity data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=atac_web_activity) | 3.8 GB |
| Single-cell ATAC peak matrix | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=atac_peak_matrix) | 20.2 GB |
| ATAC fragment archives | **Data Download → Single-cell data → ATAC → Fragments data → View & Download** | Varies by archive |
| SEACells, RNA data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=seacells_rna) | 3.8 GB |
| SEACells, ATAC peak data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=seacells_atac_peak) | 21.9 GB |
| SEACells, gene accessibility data | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=seacells_access) | 53.2 GB |

The portal distinguishes **Full data** from **Web data**. Select the resource appropriate to your task and inspect its contents and metadata before analysis. Gene activity/accessibility scores and peak-level counts are different representations and should not be treated as interchangeable matrices.

### Models, regulatory associations, structures, and variants

| Resource | Download | Approximate size |
| --- | --- | ---: |
| Fine-tuned GET, HSPC model | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=model_hspc) | 990 MB |
| Fine-tuned GET, full model | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=model_full) | 990 MB |
| Motif–motif associations by cell type | **Data Download → Fine-tuned GET models → Motif-motif data** | Varies by cell type |
| AlphaFold 3, common interaction structures | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=af_common_data) | 61.2 MB |
| AlphaFold 3, common interface-site table | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=af_common_sites) | 73.1 KB |
| AlphaFold 3, cell-type-specific interaction structures | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=af_specific_data) | 374.8 MB |
| AlphaFold 3, cell-type-specific interface-site table | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=af_specific_sites) | 229.9 KB |
| TF variants from ClinVar | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=variants_clinvar) | 15.1 MB |
| Common TF interactions and variants | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=variants_common) | 35.2 KB |
| Cell-type-specific TF interactions and variants | [Download](https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=variants_specific) | 154.3 KB |

Download only the resources needed for your analysis; the largest matrices and fragment archives require substantial disk space. For a command-line download, use the selected link, follow redirects, and save it under an appropriate local filename. For example:

```bash
mkdir -p data/variants
curl --fail --location --retry 3 \
  'https://hemelas.aigenomicsyulab.com/download/dl/dataset/?type=variants_common' \
  --output data/variants/common_tf_variant_disease.csv
```

Source dataset accessions and sample metadata are described in **Supplementary Data 1–2** of the manuscript. **Supplementary Data 3–12** describe the harmonized peak catalogue, annotation hierarchy, motif-to-TF mapping, inferred interactions, interface residues, and variant associations. The website resources are not bundled in this Git repository.

## Using this code repository

The repository provides the study's analysis notebooks, from source-data processing through regulatory and variant analysis. The numbering describes the broad analysis stages; it is not a single executable pipeline.

### Get the notebooks

```bash
git clone https://github.com/Yu-Lab-Genomics/Hemelas_code.git
cd Hemelas_code
# While this documentation update is under review:
git switch cleanup/english-portable-paths
```

### Prepare the analysis environment and inputs

1. **Choose an analysis stage** from the notebook index below. Read its imports and input/output paths before running any cells.
2. **Download the required data** from the portal and obtain any additional source-study files, reference genomes, annotations, or model assets required by that stage. The download catalogue does not guarantee a one-to-one match with every historical intermediate filename.
3. **Set up the relevant tools.** Python analyses use packages such as Scanpy, AnnData, SnapATAC2, CellTypist, CellHint, SEACells, CellRank, scVelo, PyTorch, and GET, depending on the notebook. R sections use tools such as Seurat and Signac. Peak calling and structure prediction additionally require MACS2 and AlphaFold 3, respectively. Install the dependencies for your selected stage using the corresponding projects' instructions.
4. **Configure paths.** Replace every relevant `/path/to/...` placeholder with your own data, reference, model, or executable location. Check relative paths against the intended working directory and create output directories as needed.
5. **Run selected sections in the appropriate interpreter.** Open Python sections in Jupyter with the intended environment. Run R and Bash sections in R and a shell, respectively, or explicitly configure an interpreter bridge.

For a Python analysis environment with JupyterLab installed, start the notebook interface with:

```bash
jupyter lab
```

Use a separate output directory for derived results and retain cell/feature identifiers when aligning data across modalities. Model checkpoints require the matching GET architecture and configuration; the [GET implementation](https://github.com/GET-Foundation/get_model) provides the upstream model code.

### Analysis notebooks

| Notebook | Analysis stage |
| --- | --- |
| [0_Visual.ipynb](0_Visual.ipynb) | Atlas overview and visualization |
| [1_ATAC_modality_and_cCREs.ipynb](1_ATAC_modality_and_cCREs.ipynb) | ATAC processing and candidate cis-regulatory regions |
| [2_Matrix_from two_modality.ipynb](2_Matrix_from%20two_modality.ipynb) | Assembly of RNA and ATAC matrices |
| [3_Cell_annotation_from_paper.ipynb](3_Cell_annotation_from_paper.ipynb) | Collection and harmonization of source-study cell annotations |
| [4_Preprocess_celltypist_cellhint.ipynb](4_Preprocess_celltypist_cellhint.ipynb) | Preprocessing and reference-based annotation |
| [5_Cell_annotation_from_majority_voting.ipynb](5_Cell_annotation_from_majority_voting.ipynb) | Consensus annotation by majority voting |
| [6_Integrate_using_snapatac2_and_wnn.ipynb](6_Integrate_using_snapatac2_and_wnn.ipynb) | Spectral and multimodal integration analyses |
| [7_Integrate_using_multiple_algorithms.ipynb](7_Integrate_using_multiple_algorithms.ipynb) | Comparison of additional integration methods |
| [8_New_data_and_delete_share-seq_data.ipynb](8_New_data_and_delete_share-seq_data.ipynb) | Dataset updates and atlas assembly |
| [9_Hemelas_cell_annotation.ipynb](9_Hemelas_cell_annotation.ipynb) | Harmonized Hemelas cell annotation |
| [10_Hemelas_Integrate_benchmark.ipynb](10_Hemelas_Integrate_benchmark.ipynb) | Integration benchmarking |
| [11_Subcluster_analysis.ipynb](11_Subcluster_analysis.ipynb) | Fine-grained cell-state annotation and visualization |
| [12_SEACells_analysis.ipynb](12_SEACells_analysis.ipynb) | Metacell aggregation and downstream analyses |
| [13_GET_fine_tuning.ipynb](13_GET_fine_tuning.ipynb) | GET adaptation and regulatory interpretation |
| [14_Common_and_specific_TF_interaction.ipynb](14_Common_and_specific_TF_interaction.ipynb) | Common and cell-type-specific candidate TF networks |
| [15_Variants_affect_TF_interaction.ipynb](15_Variants_affect_TF_interaction.ipynb) | Structure-based interface and variant analyses |

### Reproducibility status

These notebooks preserve historical analysis code and currently require adaptation to a local environment. The repository does not yet provide a pinned environment or a complete input manifest. Some notebooks mix Python, R, and Bash, and known execution issues are recorded in [CODE_REVIEW.md](CODE_REVIEW.md). Review the relevant findings before using **Run All**.

Stored execution outputs were cleared during publication cleanup. This cleanup did not rerun the scientific analyses or resolve all existing code issues. Original outputs remain in Git history.

## Citation and support

When using Hemelas data or analyses, please acknowledge the accompanying manuscript:

> *AI-driven single-cell multi-omic modeling reveals the regulation of human hematopoiesis and pathogenic rewiring.*

A complete bibliographic citation and publication link will be added when available. Please also cite the original datasets and analysis tools relevant to your work.

For code questions or reproducibility issues, [open a GitHub issue](https://github.com/Yu-Lab-Genomics/Hemelas_code/issues). For website and data enquiries, use **Contact us** in the [portal](https://hemelas.aigenomicsyulab.com/) footer.

## License

This repository's code is released under the [MIT License](LICENSE), copyright © 2026 Hemelas contributors. Third-party datasets, software, and model weights remain subject to their respective licenses and terms; this code license does not relicense those resources.
