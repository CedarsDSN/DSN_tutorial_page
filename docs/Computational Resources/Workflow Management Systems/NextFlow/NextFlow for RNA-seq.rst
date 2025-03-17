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
