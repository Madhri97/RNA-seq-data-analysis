Rna Seq Data Analysis: Generating Count Matrix 

Downloading the RNA seq data for breast cancer in fastq format from SRA- https://www.ncbi.nlm.nih.gov/sra  
SRA : SRR8944230: GSM3733363: RIPZ; Homo sapiens; RIP-Seq
Study: YTHDF3 Induces the Translation of m6A-enriched Metastasis-associated Gene Transcripts to Promote Breast Cancer Brain Metastasis [RIP-Seq].
Library:
Instrument: Illumina HiSeq 4000
Strategy: RIP-Seq
Source: TRANSCRIPTOMIC
Selection: other
Layout: SINGLE
GEO Accession: GSM3733363
************************************************************************************************************************************************
Unzipping the fastq. gz file using linux
Command
 gunzip SRR8944230.fastq.gz.
o/p file: SRR8944230.fastq
Downloading SRA toolkit
Commands:
sudo apt-get install sra-toolkit
vdb-config --interactive
Once you've completed the configuration, you should be able to use the SRA Toolkit commands as intended.
prefetch SRR123456
fastq-dump SRR123456
************************************************************************************************************************************************
Quality check
Command: 
fastqc SRR8944230.fastq
o/p file: SRR8944230_fastqc.html
************************************************************************************************************************************************
Cutadapt installation and Usage
sudo apt install python3
sudo apt install python3-pip
sudo pip3 install cutadapt
************************************************************************************************************************************************
Splice Junction Mapping: HISAT2
Downloading the human reference genome from UCSC browser
sudo apt-get update
sudo apt-get -y install hisat2
Command to build the reference index using HISAT2
hisat2-build hg38.fa hg38index
Command to align the reads to the reference genome using HISAT2
Hisat2 -x hg38index -U SRR8944230.fastq -S out.sam
************************************************************************************************************************************************
Samtools is a set of utilities that manipulate alignments in the SAM (Sequence Alignment/Map), BAM, and CRAM formats
sudo apt-get  install samtools
Command: 
samtools view -S -b out.sam> out.bam
************************************************************************************************************************************************
Quantification of mapped reads
Installing FeatureCounts using command:
sudo apt install subread 
Downloading the Gtf file for hg38 from UCSC Genome Browser:
Convert the BED file to GTF format using a tool such as the UCSC utility "bedToGenePred" and "genePredToGtf" utilities, which can be found in the UCSC utilities repository.

Generating count matrix using FeatureCounts 
Command: 
featureCounts -M --largestOverlap -a output1.gtf -o count.txt out.bam 
***********************************************************************************************************************************************





