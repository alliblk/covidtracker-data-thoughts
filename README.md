# covidtracker-data-thoughts

## Overview

This repository stubs out my initial data analysis plans for the CovidTracker data, to be taken over by whomever at Biohub would like to pick this up in my absence.

Currently, this directory contains a Nextstrain workflow that will perform county-level phyloeographic inference on a subsampled portion of the CovidTracker dataset.

To run the workflow, first you'll need to [make a Nextstrain conda environment](https://docs.nextstrain.org/en/latest/install.html).

Once you have that environment available to you, go ahead and clone this repo. Once you're in this directory activate your Nextstrain conda environment.

Because of github file size limitations I've compressed the fasta file with the CovidTracker sequence data. Before running the workflow, you'll need to decompress this file.

Once that fasta file has been decompressed, you can run the workflow within the top level of this directory by running:

`nextstrain build . --cores all --configfile config/covidtracker-phylogeo.yaml`

 
 ## Initial thoughts on potential questions to explore:

### Introductions of SARS-CoV-2 to California

I would be interested here in looking at patterns of SCV-2 introductions to California over time. In particular, I would be interested in the frequency of SARS-CoV-2 introductions during the early portion of the epidemic. How many are there, and how long do they circulate for after introduction? How do these patterns compare during periods of lockdown versus when lockdowns were eased?
Here I’d do a phylogeographic analysis of downsampled CovidTracker data with a lot of contextual genomic data from other parts of the US and the world. I would use genetic proximity to CovidTracker focal samples as my criteria for including contextual data. Note that the current workflow stubbed out in this repo sources context simply from the Nextstrain team's reference files. For the proper analysis, full data from GISAID should be pulled (contact Dan Lu at CZI).

### Within-CA county-level phylogeographic analysis

* Which counties have highly connected outbreaks (high phylogeographic migration rates between them)?

* Is there a North/South divide in California in terms of what strains get introduced and circulate? E.g. do we see population structure within CA?

* Is there an urban to rural dissemination pattern (phylogeographic migration rates are higher from urban counties to rural counties than they are from rural counties to urban counties)?

* Do introduction and transmission dynamics look different in the pre- and post-vaccination era? (There may not be enough data in the post-vaccination time period to look at this though).

* What is NeTau through time (skyline plots)? How does this correlate with the number of new introductions into California through time?

* What are the different patterns of introduction into different counties? Do we observe differences between counties in terms of some having high rates of introduction and shorter periods of endemic spread post-introduction? Versus fewer introductions and longer transmission chains following introduction? (As an example, see [Dudas et al, 2017](https://www.nature.com/articles/nature22040) Figure 2 and Extended Data Figure 7)

### Lineage specific dynamics

* For different lineages (e.g. Wildtype, Alpha, Delta, Epsilon etc depending on power), what are the:

* Lineage specific growth rates as estimated from genomic data.

* How many introductions of the lineage do we infer to have occurred?

* What is the TMRCA of these different introductions, and how does that relate to incidence data?

* Do we see evidence given the TMRCA and incidence data that some of these lineages circulated cryptically? If so, for how long?

### How completely have we captured circulating viral diversity?

It could potentially be interesting to use rarefaction curves to explore whether the degree of genomic surveillance we performed has captured most of the circulating diversity of SARS-CoV-2 in California (especially during the early months with CovidTracker was the primary program conducting genomic surveillance). Do we see the apparent diversity of sequences continuing to increase with more samples? Or does this level off? As an example, see Figure 6 in [Black et al, 2019](https://bmcinfectdis.biomedcentral.com/articles/10.1186/s12879-019-4566-2).

### Data analysis considerations

* Phylogeographic inference is quite sensitive to sampling patterns. All of these analyses should be done essentially as sensitivity analyses - i.e. one analysis with all the data, and then repeat that same analysis over multiple replicates of subsampled data (downsampled at random without replacement, ideally under different sampling protocols to see how sampling impacts inferences). 

* My default “unbiased” downsampling would be to sample proportionally to incidence in a jurisdiction, but if that is not possible, sampling jurisdictions according to relative population size (as a proxy for outbreak size) could work. 

* I would also have a sampling scheme where all jurisdictions are represented by an equal number of genomes (although keep in mind that this will likely artificially enrich sampling in smaller jurisdictions with smaller outbreaks, which might make you preferentially capture greater numbers of circulating lineages from smaller jurisdictions).
