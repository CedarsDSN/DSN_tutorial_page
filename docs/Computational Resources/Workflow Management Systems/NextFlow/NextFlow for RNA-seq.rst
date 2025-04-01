**NextFlow for RNA-seq**
========================

NextFlow has been set up for Cedars-Sinai in the compbio cluster (esplhpccompbio-lv01.csmc.edu). If you have access to this cluster, you can directly load NextFlow using this command 

.. code-block:: RST

  module load nextflow
  module load java/jdk-11.0.12

Along with the above, it is recommended to provide directories for singularity container execution and temporary storage. 

.. code-block:: RST

  export SINGULARITY_TMPDIR=/common/group_folder/data/project_folder
  export SINGULARITY_CACHEDIR=/common/group_folder/data/project_folder/singularity_cache

  export TMPDIR=/common/group_folder/projects/temp/project_folder

The next thing you would need is to create a samplesheet.csv file that has the information about the samples you are using for RNA-seq. The format should be comma-seperated columns and should contain the sample name, path of the FASTQ_1, path of the FASTQ_2 and the type of strandedness (Note - If you have single-ended reads, leave the third column empty like below) -

.. code-block:: RST

  sample,fastq_1,fastq_2,strandedness
  sample1,{path_for_your_data}/sample1.fastq.gz,,auto
  sample2,{path_for_your_data}/sample2.fastq.gz,,auto
  sample3,{path_for_your_data}/sample3.fastq.gz,,auto
  and so on..

You are now ready to run NextFlow by using this command providing the above samplesheet.csv

.. code-block:: RST

  nextflow run \
    nf-core/rnaseq \
    --aligner star_rsem \
    --gencode \
    --skip_bigwig \
    --input {path_for_your_samplesheet}/samplesheet.csv \
    --outdir {path_for_your_results_folder}/results  \
    --gtf {path_for_your_gtf}/gencode.vM36.primary_assembly.annotation.gtf.gz \
    --fasta {path_for_your_reference}/GRCm39.primary_assembly.genome.fa.gz \
    -profile singularity \


Note that the above code is for Mouse, but you can change the gtf and fasta to the genome that you are working with.

- --aligner is the aligner that you wish to use for your NextFlow run. You can specify out of three options - star_salmon, star_rsem, and hisat2. Default is star_salmon.

- --gencode is used to specify that your gtf annotation is in GENCODE format.

- --skip_bigwig is used to skip bigWig file creation.

- --input is used to give the sample sheet which was created above with the FASTQ files for RNAseq analysis.

- --outdir is used to provide the path of the folder which will contain the results of the NextFlow run.

- --gtf is used to provide the gene annotation file for alignment and quantification.

- --fasta is used to provide the genome FASTA file for the organism that you are conducting RNA-seq analysis with.

- --profile singularity is used because we use singularity to run NextFlow on HPC.

The GTF files and FASTA files for common organisms can be downloaded from UCSC genome browser `here <https://hgdownload.soe.ucsc.edu/downloads.html>`_ or from ENSEMBL `here <https://useast.ensembl.org/index.html>`_.

The above code combines the STAR tool for alignment and the RSEM tool for quantification. However, NextFlow for RNA-seq is not restricted to this combination. You can do various permutations depending on your end goals

- STAR + RSEM
- STAR + Salmon
- HISAT2 (No quantification)
- Pseudoalignment (Kallisto or Salmon)

There are also extensive quality control tools that are executed with the minimum parameters above. You can provide additional ones depending on your end goals. Please refer to this detailed tutorial that was developed by NextFlow developers `here <https://nf-co.re/rnaseq/3.18.0/>`_

**Results**

The results folder will have the alignment and quantification files. It will also contain all the files generated from the quality control steps such as MultiQC, FASTQC, etc. For more information about the results generated, navigate to the "Results" section.
