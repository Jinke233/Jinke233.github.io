---
title: platanus
date: 2021-04-18 14:34:47
tags:Platanus
---

#### Assembly processes

#### Trimming

Since the trimming is different for each type of library (paired-end and mate-pair), we will create a file of filenames (fofn) to process them separately.

**pe.fofn**

```markdown
SRR3157034_1.fastq
SRR3157034_2.fastq
SRR3166543_1.fastq
SRR3166543_2.fastq
```

**mp.fofn**

```markdown
SRR3156163_1.fastq
SRR3156163_2.fastq
SRR3156596_1.fastq
SRR3156596_2.fastq
```

Now run the trimming as follows (here `-i` is for input file and `-t` for number of threads):

```bash
platanus_trim -i pe.fofn -t 16
platanus_internal_trim -i mp.fofn -t 16
```

####  Contig generation:

The main executable for this assembler is `platanus`. This comes with 3 options. `assemble`, `scaffold` and `gap_close`. For this step, we need the `assemble` option.

```bash
platanus assemble \
   -o platanus \
   -f {SRR3157034,SRR3166543}_?.fastq.trimmed \
   -t 20 \
   -m 115 \
```

assembly stdout:

There are only 3 output files from this step:

```markdown
platanus_contig.fa : assembled contiguous sequences
platanus_contigBubble.fa : merged and removed bubble sequences
platanus_32merFrq.tsv : kmer frequency distribution
```

#### Scaffolding

In this step, we will use the contigs create in the previous step, along with trimmed reads (PE and MP) to scaffold the initial set of contigs. We will run the command as follows:

```markdown
platanus scaffold \
    -o platanus \
    -c platanus_contig.fa \
    -b platanus_contigBubble.fa \
    -IP1 {SRR3157034,SRR3166543}_?.fastq.trimmed \
    -OP2 SRR3156163_?.fastq.int_trimmed \
    -n2 7000 \
    -a2 8000 \
    -d2 1000 \
    -OP3 SRR3156596_?.fastq.int_trimmed \
    -n3 19000 \
    -a3 20000 \
    -d3 2000 \
    -t 12 
```

There will 3 output files again:

```markdown
platanus_scaffold.fa: assembled sequences with gaps
platanus_scaffoldBubble.fa: removed bubble sequences
platanus_scaffoldComponent.tsv: table describing contig joins
```

#### Gap closing

The final step is to close the gaps (reduce the N content in the genome introduced during scaffolding). We will need the scaffolds generated in the previous step. For this we will use the `gap_close` module. We will run it as follows:

```markdown
./platanus gap_close \
    -o platanus \
    -c platanus_scaffold.fa \
    -IP1 {SRR3157034,SRR3166543}_?.fastq.trimmed \
    -OP2 SRR3156163_?.fastq.int_trimmed \
    -OP3 SRR3156596_?.fastq.int_trimmed \
    -t 30 
```

