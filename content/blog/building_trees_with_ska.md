---
title: "Building trees with SKA"
date: 2023-07-21T16:22:28+01:00
draft: false
author: "Tommi M&auml;klin"
---
[SKA](https://github.com/bacpop/ska.rust) is a tool for comparing small and highly similar genomes using [split _k_-mers](https://www.biorxiv.org/content/early/2018/10/25/453142). This blogpost will explain how to use SKA to build a phylogenetic tree for different _Escherichia coli_ lineages in a few minutes. Although SKA is tailored more towards analysing variation within a lineage, tree-building ends up working fine for the whole species but requires more memory.

![SKA logo](/images/ska-trees/ska_logo.png)

## Why SKA is good for building phylogenetic trees
The basic approach to building a tree with SKA is to generate a SNP alignment using split _k_-mers and then feed that to a tree building algorithm of choice. Since SKA does not require a specifying a reference sequence to determine the SNPs, SKA gets around potential biases introduced by reference choice and is thus particularly well suited to analysing microbial genomes derived from outbreaks or pathogen surveillance.

## Installing SKA
SKA can be installed in multiple ways:
1. Precompiled binary from the [SKA GitHub repository](https://github.com/bacpop/ska.rust/releases).
2. Through the rust programming language's package manager cargo with `cargo install ska`.
3. From bioconda with `conda install -c bioconda ska2`.
4. Building from source.

In this tutorial I used SKA v0.3.2 to run everything.

## Input data
We will use a collection of 46 _E. coli_ hybrid Nanopore+Illumina assemblies isolated from travellers visiting the city of Vientiane in Laos. These assemblies were published as part of [Snaith et al. (2023)](https://doi.org/10.1099/mgen.0.001000).

All materials for running the analysis in this post can be downloaded from [zenodo](https://zenodo.org/record/8172518/files/building_trees_with_ska.tar) with wget
```
wget assemblies.tar
```
After downloading the assemblies, run `tar -xvf assemblies.tar` to extract the files.

## Indexing the assemblies
To run the split _k_-mer alignment, we first need to build an index of the split _k_-mers from the assemblies. This is accomplished with the `ska build` command which requires a tab-separated list consisting of the sequence name and assembly file path as input:
```
LA002	assemblies/LA002.fa.gz
LA022	assemblies/LA022.fa.gz
LA023	assemblies/LA023.fa.gz
.
.
.
```
which is provided in `data/laos_ska_input.tsv`, or can be created using the command
```
paste <(ls assemblies | sed 's/[.].*$//g') <(ls -d assemblies/*) > data/laos_ska_input.tsv
```
The above only works if you're using bash as your shell.

The split _k_-mers index is built from the input list by running
```
ska build -f data/laos_ska_input.tsv -k 31 -o output/laos_ska_index --threads 4
```
which will take a few minutes and use ~8GB of memory. SKA uses a lot of memory for species-wide analyses but when doing within-lineage analyses the method would be more efficient.

![Screenshot of the output written by SKA to terminal](/images/ska-trees/ska_run.png)


In the example we chose the value of _k_ as 31 which is a commonly used choice for analysing bacterial genomes. For a more detailed analysis of the different possible values of _k_, have a look at the paper by [Bussi, Kapon, and Reich](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0258693) in PLOS ONE.

## Producing the SNP alignment
The SNP alignment can be extracted from the .skf file produced in the previous step by running
```
ska align --min-freq 1 --filter no-filter output/laos_ska_index.skf -o output/laos_ska_alignment.aln --threads 4
```
which will again take around a few minutes and use around 1.5GB memory. The resulting alignment has around 435k sites.

In the above command, the `--min-freq` option sets the maximum number of missing sites in the alignment to 1 and the `--filter no-filter` option specifies that no extra filtering should be performed. Other options include filtering all constant sites with `--filter no-const` or all constant and ambiguous sites with `--filter no-ambig-or-const`. Using the last option is equivalent to treating any ambiguous site as an N.

## Build a tree
If no further pruning is needed, we can just use the alignment from the previous step to build a phylogeny. A good tool for doing this quickly is [VeryFastTree](https://github.com/citiususc/veryfasttree) but if you have a lot of time [RAxML](https://github.com/amkozlov/raxml-ng) is also a good choice. Both can be installed from bioconda.

Build the tree with VeryFastTree (v4.0.1) by running
```
VeryFastTree -nt -gamma -gtr -threads 4 output/laos_ska_alignment.aln > output/laos_ska_tree.tree
```
As the name might suggest, VeryFastTree is fast and manages to build the tree in a few minutes.

## Look at the tree
We can use the minimalistic [plottree](https://github.com/iBiology/plottree) (install with `pip install plottree`) to quickly look at the tree using
```
plottree plottree output/laos_ska_tree.tree
```
This seems to show some clustering of the samples but the branch lengths within the perceived clusters are fairly long.

![Phylogenetic tree from raw SKA output](/images/ska-trees/plottree_ska.png)

## Removing recombination
Before building the tree as described previously, a typical genomic epidemiology workflow would remove recombination from the alignment. We can do this using [gubbins](https://github.com/nickjcroucher/gubbins). Gubbins, however, accepts only characters in the ACGTN range but SKA reports the alignment using the [IUPAC notation](https://en.wikipedia.org/wiki/Nucleic_acid_notation).

We can convert all non-ACGT characters to ambiguous bases with the symbol N using a simple sed command
```
sed 's/[UWSMKRYBDHV-]/N/g' output/laos_ska_alignment.aln > output/laos_clean_alignment.aln
```
alternatively, the sites could have been removed when running `ska align` by adding the filter `--filter no-ambig-or-const`.

After replacing the ambiguous sites with N's, run gubbins (v3.2.1 in our example) with
```
run_gubbins.py --prefix output/gubbins output/laos_clean_alignment.aln --threads 4
```
This will create the recombination-free tree `output/gubbins.final_tree.tre`.

Gubbins produces an alignment where recombination has been removed and only ~8000 sites remain. While this might seem small, it's a result of running both gubbins and ska on a collection of _E. coli_ genomes from multiple lineages rather than from within a single lineage which is what both tools are designed for.

The 8000 sites are still enough to differentiate the lineages which we can see by visualising the tree with plottree
```
plottree output/gubbins.final_tree.tre
```
Compared to the previous tree, the branch lengths within the visible clusters are noticably shorter.

![Phylogenetic tree from Gubbins](/images/ska-trees/plottree_gubbins.png).

## Visualizing the tree
Finally, we can add in some Fancy visualization code with colors and legends using a provided R script (included in the download and at the end of the post):
```
Rscript plot_tree.R`
```
which looks something like this

![Two phylogenetic trees constructed with SKA. The left panel contains a tree built with SKA and VeryFastTree, which has noticably longer branch lengtsh within the visible clusters. The right panel contains a tree built with SKA and Gubbins, where the branch lengths within each cluster are shorter due to the reombination removal performed in Gubbins.](/images/ska-trees/SKA_trees.png).

And that's it! Happy tree-building.

## About the author
I visited John Lees' lab in Spring 2023 and have been using both SKA v1 and v2 to build lots of trees. This blogpost was a result of wanting to get others to do the same because installing snippy gets increasingly more difficult over time and reference-free approaches should be preferred anyway. If you want to know what I'm doing now, check out my personal website [https://maklin.fi](https://maklin.fi).

## R script for plotting trees
```
#!/usr/bin/env Rscript
#
## Plot a tree and add some colors

library("ape")
library("phytools")

## Okabe-Ito color palette for the 7 most common clusters
colors <- c("#e69f00", "#56b4e9", "#009e73", "#f0e442", "#0072b2", "#d55e00", "#cc79a7")

## Read the gubbins tree in and midpoint root it
tree <- read.tree("output/gubbins.final_tree.tre")
midpoint_rooted_tree <- midpoint.root(tree)

## Read in the PopPUNK clusters for each assembly
sts <- read.table("data/laos_poppunk_clusters.tsv", sep='\t', comment.char='@', header=FALSE)
sts <- sts[match(tree$tip.label, sts$V1), ]

## Get the 7 most common clusters
top_st_names <- names(tail(sort(table(sts$V2)), 7))
top_st_colors <- cbind(top_st_names, colors[as.numeric(factor(top_st_names))])

## Set up the colors so that the 7 most common have a different color from the rest
other_st_names <- setdiff(unique(sts$V2), top_st_names)
st_colors <- rbind(top_st_colors, cbind(other_st_names, rep("black", length(other_st_names))))
st_colors <- st_colors[match(sts[, 2], st_colors), ]

## Add the PopPUNK clusters to the leaf labels
tree$tip.label <- paste(tree$tip.label, sts[, 2], sep='_')
tree.colors <- st_colors[, 2]

## Read the raw SKA alignment + VeryFastTree tree in and midpoint root it
tree2 <- read.tree("ska.aln.tree")
midpoint_rooted_tree <- midpoint.root(tree2)

## Add colors and labels, same as above
sts <- sts[match(tree2$tip.label, sts$V1), ]
st_colors <- st_colors[match(sts[, 2], st_colors), ]
tree2$tip.label <- paste(tree2$tip.label, sts[, 2], sep='_')
tree2.colors <- st_colors[, 2]

## Plot both trees side-by-side
pdf(file="SKA_trees_pretty.pdf", width=10, height=10)
par(mfrow=c(1, 2), mar=c(1, 1, 3, 1))
plot.phylo(tree2, tip.color=tree2.colors)
title(main="Maximum likelihood tree\n(SKA + VeryFastTree)", adj=0, font.main=1)
legend("bottomright", legend=top_st_colors[order(as.numeric(gsub("SC", "", top_st_colors[, 1]))), 1], fill=top_st_colors[order(as.numeric(gsub("SC", "", top_st_colors[, 1]))), 2], bty='n', title="PopPUNK\ncluster")
plot.phylo(tree, tip.color=tree.colors)
title(main="Recombination removed tree\n(SKA + Gubbins)", adj=0, font.main=1)
dev.off()
```
