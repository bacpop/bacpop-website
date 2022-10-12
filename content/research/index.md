---
title: "Research"
description: "Overview of current projects"
featured_image: '/images/header13.jpg'
type: 'page'
menu:
  main:
    weight: 1
---

We currently work in the following overlapping areas:

{{< toc >}}

See the [software]({{< ref "/software" >}}) page if you prefer a more code/project centric view!
## Mathematical modelling

We are creating some stochastic, mechanistic models of competition and transmission. We're using
tools developed during the COVID-19 pandemic to better understand the transmission of
bacterial pathogens, and eventually aim to combine models of within-host pathogen evolution with models of between-host
transmission (bacterial phylodynamics).

Examples:
- odin.dust framework: https://wellcomeopenresearch.org/articles/5-288/v2

## Real-time genomic epidemiology

Public databases of pathogen genome variation have grown rapidly, with the largest having surpassed one million sequences.
As these sequence databases grow, they are becoming more difficult for many researchers to take full advantage of. We are developing methods which help local surveillance labs integrate their data into large sequence databases, using a ‘one-by-one’ analysis approach.

Examples:
- PopPUNK for genomic epidemiology: www.poppunk.net and the paper http://dx.doi.org/10.1101/gr.241455.118
- PopPIPE for transmission analysis: https://github.com/bacpop/PopPIPE
- ggCaller for annotation: https://github.com/samhorsfield96/ggCaller
## Pathogen evolution and statistical genetics

We are designing tools to find evolutionary signatures in the masses of genomic data available, and link these findings to function.

We are also developing automated tools to mark and track concerning lineages as they emerge, predict antimicrobial resistance status, and observed the effects of vaccination on local populations.

We've got a long standing interest in genome-wide association studies, and continue to
develop new methods in this area.

Examples:
- pyseer for GWAS and phenotype prediction: https://pyseer.readthedocs.io/en/master/
- Applying GWAS to improve vaccine design: https://elifesciences.org/articles/69244

## Sequencing within-host diversity

Pathogen populations also evolve within a single host, sometimes developing mutations with consequences for the whole population. We will develop tools which combine population genetic knowledge, fast informatics approaches, and flexible sequence to streamline the process of sequencing diversity directly from complex samples.

Examples:
- Within-host diversity in meningitis patients: https://doi.org/10.1099/mgen.0.000103

## GPU algorithms

The rate of genomic data growth has outpaced the rate of computational capacity for a number of years. GPUs, with tens of thousands of processing cores, offer a promising solution. Faster algorithms will allow rapid analysis suitable for real-time surveillance of pathogens, and more ambitious analyses of larger datasets, yielding greater discovery power. We aim to address scalability of bioinformatics and mathematical modelling by programming efficient algorithms to run on GPUs, hundreds of times faster than their traditional counterparts.

Examples:
- Modelling: https://github.com/mrc-ide/dust/tree/master/inst/cuda
- Microbial genomics: https://github.com/bacpop/pp-sketchlib
- Visualisation: https://github.com/bacpop/mandrake

## Democratising bioinformatics

We aim to keep all of our research useful, reusable and accessible – this guides many of our design decisions in the above themes. On top of this, we have specific projects which aim to advance open science, making our research accessible to as many people as possible.

Projects include: searching and indexing genome analysis and metadata; developing WebAssembly versions of tools which both keep user data private, and are easily run in a web browser; computational biology outreach and teaching.

Examples:
- www.bacquerya.com
- http://amr.poppunk.net

# Collaborators

We work with a range of other groups inside EMBL.
Outside of EMBL, we currently work with following people and groups on some of our projects,
many of which are listed above:

* Nick Croucher and the [Bacterial Evolutionary Epidemiology Group](https://www.imperial.ac.uk/mrc-global-infectious-disease-analysis/hosted-initiatives-and-groups/bacterial-evolutionary-epidemiology-group/) (Imperial College London).
* Rich Fitzjohn and the [RESIDE Group](https://reside-ic.github.io/) (Imperial College London).
* Stephen Bentley, [his team](https://bentleygroup.sanger.ac.uk/), and the [GPS](https://www.pneumogen.net/gps/) and [Juno](https://www.gbsgen.net/) projects (Wellcome Sanger Institute).
* Jukka Corander and the [Probabilistic Inference Lab](https://www.med.uio.no/imb/english/research/groups/probabilistic-inference-lab/index.html) (University of Oslo).

We're always interested in growing this network, and have short- and medium-term
visitors to the lab. Please get in touch if you'd like
to collaborate with us.