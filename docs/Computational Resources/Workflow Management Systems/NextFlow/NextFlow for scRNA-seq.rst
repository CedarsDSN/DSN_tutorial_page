**NextFlow for scRNA-seq**
===========================

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

  sample,fastq_1,fastq_2,expected_cells
  pbmc8k,pbmc8k_S1_L007_R1_001.fastq.gz,pbmc8k_S1_L007_R2_001.fastq.gz,10000
  pbmc8k,pbmc8k_S1_L008_R1_001.fastq.gz,pbmc8k_S1_L008_R2_001.fastq.gz,10000

Each row represents a fastq file (single-end) or a pair of fastq files (paired end).

Now, you can run the pipeline using:

.. code-block:: RST

  nextflow run nf-core/scrnaseq \
   -profile singularity \
   --input samplesheet.csv \
   --genome_fasta GRCm38.p6.genome.chr19.fa \
   --gtf gencode.vM19.annotation.chr19.gtf \
   --protocol 10XV2 \
   --aligner <alevin/kallisto/star/cellranger/universc> \
   --outdir <OUTDIR>

Note that the above code is for Mouse, but you can change the gtf and fasta to the genome that you are working with.

- -profile singularity is used because we use singularity to run NextFlow on HPC.

- --input is used to give the sample sheet which was created above with the FASTQ files for single-cell RNAseq analysis.

- --genome_fasta is used to provide the genome FASTA file for the organism that you are conducting single-cell RNA-seq analysis with.

- --gtf is used to provide the gene annotation file for alignment and quantification.

- --protocol is used to specify the protocol that was used to generate the single cell data e.g. 10x Genomics v2 Chemistry. Can be 'auto' (cellranger only), '10XV1', '10XV2', '10XV3', '10XV4', or any other protocol string that will get directly passed the respective aligner. 

- --aligner is the aligner that you'd like to use for your NextFlow scRNA alignment. It can be one of the following - simpleaf, kallisto, star, cellranger, cellrangerarc, cellrangermulti. simpleaf is the default. 

- --outdir is used to provide the path of the folder which will contain the results of the NextFlow run.

The GTF files and FASTA files for common organisms can be downloaded from UCSC genome browser `here <https://hgdownload.soe.ucsc.edu/downloads.html>`_ or from ENSEMBL `here <https://useast.ensembl.org/index.html>`_.


Depending on which pipeline you would like to run, you could run different pipelines under aligner -

- Alevin-Fry + AlevinQC

- STARSolo

- Kallisto + BUStools

- Cellranger

- UniverSC

Extensive quality checks are performed at each stage. Furthermore, depending on the aligner you would like, you can opt for additional parameters. Please refer to this detailed tutorial that was developed by NextFlow developers `here <https://nf-co.re/scrnaseq/4.0.0/>`_.

**Results**
The output directory will contain all the quality control reports and the outputs specific to the aligner chosen. 





