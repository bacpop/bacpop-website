---
title: "Research"
description: "Overview of current projects"
featured_image: '/images/bacpop_header.png'
type: 'page'
menu:
  main:
    weight: 1
---

We want to understand how microbes (particularly pathogenic bacteria) evolve, becoming pathogenic
and more transmissible. Understanding the mechanisms by which bacteria evolve and adapt to their environments is crucial to
address many practical questions: designing drugs and vaccines against pathogens, optimising
commercial processes, predicting future population dynamics and disease. The enormous diversity, but
relatively simple biology of bacteria also offers an ideal system to answer fundamental questions in
evolutionary biology. *Do evolutionary processes repeat themselves? At what timescales do modes of
evolution dominate? Can we predict future evolution?*

Secondly, we want to increase the performance and accessibility of evolutionary methods,
including both bioinformatics and modelling. As well as increasing equity between regions, there are other advantages
to making these techniques usable locally: global surveillance is more effective than concentrating resource in single
regions; many regions without this technology have a higher burden of infectious disease due to existing inequities; data
generators have unique knowledge of biases and important questions in their data, if they are able to analyse the data
locally and without external support they can answer these questions more quickly, and more easily develop their own
research and infection control programmes. We develop methods that can be easily run
in a web-browser, on a typical laptop, and on high-performance GPUs.

We currently work in the following overlapping topic areas:

{{< toc >}}

## Pangenome evolution

Compare two bacterial genomes and they will share only some of their sequence content. The
content shared by all members of the population is the core genome, content shared by some members
is the accessory genomes, content private to one (or a few) members is rare. Bacterial species
have between 15-85% of their genetic content in their accessory (compared to a few percent for
vertebrates).

We want to understand the evolutionary and ecological reasons why bacteria maintain such an extensive accessory genome.
How much does the accessory genome contribute to adaptation? Can we use this predict future dynamics?

Current projects in this area include:

* Fitting models of pangenome evolution to large bacterial populations.
* Predicting pangenome dynamics using surveillance data over and vaccine introductions.
* Within-host evolution during carriage.

## Evolution across the bacterial domain

Many population analyses of bacteria are restricted to single species as genome sequences
are too divergent to align across the breadth of bacterial taxonomic diversity. The combination
of protein family models, structure prediction and alignment, and protein language models now
allow us to align across this gap. We are using this to compare gene functions and study their evolution across all species.

Current projects in this area include:

* Evolution and structure of bacterial capsule.
* Linking positive selection, protein structure and function.
* Processes of speciation.

## Machine learning

A growth in bacterial datasets and new generation of model architectures has reignited
interest in application of statistical models to bacterial populations. This can be at the
genome (DNA), protein (AA) or gene (synteny) level, and may also link to other phenotypes. These
models are particularly useful when they are designed to capture biological complexity which
may not be tractable through traditional mechanistic/statistical approaches.

Current projects in this area include:

* Models of gene order in bacteria.
* Predicting minimum inhibitory concentration from genome sequence.
* Serotype prediction.

## Bioinformatic methods development

We have made many tools used by other bioinformatics and modelling research groups,
and some are also used within public health and clinical practice. Our current focuses
are on methods which scale to the tens of millions of genomes now available, and lightweight
methods which can be run in low resource settings.

Current projects in this area include:

* Genome sketching and metagenome containment.
* Genome dereplication.
* WebAssembly methods for genomic epidemiology and bioinformatics.
* Pangenome construction.
* GPU acceleration of state space models.

Also see the [software]({{< ref "/software" >}}) page.

## Reusable and accessible resources

We also want to increase access to microbial data, particularly genomic data. Making
resources which are suitable for power-users who want to easily download and reuse
preprocessed data for their own purposes will save effort and ensure reproducibility. If the
same resources can be interactively explored, plotted, and manipulated, this will increase
their breadth of access.

Current projects in this area include:

* [AllTheBacteria](https://www.allthebacteria.org/) -- all bacterial genomes assembled, accessible and searchable.
* AMR data portals (phenotype and genotype).
* Genomic nomenclature.
* Teaching resources for programming and modelling.

Also see the [resources]({{< ref "/resources" >}}) page.
