#build reference genome:
##hs37d5
This README explains where and how we get hs37d5 and its index files.

##Reference sequences
The reference fasta file in this directory was downloaded from the 1000 genome referfence hs37d5:

[ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/technical/reference/phase2_reference_assembly_sequence/](ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/technical/reference/phase2_reference_assembly_sequence/)

##Reference index:
we used *samtools-1.3*, *bwa-0.7.12* and *blasr* to build reference indexes 
```
samtools index hs37d5.fa
bwa index hs37d5.fa
sawriter hs37d5.blasr.sa hs37d5.fa
```

