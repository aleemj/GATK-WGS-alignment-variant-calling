# GATK WGS Alignment & Variant Calling Pipeline

Pipeline for whole genome sequencing (WGS) alignment and variant calling using GATK software

#Last updated by Adrian on 6 January 2026

--------------------------------------------------------------------------------------------

Overview
--------------------------------------------------------------------------------------------
This pipeline contains four main steps for WGS analysis. It is designed to process raw sequencing reads, perform alignment, variant calling, joint genotyping, and filtering to produce analysis ready genotype files (SNPs and INDELs).

Before running this pipeline, ensure you have a parent directory containing subfolders for each sample, each with the raw sequencing reads (FASTQ files). All necessary output directories will be created automatically.

--------------------------------------------------------------------------------------------

Step 1: Generate per-sample alignment & variant calling scripts
--------------------------------------------------------------------------------------------
Run once to:

Create output directories (BAM, VCF, intermediate, scripts)

Index the reference genome if necessary

Generate PBS compatible .sh scripts for each sample

Each generated script performs:

1. FASTQ concatenation
2. BWA-MEM alignment
3. BAM sorting
4. GATK MarkDuplicates
5. BAM indexing
6. GATK HaplotypeCaller (GVCF)

#Warning: Multithreaded. Does not submit jobs — generates scripts only.

Step 2: Submit jobs for each sample
--------------------------------------------------------------------------------------------
Submits .sh scripts generated in Step 1

Automatically skips samples whose BAM files already exist

Can be run repeatedly over several days until all samples are processed

Step 3: Joint Genotyping
--------------------------------------------------------------------------------------------
Computationally intensive

Merges all individual GVCF files into a GenomicsDB workspace

Runs GenotypeGVCFs to produce a joint VCF

Consider breaking the process by intervals or chromosomes if the dataset is very large

Can add new samples later using --genomicsdb-update-workspace-path

Step 4: Variant Filtering
--------------------------------------------------------------------------------------------
Splits the joint VCF into SNPs and INDELs

Applies GATK hard filtering for quality control

Produces PASS only VCFs ready for downstream analysis

Recommended: index filtered VCFs for faster downstream usage

Notes / Recommendations
--------------------------------------------------------------------------------------------
Edit user defined variables (paths, memory, threads, output names) before running

Steps 2 and 3 are resource intensive; monitor memory and walltime

Downstream tools (GWAS, annotation) require indexed VCFs

Helpful Resources:
--------------------------------------------------------------------------------------------
1. https://ngs101.com/how-to-analyze-whole-genome-sequencing-data-for-absolute-beginners-part-1-from-raw-reads-to-high-quality-variants-using-gatk/
2. https://gatk.broadinstitute.org/hc/en-us/articles/360035535912-Data-pre-processing-for-variant-discovery
3. https://gatk.broadinstitute.org/hc/en-us/articles/360035535932-Germline-short-variant-discovery-SNPs-Indels
4. https://gatk.broadinstitute.org/hc/en-us/articles/360035890431-The-logic-of-joint-calling-for-germline-short-variants
5. https://hpc.nih.gov/training/gatk_tutorial/
6. Van der Auwera GA & O'Connor BD. (2020). Genomics in the Cloud: Using Docker, GATK, and WDL in Terra (1st Edition). O'Reilly Media.
