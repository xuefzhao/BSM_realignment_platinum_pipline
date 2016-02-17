# BSM_realignment_platinum_pipline

##build reference genome:

###GRCh38_BSM.fa

This README explains how we built the GRCh38_BSM.fa and its index files.

##Reference datasets/programs
1. Samtools 1.3:  
    [http://www.htslib.org/doc/samtools-1.3.html](http://www.htslib.org/doc/samtools-1.3.html)

2. Aligner BWA-MEM bwakit-0.7.12: 
    [http://sourceforge.net/projects/bio-bwa/files/bwakit/bwakit-0.7.12_x64-linux.tar.bz2/download](http://sourceforge.net/projects/bio-bwa/files/bwakit/bwakit-0.7.12_x64-linux.tar.bz2/download)
    
    [bwa readme](https://github.com/lh3/bwa/blob/master/bwakit/README.md)

3. Pacbio Alignmer blasr from EichlerLab: 
    [https://github.com/EichlerLab/blasr](https://github.com/EichlerLab/blasr)

##Reference sequences
The reference fasta file in this directory was modified from the 1000 genome referfence GRCh38:

[ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/technical/reference/GRCh38_reference_genome/GRCh38_full_analysis_set_plus_decoy_hla.fa](ftp://ftp-trace.ncbi.nih.gov/1000genomes/ftp/technical/reference/GRCh38_reference_genome/GRCh38_full_analysis_set_plus_decoy_hla.fa)

####in this version, we INCLUDE:
1.  **Chromosomes:**
    chr{chromosome number or name}
    e.g. chr1 or chrX
    chrM for the mitochondrial genome.

2.  **Unlocalized scaffolds:**
    chr{chromosome number or name}_{sequence_accession}v{sequence_version}_random
    e.g. chr17_GL000205v2_random
    
3.  **Unplaced scaffolds:**
    chrUn_{sequence_accession}v{sequence_version}
    e.g. chrUn_GL000220v1
    
4.  **Decoy sequences:**
    chrUn_{sequence_accession}v{sequence_version}_decoy
    e.g. chrUn_KN707606v1_decoy


####and EXCLUDE:
 1. **Alternate loci scaffolds:**
    chr{chromosome number or name}_{sequence_accession}v{sequence_version}_alt
    e.g. chr6_GL000250v2_alt
    
2.  **Patch scaffolds:**
    chr{chromosome number or name}_{sequence_accession}v{sequence_version}_patch
    e.g. chrY_KN196487v1_patch 
    
3.  **HLA sequences:**
    HLA-{id}
    e.g. HLA-A*02:53N
 

##Modified reference:
we used our own python script to exclude:Alternate loci scaffolds, Patch scaffolds and HLA sequences from the reference; 

modified references were indexed in file: **GRCh38_BSM.fa**

and excluded references were indexed in file: **GRCh38_BSM_excluded.fa**

we used *samtools-1.3*, *bwa-0.7.12* and *blasr* to build reference indexes 

for detailed linux commands and python code, please refer to **README_GRCh38_BSM_Command**
