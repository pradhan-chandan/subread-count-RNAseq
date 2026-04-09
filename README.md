# RNA-seq Gene Expression Quantification with featureCounts

A lightweight Bash script for counting reads per gene from paired-end RNA-seq alignments using [featureCounts](https://subread.sourceforge.net/) (part of the Subread package).

## Overview

This script automates gene-level read quantification across multiple BAM files using a reference genome annotation (GFF format). It is designed for paired-end RNA-seq data and outputs a count matrix suitable for downstream differential expression analysis (e.g., DESeq2, edgeR).
This script ignores multi mapped reads and only takes uniquely mapped reads into account
## Requirements

- [`featureCounts`](https://subread.sourceforge.net/) (Subread ≥ 2.0)
- Sorted and indexed BAM files (e.g., from HISAT2 or STAR alignment)
- A genome annotation file in GFF/GFF3 format

# Script for read count
```
#!/bin/bash

ANNOTATION=/path/genome.gff \
BAM_DIR=/path to folder of .bam files/ \
OUTPUT=/path/align_500max_paired_geneexp.txt

# -------- Parameters --------
THREADS=8 \
FEATURE_TYPE=gene \
GENE_ID=ID

# -------- Run featureCounts --------
featureCounts \
  -T ${THREADS} \
  -a "${ANNOTATION}" \
  -t ${FEATURE_TYPE} \
  -g ${GENE_ID} \
  -p \
  --countReadPairs \
  -o "${OUTPUT}" \
  "${BAM_DIR}"/*.bam

echo "featureCounts completed successfully"
```
