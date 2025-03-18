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
  sample1,/common/group_folder/data/project_folder/large_data/sample1.fastq.gz,,auto
  sample2,/common/group_folder/data/project_folder/large_data/sample2.fastq.gz,,auto
  sample3,/common/group_folder/data/project_folder/large_data/sample3.fastq.gz,,auto
  and so on..

You are now ready to run NextFlow by using this command providing the above samplesheet.csv

.. code-block:: RST

  nextflow run \
    nf-core/rnaseq \
    --aligner star_rsem \
    --gencode \
    --skip_bigwig \
    --input /common/group_folder/data/project_folder/analysis/nextflow/samplesheet.csv \
    --outdir /common/group_folder/data/project_folder/analysis/nextflow/results  \
    --gtf /common/group_folder/reference/Mouse/gencode.vM36.primary_assembly.annotation.gtf.gz \
    --fasta /common/compbiomed-dsn/reference/Mouse/GRCm39.primary_assembly.genome.fa.gz \
    -profile singularity \


Note that the above code is for Mouse, but you can change the gtf and fasta to the genome that you are working with.

The above code combines the STAR tool for alignment and the RSEM tool for quantification. However, NextFlow for RNA-seq is not restricted to this combination. You can do various permutations depending on your end goals

- STAR + RSEM
- STAR + Salmon
- HISAT2 (No quantification)
- Pseudoalignment (Kallisto or Salmon)

There are also extensive quality control tools that are executed with the minimum parameters above. You can provide additional ones depending on your end goals. Please refer to this detailed tutorial that was developed by NextFlow developers `here <https://nf-co.re/rnaseq/3.14.0/>`_

**Results**

The results folder will have the alignment and quantification files. It will also contain all the files generated from the quality control steps such as MultiQC, FASTQC, etc.
