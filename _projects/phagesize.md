---
name: Bacteriophage genome sizes
tools: [science, python, data viz]
order: 2
image: ../assets/figs/2025.png
description: Phage sizes vary widely, with genomes spanning several orders of magnitude. I couldn’t find a recent, clear plot to illustrate this, so I made one.
---

# Bacteriophage genome sizes

_What even is a "big" phage? Or a "small" one?_ I wanted a figure to discuss this very question in a talk, but I couldn’t find a plot I actually liked. The closest thing was [this](https://cdn.ncbi.nlm.nih.gov/pmc/blobs/41af/3820453/6e59e77cc92a/SCIENTIFICA2012-734023.002.jpg) figure from [Hyman and Abedon (2012)](https://pmc.ncbi.nlm.nih.gov/articles/PMC3820453/), which is helpful, but over a decade old, the y-axis labels are mysteriously missing (?), and more importantly, there’s been a major [taxonomic overhaul](https://pmc.ncbi.nlm.nih.gov/articles/PMC9868039/) since then. So, I figured it was time for a much-needed update.

[2025-08-22] EDIT: I actually just came across [this one](https://www.nature.com/articles/s41579-019-0311-5/figures/2) too.

If you use these figures or code, please cite it like:
> Quinones-Olvera, N. Bacteriophage genome sizes https://github.com/nataquinones/phage_genome_size/

### Phage genome size distribution by family
(Get this plot as a [png](https://github.com/nataquinones/phage_genome_size/blob/master/data/pngs/2025.png?raw=true))
<!-- <iframe id="phage-frame" src="../assets/figs/phage_sizes_all.html" width="100%" height="900" scrolling="yes" frameborder="0"></iframe> -->
<iframe id="phage-frame" src="../assets/figs/2025.html" width="100%" height="650" scrolling="yes" frameborder="0"></iframe>

I did minimal data curation, so there are likely to be errors and odd outliers, but overall the numbers should be reasonable. If you spot any major issues in the code or visualization, please let me know.

### A (now outdated) update of the 2012 plot
Right before the taxonomic change, I made this version, with the same families and color scheemes as the Hyman and Abedon 2012 plot:

(Get this plot as a [png](https://github.com/nataquinones/phage_genome_size/blob/master/data/pngs/phage_sizes_selection.png?raw=true))


<iframe id="phage-frame" src="../assets/figs/2022.html" width="100%" height="600" scrolling="no" frameborder="0"></iframe>

## Data source and code
You can find everything about the source data and the code that produced this plot in my GitHub: [nataquinones/phage_genome_size](https://github.com/nataquinones/phage_genome_size)
