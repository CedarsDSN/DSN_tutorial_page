**Results from RNA-seq**
========================

After running the Nextflow RNA-seq workflow, the following output folders are generated. Each contains key intermediate or final results essential for evaluating data quality, alignment, quantification, and overall pipeline execution.

If you run alignemnt using star_rsem aligner, then the following folders will be generated. Note, if you use star_salmon, then the star_rsem folder below will be renamed as star_salmon. If you choose to use hisat2, then the star_rsem folder will be renamed as hisat2. 

.. code-block:: RST

  results/
  ├── fastqc/
  ├── fq_lint/
  ├── trimgalore/
  ├── star_rsem/
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
     - .html, .zip
     - Raw read quality control reports from FastQC. These provide per-base quality scores, adapter content, sequence duplication levels, etc.
   * - fq_lint/
     - .json, .txt
     - Quality statistics and metadata from fastq-lint. Helps in checking FASTQ file structure, line integrity, and format issues.
   * - trimgalore/
     - .fq.gz, .html, .txt
     - Trimmed FASTQ files and reports from Trim Galore! Used to remove adapter sequences and low-quality bases.
   * - star_rsem/
     - .bam, .genes.results, .stat
     - STAR-aligned BAM files and gene/transcript quantifications from RSEM. This is where expression quantification happens.
   * - multiqc/
     - multiqc_report.html
     - Unified quality control summary compiled from all tools using MultiQC. Includes FastQC, Trim Galore, STAR, and RSEM summaries.
   * - pipeline_info/
     - .log, .yaml, .txt
     - Runtime information about the pipeline execution including software versions, parameters used, and Nextflow logs.

