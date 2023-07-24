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
wget https://zenodo.org/record/8172518/files/building_trees_with_ska.tar
```
After downloading the assemblies, run `tar -xvf building_trees_with_ska.tar` to extract the files.

## Reference-free workflow
The first example describes using a reference-free workflow to analyse assemblies in a case where we are only interested in the SNPs and do not care about structural rearrangements or other global changes. This is accomplished with the `ska align` command and the result can be used to e. g. build a tree for across-species variation.

### Indexing the assemblies
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

### Producing the SNP alignment
The SNP alignment can be extracted from the .skf file produced in the previous step by running
```
ska align --min-freq 1 --filter no-filter output/laos_ska_index.skf -o output/laos_ska_alignment.aln --threads 4
```
which will again take around a few minutes and use around 1.5GB memory. The resulting alignment has around 435k sites.

In the above command, the `--min-freq` option sets the maximum number of missing sites in the alignment to 1 and the `--filter no-filter` option specifies that no extra filtering should be performed. Other options include filtering all constant sites with `--filter no-const` or all constant and ambiguous sites with `--filter no-ambig-or-const`. Using the last option is equivalent to treating any ambiguous site as an N.

### Build a tree
If no further pruning is needed, we can just use the alignment from the previous step to build a phylogeny. A good tool for doing this quickly is [VeryFastTree](https://github.com/citiususc/veryfasttree) but if you have a lot of time [RAxML](https://github.com/amkozlov/raxml-ng) is also a good choice. Both can be installed from bioconda.

Build the tree with VeryFastTree (v4.0.1) by running
```
VeryFastTree -nt -gamma -gtr -threads 4 output/laos_ska_alignment.aln > output/laos_ska_tree.tree
```
As the name might suggest, VeryFastTree is fast and manages to build the tree in a few minutes.

### Look at the tree
We can use the minimalistic [plottree](https://github.com/iBiology/plottree) (install with `pip install plottree`) to quickly look at the tree using
```
plottree output/laos_ska_tree.tree
```
This shows that some of the assemblies are more closely related than the others.

![Phylogenetic tree from raw SKA output](/images/ska-trees/plottree_ska.png)

### Add in some colours
To build a fancier tree, we can use the R script provided at the end of this post to visualize and [midpoint root](https://www.ebi.ac.uk/training/online/courses/introduction-to-phylogenetics/what-is-a-phylogeny/aspects-of-phylogenies/root/) the tree with the leaves coloured according to PopPUNK clusters provided in `data/laos_poppunk_clusters.tsv`. Adding the cluster colours and labels shows that SKA + VeryFastTree has managed to infer a phylogeny that preserves their locality (defined as two assemblies belonging to the same cluster).

![A phylogenetic trees constructed with SKA + VeryFastTree and coloured by PopPUNK cluster. The topography nicely corresponds with the clusters.](/images/ska-trees/SKA_tree_fancy.png)

Next, we'll take a look at using the other mode SKA provides for producing alignments: mapping against a reference sequence.

## Alignment-based workflow
In addition to the reference-free alignments, SKA can also be used to produce alignments against a reference genome. This is useful if the order of the output alignment is meaningful, such as when planning to use [gubbins](https://github.com/nickjcroucher/gubbins) to remove recombination.

Note that gubbins is not suitable for analysing variation across a species (see the note about _"What type of dataset can be analysed with Gubbins?"_ in the [gubbins documentation](https://nickjcroucher.github.io/gubbins/) for more details). To avoid running gubbins on unsuitable data, we'll focus our analysis on variation within the largest PopPUNK cluster in the collection, SC4. This cluster corresponds to the _E. coli_ ST10 clonal complex.

### Reference sequence for SC4
Fortunately for us, ST10 has a downloadable a reference genome in the ENA that we can download with wget
```
wget -q -O - https://www.ebi.ac.uk/ena/browser/api/fasta/U00096.3?download=true | gzip > GCA_000005845.2.fna.gz
```

Since we now only want to use a subset of the assemblies, we'll need to rebuild the index for the genomes that belong to SC4. This info is contained in the `data/laos_poppunk_clusters.tsv` file and we use the following commands to both convert it to an input list for SKA and to add the reference sequence to the index
```
paste <(grep "SC4$" data/laos_poppunk_clusters.tsv | cut -f1) <(grep "SC4$" data/laos_poppunk_clusters.tsv | cut -f1 | sed 's/^/assemblies\//g' | sed 's/$/.fa.gz/g') > output/laos_SC4_input_list.tsv
echo -e "GCA_000005845.2\t$(pwd)/GCA_000005845.2.fna.gz" >> output/laos_SC4_input_list.tsv
```

### Aligning with ska map
Build the index as previously with `ska build` and then run `ska map` to align the indexed assemblies against the reference genome with
```
ska build -f output/laos_SC4_input_list.tsv -k 31 -o output/laos_SC4_index --threads 4
ska map -o output/laos_SC4_map.aln --ambig-mask --threads 4 GCA_000005845.2.fna.gz output/laos_SC4_index.skf
```
This time the alignment has 4 641 653 sites, which is the number of bases in the reference genome. Compared to `ska align`, using `ska map` keeps all bases in the reference sequence and replaces the sites it cannot find in the indexed assemblies with gaps. If you use the command
```
sed -n '4p' output/laos_SC4_map.aln | less
```
to look at the alignment of the first assembly against the reference you'll see that some sites are marked as missing/gaps.

### Removing recombination
In a typical genomic epidemiology workflow looking at variants **within a lineage** one typically wants to remove recombination from the alignment. For our SC4 alignment, we will do this using [gubbins](https://github.com/nickjcroucher/gubbins). Since Gubbins only accepts characters in the ACGTN- range, we had to use the `--ambig-mask` option with `ska map` to mask ambiguous bases (SKA uses the [IUPAC notation](https://en.wikipedia.org/wiki/Nucleic_acid_notation) which gubbins does not support) with N's.

Gubbins (v3.2.1 in our example) can be run on the reference mapping with
```
run_gubbins.py --prefix output/gubbins output/laos_SC4_map.aln --threads 4 --filter-percentage 27.0
```
This will create the recombination-free tree `output/gubbins.final_tree.tre`. We had to increase the `--filter-percentage` parameter from the default 25.0 to 27.0 because one of the input sequences had ~26% missing sites.

Gubbins produces an alignment where recombination has been removed and only ~7 000 sites remain. These sites are enough to differentiate the assemblies belonging to SC4 and we can check this by visualising the tree with plottree
```
plottree output/gubbins.final_tree.tre
```

![Phylogenetic tree from Gubbins](/images/ska-trees/plottree_sc4.png)

In this tree the assemblies from Laos cluster into several distinct groups within the lineage, and none of them are closely related to the reference genome which is sensible since the reference genome is from the _E. coli_ K-12 strain that was isolated a hundred years ago on the other side of the world in [Palo Alto, California, USA in 1922](https://www.genome.wisc.edu/resources/strains.htm).

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

## Read the raw SKA alignment + VeryFastTree tree in and midpoint root it
tree2 <- read.tree("ska.aln.tree")
midpoint_rooted_tree <- midpoint.root(tree2)

## Read in the PopPUNK clusters for each assembly
sts <- read.table("data/laos_poppunk_clusters.tsv", sep='\t', comment.char='@', header=FALSE)
sts <- sts[match(tree2$tip.label, sts$V1), ]

## Get the 7 most common clusters
top_st_names <- names(tail(sort(table(sts$V2)), 7))
top_st_colors <- cbind(top_st_names, colors[as.numeric(factor(top_st_names))])

## Set up the colors so that the 7 most common have a different color from the rest
other_st_names <- setdiff(unique(sts$V2), top_st_names)
st_colors <- rbind(top_st_colors, cbind(other_st_names, rep("black", length(other_st_names))))
st_colors <- st_colors[match(sts[, 2], st_colors), ]

## Add colors and labels, same as above
st_colors <- st_colors[match(sts[, 2], st_colors), ]
tree2$tip.label <- paste(tree2$tip.label, sts[, 2], sep='_')
tree2.colors <- st_colors[, 2]

## Plot both trees side-by-side
pdf(file="SKA_tree_fancy.pdf", width=9, height=9)
par(mar=c(1, 1, 3, 1))
plot.phylo(tree2, tip.color=tree2.colors)
title(main="Maximum likelihood tree\n(SKA + VeryFastTree)", adj=0, font.main=1, cex.main=1.5)
legend("bottomright", legend=top_st_colors[order(as.numeric(gsub("SC", "", top_st_colors[, 1]))), 1], fill=top_st_colors[order(as.numeric(gsub("SC", "", top_st_colors[, 1]))), 2], bty='n', title="PopPUNK\ncluster", cex=1.33)
dev.off()
```
