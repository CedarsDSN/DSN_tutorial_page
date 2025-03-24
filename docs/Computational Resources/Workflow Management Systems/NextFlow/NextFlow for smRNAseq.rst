**NextFlow for smRNAseq**
=========================

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

  sample,fastq_1
  Clone1_N1,s3://ngi-igenomes/test-data/smrnaseq/C1-N1-R1_S4_L001_R1_001.fastq.gz
  Clone1_N3,s3://ngi-igenomes/test-data/smrnaseq/C1-N3-R1_S6_L001_R1_001.fastq.gz
  Clone9_N1,s3://ngi-igenomes/test-data/smrnaseq/C9-N1-R1_S7_L001_R1_001.fastq.gz
  and so on..

You are now ready to run NextFlow by using this command providing the above samplesheet.csv

.. code-block:: RST

  nextflow run nf-core/smrnaseq \
   -profile singularity \
  --input samplesheet.csv \
  --genome 'GRCh37' \
  --mirtrace_species 'hsa' \
  --protocol 'illumina' \
  --outdir <OUTDIR>

Note that the above code is for Human, but you can change the genome and mirtrace_species to the genome that you are working with.

- -profile singularity is used because we use singularity to run NextFlow on HPC.

- --input is used to give the sample sheet which was created above with the FASTQ files for small RNAseq analysis.

- --genome is used to provide the iGenomes reference.

- --mirtrace_species is used to provide the species for miRTrace. Example values: hsa, mmu... Note that mirTrace relies on miRBase for its species reference. For thr full list of species codes, refer `this <https://www.mirbase.org/browse/>`_.

- --protocol is used to specify the protocol that was used to construct the smRNAseq libraries. Choose on out of these - illumina, nextflex, qiaseq, cats, custom. When running --protocol custom the user must define the 3' Adapter Sequence. If trimming parameters aren't provided the pipeline will deafult to clip_R1 = 0 and three_prime_clip_R1 = 0 (i.e. no extra clipping).

- --outdir is used to provide the path of the folder which will contain the results of the NextFlow run.

The workflow conducts many quality control checks and filtering, after which it carries out miRNA quantification. Genome quantification is also an option but it's optional. You can also discover Novel and known miRNAs which is also optional. You can explore the other parameters and details using this tutorial developed by the NextFlow developers here.

**Results**
The quality control files generated through the pipeline will be saved in the results/out directory. The miRNA quantification files will also be available in the same folder. Please navigate to the "Results" section for more information on understanding the results. 

