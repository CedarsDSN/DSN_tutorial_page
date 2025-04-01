**Results from WGS**
====================

After running the WGS analysis pipeline, a set of structured output folders is generated. These outputs include raw data processing, variant calling, annotation, and summary reports, all essential for downstream interpretation and reproducibility.

This section outlines the purpose of each output folder and what you should expect to find inside. Below is the file structure of the results folder -

.. code-block:: RST

  results/
  ├── annotation/
  ├── csv/
  ├── multiqc/
  ├── pipeline_info/
  ├── preprocessing/
  ├── reference/
  ├── reports/
  └── variant_calling/

The table below describes the contents of each folder -

.. list-table:: Folder with outputs
   :widths: 20 20 60
   :header-rows: 1

   * - Folder
     - Contents
     - Description
   * - preprocessing/
     - FASTQ, BAM, trimming reports
     - Contains cleaned, aligned, and sorted reads. May include outputs from tools like BWA, SAMtools, GATK MarkDuplicates (e.g., duplicate marking).
   * - variant_calling/
     - .vcf, .bcf, .g.vcf
     - Raw and filtered variant call files from GATK or other callers. May include SNPs, INDELs, and structural variants.
   * - annotation/
     - .vcf, .txt, .csv
     - Functionally annotated variants (e.g., via VEP, SnpEff, ANNOVAR), including gene impacts, allele frequencies, and clinical significance.
   * - csv/
     - Summarized tables
     - Processed or summarized tabular results, often for downstream stats, visualization, or integration.
   * - multiqc/
     - multiqc_report.html
     - Unified quality control report covering FastQC, alignment stats, duplicate rates, coverage, etc.
   * - pipeline_info/
     - .yaml, .txt, .log
     - Workflow configuration, software versions, and run metadata for reproducibility.
   * - reference/
     - Reference genome, index files
     - FASTA and prebuilt index files (e.g., BWA, GATK, VEP), used during alignment and variant calling.
   * - reports/
     - PDF/HTML/Markdown summaries
     - High-level summaries including coverage reports, alignment metrics, variant stats, or project-level documentation.

-----------

**Key output files**

.. list-table:: Checklist
   :widths: 30 30
   :header-rows: 1

   * - File type
     - Description
   * - *.bam, *.bai
     - Aligned reads and index files (for IGV or variant callers)
   * - *.vcf, *.bcf
     - Variant calls, raw and filtered
   * - annotated.vcf
     - Variants with gene annotations and clinical tags
   * - coverage.txt, stats.csv
     - Coverage summaries per chromosome or sample
   * - multiqc_report.html
     - Visual dashboard for QC metrics

-----------

**Output Validation Checklist**

.. list-table:: Checklist
   :widths: 30 30
   :header-rows: 1

   * - Step
     - Validation
   * - Read quality (FastQC)
     - Mean Q > 30, even distribution
   * - Alignment (BAM files)
     - >95% mapped reads, proper pairing
   * - Duplicate removal
     - Duplicates marked or removed
   * - Variant calling success
     - Reasonable number of SNPs/INDELs
   * - Variant annotation
     - Annotated VCFs with gene and effect info
   * - QC overview
     - All tools successfully summarized in MultiQC



