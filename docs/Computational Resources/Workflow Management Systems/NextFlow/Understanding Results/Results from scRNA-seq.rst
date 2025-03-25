**Results from scRNA-seq**
==========================

Upon completion of the single-cell RNA-seq workflow, several output folders are generated. These capture each step of the pipeline, from raw quality checks and alignments to gene-level quantification and downstream-ready data objects.

This section describes the content and purpose of each output folder to help you understand what was generated and how to use it. Below is the file structure if CellRanger is chosen as the aligner.

.. code-block:: RST

  results/
  ├── fastqc/
  ├── fq_lint/
  ├── trimgalore/
  ├── cellranger/
  ├── counts/
  ├── qc/
  ├── scanpy/
  ├── multiqc/
  └── pipeline_info/


The table below describes the contents of each folder -

.. list-table:: Folder with outputs
   :widths: 20 20 60
   :header-rows: 1

   * - Folder
     - Contents
     - Description
   * - fastqc/
     - FastQC .html, .zip
     - Raw read quality reports
   * - fq_lint/
     - fastq-lint .txt, .json
     - FASTQ integrity and formatting checks
   * - trimgalore/
     - Trimmed reads and reports
     - Adapter removal and quality trimming
   * - cellranger/
     - Count matrices and QC reports
     - Primary Cell Ranger output (see below)
   * - counts/
     - Processed matrices (.tsv, .h5)
     - Unified or filtered count matrices
   * - qc/
     - Doublet detection & cell filtering
     - DoubletFinder, Scrublet, etc.
   * - scanpy/
     - .h5ad AnnData objects
     - Downstream-ready files for analysis
   * - multiqc/
     - Aggregated QC report
     - Combines reports from FastQC, Trim Galore, etc.
   * - pipeline_info/
     - Logs, software versions, config
     - For reproducibility and debugging

============

**Exploring CellRanger output**

Each sample under cellranger/ contains:

.. code-block:: RST

  cellranger/
  └── sample1/
      └── outs/
          ├── filtered_feature_bc_matrix/
          │   ├── matrix.mtx.gz
          │   ├── barcodes.tsv.gz
          │   └── features.tsv.gz
          ├── metrics_summary.csv
          ├── web_summary.html
          └── ... (optional: BAM files, clustering outputs)

You can:

Open web_summary.html for key stats (e.g., # of cells, reads per cell, UMI counts).

Load the filtered matrix into Scanpy or Seurat.

Use metrics_summary.csv for structured QC across samples.

================

**Output Differences with Other Pipelines**

- **STARsolo**

If you run the workflow using STARsolo, you'll find:

.. code-block:: RST

  star_solo/
  └── sample1/
      └── Solo.out/
          └── Gene/
              ├── matrix.mtx
              ├── features.tsv
              └── barcodes.tsv

* Outputs are similar in structure to Cell Ranger.

* You can load directly into Scanpy or convert as needed.

- **Kallisto + BUStools**

If using Kallisto + BUStools, the structure is:

.. code-block:: RST

  kallisto/
  └── sample1/
      ├── counts_unfiltered/
      │   ├── matrix.mtx
      │   ├── features.tsv
      │   └── barcodes.tsv
      └── counts_filtered/
          ├── matrix.mtx
          ├── features.tsv
          └── barcodes.tsv

* Filtering may be done via bustools correct and bustools count.

* Compatible with standard analysis pipelines after conversion.

- **SimpleAF (Alevin-Fry) + AlevinQC**

With SimpleAF, the outputs live in:

.. code-block:: RST

  alevin/
  └── sample1/
      ├── quant.json
      ├── featureDump.txt
      ├── filtered_mtx/
      │   ├── matrix.mtx
      │   ├── features.tsv
      │   └── barcodes.tsv
      └── alevinqc/
          └── alevinqc_report.html

* filtered_mtx/ is analogous to the filtered Cell Ranger output.

* alevinQC_report.html provides detailed QC like gene diversity, knee plots, and barcode filtering.

==================

**Output Validation Checklist**


