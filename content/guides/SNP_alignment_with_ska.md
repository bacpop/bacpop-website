---
title: "Filtering SNP alignments with SKA"
date: 2024-08-20T08:51:31+01:00
draft: false
author: "Romain Derelle"
---

[SKA](https://github.com/bacpop/ska.rust) is a tool for comparing small and highly similar genomes using [split _k_-mers](https://www.biorxiv.org/content/early/2018/10/25/453142).
This guide explains how to create a SNP alignment from a skf file using the different options implemented in the command ska align (here using ska v0.3.5).

![SKA logo](/images/ska-trees/ska_logo.png)


## Recommended command line
For those in a hurry, the recommended command line for filtering for precise SNP calling is:
```bash
ska align --no-gap-only-sites --filter-ambig-as-missing --filter no-ambig-or-const
```


## Breakdown using an example
In this example, let’s consider a skf file generated using k=51 from Illumina sequencing reads of 45 _Mycobacterium tuberculosis_ isolates collected by the UKHSA, and belonging to the same transmission cluster (i.e. less than 12 SNPs between isolates).

Using the default command ska align, SKA creates a SNP alignment containing 262,123 positions. This is because SKA considers by default the absence of a split _k_-mer as a potential evolutionary event, and any split _k_-mer absent in at least one sample will be output.

![alignment obtained by default](/images/ska-align/ska_align_0.png)

Some of these samples have quite low coverage, causing _k_-mers to be erroneously missing. So, we can ask SKA not to output split _k_-mers differing solely by the presence of missing data (i.e. without any SNP variation) using the command ska align `--no-gap-only-sites`. In this case, the SNP alignment is reduced to 181 positions.

![alignment obtained with --no-gap-only-sites](/images/ska-align/ska_align_1.png)

This alignment still contains many positions with a large fraction of ambiguous characters. In Mtb, these positions likely correspond to split _k_-mers with different middle-bases duplicated in the genome. Variations in coverage between samples mean that in some cases only one of the duplicated split _k_-mer will be present in the skf file, potentially leading to spurious variation between isolates.

As these are largely due to repeats, to remove these positions, we can ask SKA to consider all ambiguous characters as missing data by adding `--filter-ambig-as-missing`. In this case, split _k_-mers containing a lot of ambiguous characters will be seen as filled with missing data and discarded by the `--min-freq` parameter (0.1 by default), producing an alignment of 154 SNPs.

![alignment obtained with --no-gap-only-sites --filter-ambig-as-missing](/images/ska-align/ska_align_2.png)

Finally, this alignment still contains lot of positions differing solely by the presence of an ambiguous character. These variants might be real: e.g. SNP in a duplicated split _k_-mer with same middle-base or intra-isolate polymorphism. They may also be the result of errors: e.g. split _k_-mer introduced by contamination, unfiltered sequencing errors in high coverage samples, split _k_-mer introduced by more complex variants.

We can also remove these variants by asking SKA to only output split _k_-mers with unambiguous ATGC variations by adding `--filter no-ambig-or-const`. This produces an alignment of 81 SNPs, identical to those obtained by reference-based read-alignment pipelines.

![alignment obtained with --no-gap-only-sites --filter-ambig-as-missing –filter no-ambig-or-const](/images/ska-align/ska_align_3.png)


Hopefully this brief overview gave you a good understanding of ska align's filtering options.


