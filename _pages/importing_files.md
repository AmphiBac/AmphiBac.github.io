---
layout: page
title: Importing files for use in the AmphiBac R-package
permalink: /importing/
---
### Importing your fasta file of representative sequences of ASV/OTUs
To do this well use the biostrings package (a dependancy of AmphiBac, so its already installed)
```
library(biostrings)
fasta.file<-readDNAStringSet("fasta.file.fna")
```
Thats it. Not everything has to be hard with coding. With your sequences imported you'll be able to compare them to the databse. See THIS TUTORIAL for how to do that.

---
AmphiBac's core function is to compare 16S rRNA sequences to our database with the use of vsearch. However, the R-package does offer the ability to do more advanced analyses. As such, here's some scripts for how to import metadata and your ASV/OTU table from a wide variety of bioinformatics paltforms. 

### Reading in your metadata

Metadata aka all that lovely extra information about your hard collected samples (e.g. salinity, life stage, length) is a important part of data analysis. The AmphiBac package can use your metadata, so lets talk about how to import it. Most metadata is easily imported with the base R function 'read.delim'.

```
meta<-read.delim("metadata_file.txt", header=T)
```

### From biom format
Do you have a file with an extension ".biom"? This is the Biological Observation Matrix (BIOM, http://biom-format.org/). This is a fairly common format, in particular if youve used QIIME1 or things associated with the Earth Microbiome Project. 

To use this type of file in R, well need to harness the 'phyloseq' in R. Lets start by installing it:

```
#first we need bioconductor as this isn't on CRAN
if (!require("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install(version = "3.16")

#when prompted enter 'a' into the terminal and press enter. There's also likely a popup asking for your okay so pay attention for that too.

#next install phyloseq package
library(BiocManager)
BiocManager::install("phyloseq")
#when prompted enter 'a' into the terminal and press enter.
```

With that installed let import your biom file into R as shown below. 

```
library(phyloseq)
asv.tabl<- import_biom("path/to/file/feature-table.biom")
```

Thats it. 

### From Mothur

Mothur ASV/OTU tables are usually in the format below (as of 1/11/2023).

```
label	Group	numOtus	Otu01...
1	    D6306	51	    7891...
1	    HM782	51	    5420...
1	    HM783	51	    40524...
```
We only want the 'group' column and the otu columns. So well run the following command to import the ASV/OTU table into R.

```
mothur.table<-read.table("/Users/patty/Desktop/mothu.txt", header=T, row.names=2)[,-c(1:3)]

#then we need to transpose it to have samples as columns and OTUs as rows
mothur.table<-t(mothur.table)
```
If mothur decides to change its column names, you can simply edit the script above to change the column numbers parenthases.

### From phyloseq
If you have data as a phyloseq object, converting it to AmphiBac ready is easy enough.

```
library(phyloseq)

#assuming your phyloseq object is called 'terrific_data'

asv.tab <- as(otu_table(terrific_data), "matrix")
```
The resulting output should have ASVs/OTUs as rows and samples as columns. IF its teh other way around, simply run:

```
asv.tab<-as.data.frame(t(asv.tab))
```

### QIIME2 QZA
To import your QZA file from QIIME2 to R we'll need to take advantage of the R package 'qiime2R'. We will also need the 'devtools' package. Lets install 'qiime2r' first.

```
if (!requireNamespace("devtools", quietly = TRUE)){install.packages("devtools")}
library(devtools)
devtools::install_github("jbisanz/qiime2R")
```

Next, lets import your QZA file.
```
library(qiime2R)
asv.tabl<-read_qza("./Github/panama_golden_frogs/Run11_table-deblur.qza")

```
This gives you a list of things (from the documentation for qiime2r):

```
a named list of the following objects:

artifact$data - the raw data ex OTU table as matrix or tree in phylo format
artifact$uuid - the unique identifer of the artifact
artifact$type - the semantic type of the object (ex FeatureData[Sequence])
artifact$format - the format of the qiime artifact
artifact$provenance - information tracking how the object was created
artifact$contents - a table of all the files contained within the artifact and their file size
artifact$version - the reported version for the artifact, a warning error may be thrown if a new version is seen
```

From here we want to write 'data' to a data.frame.
```
asv.tabl2<-asv.tabl$data
```

Youre good to go!

### DADA2 (R)
At the end of the DADA2 R SOP (e.g. https://benjjneb.github.io/dada2/tutorial.html) you should have a data frame with ASVs as rows and sample anmes as columns. So nothing more should be necessary here. :)

### USEARCH/VSEARCH
vsearch and usearch both produce (after runnning the OTU/ASV calling step) a text file that has sample names as columns and ASVs/OTUs as rows. As such we simple need to run:

```
asv.table<-read.delim("otu_tab.txt", header=T, row.names=1)
```
