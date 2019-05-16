The purpose of this study was to identify genetic differences between Borrelia that cause lyme disease and Borrelia that don't. To do this we took, three lyme-causing
and three non-Lyme-causing Borrelia. The file structure in this directory is the set up for some of the analyses done. Namely, the gene set analysis and the GO term 
enrichment analysis. The other analyses done (KEGG pathway analysis, synteny anlysis) were done using other softwware.
After downloading the FASTA files of the genomes of the six bacteria, we annotated the genomes using the Prokka pipeline, as well as with GO terms. Then, we wrote the 
scripts necessary to query, analyze, and extract neecessary information from the annotated genomes. This document will explain the scripts, their usages, as well as the
file struture.

## File Structure
There's a folder created for each of the six organisms. The Lyme-disease (LD) causing Borrelia are: burgdorferi, afzelii, and garinii. The other three (parkeri, miyamotoi,
and hermsii) aren't associated with lyme disease.
Each folder has the .fna file for that organism. Prokka is run on the .fna file to generate a list of annotated genes. A file of unique genes is created for that organism
with the form `organism_unique_gene_list.txt`. There are also other files generated for each organism during the prokka and GO annotations.
Scripts needed to analyze these files were written (see next section) and relevant information was extracted from the annnotated sets (e.g. the core genome for LD bacteria 
and non-LD bacteria, pan-genome for LD and non-LD bacteria, GO annotations for the two groups, etc...)


## Scripts
### annotateGenome
This script takes in one argument: the name of the the directory which contains the .fna file that needs to be annotated. It the ncreates a list of annotated genes, and a
unique list of annotated genes for the .fna file.
It's used as follows

	./annotateGenome garinii

### getGOTerms
This script takes one argument: the name of a file that contains prokka_annotated gene names (one gene per line), and goes through the tsv files and the .annotations file
of the organisms to print out the GO terms associated with the genes. Note that some of the prokka annotated genes may not have GO annotations.
It's used as follows

	./getGOTerms lyme_pan.txt

### extractGOTerms
This script just applies the getGOTerms script to the file name provided, and removes the irrelevant information from the tsv files, leaving only the list of GO terms
Note, the file will probably have duplicate GO terms. 
Useage:

	./extractGOTerms lyme_pan.txt

### findCoreGenome
Given a list of folder names for organisms (e.g. burdorferi, garinii, etc.) as command line arguments, this script
finds genes in the intersection of the unique gene lists of those organisms.
Usage:

	./findCoreGenome burgdorferi garinii afzelii


### findPanGenome
Given a list of folder names for organisms (e.g. burdorferi, garinii, etc.) as command line arguments, this script
finds genes in the union of the unique gene lists of those organisms.
Usage:

	./findPanGenome burgdorferi garinii afzelii


### findGeneIn
Givne a Uniprot gene name, goes through the unique gene list of each organism (in that organism's folder) and looks for it. If found, ouputs the organisms name to the screen
Usage:

	./findGeneIn "dnaB" burgdorferi garinii hermsii parkeri afzelii miyamotoi
