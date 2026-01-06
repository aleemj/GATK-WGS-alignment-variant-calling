# GATK-WGS-alignment-variant-calling

Pipeline for WGS alignment and variant calling using GATK Software

Last updated by Adrian on 5 January 2026

##########READ ME!########
**
The following code contains 3 steps. Step 1 should be run once first, step 2 continuosly over the course until all samples are aligned. Then Step 3 and 4 once.

Before running this code, one should already have a sub-folder (raw) in the alignment folder containning many other subfolders - one for every sample containing the sequencing raw reads

Refer to Directory Structure for recommended directory structure.

Running these steps will create all subdirectories and store files accordingly

The final output will be genotype files (SNP and INDEL) ready for analysis depending on filtering applied.

Please edit directories accordingly before running.

#STEP 1

Run this once to create respective directories, index reference if required and write sh files for alignment of every sample until individual gvcf files.

#STEP 2 (Computationally intense)

runs as many sample sh files as the system allows, will check for already completed bam files before running remaining sh files. This line of code can be run as many times over the course of a few days until all samples are created.

#STEP 3 (Computationally intense, may consider breaking into smaller parts)

Joint genotyping step across all samples, merges all individual gvcf files and genotypes them. 

#STEP 4

Filters variants to provide analysis ready genotype file. Output final genotype files into a new subdirectory.

**Useful References
**
1. https://ngs101.com/how-to-analyze-whole-genome-sequencing-data-for-absolute-beginners-part-1-from-raw-reads-to-high-quality-variants-using-gatk/
2. https://gatk.broadinstitute.org/hc/en-us/articles/360035535912-Data-pre-processing-for-variant-discovery
3. https://gatk.broadinstitute.org/hc/en-us/articles/360035535932-Germline-short-variant-discovery-SNPs-Indels
