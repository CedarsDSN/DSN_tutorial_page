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
