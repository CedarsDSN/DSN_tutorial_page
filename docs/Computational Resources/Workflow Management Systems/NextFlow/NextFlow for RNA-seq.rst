**NextFlow for RNA-seq**
========================

NextFlow has been set up for Cedars-Sinai in the SGE cluster (csclprd3-s001v.csmc.edu). If you have access to this cluster, you can directly load NextFlow using this command 

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
  ...
