# Wright Fisher Simulator
## About
<a href="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/main/WrightFisher.ipynb">This Jupyter notebook</a> contains a simulator for the classic and modified versions of Wright-Fisher model of genetic drift. The standard Wright-Fisher model simulates a haploid, asexual, panmictic population of size N over t generations for a single loci with two alleles a and A. The modified simulator models a diploid population with both sexual and asexual reproduction featuring two alleles in linkage disequilibrium.

<div align="center">
  <img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Population-Diagrams.png" width=800>
</div>

## Single Site Simulation
For the haploid model, the effects of introducing positive or negative selection were investigated with the model demonstrating higher average fixation towards alleles with a positive fitness advantage.

## Linked Loci Simulation
For the diploid model, three common linkage disequilibrium metrics ($D$, $D'$ and $r^{2}$) were evaluated, with $D$ and $r^{2}$ shown to be highly dependent on the haplotype frequencies in the initial population, and $D'$ found to be consistently initialised at 1. Furthermore, the effects of recombination rate and selection on LD were tested with the simulation demonstrating that LD can be broken down faster with higher recombination and negative selection.
