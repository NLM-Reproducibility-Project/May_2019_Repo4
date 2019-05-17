# Summary Presentation

## Introduction 
As part of the 2019 NLM Reproducibility workshop,five of us attempted to reproduce the work in the paper:
A functional genomics predictive network model identifies regulators of inflammatory bowel disease



## Approaches to reproduce paper

## Issues with specific analysis

### eQTL
Authors performed eQTL analysis to identify all genes using the known/published IBD eQTLs. The genes identified by this analysis will be used to generate the IBD genes as SEEDs to downstream analyses. In the Synapse, the codes used to this analysis are included in 'synapse_data/Code/eQTL/code' <br>

<pre>
step.1.1.pickup.sub.eqtl-lm-peaks.pl
step.2.merge.peaks.pl
step.3.fdr.pl
step.4.cut.peak.pl
</pre>

Four perl scripts were included for the four-step analysis. But the problem is that the codes have hard-coded I/O directories on authors personal computers using file names that could not be found in your Synapse repository. Below are examples:
 
<pre>
$PROG="/hpc/users/dinara01/packages/eqtl.tools-0.0.28/eqtl-lm-peaks";
        $genespos="/projects/haok01a/haok/work/Projects_2013/Cancer.Genome/tools/RNAseq/Ucsc.annotation.hg19.eQTL.txt" if ($ARGV[0]=~/UCSC/i);
        $genespos="/projects/haok01a/haok/work/Projects_2013/Cancer.Genome/tools/RNAseq/Ensemble.annotation.hg19.eQTL.txt" if ($ARGV[0]=~/ENSEMBLE/i);
</pre>

### Network_enrichment
Authors performed their network enrichment using the SEED IBD genes identified by GWAS and eQTL analyses on the co-expression network from three different coherts with varying severity of disease. Authors have the codes for the network enrichment (see below):

<pre>
#synapse_data/Code/Network_enrichment/co-expression_network
codeforenrichmenttable.R
co-expression_network/
</pre>

But the codes contain hard-coded input and output files to their personal computers. The input files used were not found in their Synapse repositry.

<pre>
# codeforenrichmenttable.R 
x = read.table("/Users/user/Documents/Renrichment.csv",sep=",",header=T)
....
write.table(x, "/Users/user/Documents/Renrichmentresults.csv",sep=",",quote=F)
</pre>

The authors also included codes to generate the co-expression networks. But again the input data are nowhere to be found.

<pre>
# synapse_data/Code/Network_enrichment/co-expression_network/
Curate_Signature.R
DEG.curated.RData
R_functions.R
RUN_KDA.R

## Curate_Signature.R
###### script to extract signatures
rm(list = ls())

wkdir <- "G:/IBD_KDA/Updated_Lauren_DEG_Signatures";setwd(wkdir)
</pre>

## Obstacles

### Data


The referenced epigenetic region data is not clearly specified. Instead of providing specifiers about _what_ data was used, the paper merely references GEO data is available at NCBI: http:// www.ncbi.nlm.nih.gov/geo/roadmap/epigenomics/

### Synapse

Other data is supposed to be available via Synapse platform (Sage Bionetworks https://www.synapse.org/IBDNetworks), however, the provided link/identifier does not work.  (the work was found after creating an account and using their search feature. The data was instead at: https://www.synapse.org/#!Synapse:syn10792659


Furthermore, some of the data appears to be corrupted and others appears to be missing entirely. For example, a large 16Gb data file would not download (the system cites that the MD5 signature does not match the data on the system). 

There are empty directories in their work.  

There was significant problems trying to download the data from Synapse platform. In order to download data from Synapse, you must use their software. There is a link for "Download Options",  - and there were two options: 
(1) Add to download list
(2) Programmatic options

I could not easily figure out how to use "add to download list". It appears that there isn't an easy way to download the entire project all at once. When I attempted to use the "download list", I got the error/warning:
```
If a folder contains no files, no files will be added to the download list. Additionally, sub-folders cannot be added directly; please navigate into the directory that contains the files you’d like to download to add them.
```
(This appears to mean that the "add to download list" only downloads 1 level deep? which is not good for trying to download the entire project all at once - meaning a piecemeal attempt is required.)

The second approach is to use "programmatic options". However, there were significant issues with this approach.
The command line option was to use `synapse` command - but it was not inherently obvious how to get it. There appeared to be a couple of pieces of software when searching with google.

We attempted to use the python programmatic approach. Documentation
signifcant problems with their code (for example the required `synapseutils.py` could not be found anywhere for installation).


```
    Python
    R
    Command Line

								
 import synapseclient
 import synapseutils
 
 syn = synapseclient.Synapse()
 syn.login('synapse_username','password')
 files = synapseutils.syncFromSynapse(syn, 'syn10792659')
``` 

							
