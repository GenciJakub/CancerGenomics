# Determining the SARS-CoV-2 lineage

I used [this](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512) SARS-CoV-2 genome as a reference.

Indexing was done by BWA using the command

`bwa index sequence.fasta`

Alignment and sorting the aligned reads was dome by the command

`bwa mem sequence.fasta Plate135H10.R1.fastq.gz Plate135H10.R2.fastq.gz | samtools sort -o aligned.bam -`

Indexing the bam file (in order to open in IGV to check possible misalignments)

`samtools index aligned.bam`

For example, we can see a deletion around the position 11,290. All aligned reads there have 9 nucleotide deletion or sequnce different from the reference. When we look closely at these reads, we will see that they are misaligned and should contain the deletion too. Most of the misaligned reads start or end near the position of this deletion and they are misaligned (most probably) because of that.

Variant calling is done by this command

`bcftools mpileup -f sequence.fasta aligned.bam | bcftools call --ploidy 1 -mv -Ob -o variants.bcf`

BCFTools called these variants:

```
NC_045512.2	241	.	C	T
NC_045512.2	507	.	ATGGTCATGTTATGGTTG	ATG
NC_045512.2	2832	.	A	G
NC_045512.2	3037	.	C	T
NC_045512.2	5386	.	T	G
NC_045512.2	5730	.	C	T
NC_045512.2	6512	.	AGTT	A
NC_045512.2	8393	.	G	A
NC_045512.2	10029	.	C	T
NC_045512.2	10449	.	C	A
NC_045512.2	11279	.	ACTAGTTTGTCT	ACT
NC_045512.2	11282	.	AGTTTGTCTGGTTT	AGTTT
NC_045512.2	11291	.	G	A
NC_045512.2	11537	.	A	G
NC_045512.2	13195	.	T	C
NC_045512.2	14408	.	C	T
NC_045512.2	15240	.	C	T
NC_045512.2	18163	.	A	G
NC_045512.2	21762	.	C	T
NC_045512.2	21764	.	ATACATGT	AT
NC_045512.2	21846	.	C	T
NC_045512.2	21985	.	GGGTGTTTATT	GT
NC_045512.2	21986	.	GGTGTTTATT	G
NC_045512.2	22033	.	C	A
NC_045512.2	22193	.	AATT	A
NC_045512.2	22578	.	G	A
NC_045512.2	22673	.	T	C
NC_045512.2	22674	.	C	T
NC_045512.2	22679	.	T	C
NC_045512.2	22686	.	C	T
NC_045512.2	22813	.	G	T
NC_045512.2	22882	.	T	G
NC_045512.2	22898	.	G	A
NC_045512.2	22992	.	G	A
NC_045512.2	22995	.	C	A
NC_045512.2	23013	.	A	C
NC_045512.2	23040	.	A	G
NC_045512.2	23048	.	G	A
NC_045512.2	23055	.	A	G
NC_045512.2	23063	.	A	T
NC_045512.2	23075	.	T	C
NC_045512.2	23202	.	C	A
NC_045512.2	23403	.	A	G
NC_045512.2	23525	.	C	T
NC_045512.2	23599	.	T	G
NC_045512.2	23604	.	C	A
NC_045512.2	23854	.	C	A
NC_045512.2	23948	.	G	T
NC_045512.2	24130	.	C	A
NC_045512.2	24424	.	A	T
NC_045512.2	24469	.	T	A
NC_045512.2	24503	.	C	T
NC_045512.2	25000	.	C	T
NC_045512.2	25584	.	C	T
NC_045512.2	26270	.	C	T
NC_045512.2	26530	.	A	G
NC_045512.2	26577	.	C	G
NC_045512.2	26709	.	G	A
NC_045512.2	27259	.	A	C
NC_045512.2	27389	.	C	T
NC_045512.2	27807	.	C	T
NC_045512.2	28271	.	A	T
NC_045512.2	28311	.	C	T
NC_045512.2	28361	.	GGAGAACGCAG	GG
NC_045512.2	28363	.	AGAACGCAGTG	AG
NC_045512.2	28881	.	G	A
NC_045512.2	28882	.	G	A
NC_045512.2	28883	.	G	C
NC_045512.2	29688	.	G	T
NC_045512.2	29837	.	C	T

```
