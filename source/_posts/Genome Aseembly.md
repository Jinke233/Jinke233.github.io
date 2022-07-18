#### Genome Aseembly

##### 1.Download_data

```bash
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR209/001/SRR2093871/SRR2093871_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR209/001/SRR2093871/SRR2093871_2.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR209/002/SRR2093872/SRR2093872_1.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR209/002/SRR2093872/SRR2093872_2.fastq.gz
wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR209/006/SRR2093876/SRR2093876_subreads.fastq.gz

```

##### 2.Assembly

```bash
canu -p Bt2 -d Bt2_assembly genomeSize=6.2m  -pacbio-raw SRR2093876_subreads.fastq.gz 
```

##### 3. GenomeScope

```
jellyfish count -C -m 21 -s 1000000000 -t 10 *.fastq -o reads.jf

jellyfish histo -t 10 reads.jf > reads.histo

```

##### 4. Checking your Assembly for contaminants using VecScreen

```bash
wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/002/814/215/GCF_002814215.1_Sedor1/GCF_002814215.1_Sedor1_genomic.fna.gz
```

##### 5. Genome Scaffolding with pyScaf

```
git clone https://github.com/lpryszcz/pyScaf.git
```