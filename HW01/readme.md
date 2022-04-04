# Determining the SARS-CoV-2 lineage

I used [this](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512) genome as a reference.

Indexing was done by BWA using the command
`bwa index sequence.fasta`

Alignment and sorting the aligned reads was dome by the command
`bwa mem sequence.fasta Plate135H10.R1.fastq.gz Plate135H10.R2.fastq.gz | samtools sort -o aligned.bam -`

Indexing the bam file (in order to open in IGV to check possible misalignments)
`samtools index aligned.bam`
