---
title: "Mutation Spectra in Streptococcus pneumoniae"
description: "Patterns of mutation in biological systems ranging from cancer cells to disease-associated bacteria to SARS-CoV2 have been shown to reflect features of those systems, such as their ecological niches and in the case of cancers, their etiology. We set out trying to investigate if mutational spectra from pneumococci could similalrly be linked to the microbes' epidemiological features."
date: 2022-12-13T17:00:00+01:00
author: "Bruhad Dave"
type: "post"
draft: false
featured_image: "/images/header11.jpg"
math: true
---

{{< toc >}}

## An Introduction to Mutation Spectra  

It is intutitive that an organism's ecological, phenotypic, or epidemiological context exposes it to distinct mutagens, and might thus produce specific signatures and patterns of mutation -- that organism's mutational spectrum.  

This idea is well-established in oncology. Cancer epidemiolgy studies have shown that a handful of genes, most prominently the human p53 gene, show patterns of mutation specific to the corresponding cancer types. Further, certain mutagens are associated with certain mutation types or patterns. For example, in Pfeifer & Besaratinia's 2009 review[^1] on the subject, they summarised findings from various studies on mouse models containing human p53 genes (_Hupki_ mouse models).  

{{< figure src="/images/mutspect/fig1.png" title="Figure 1: Mutation spectra for the p53 in Hupki mouse embryonic fibroblasts when exposed to benzo(a)pyrene (A), aristolochic acid (B), 3-nitrobenzanthrone (C), and control conditions (D)" >}}  

Mutational spectra in the (human) p53 gene in _Hupki_ mouse embryonic fibroblasts were enriched in G>T mutations when exposed to a tobacco-derived carcinogen (panel A above) and the overall pattern of mutation resembled that from lung-cancer patients who smoked. Similarly, exposure to a plant extract implicated in the etiology of urothelial cancers produced a elevated A>T mutations (panel B above), a hallmark for those cancers (panel B above), and exposure to a particulate air pollutant produced a mutational pattern identical to that seen in other systems exposed to that pollutant (panel C above).  

### Mutational Spectra in Microbes

In a 2021 paper[^2], Chris Ruis and colleagues observed that _Mycobacterium abscessus_ isolated from the lungs of cystic fibrosis sufferers showed spectra of mutations that were distinct from environmental isolates (Fig 2 below). In a subsequent work[^3], Ruis, et al., calculated mutational spectra for data from a range of microbial samples, and attempted to associate them with specific mutagenic contexts. They found that distinct patterns of variation were associated with specific DNA-repair defects and ecological niches. To resonctruct these mutational spectra, Chris wrote a tool called [MutTui](https://chrisruis.github.io/MutTui/#/), which they later used to show that mutation patterns in SARS-CoV2 were different between virus lineages that replicated in the upper and lower respiratory tracts[^4].  

{{< figure src="/images/mutspect/fig2.png" title="Figure 2: Mutational spectra for environmental M. abscessus samples (above) and patient-isolate samples (below, shown as difference from environmental spectrum)" >}}  

## Mutational Spectra in Pneumococcal Epidemiology

Given the evidence for associations between the ecological niche a microbe occupies and the patterns of mutation it accumulates, we reasoned that mutational spectra might be likewise correlated to epidemiological factors in _Streptocuccus pneumoniae_. _S. pneumoniae_ is a genetically diverse, pathogenic bacterium that can cause pneumonia and meningitis in individuals with weaker or weakened immune systems, such as children or the elderly, and immunodeficient or immunosuppressed individuals. One epidemiological feature of interest was carriage duration (CD), the length of time that the bacterium resides in a given individual before it is transmitted to another. A 2017 study led by John[^5] estimated CD for samples from the Maela dataset[^6], a densely sampled, longitudinal dataset derived from a camp for displaced persons in Thailand. That work showed that CD is heritable, and variability in CD is attributable to the pathogen's genotype.  

We used CD data estimated from this study, and combined it with information about sample lineage derived from the [Global Pneumococcal Sequencing (GPS)](https://www.pneumogen.net/gps/) project. The GPS project uses [PopPUNK](https://github.com/bacpop/PopPUNK), which applies a kmer-based approach to calculate similarity between the input samples and assigns them to lineages, or clusters, which, in the GPS database, are referred to as GPS clusters (henceforth referred to as GPSCs).  

{{< figure src="/images/mutspect/fig3.png" title="Figure 3: Our MutTui workflow" >}}  

In our workflow, we first obtained precalculated GPSC assignments for each Maela sample, and then aggregated the Maela dataset by GPSC. We then used MutTui to reconstruct mutational spectra for all the GPSCs represented in the data, that contained more than 20 samples. As the 33 clusters we retained, represented an intersection of the Maela data and the larger GPS dataset, each of the clusters is represented as maela_gpsc (e.g. maela_1 = Maela samples assigned to GPSC-1).  

### MutTui: An Overview

As noted above MutTui reconstructs mutational spectra for microbial samples. The tool does so using a phylogenetic tree of each subset of the data (in our case, a tree for each GPSC), a variant alignment of all the samples in that subset (we used [Gubbins](https://github.com/nickjcroucher/gubbins) to produce both the phylogenetic tree and the variant alignment), a reference genome (we used _Streptococcus pneumoniae_ ATCC 700669[^7]), and a conversion file (this maps variants in the Gubbins VCF file back to their genomic position; this is achieved using a call to `MutTui convert-vcf`).  

The tool performs ancestral reconstruction on the phylogenetic tree using TreeTime, and then calculates a Single Base-Substitution (SBS) spectrum, and also a Double Base-Substitution (DBS) spectrum. Note that here, we only worked with SBS spectra. MutTui outputs include plots showing proportions of SBS and DBS, as well as csv files containing frequencies for each type of mutation. MutTui takes into account the context of each mutation, i.e. the nucleotides flanking each mutation site, in its outputs.  

{{< figure src="/images/mutspect/fig4.png" title="Figure 4: MutTui plot showing skewed spectra (at left), and corrected spectra obtained after branch-rescaling (at right)" >}}  

Our initial trials with MutTui produced skewed SBS spectrum plots, but we discovered that rescaling the branches of the Gubbins phylogenetic tree (wherein branch lengths are in the units of substitutions _per genome_) by the length of the reference genome, so that the branches were represented in substitutions _per site_, fixed this issue. Chris confirmed that this step was necessary when working with Gubbins phylogenetic trees.  

### An Initial Trial

{{< figure src="/images/mutspect/fig5.png" title="Figure 5: PCA plot produced by `MutTui cluster`" >}}  

While we were setting up our workflow, Chris was kind enough to send us mutational spectra that he had reconstructed for a subset of GPSCs. We used `MutTui cluster` to see how these GPSCs clustered. One thing we looked at was whether GPSC2, which contains a majority of the Sertotype 1 (which is implicated as the most pathogenic) samples in GPS, stood out from the rest, but this was not the case. The outlier GPSCs did contain samples from other pathogenic serotypes (namely 14 and 19A), but these serotypes are represented in multiple GPSCs, so this observation does not point to a strong correlation between mutation spectra and serotypes (as a proxy for pathogenicity).  

### Mutational Spectra and Carriage Duration

{{< figure src="/images/mutspect/fig6A.png" title="Figure 6A: UMAP projection of mutational spectra, points are coloured and sized by mean carriage duration" >}}  

Having reconstructed spectra for the 33 Maela_GPSCs, we plotted a UMAP clustering of these spectra and found that the scatterplot showed 2 distinct groupings. Colouring each point on this plot by the average CD of the corresponding Maela_GPSC showed that the two groups were not separated based on CD, nor did CD appear to be a driver for this clustering, indicating that mutation spectra might not be correlated with duration of carriage.  

{{< figure src="/images/mutspect/fig6B.png" title="Figure 6B: UMAP projections of mutational spectra of the 33 Maela_GPSC clusters, coloured by various metadata" >}}  

We also coloured this UMAP projection with a range of metadata: we converted categorical and binary data into 1s and 0s, and plotted averages for a quick, overall view. For examples, for drug susceptibility, we assigned 1 to susceptible samples and 0 to both resistant ones and ones that had intermediate phenotypes; averaging over such data would yeild the fraction of susceptible samples in each cluster. However no clear patterns emerged for any of the metadata we tested. As noted earlier, MutTui produces mutation spectra that account for mutation context, i.e. the nucleotides on either side of the variant site. We removed this context, summing all mutations of the same type, and ran UMAP on this simpler dataset, obtaining similar results. 

Next, we performed a risk calculation for each substitution type, calculating a True/False value for:  

$\frac{\mathrm{Proportion \\ of \\ a \\ substitution \\ in \\ mutations \\ in \\ each \\ cluster}}{\mathrm{Proportion \\ of \\ that \\ substitution \\ in \\ all \\ mutations \\ in \\ the \\ data}} > 1$  

for each substitution type. Here again, we found that the 33 Maela_GPSC clusters separated into two groups. However, we note that the two groups obtained in the UMAP projection of mutation spectra are not the same as the two obtained using this risk analysis. The grouping we observed with the risk analysis also did not seem to be correlated to mean CD.  

{{< figure src="/images/mutspect/fig7.png" title="Figure 7: Risk analysis for substitutions with (above) and without (below) context (Purple=True, Yellow=False)" >}}  

We then calculated the mean spectrum for the two groups we observed in the UMAP, and compared them by subtracting the mean spectrum of group 2 (on the right of the plot, n=10) from group 1 (on the left, n=23). We observed that group2 had a higher proportion of T>C mutations across all contexts.  

{{< figure src="/images/mutspect/fig8.png" title="Figure 8: The difference between mean mutational spectra for groups 1 and 2 in the UMAP projection of mutational spectra (see Fig. 6A)" >}}  

## Conclusion

In the brief, exploratory analysis we performed, we did not uncover any particularly striking correlations between the pattern of mutations for a group of related samples, and epidemiological information such as antimicrobial susceptibility or whether, for example, the samples in that group were collected mostly from infants.  

However, more fine-grained investigation into associations between pneumococcal mutational spectra and phenotypes or ecology is certainly merited. One obvious extension would be to incorporate more types of metadata where it is available. As is often the case with open-ended analyses, there is a fair chance that potential associations turn up. The clear obstacle to this is that many interesting types of metadata might not be available for some or most of the input data, or indeed, not available at all.  

Another potential way forward might be to decompose clusterwise mutation spectra into per-sample mutation spectra. This would be a useful way to increase the resolution of the analysis, and it could prove a good way to handle the fact that metadata is often collected on a per-sample basis, and can be binary or categorical rather than continuous. One part of this approach might be to start from raw sequencing reads (or better yet, variants called from reads) instead of assemblies, as this is likely to help create more complete sample-wise mutation spectra. In a similar vein, applying this sort of analysis on a larger dataset might also create robust spectra. We restricted our analysis to Maela data such that it contained only GPSC clusters represented by >20 Maela samples: it might be useful to increase the cutoff to 50, for example.  

Finally, while UMAP and other clustering algorithms are extremely useful to quickly get an idea about data like mutational spectra, it might be useful to apply other statistical approaches, including perhaps those from machine-learning, to deconvolute relationships between a sample's (or cluster's) mutational spectrum and associated biological or ecological information. This might ultimately lead to potential predictive models whereby one might be able to estimate phenotypes, ecological niches, or active mutagenic forces more broadly, using patterns of mutation, something that would be quite useful in outbreak surveillance and the genomic epidemiology of emerging or nosocomial pathogens.  

### References and Links

[^1]: [Pfeifer, G. P. & Besaratinia, A. Mutational spectra of human cancer. Hum Genet 125, 493–506 (2009).](https://doi.org/10.1007%2Fs00439-009-0657-2)  
[^2]: [Ruis, C. et al. Dissemination of Mycobacterium abscessus via global transmission networks. Nature Microbiology 6, 1279–1288 (2021).](https://doi.org/10.1038/s41564-021-00963-3)  
[^3]: [Ruis, C. et al. Mutational spectra analysis reveals bacterial niche and transmission routes. bioRxiv 2022.07.13.499881 (2022) doi:10.1101/2022.07.13.499881.](https://doi.org/10.1101/2022.07.13.499881)  
[^4]: [Ruis, C. et al. Mutational spectra distinguish SARS-CoV-2 replication niches. bioRxiv 2022.09.27.509649 (2022) doi:10.1101/2022.09.27.509649.](https://doi.org/10.1101/2022.09.27.509649)  
[^5]: [Lees, J. A. et al. Genome-wide identification of lineage and locus specific variation associated with pneumococcal carriage duration. eLife 6, e26255 (2017).](https://doi.org/10.7554/elife.26255)  
[^6]: [Chewapreecha, C. et al. Dense genomic sampling identifies highways of pneumococcal recombination. Nat Genet 46, 305–309 (2014).](https://doi.org/10.1038%2Fng.2895) . 
[^7]: _Streptococcus pneumoniae_ ATCC700669 EMBL Accession: [FM211187](https://www.ncbi.nlm.nih.gov/nuccore/FM211187)