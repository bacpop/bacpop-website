---
title: "Initial genomic analysis of the 2026 menB outbreak in Kent, UK"
date: 2026-03-23
author: ["John Lees", "Leonie Lorenz", "Neil Macalasdair", "Matthew Russell", "Víctor Rodríguez Bouza", "Ouli Xie", "Johanna von Wachsmann"]
math: true
featured_image: '/images/ska-align/ska_align_0.png'
---
We've done a quick analysis on the meningitis outbreak genome to try and answer whether there is anything obviously genetically unusual about the publicly available outbreak strain.

We aimed for three things:
- To see if the outbreak genome is on an unusually long branch, or otherwise different phylogenetically from its neighbours.
- Look for where mutation/recombination has occurred on the branch leading to the outbreak.
- Look for any effect of phase variable loci in the outbreak.

The final one of these didn't work reliably without a close high-quality reference and/or more careful analysis time.

Background thinking:
- Background and initial thoughts on why this outbreak is happening: https://johnlees.me/posts/menb-outbreak/
- Updated thoughts on why this outbreak is happening (immunity, season, transmission, virulence): https://johnlees.me/posts/menb-outbreak-more/
- Single genome analysis: https://johnlees.me/posts/menb-outbreak-genome/

## Results

- Doesn't appear to be a hypermutator.
- On a long branch, but no longer/more different than other invasive isolate neighbours.
- Phase-variable analysis incomplete/inconclusive without a better reference and more outbreak genomes.
- Private recombination in the following loci (slightly curated, raw data below):
    - _porB_
    - Various pilus associated proteins (at least three separate loci)
    - Iron-uptake regulator
    - transferrin binding. Common in other isolates too.
    - Carbon starvation. Common in other isolates too
    - _argS_
    - _smc_
    - _secA_ / _dnaG_
- and from the draft mapping (likely less good annotation names and may overlap with the above):
    - ferredoxin
    - _abpC_

PorB and the pilus are expected to me ([see within-host table 2 here](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000103)), they are known to vary rapidly. Not sure about the others.

Unclear whether these changes are in any way associated with increased invasion potential.

## Methods and caveats

We essentially followed the methodology of the [PopPIPE](https://github.com/bacpop/PopPIPE) outbreak investigation pipeline:
- Find and download related genomes. We did this by getting all the ST485 genome assemblies in PubMLST using their API.
- Find a reference and draft genome which is as close to the reference as possible. We used sketchlib to pick GCF_000191525.1 on RefSeq and 135095 on PubMLST. We annotated the draft with [Bakta web](https://bakta.computational.bio/).
- Use [`ska map`](https://github.com/bacpop/ska.rust) to generate a whole genome alignment against these references.
- Use [gubbins](https://github.com/nickjcroucher/gubbins) to create a maximum likelihood tree, detecting and removing recombination.
- Create a timed tree with [bactdating](https://github.com/xavierdidelot/BactDating).

Caveats/issues:
- We had to do the mapping with the reference as reads aren't publicly available. ska will limit our resolution of detecting close SNPs.
- For similar reasons, I am suspicious of any recombination in repeat regions (e.g. tRNAs, rRNAs).
- We could also have used more global genomes e.g. from [AllTheBacteria](https://www.allthebacteria.org), which may help with the interpretation.

## Data downloads

These two bundles (unzip with `tar xf <file>`) can be loaded in https://jameshadfield.github.io/phandango to view the recomination results:
- [Mapping to nearby reference](/menB_refseq_gubbins.tar.bz2)
- [Mapping to nearby draft](/menB_draft_gubbins.tar.bz2)

## What next for genomic study of the outbreak

In rough order of importance it would be helpful to have:
- More outbreak genomes (phase variation, confirm whether a single outbreak/compare with contact tracing).
- Carriage sequence data from contacts (carriage vs invasion comparisons). Likely impossible from cases.
- Within-host diversity data e.g. plate sweep metagenomics (bottleneck sizes). Likely impossible from cases.
- Long read assembly (better mapping of function and phase variable regions).

