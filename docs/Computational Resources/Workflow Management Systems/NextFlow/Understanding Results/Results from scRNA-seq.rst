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

