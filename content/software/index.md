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

##  Bioinformatics

### {{< logo "images/ggcaller_logo.png" 200 120 >}} ggcaller

graph-gene Caller (`ggCaller`), combines gene annotation and pangenome clustering steps within population-wide de Bruijn Graphs. Using population-frequency information, ggCaller improves consistency of gene annotations, leading to more accurate clustering and significantly reduced run-times versus linear-genome based annotation and pangenome analysis.
*ggcaller is written by [Sam Horsfield]({{< ref "/group" >}}), and in collaboration with [Nicholas Croucher](https://www.imperial.ac.uk/people/n.croucher).*

* Download (conda): https://anaconda.org/bioconda/ggcaller
* Paper (preprint): https://www.biorxiv.org/content/10.1101/2023.01.24.524926v1
* Documentation: https://ggcaller.readthedocs.io
* Code: https://github.com/samhorsfield96/ggCaller

### {{< logo "images/ska_logo.png" 200 120 >}} SKA (version 2)

Split k-mer analysis (`SKA`) can be used to produce alignments from closely related sequence assemblies or
reads, quickly (because it is alignment-free) and with minimal fuss (due to the interface).
This enables downstream analysis such as phylogenetics or sequence completeness.
*In collaboration with [Simon Harris](https://github.com/simonrharris).*

* Download (cargo): https://crates.io/crates/ska
* Download (conda): https://anaconda.org/bioconda/ska
* Documentation: https://docs.rs/ska/latest
* Code: https://github.com/bacpop/ska.rust

### {{< logo "images/sketchlib_logo.png" >}} pp-sketchlib

Library of sketching functions used to rapidly calculate core and accessory distances between bacterial genomes. Designed as a faster drop-in back-end for PopPUNK, you can also use to replace mash (100x speedup, further 50x with GPUs).

* Download (conda): https://anaconda.org/bioconda/pp-sketchlib
* Code: https://github.com/bacpop/pp-sketchlib

### sketchlib.rust (beta)

A rust rewrite of pp-sketchlib particularly targeted at very large datasets by using a new file format. To find nearest neighbours or
perform subset queries, this code is an improvement over pp-sketchlib.

* Code: https://github.com/bacpop/sketchlib.rust

### {{< logo "images/celebrimbor_logo.png" >}} CELEBRIMBOR

Create pangenomes from metagenome assembled genomes (MAGs), using completeness information
to adjust observed frequencies.

* Download (pipeline): https://hub.docker.com/r/samhorsfield96/celebrimbor
* Download (model): https://crates.io/crates/cgt_bacpop
* Code (pipeline): https://github.com/bacpop/CELEBRIMBOR
* Code (model): https://github.com/bacpop/cgt

## Genomic epidemiology

### {{< logo "images/poppunk_logo.png" >}} PopPUNK

List of databases is on the [PopPUNK page]({{< ref "/poppunk-databases" >}}).

Tools for bacterial genomic epidemiology. Quickly find core and accessory distances between whole-genome sequences, and use these to find genetically clusters. New data can be rapidly ‘queried’ against existing clusters, giving consistent nomenclature.
*In collaboration with [Nicholas Croucher](https://www.imperial.ac.uk/people/n.croucher).*

* Download (conda): https://anaconda.org/bioconda/poppunk
* Download (pip): https://pypi.org/project/poppunk/
* Paper: https://doi.org/10.1101/gr.241455.118
* Documentation: https://poppunk-docs.bacpop.org
* Code: https://github.com/bacpop/poppunk

### PopPIPE

Poplation analysis PIPEline. Designed to be run downstream of PopPUNK, to obtain subclusters and visualisations.
A Snakemake pipeline that requires some config modifications to run.

* Code and download: https://github.com/bacpop/PopPIPE
* Documentation: https://poppunk-docs.bacpop.org/subclustering.html

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

### SBMLtoOdin

An R package to download and translate models in SBML format (e.g. from BioModels) automatically to odin code.

https://github.com/bacpop/SBMLtoOdin


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

(*older unitig-counter is still available but no longer supported*):
* unitig-counter (github): https://github.com/bacpop/unitig-counter
* unitig-counter (conda): https://anaconda.org/bioconda/unitig-counter

## Visualisation

### {{< logo "images/mandrake_logo.png" >}} mandrake

Rapid stochastic cluster embedding (like t-SNE, UMAP) for genetic distances, particularly pathogen genome sequences.
In collaboration with [Gerry Tonkin-Hill](https://gtonkinhill.github.io/).

* Download (conda): https://anaconda.org/conda-forge/mandrake
* Preprint: https://www.biorxiv.org/content/10.1101/2021.10.28.466232v1
* Documentation: https://mandrake.readthedocs.io/en/latest/
* Code: https://github.com/bacpop/mandrake

## Web tools

### {{< logo "images/Menelmacar_logo.png" 200 120>}} [Menelmacar](https://biomodels.bacpop.org/) (Making Execution of (Nearly) Every Life-science Model ACcessible to All Researchers)

Interactive visualisations of mathematical models from BioModels.

Code: https://github.com/bacpop/Menelmacar

### {{< logo "images/beebop_logo_transparent.png" 200 120 >}} [BeeBOP](https://beebop.dide.ic.ac.uk/) (*beta*)

An in-browser AMR and strain prediction tool for *Streptococcus pneumoniae*.

Code:
* Front-end: https://github.com/bacpop/beebop/

### [mandrake-web](https://gtonkinhill.github.io/mandrake-web/)

A WebAssembly version of the mandrake stochastic cluster embedding tool. Written by [Gerry Tonkin-Hill](https://gtonkinhill.github.io/).

Code:
* https://github.com/gtonkinhill/mandrake-web
