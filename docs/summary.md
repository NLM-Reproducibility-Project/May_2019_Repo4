# Summary Presentation

## Introduction 
As part of the 2019 NLM Reproducibility workshop,five of us attempted to reproduce the work in the paper:
A functional genomics predictive network model identifies regulators of inflammatory bowel disease



## Approaches to reproduce paper


## Obstacles

### Data


The referenced epigenetic region data is not clearly specified. Instead of providing specifiers about _what_ data was used, the paper merely references GEO data is available at NCBI: http:// www.ncbi.nlm.nih.gov/geo/roadmap/epigenomics/

### Synapse

Other data is supposed to be available via Synapse platform (Sage Bionetworks https://www.synapse.org/IBDNetworks), however, the provided link/identifier does not work.  (the work was found after creating an account and using their search feature. The data was instead at: https://www.synapse.org/#!Synapse:syn10792659


Furthermore, some of the data appears to be corrupted and others appears to be missing entirely. For example, a large 16Gb data file would not download (the system cites that the MD5 signature does not match the data on the system). 

There are empty directories in their work.  

There was significant problems trying to download the data (in order to download data from Synapse, you must use their software - and there were signifcant problems with their code (for example the required `synapseutils.py` could not be found anywhere for installation).
