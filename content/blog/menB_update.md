---
title: "Updated genomic analysis of the 2026 menB outbreak in Kent, UK"
date: 2026-03-30
author: ["John Lees"]
math: true
featured_image: '/images/ska-align/ska_align_0.png'
---
This is a brief update to the [previous menB analysis]({{< relref "menB" >}}) we'd posted here.

UKHSA have released a [technical briefing](https://www.gov.uk/government/publications/invasive-meningococcal-disease-outbreak-2026-technical-briefings/invasive-meningococcal-disease-outbreak-2026-technical-briefing-1) and [further data](https://www.gov.uk/government/publications/invasive-meningococcal-disease-statistical-releases/notified-cases-of-invasive-meningococcal-disease#further-information-about-genomic-sequencing) which includes four further isolates from the outbreak, and a high quality hybrid assembly of the first isolates.

I repeated our analysis from before mapping everything to this new reference, and including the new genomes. In summary:
- Certainly looks like a very closely related outbreak, there is only a single likely SNP separating the isolates.
- There are no recombination events found within the outbreak.
- As before, pilus and PorB recombinations would be what I'd investigate further, but I still think it will be hard to distinguish between diversifying selection and more invasive.
- The alignment had 196083 as ancestral to the other samples, but when doing stricter filtering on the SNPs this went away. Ideally I'd want the reads to confirm this, and to ultimately match with any contact tracing data.

We did also look at the pangenome, but didn't find any gene level differences either.

Overall I think the results and conclusions are consistent as UKHSA's (both on genetics and epidemiology). We didn't look at AMR specifically but it's reassuring that the isolates were predicted to be sensitive to the relevant antibiotic treatments in UKHSA's analysis.

Of the ['further studies' proposed by UKHSA](https://www.gov.uk/government/publications/invasive-meningococcal-disease-outbreak-2026-technical-briefings/invasive-meningococcal-disease-outbreak-2026-technical-briefing-1#part-3-further-studies), a matched carriage study would probably be the most helpful for determining if there are genetic determinants enhancing invasiveness.

## Data download

This two bundle (unzip with `tar xf <file>`) can be loaded in https://jameshadfield.github.io/phandango to view the recomination results: [mapping to internal reference](/menB_internal_ref_gubbins.tar.bz2).
