---
title: "Review: Wellcome Ideathon 2023"
description: "A short post about our project and experience at the 2023 Wellcome Data Science Ideathon."
date: 2023-07-18T13:00:00+01:00
type: "post"
draft: false
author: "Leonie Lorenz, Jacqueline Toussaint, Sam Horsfield & Tim Russell"
featured_image: '/images/header4.jpg'
---

{{< toc >}}

We attended the Wellcome Data Science Ideathon as semi-finalists in July 2023, which saw the Wellcome Trust invite around 100 researchers across 25 teams to compete to answer some of the biggest public health challenges we face today.

## The format

The Ideathon was similar to a Hackathon; groups were tasked with answering specific questions in one of three themes - Infectious Disease, Climate & Health, and Mental Health. The tasks were principally focused on providing low-code solutions employing machine-learning techniques to analyse diverse qualitative and quantitative data. 

Naturally, we chose the Infectious Disease theme, tackling the social-media sentiment analysis challenge. The aim was to identify temporal and geographical trends in negative sentiment towards public health interventions, in this case vaccinations, to aid in predicting declines in vaccine uptake that may ultimately reduce population immunity. We were given 100,000 tweets, all mentioning the hashtag “#COVIDVaccine”, and asked to implement Natural Language Processing (NLP), a form of machine learning that can parse unstructured text to produce a structured output.

Beyond our challenge, a selection of speakers from Wellcome talked to us about their expectations when reviewing grant proposals, such as equality, diversity, and inclusion. They also outlined the overall directions Wellcome is moving towards when funding projects across the three themes. We took part in a number of networking sessions with other participants, scoping out how our research project is novel, how it impacts the research community as well as the public, and how we can communicate with policymakers to make our research actionable. These numerous sessions aimed to solidify each team’s proposal before submitting either our presentation slides (for the student teams) or full proposals (for the researcher teams).

## Our Project (Student Team)

Our student team, the Excellent Biological Investigators, was comprised of Sam Horsfield, Jacqueline Toussaint, and Leonie Lorenz. As mentioned, we decided to tackle the sentiment challenge within the infectious disease category.

*Our solution*

We applied two NLP models: [one](http://dx.doi.org/10.18653/v1/2020.findings-emnlp.148) which was trained to identify positive, neutral or negative sentiment, and [another](https://pypi.org/project/geograpy3/) that predicted a likely location from a text input (see figure below for an outline of NLP). We incorporated bootstrapping to estimate uncertainty. The confidence intervals were then used to identify times at which negative sentiment was high. We combined these results with vaccine availability data and COVID-19 case numbers to inform a mechanistic model for predicting vaccine uptake.

{{< figure src="/images/ideathon/nlpfigure.png" title="The basic workings of an NLP model" >}}

*SentimentHub website*

We created a website for the project using GitHub pages and Hugo. Source code for the website is archived [here](https://github.com/WellcomeIdeathon2023/Excellent_Biological_Investigators/tree/main) and the website can be accessed at [https://qtoussaint.github.io/](https://qtoussaint.github.io/) until we retire it in August 2023.

{{< figure src="/images/ideathon/sentimenthub.png" title="A screenshot of the SentimentHub website" >}}

The SentimentHub website aims to provide information about our pipeline and results in a format suitable for a public (non-professional) audience as well as a research audience. For the public-targeted section, we used real-world analogies to explain each step in the pipeline. By familiarising the audience with possibly unnerving concepts such as NLP, we hoped to dispel common myths and misconceptions about “artificial intelligence” and thus improve support for similar research projects. We also believe it’s important to provide accessible descriptions to inform the public about how we’re using these datasets, particularly when the data are collected from social media sites like Twitter.

The research-facing side of the website provides a more detailed description of the pipeline suited for those wishing to reproduce our results. The guide displays some of our most informative figures with captions and explanations of how they were generated, and the source code is linked throughout the articles.

In addition to our guides, we’ve included an About Us section describing our ethical guidelines, backgrounds, and project roles. Contact information can be found at the bottom of each page, and we’ve encouraged website visitors to reach out to us with comments or questions. 

Overall, the website acts as a guide to our project code and a public-facing repository of some of our main conclusions. 

## Our Experience

Spending three days at the Ideathon was a rewarding experience. Thanks to the variety of challenge topics, we met researchers and PhD students working in a range of fields. Although the setup was somewhat more competitive than most hackathons, people were happy to share and discuss ideas, especially across disciplines.

The itinerary was well planned and there were a variety of networking activities throughout the three days, which seemed to be a primary goal for Wellcome. Although we were under time constraints, all teams exuded a collaborative attitude and came up with impressive proposals.

The Ideathon was the first time any of us visited the Wellcome Building in London, home to one of the biggest funders for health research. It was insightful to learn about which aspects of grant proposals play a role in their decision process regarding funding. Beyond the competitiveness of a project, they paid a great deal of attention to the research environment, focusing on equality, diversity and inclusion throughout the event. It was refreshing to see the inner workings of an important funder in our field and to hear directly from the people making decisions on Wellcome’s research directions about what they feel is important, not just in terms of science, but about the environment in which science is done.
