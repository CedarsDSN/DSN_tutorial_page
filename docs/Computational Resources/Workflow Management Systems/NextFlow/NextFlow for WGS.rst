**NextFlow for WGS**
====================

NextFlow has been set up for Cedars-Sinai in the compbio cluster (esplhpccompbio-lv01.csmc.edu). If you have access to this cluster, you can directly load NextFlow using this command

.. code-block:: RST

  module load nextflow
  module load java/jdk-11.0.12

Along with the above, it is recommended to provide directories for singularity container execution and temporary storage. 

.. code-block:: RST

  export SINGULARITY_TMPDIR=/common/group_folder/data/project_folder
  export SINGULARITY_CACHEDIR=/common/group_folder/data/project_folder/singularity_cache

  export TMPDIR=/common/group_folder/projects/temp/project_folder

The next thing you would need is to create a samplesheet.csv file with information about the samples you are using for WGS analysis. The format should be comma-separated columns and should contain the patient ID, sample name, the lane, and the path of the paired fastq files. Each row represents a pair of fastq files. 

.. code-block:: RST

  patient,sample,lane,fastq_1,fastq_2
  ID1,S1,L001,ID1_S1_L001_R1_001.fastq.gz,ID1_S1_L001_R2_001.fastq.gz
  ID1,S1,L002,ID1_S1_L002_R1_001.fastq.gz,ID1_S1_L002_R2_001.fastq.gz
  ID1,S2,L001,ID1_S2_L001_R1_001.fastq.gz,ID1_S2_L001_R2_001.fastq.gz
  ID2,S1,L001,ID2_S1_L001_R1_001.fastq.gz,ID2_S1_L001_R2_001.fastq.gz
  ID2,S1,L002,ID2_S1_L002_R1_001.fastq.gz,ID2_S1_L002_R2_001.fastq.gz
  ID2,S2,L001,ID2_S2_L001_R1_001.fastq.gz,ID2_S2_L001_R2_001.fastq.gz
  ID3,S1,L001,ID3_S1_L001_R1_001.fastq.gz,ID3_S1_L001_R2_001.fastq.gz
  ID3,S1,L002,ID3_S1_L002_R1_001.fastq.gz,ID3_S1_L002_R2_001.fastq.gz
  ID3,S2,L001,ID3_S2_L001_R1_001.fastq.gz,ID3_S2_L001_R2_001.fastq.gz
This supports multi-lane, multi-sample, and tumor/normal pairings.


You are now ready to run NextFlow by using this command providing the above samplesheet.csv.
The nf-core/sarek pipeline is a best-practice-compliant, production-ready pipeline for variant calling (both germline and somatic) from Whole Genome (WGS) or Whole Exome Sequencing (WES) data. Built on Nextflow, it supports containerization (Docker/Singularity), cloud computing, and HPC environments, making it reproducible and scalable.

.. code-block:: RST

  nextflow run nf-core/sarek \
     -profile singularity \
     --input samplesheet.csv \
     --outdir {path_for_your_results_folder}/results

This is the default command line that you can use when you don't want to change any parameters. 

- --profile singularity is used because we use singularity to run NextFlow on HPC.
- --input is the samplesheet.csv that you would create for your samples using the format above
- --outdir is the folder that would be used by NextFlow to save all results of the pipeline

*Note* - The default genome here is GATK.GRCh38. If you would like to change it to the genome of your choice, you can provide the ID for your reference. The reference for your genome of choice can be found `here <https://support.illumina.com/sequencing/sequencing_software/igenome.html>`_

.. list-table:: Key pipeline options
   :widths: 30 30
   :header-rows: 1

   * - Additional Parameters
     - Description
   * - --genome
     - Genome build (e.g. GRCh38, GRCh37)
   * - --tools
     - Comma-separated list of variant callers
   * - --somatic
     - Enables somatic calling (requires tumor/normal pairs)
   * - --germline
     - Enables germline variant calling
   * - --step
     - Run from a specific step (mapping, variant_calling, etc.)
   * - --saveReference
     - Saves intermediate reference files (useful for large-scale runs)

.. list-table:: Tools used in Sarek
   :widths: 30 30
   :header-rows: 1

   * - Step
     - Tools
   * - QC
     - FastQC, MultiQC, BCFtools stats
   * - Trimming (optional)
     - FastP
   * - Alignment
     - bwa-mem (default), bwa-mem2, dragmap, sentieon-bwamem
   * - MarkDuplicates
     - GATK MarkDuplicates, Sentieon LocusCollector and Sentieon Dedup
   * - Base Recalibration
     - GATK BaseRecalibrator and GATK ApplyBQSR
   * - Variant Calling
     - GATK HaplotypeCaller (germline), Mutect2 (somatic), Strelka2, FreeBayes, VarDict
   * - Annotation
     - VEP (Variant Effect Predictor)
   * - Structural Variant
     - Manta (optional)

There are also extensive quality control tools that are executed with the minimum parameters above. You can provide additional ones depending on your end goals. Please refer to this detailed tutorial that was developed by NextFlow developers `here <https://nf-co.re/sarek/3.5.1/>`_

**Results**

The results folder will have the alignment, annotation and variant calling files. It will also contain all the files generated from the quality control steps such as MultiQC, FASTQC, etc. For more information about the results generated, navigate to the "Results" section.
