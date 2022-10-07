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

## Real-time genomic epidemiology

Public databases of pathogen genome variation have grown rapidly, with the largest having surpassed one million sequences.
As these sequence databases grow, they are becoming more difficult for many researchers to take full advantage of. We are developing methods which help local surveillance labs integrate their data into large sequence databases, using a ‘one-by-one’ analysis approach.

## Pathogen evolution and statistical genetics

We are designing tools to find evolutionary signatures in the masses of genomic data available, and link these findings to function.

We are also developing automated tools to mark and track concerning lineages as they emerge, predict antimicrobial resistance status, and observed the effects of vaccination on local populations.

We've got a long standing interest in genome-wide association studies, and continue to
develop new methods in this area.

## Sequencing within-host diversity

Pathogen populations also evolve within a single host, sometimes developing mutations with consequences for the whole population. We will develop tools which combine population genetic knowledge, fast informatics approaches, and flexible sequence to streamline the process of sequencing diversity directly from complex samples.

## GPU algorithms

The rate of genomic data growth has outpaced the rate of computational capacity for a number of years. GPUs, with tens of thousands of processing cores, offer a promising solution. Faster algorithms will allow rapid analysis suitable for real-time surveillance of pathogens, and more ambitious analyses of larger datasets, yielding greater discovery power. We aim to address scalability of bioinformatics and mathematical modelling by programming efficient algorithms to run on GPUs, hundreds of times faster than their traditional counterparts.
## Democratising bioinformatics

We aim to keep all of our research useful, reusable and accessible – this guides many of our design decisions in the above themes. On top of this, we have specific projects which aim to advance open science, making our research accessible to as many people as possible.

Projects include: searching and indexing genome analysis and metadata; developing WebAssembly versions of tools which both keep user data private, and are easily run in a web browser; computational biology outreach and teaching.