# GATK-WGS-alignment-variant-calling

Pipeline for WGS alignment and variant calling using GATK Software

Last updated by Adrian on 2 January 2026

##########READ ME!##########

the following code contains 3 steps. Step 1 should be run once first, step 2 continuosly over the course until all samples are aligned. Then Step 3 once.

before running this code, one should already have a sub-folder (raw) in the alignment folder containning many other subfolders - one for every sample containing the raw reads

Recommended directory structure

project/

├── ref/

    ├── genome.fa

    ├── genome.fa.fai

    └── genome.dict

├── fastq/

    ├── sample1

    ├── sample2

    └── ...

├── bam_files/

├── vcf_files/

├── sh_files/

├── intermediate_files/


running these steps will create all subdirectories and store files accordingly

the final output will be genotype files ready for analysis depending on filtering applied

please edit directories accordingly

#STEP 1

Run this once to create respective directories, index reference if required and write sh files for alignment of every sample until individual gvcf files.

#STEP 2

runs as many sample sh files as the system allows, will check for already completed bam files before running remaining sh files. This line of code can be run as many times over the course of a few days until all samples are created.

#STEP 3

Joint genotyping step across all samples, merges all individual gvcf files and genotypes them. Filters variants to provide analysis ready genotype file. Output final genotype files into a new subdirectory.
