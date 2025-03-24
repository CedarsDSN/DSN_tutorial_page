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




**Tips for Exploring Outputs**

- Open HTML reports (fastqc/*.html, multiqc/multiqc_report.html) in your browser to review quality metrics.

- Inspect alignments with tools like samtools or load BAM files into IGV:

.. code-block:: RST

  samtools view star_rsem/sample1.Aligned.toTranscriptome.out.bam | head

- Check gene expression values in star_rsem/sample1.genes.results – it includes estimated counts, TPM, and FPKM values from RSEM.



**Output Validation Checklist**

.. list-table:: Checklist
   :widths: 30 30
   :header-rows: 1

   * - Checkpoint
     - Expected outcome
   * - FastQC quality scores
     - > Q30 in most regions
   * - Trim Galore adapter removal
     - Adapter content minimized
   * - STAR alignment rate
     - >80% uniquely mapped reads
   * - RSEM gene counts
     - Non-zero counts for expressed genes
   * - MultiQC report
     - Aggregated view with no major warnings

To explore more indepth explanations for interpreting your FASTQC and multiQC reports, you can use this video link for multiQC and this manual for FASTQC. 
https://www.youtube.com/watch?v=qPbIlO_KWN0&ab_channel=PhilEwels
