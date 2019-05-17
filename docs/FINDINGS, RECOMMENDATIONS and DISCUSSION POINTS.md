
May 17, 2019 at 9:35 AM

# **FINDINGS, RECOMMENDATIONS and DISCUSSION POINTS**

## **Summary:**

The following describes selected findings that team_ibd_a identified while attempting to reproduce the data analysis documented in the Nature article on “A functional genomics predictive network model identifies regulators of inflammatory bowel disease” by Peters et al. (https://www.nature.com/articles/ng.3947#results). The team presents ideas on better practices should have 

### **Key findings of the analysis:**

*availability and accessibility of data:*
**key data were not available (empty folder, corrupted R.data file), accessibility was not straightforward (Synapse), recursive download failed; details on 205 position-specific weight matrices (PWMs) from JASPAR CORE database were not provided.**

*data and code integrity:*
**we encountered a corrupted R.data file in Synapse (16.6Gb) at the entry point of the data analysis. R code files often point to data that are not present in the Synapse repository**

*long-term accessibility of data and software packages:*
**RIMBANET software was not usable due to issues with compiling; some software requires more detailed compilation/installation information than others**

*finding data and code:*
**there was a graphical representation of the overall workflow (Fig. 1) that referenced supplemental tables at discrete processing steps; but that did not allow to identify which data (location in Synapse, else) were processed in what way (which R code) to arrive at these steps; to reproduce the results presented in this article, a detailed processing protocol has to be provided that ties in all primary data and processed data together with the processing tools that were used to advance through the data analysis into a coherent processing pipeline; although links to data files (GO) and software resources were provided, other important information was burried in the supplemental (39 pages). Supplemental tables were organized into one Master spreadsheet. But that lacked a table index making it hard to navigate.**

### **Conclusions:**
The material and methods provided concerning the data analysis presented in the article were not conducive to reproducing the published findings. Major shortcomings were the poor organization of many of the components of the analysis, poor quality of coding practice, use of software that was poorly supported, and lack of analysis details necessary to reproduce the data processing.


### **Strategies to favor reproducibility by implementing the following concepts:**

**curated code:**  
*goal: code that runs everywhere*
provide code that is robustly tested on more than one computer/OS; limited hard-coding of arguments/parameters; well documented as notebook/Markdown in terms of dependencies others

**processing pipeline:** 
*goal: structured, annotated ‘inventory’ of data - map showing how code and data are connected*
provide detailed outline and explanation of processing pipeline revealing all processing steps with I/O documentation (Snakemake); detailed documentation (spreadsheet, graphically) of data and code organization in repositories; master spreadsheet of all resources required for project possibly listing alternative processing paths if proprietary software or no-longer supported software has been utilized; use notebooks/Markdown for any code

**portability:** 
*goal: make processing pipeline platform independent and universally functional*
use container-based approach or Snakemake approach to improve portability and reproducibility of processing pipeline; try to integrate as many processing steps as possible into a container that can be used to ‘reproduce/replicate’ pipeline with the goal to arrive at a containerized final processing pipeline; alternatively, use Snakemake to provide portable pipeline(s). Both approaches are likely tricky to implement but even the attempt to generating them will improve reproducibility inherently.

**General questions for discussion:**

*quality control of data/code going into repository:*
was the relevant R.data file (16Gb) already corrupted at time of upload into Synapse or did the upload cause the corruption? Can data get corrupted in repositories? Are there mechanisms at repository sites that check for data integrity? Are repositories build to include redundancies? What are the responsibilities of the researcher(s)?

*reproducibility and peer-review:*
What are the responsibilities of the reviewers in the peer-review process in terms of commenting on availability of detailed methods and supplemental materials in light of data reproducibility?
Should data only be reproducible to the experts in the respective field or should they be ‘accessible’ to anybody interested in any given topic?

