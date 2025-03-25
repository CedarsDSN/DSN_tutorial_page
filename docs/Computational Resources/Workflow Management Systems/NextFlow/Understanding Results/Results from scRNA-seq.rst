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
