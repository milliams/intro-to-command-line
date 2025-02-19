---
title: "∙ Bioinformatics"
subtitle: "Managing sequence data on the command line"

date: 2022-09-20T00:00:00+01:00

fontawesome: true
linkToMarkdown: true

toc:
  enable: true
  keepStatic: false
  auto: false
code:
  copy: true
math:
  enable: true
share:
  enable: true
comment:
  enable: true
---

This section is aimed at those wanting to use the command line, and perhaps computing clusters, to work with sequence information (that is, genetic, genomic, proteomic and other bioinformatic data). While we recommend using a dedicated programming language for more complex work (this is easier to share, test and replicate), the command line remains a useful environment to acquire and manage data, especially as the first part of an analysis pipeline.

### Sequence archives and repositories
All publicly-funded research generating sequence information is obliged to share their data, and this is typically done by placing it with one of the major sequence repositories, for example [GenBank](https://www.ncbi.nlm.nih.gov/genbank/) at the National Centre for Biotechnology Information (NCBI), or [Ensembl](https://www.ensembl.org/index.html) at the European Bioinformatics Institute (EBI). Given the scale of these repository, and the varied working practices of many labs across the world, you will sometimes come across poorly-annotated, mislabeled or otherwise inaccurate data. However, just keep this in mind - the vast majority of deposited data is accurate and well-catalogued!

### Exercises
Let's work with some real data to answer some real research questions. Firstly, we are going to acquire a small genome to work with. Go to [NCBI genbank](https://www.ncbi.nlm.nih.gov/genbank/), and in the search dropdown menu, select `Genome`. While you are here, notice the other databases that NCBI hosts (each of the items in the dropdown is a database). Many of these are quite niche, but common ones to use are `Genome`, `Gene`, `Protein` and `SRA`, the latter for raw, unassembled sequence reads.

With `Genome` as your search database, enter "SARS-CoV-2", and run the search. You should get one result (if you get more, choose the top result). Note the information get here, and follow the link to the reference genome by clicking "Severe acute respiratory syndrome coronavirus 2", near the top of the page. On this screen, get both the nucleotide and amino acid genome, by clicking the links next to "Download sequences in FASTA format". Move these two files to a suitable folder to work in, and unzip them. Note their file extensions - `faa` is "FASTA, amino acids", `fna` is "FASTA, nucleotides", (these are just plain text files, like almost all files we work with on the command line). FASTQ files are the same as FASTA, except with read quality scores, and are typically untrimmed.

We'll start with the nucleotide genome - view the file with `less` to get a feel of what the data looks like.

{{< admonition type="question" title="Exercise 1" open=true >}}
Use command line tools taught earlier in this course to answer these questions:
- How long is this genome, in kilobases? (Hint: use `wc` with a flag. Exclude the FASTA header line however you like: you could make a new file and edit it manually, or use pipes with `head` or `tail`.)
- What is the total nucleotide count each for A, T, C and G in the genome? Is it G-C enriched, or A-T enriched? (Hint: `grep` with a flag, and `wc` will help you here.)
- How many times do we see the start codon (Methionine) in the genome?  (**Ignore line-breaks for this exercise, and all following questions**)
- How many times does the motif ATGTAG occur in the genome?
- Assume that all protein-coding genes in this genome start with the motifs ATGACC, ATGTTTTAT and ATGCTTTAA (they don't, this is just an exercise!). How many genes does this covid-19 genome appear to contain?
- The covid nucleocapsid phosphoprotein starts with the motif ATGTCTGATAAT and ends with AACTCAGGCCTA
  - What line does the capsid gene start? And end?
  - Isolate the capsid gene and make a new file, containing just that gene. Manually trim any non-capsid sequence with a text editor. Make sure it is in FASTA by adding a header line, and give the sequence a name.
{{< /admonition >}}

Now let's have a look at the proteome. Again, open it with `less` and have a look at how it is structured and annotated, noting the differences compared to the nucleotide version of this genome.

{{< admonition type="question" title="Exercise 2" open=true >}}
Answer these questions about the proteome:
- How many protein-coding genes does SARS-CoV-2 contain?
- What is the shortest protein sequence in this genome? (Pick out the short ORF sequences and compare them against each other.)

The following questions are to introduce you to genomic repositories, and encourage you to explore the archives.
- Take this sequence for the shortest protein (as in cut/copy it). Open [NCBI's BLAST portal](https://blast.ncbi.nlm.nih.gov/Blast.cgi) and select the protein -> protein option. On the next page, paste your AA sequence into the search box. Choose the program selection (near the bottom) as "Quick BLASTP". Run the search - this might take a minute or so.
  - Scroll down through the results. From *what species of host organism* is the closest related gene to your sequence? (*ie, not human*)
  - What is the name of the paper in which this sequence was generated?
  - What are the differences in (amino acid composition) for this sequence?
  - In the codon responsible for this change, which nucleotide position(s) are substituted? (ie, 1st, 2nd or 3rd?)
  - What is the name of this kind of substitution?
{{< /admonition >}}


