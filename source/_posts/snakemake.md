---
title: snakemake
date: 2021-03-14 12:54:36
tags: snakemake
---

 全部流程：

```python
SAMPLES = {"A","B"}

rule bwa_map:
	input:
		"data/genome.fa",
		"data/samples/A.fastq"
	output::
		"mapped_reads/A.bam"
	shell:
		"bwa mem {input} | samtools view -Sb - > {output}"
		
rule samtools_sort:
	input:
		"mapped_reads/{sample}.bam"
	output:
		"sorted_reads/{sample}.bam"
	shell:
		"samtools sort -T sorted_reads/{widecards.sample}"
		"-O bam {input} > {output}"
		
rule samtools_index:
	input:
		"sorted_reads/{sample}.bam"
	output:
		"sorted_reads/{sample}.bam.bai"
	shell:
		"samtools index {input}"
		
rule bcftools_call:
	input:
		fa="data/genome.fa",
		bam=expand("sorted_reads/{sample}.bam",sample=SAMPLES),
		bai=expand("sorted_reads/{sample}.bam.bai",sample=SAMPLES)
	output:
		"calls/all.vcf"
	shell:
		"samtools mpileup -g -f {input.fa} {input.bam}|"
		"bcftools call -mv - > {output}"
		
rule plot_quals:
	input:
		"calls/all.vcf"
	output:
		"plots/quals.svg"
	script:
		"scripts/plot-quals.py"
```

