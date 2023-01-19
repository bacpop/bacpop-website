---
title: "Software"
description: "Packages we have written or contributed to"
featured_image: '/images/header9.jpg'
type: 'page'
menu:
  main:
    weight: 1
---

{{< toc >}}

##  Genomic epidemiology & bioinformatics

### {{< logo "images/ggcaller_logo.png" >}} ggcaller

graph-gene Caller (`ggCaller`), combines gene annotation and pangenome clustering steps within population-wide de Bruijn Graphs. Using population-frequency information, ggCaller improves consistency of gene annotations, leading to more accurate clustering and significantly reduced run-times versus linear-genome based annotation and pangenome analysis.
*ggcaller is written by [Sam Horsfield]({{< ref "/group" >}}), and in collaboration with [Nicholas Croucher](https://www.imperial.ac.uk/people/n.croucher).*

* Download (conda): https://anaconda.org/bioconda/ggcaller
* Paper: biorxiv
* Documentation: https://ggcaller.readthedocs.io
* Code: https://github.com/samhorsfield96/ggCaller

### {{< logo "images/ska_logo.png" >}} SKA (version 2)

Split k-mer analysis (`SKA`) can be used to produce alignments from closely related sequence assemblies or
reads, quickly (because it is alignment-free) and with minimal fuss (due to the interface).
This enables downstream analysis such as phylogenetics or sequence completeness.
*In collaboration with [Simon Harris](https://github.com/simonrharris).*

* Download (cargo): https://crates.io/crates/ska
* Download (conda): https://anaconda.org/bioconda/ska
* Documentation: https://docs.rs/ska/latest
* Code: https://github.com/bacpop/ska.rust

### {{< logo "images/poppunk_logo.png" >}} PopPUNK

List of databases is on the [PopPUNK page]({{< ref "/poppunk" >}}).

Tools for bacterial genomic epidemiology. Quickly find core and accessory distances between whole-genome sequences, and use these to find genetically clusters. New data can be rapidly ‘queried’ against existing clusters, giving consistent nomenclature.
*In collaboration with [Nicholas Croucher](https://www.imperial.ac.uk/people/n.croucher).*

* Download (conda): https://anaconda.org/bioconda/poppunk
* Download (pip): https://pypi.org/project/poppunk/
* Paper: https://doi.org/10.1101/gr.241455.118
* Documentation: https://poppunk.readthedocs.io
* Code: https://github.com/bacpop/poppunk

### {{< logo "images/sketchlib_logo.png" >}} pp-sketchlib

Library of sketching functions used to rapidly calculate core and accessory distances between bacterial genomes. Designed as a faster drop-in back-end for PopPUNK, you can also use to replace mash (100x speedup, further 50x with GPUs).

* Download (conda): https://anaconda.org/bioconda/pp-sketchlib
* Code: https://github.com/bacpop/pp-sketchlib

### PopPIPE

Poplation analysis PIPEline. Designed to be run downstream of PopPUNK, to obtain subclusters and visualisations.
A Snakemake pipeline that requires some config modifications to run.

* Code and download: https://github.com/bacpop/PopPIPE
* Documentation: https://poppunk.readthedocs.io/en/latest/subclustering.html

## Modelling

### {{< logo "images/dust_logo.png" >}} odin, dust and mcstate

A suite of R packages to assist in fast, reproducible state-space models, particularly compartmental models used in epidemiology.
*In collaboration with [Rich Fitzjohn](https://github.com/richfitz) and [RESIDE at MRC GIDA](https://reside-ic.github.io/)*

*odin*: a domain-specific language that makes compartmental models easy to write, extend, and are fast to run:

*dust*: parallelised code for random number generation for Monte Carlo models, used to actually run state space models forward in time

*mcstate*: statistical support which allows running, forecasting and inference from these models

* Paper: https://wellcomeopenresearch.org/articles/5-288/v1
* Documentation: https://mrc-ide.github.io/mcstate/articles/sir_models.html (and links above)
* Code:
    * https://mrc-ide.github.io/odin
    * https://mrc-ide.github.io/odin.dust
    * https://github.com/mrc-ide/dust
    * https://mrc-ide.github.io/mcstate

## Statistical genetics

### {{< logo "images/pyseer_logo.png" >}} pyseer

Comprehensive pangenome-wide association studies in microbes. Find genetic variation that is linked to a phenotype or clone of interest.
*In collaboration with [Marco Galardini](https://www.resist-cluster.de/en/about-us/research-team/prof-dr-marco-galardini/).*

* Download (conda): https://anaconda.org/bioconda/pyseer
* Download (pip): https://pypi.org/project/pyseer
* Paper:  https://doi.org/10.1093/bioinformatics/bty539
* Documentation: https://pyseer.readthedocs.io
* Code: https://github.com/mgalardini/pyseer

### unitigs

Packages to count and determine presence of non-redundant sequence elements. Use ‘caller’ both to determine what the are unitigs in a population, and to quickly determine presence/absence in a new population. The ‘counter’ is no longer supported, but is an alternative to the first purpose.

* unitig-caller (github): https://github.com/bacpop/unitig-caller
* unitig-caller (conda): https://anaconda.org/bioconda/unitig-caller

(*no longer supported*)
* unitig-counter (github): https://github.com/bacpop/unitig-counter
* unitig-counter (conda): https://anaconda.org/bioconda/unitig-counter

### SEER (*no longer supported*)

First version of software for association studies in bacteria (superseded by pyseer, above). Find k-mers that are linked to a phenotype of interest.

* Download (conda): https://anaconda.org/bioconda/seer
* Download (github):  https://github.com/johnlees/seer/releases
* Paper: https://doi.org/10.1038/ncomms12797
* Documentation: https://github.com/johnlees/seer/wiki
* Code: https://github.com/johnlees/seer

## Visualisation

### {{< logo "images/mandrake_logo.png" >}} mandrake

Rapid stochastic cluster embedding (like t-SNE, UMAP) for genetic distances, particularly pathogen genome sequences.
In collaboration with [Gerry Tonkin-Hill](https://gtonkinhill.github.io/).

* Download (conda): https://anaconda.org/conda-forge/mandrake
* Preprint: https://www.biorxiv.org/content/10.1101/2021.10.28.466232v1
* Documentation: https://mandrake.readthedocs.io/en/latest/
* Code: https://github.com/bacpop/mandrake

## Web tools

### {{< logo "images/bacquerya_logo.png" 200 120 >}} [BacQuerya](wwww.bacquerya.com) (*beta*)

A search engine for bacterial genomes and metadata.

Code:
* Front-end: https://github.com/bacpop/BacQuerya
* API (middle layer): https://github.com/bacpop/BacQuerya-api
* Sequence processing: https://github.com/bacpop/BacQuerya-processing

### {{< logo "images/amima_logo.png" 200 120 >}} [AMIMA](https://amima.poppunk.net/) (*beta*)

An in-browser AMR prediction tool for *Streptococcus pneumoniae*.

Code:
* Front-end: https://github.com/bacpop/AMR_ReactApp
* WebAssembly: https://github.com/bacpop/AMR_prediction

### [mandrake-web](https://gtonkinhill.github.io/mandrake-web/)

A WebAssembly version of the mandrake stochastic cluster embedding tool. Written by [Gerry Tonkin-Hill](https://gtonkinhill.github.io/).

Code:
* https://github.com/gtonkinhill/mandrake-web
