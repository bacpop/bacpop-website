---
title: "Filtering SNP alignments with ska"
date: 2024-08-20T08:51:31+01:00
draft: false
author: "Romain Derelle"
---

[SKA](https://github.com/bacpop/ska.rust) is a tool for comparing small and highly similar genomes using [split _k_-mers](https://www.biorxiv.org/content/early/2018/10/25/453142).
This guide explains how to create a SNP alignment from a skf file using the different options implemented in the command ska align (here using ska v0.3.5).

![SKA logo](/images/ska-trees/ska_logo.png)


## Recommended command line
For those in a hurry, the recommended/safest command line is:
```
ska align --no-gap-only-sites --filter-ambig-as-missing –filter no-ambig-or-const
```


## Breakdown using an example
In this example, Iet’s consider a skf file generated using k=51 from Illumina sequencing reads of 45 _Mycobacterium tuberculosis_ isolates collected by the UKHSA and belonging to the same transmission cluster (ie, less than 12 SNPs between isolates).

Using the default command ska align, SKA creates a SNP alignment containing 262,123 positions. This is because SKA considers by default the absence of a split _k_-mer as a potential evolutionary event, and any split _k_-mer absent in at least one sample will be output.

![alignment obtained by default](/images/ska-align/ska_align_0.png)

Instead, we can ask SKA not to output split _k_-mers differing solely by the presence of missing data (ie, without nucleotide variation) using the command ska align **--no-gap-only-sites**. In this case, the SNP alignment is reduced to 181 positions.

![alignment obtained with --no-gap-only-sites](/images/ska-align/ska_align_1.png)

However, this alignment still contains many positions with a large fraction of ambiguous characters. These positions likely correspond to split _k_-mers with different middle-bases duplicated in the genome. Unfortunately, variations in coverage mean that in some cases only one of the duplicated split _k_-mer will be present in the skf file, potentially leading to spurious variations between isolates.

To remove these positions, we can ask SKA to consider all ambiguous characters as missing data using the command ska align --no-gap-only-sites **--filter-ambig-as-missing**. In this case, split _k_-mers containing a lot of ambiguous characters will be seen as filled with missing data and discarded by the --min-freq parameter (0.1 by default), producing an alignment of 154 SNPs.

![alignment obtained with --no-gap-only-sites --filter-ambig-as-missing](/images/ska-align/ska_align_2.png)

Finally, the previous alignment contains lot of positions differing solely by the presence of an ambiguous character. These variations might be biological (SNP in a duplicated split _k_-mer with same middle-base, intra-isolate polymorphism or strain mixture) or spurious (split _k_-mer introduced by contaminations, unfiltered sequencing errors in high coverage samples, split _k_-mer introduced by other types of variant, etc …).

We can finally remove these variants by asking SKA to only output split _k_-mers with ATGC variations using the command ska align --no-gap-only-sites --filter-ambig-as-missing  **–filter no-ambig-or-const**. This produces an alignment of 81 SNPs, equivalent to those obtained by traditional read-alignment pipelines.

![alignment obtained with --no-gap-only-sites --filter-ambig-as-missing –filter no-ambig-or-const](/images/ska-align/ska_align_3.png)


Hopefully this brief overview gave you a good understanding of ska align options.


