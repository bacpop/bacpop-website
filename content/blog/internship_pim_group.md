---
title: "Internship in the PIM group"
description: "Summary of the internship of two french students in Lee's group"
date: 2024-08-01
featured_image: ''
draft: false
type: "post"
author: "Antoine Andréoletti & Lale Maouloud"
---

{{< toc >}}

# Introduction

The intersection of biology and computer science has given rise to the rapidly evolving field of bioinformatics. For aspiring scientists in this field, the opportunity to work alongside leading experts at a research institute is a unique experience.  Each year, the French Embassy Internship Program makes this dream a reality for a small group of French students, opening the doors to EMBL-EBI.

In 2024, we, Antoine and Lale, were among eight French students fortunate enough to be chosen for this prestigious internship program. Coming from diverse academic backgrounds and regions of France, we found ourselves embarking on a four-month journey to gain more experience in professional bioinformatics. Spread across both research and service teams at EBI, we had the unique opportunity to tailor our internship experiences to our individual interests. While each of us had a distinct path, we were united by a shared curiosity and a thirst for knowledge.

![](images/internship_french_students/30th_anniversary.jpg)

Both of us decided to work under the mentorship of John Lees in the Pathogen Informatics and Microbiome (PIM) group. The PIM group's focus on understanding the complex world of pathogens resonated with our own interests. We were drawn to the group's innovative approach, which combines cutting-edge computational methods with a deep understanding of biological processes. This unique environment fostered collaboration and encouraged us to think critically and creatively about the challenges facing modern bioinformatics.

In the following sections, we will share our personal journeys through the French Embassy Internship Program at EMBL-EBI. We'll talk about the specific projects we undertook. Our hope is that our experiences will inspire other young scientists to pursue their passion for bioinformatics and to seize the opportunities that can shape their careers and contribute to the advancement of scientific knowledge.

# Antoine - Lale : Our internship experience

## Antoine's experience at EBI

![](images/internship_french_students/Antoine.jpg)

My internship began with a group bonding activity where I had the opportunity to hear about everyone's projects, enjoy traditional English food, play bowling, and get to know my colleagues for the next four months. While starting an internship with a social event might seem unusual, it proved to be an excellent way to connect with the team and understand their work.

During my internship at EBI, I focused on developing user-friendly web interfaces for two tools designed by the team. These tools aim to make complex biological data analysis accessible to professionals without a strong computer science background. Given the importance of biological data for various fields, from public health to medicine, simplifying the analysis process is crucial.
My first project involved SKA, a tool utilising Split-Kmer Analysis using sequence reads files to efficiently align multiple sequences without full reconstruction. This technique enhances alignment performance and is particularly valuable for analysing sequence variation within pathogen populations, a critical aspect of public health and evolutionary genomics. The online platform I developed for SKA streamlines data input, analysis execution, and result visualisation for reference-based mapping and reference-free alignment, expanding its reach to a broader audience. You can learn more about it [here](https://github.com/bacpop/DATACIN).

Subsequently, I worked on SBMLtoOdin, a tool created by Leonie Lorentz. EBI hosts a platform called Biomodels, containing thousands of biological models in SBML format. SBMLtoOdin converts these complex models into Odin, a language designed for ordinary differential equations, enabling researchers to explore model behaviour under different initial parameters. The online platform I built for SBMLtoOdin simplified model selection, visualisation of component evolution over time, and graph generation, promoting the reuse of research findings and fostering collaboration. You can learn more about it [here](https://github.com/bacpop/odinviewer/).

My experience at EBI provided valuable insights into my interests and career path. I thoroughly enjoyed my work and sincerely hope that the tools I developed will prove beneficial to professionals in various fields. I am deeply grateful to the entire team for their warm welcome and camaraderie. Thanks to them, I had the opportunity to play badminton, attend pathogen events at the university, explore new restaurants and cities, and create lasting memories. I extend my special thanks to John for his guidance throughout my internship and to Leonie for her patience in explaining her tool and working with me to make it more accessible. 

## Lale's experience at EBI

![](images/internship_french_students/Lale.jpg)

My name is Lale (Layla), and I'm a 21-year-old Bioinformatics master's student at the University of Rouen Normandy. I have a deep curiosity for the unseen world of biology, and I've been developing my expertise in the dynamic field of computational biology. When I first heard about the opportunity to intern with the BacPop group at EMBL-EBI, I knew it was the perfect chance to apply everything I had learned in a real-world setting, working alongside some of the brightest minds in the field. What I didn’t realise at the time was just how transformative this experience would be. 

From the moment I stepped onto the EMBL-EBI campus, I felt a sense of excitement and anticipation. The campus itself is a hub of innovation, nestled in the serene countryside near Cambridge, and it’s easy to see why it’s a place where groundbreaking research happens. One of the most rewarding aspects of my internship was the projects I was assigned to.
The universe, in all its vastness, is a realm filled with wonders — from distant galaxies to the countless stars and planets that populate them. Similarly, the microscopic world of bacterial genomics reveals a complexity and diversity that is equally astonishing. Recent estimates suggest that there are approximately one trillion microbial species on Earth, with 99.999% of these still undiscovered. This highlights the importance of pangenomics, the study of the complete set of genes across all strains of a species. Pangenomics uncovers the immense genetic diversity and potential within the microbial world. Just as the observable universe represents only a fraction of the entire cosmos, the microbial species we currently know represent only a tiny portion of the total microbial diversity on Earth. Exploring this "genomic dark matter" could revolutionise our understanding of biology, ecology, and evolution.

During my internship, I had the opportunity to work on the innovative graph-based annotation tool, ggCaller. This innovative tool predicts genes within a network-like structure, known as a ‘graph,’ constructed from bacterial pangenomes to identify potential gene sequences called open reading frames (ORFs). When constructing pangenomes from metagenomic data, researchers aim to capture a comprehensive overview of all genes present in a microbial community, including both core and accessory genes. My first project involved developing and applying a metagenome annotation workflow using ggCaller, which I named MAGGIMPUTE (Metagenome-Assembled Genomes Gene-Graph Caller Imputation-based Workflow). You can learn more about my work [here](https://github.com/Lalemaouloud/MAGGImpute). 

After completing my first project, I transitioned to a new and exciting challenge: training a machine learning model to predict the expression of short Open Reading Frames (short ORFs) using ggCaller.Short ORFs, typically defined as sequences encoding peptides of fewer than 100 amino acids, are often underrepresented in genomic annotations. This underrepresentation occurs because traditional gene prediction algorithms tend to overlook short ORFs, either dismissing them as non-coding regions or failing to recognise their biological significance.
Despite their small size, short ORFs can play crucial roles in various cellular processes, including regulation of gene expression, signalling pathways, and stress responses. Predicting the expression of these short ORFs is important because it allows us to better understand their functional roles and their potential contributions to the organism’s phenotype.

Under the guidance of my supervisor, Dr. Samuel Horsfield, I learned not only the technical skills needed to work with these datasets but also how to critically evaluate the biological implications of our findings.
As I return to my studies in France, I do so with a renewed sense of purpose and a wealth of experience that will undoubtedly influence the next steps in my academic and professional journey. The PIM group and EMBL-EBI have left an indelible mark on me, and I will carry the lessons I’ve learned here with me wherever my career takes me.

Top things I like the most about my internship:
- Working at one of the world’s leading bioinformatics institutes was a dream come true. A highlight of my internship was the opportunity to attend weekly seminars and workshops. A particularly memorable experience was participating in the "Industry Workshop: Advances in Machine Learning for Protein Design," where I interacted with leading researchers and gained valuable insights into current and future research perspectives.
- Beyond the technical aspects, what inspired me most was the impact of our work. Knowing that our research could inform strategies to combat bacterial outbreaks gave me a sense of purpose and motivated me to push the boundaries of my knowledge. Living in the UK and experiencing the vibrant culture of Cambridge added an extra dimension to my internship, and the connections I made, both professionally and personally, are something I will always cherish.
- Designing a logo for my pipeline allowed me to tap into my creative side, an aspect of the work I thoroughly enjoyed.
- This internship experience solidified my decision to pursue a PhD after my master's, as I left with a deeper commitment to advancing in this field.
- Being part of such a positive and intellectually stimulating environment has truly enriched my internship experience. After all, who wouldn't thrive when surrounded by smart, friendly, and encouraging people?

# Conclusion

The French Embassy Internship Program at EMBL-EBI provided us both with unique and invaluable experiences in the field of bioinformatics. Both our experiences highlight the critical role of bioinformatics in addressing some of the most pressing challenges in modern biology and medicine, as well as the importance of fostering international collaboration and providing opportunities for young scientists to develop their skills and contribute to this rapidly evolving field.

We are deeply grateful to the French Embassy in London for providing us with this incredible opportunity, and to the PIM group at EMBL-EBI for their warm welcome and unwavering support throughout our internship. This experience has been truly enriching and invaluable for our professional development.
