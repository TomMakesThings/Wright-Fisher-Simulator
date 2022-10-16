<div align="center">
  <h1><b>Wright-Fisher Simulator</b></h1>
  <img src="https://images.weserv.nl/?url=avatars.githubusercontent.com/u/61354833?v=4&h=100&w=100&fit=cover&mask=circle&maxage=7d">
  <p><b>🟢🟢🟢 Code by <a href="https://github.com/TomMakesThings">TomMakesThings</a> 🟢🟢🟢</b></p>
  <p><b><sub>April 2022</sub></b></p>
</div>

---

## About
<a href="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/main/WrightFisher.ipynb">This Jupyter notebook</a> contains a simulator used to experiment with the classic and modified versions of Wright-Fisher model of genetic drift (see [Results](#results)). The standard Wright-Fisher model simulates a haploid, asexual, panmictic population of size $N$ over $t$ generations for a single loci with two alleles $a$ and $A$. The modified simulator models a diploid population featuring two alleles in linkage disequilibrium and partial recombination ([Figure A](#figureA)).

<a name="figureA"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Population-Diagrams.png" width=800>

<sub>Figure (A) Diagram demonstrating allele genetic drift over time for the standard Wright-Fisher model (left) and the modified two loci model (right).</sub>

<a name="results"></a>
## Results
### Single Site Simulation
For the haploid model, the effects of introducing positive or negative selection on the genetic drift of an allele with an initial frequency of $n = 1$ were investigated by running the simulator for 1,000 iterations with selection coefficient $s = 0.02$, $s = 0.005$, $s = 0$, $s = -0.005$ and $s = -0.02$. The number of times the allele fixed or was lost was recorded in [Table A](#tableA) with the results showing that higher than average occurrences of fixation occur with positive selection coefficients. This is to be expected as these correspond to situations in which the allele is beneficial and thus confers a positive fitness advantage. By contrast for negative selection coefficients, the fixation rate is lower as the allele is deleterious. When comparing fixation and loss times, fixation on average occurs faster for a higher positive $s$, while loss is slightly quicker for a lower negative $s$.

<a name="tableA"></a>
<table>
  <tr>
    <th>Selection Coefficient (s)</th>
    <th>Selection Effect</th>
    <th>Number Fixed </th>
    <th>Number Lost</th>
    <th>Mean Fixation Time</th>
    <th>Mean Loss Time</th>
  </tr>
  <tr>
    <th>0.02</th>
    <th>Strongly beneficial</th>
    <th>40</th>
    <th>960</th>
    <th>171.475</th>
    <th>7.554</th>
  </tr>
  <tr>
    <th>0.005</th>
    <th>Weakly beneficial</th>
    <th>29</th>
    <th>970</th>
    <th>198.931</th>
    <th>8.737</th>
  </tr>
  <tr>
    <th>0</th>
    <th>Alleles have equal fitness</th>
    <th>12</th>
    <th>988</th>
    <th>171.0</th>
    <th>8.694</th>
  </tr>
  <tr>
    <th>-0.005</th>
    <th>Weakly deleterious</th>
    <th>7</th>
    <th>993</th>
    <th>194.143</th>
    <th>9.986</th>
  </tr>
  <tr>
    <th>-0.02</th>
    <th>Strongly deleterious</th>
    <th>1</th>
    <th>999</th>
    <th>114.0</th>
    <th>8.269</th>
  </tr>
</table>
<sub>Table (A) Summary statistics of the classic Wright-Fisher model with and without selection for 1,000 simulations and population size N = 100. Each time the population is initialised with a singleton allele, n = 1.</sub>

### Linked Loci Simulation
#### Comparing LD at Initialisation
For the diploid model, the initial values for three common linkage disequilibrium metrics $D$, $D'$ and $r^{2}$ were evaluated by repeatedly generating an initial population via random sampling 1,000 times. The haplotype frequencies for the first five runs are recorded in [Table B](#tableB), while the distribution of $r^{2}_{1}$ is plotted in [Figure B](#figureB). This demonstrates that $D$ and $r^{2}$ are highly dependent on the haplotype frequencies in the initial population as these measures are calculated based on the frequency of the background allele $A$. Only $D'$ is consistently initialised as 1 suggesting the population is in complete LD. 

<a name="tableB"></a>
<table>
  <tr>
    <th>Run ID</th>
    <th>Singleton Haplotype</th>
    <th>AB</th>
    <th>Ab</th>
    <th>aB</th>
    <th>ab</th>
    <th>$D_{1}$</th>
    <th>$D'_{1}$</th>
    <th>$r^{2}_{1}$</th>
  </tr>
  <tr>
    <th>1</th>
    <th>Ab</th>
    <th>4</th>
    <th>1</th>
    <th>95</th>
    <th>0</th>
    <th>0.0095</th>
    <th>1</th>
    <th>0.1919</th>
  </tr>
  <tr>
    <th>2</th>
    <th>ab</th>
    <th>27</th>
    <th>0</th>
    <th>72</th>
    <th>1</th>
    <th>0.0027</th>
    <th>1</th>
    <th>0.0037</th>
  </tr>
  <tr>
    <th>3</th>
    <th>AB</th>
    <th>1</th>
    <th>1</th>
    <th>0</th>
    <th>98</th>
    <th>0.0098</th>
    <th>1</th>
    <th>0.4949</th>
  </tr>
  <tr>
    <th>4</th>
    <th>aB</th>
    <th>0</th>
    <th>3</th>
    <th>1</th>
    <th>96</th>
    <th>0.0003</th>
    <th>1</th>
    <th>0.0003</th>
  </tr>
  <tr>
    <th>5</th>
    <th>Ab</th>
    <th>22</th>
    <th>1</th>
    <th>77</th>
    <th>0</th>
    <th>0.0077</th>
    <th>1</th>
    <th>0.0338</th>
</table>

<sub>Table (B) Measuring linkage disequilibrium for the initial population across 5 runs.</sub>

<a name="figureB"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Initial-r2.png" width=400>

<sub>Figure (B) Initial distribution of $r^{2}$ for 1000 two-loci Wright-Fisher simulations without selection.</sub>

#### Testing Recombination Rates and Selection
For each generation in the diploid simulator, recombinant haplotypes are created between two loci with probability $r$. To test the effects of recombination rate on LD, an initial population was randomly generated giving haplotypes frequencies: $\{AB: 1, Ab: 10, aB: 0, ab: 89\}$. In this case, the singleton $B$ allele occurred on a chromosome with the $A$ allele, and so the haplotype $aB$ initially has frequency zero. These initial haplotype frequencies were consistently used to seed the experiments so that results of changing parameters were comparable and averages could be calculated. The simulator was the run 1,000 times for $r = 0.05$, $r = 0.01$ and $r = 0.02$. In real populations, higher recombination rate is expected when two loci are further apart and so this can be used to model the effect of distance between loci on LD and haplotype frequencies.

The LD measures over time were plotted in [Figure C](#figureC),  where the results for each simulation per time point, as well as the average over time are depicted. The average across all simulations suggests that linkage equilibrium is reached after fewer generations when $r$ is increased. This trend is apparent across all three measures with their values reducing the fastest for $r = 0.05$. Unsurprisingly, the LD measurements for $r = 0.01$ and $r = 0.02$ are more similar to one another as their recombination rates are more alike.


were tested with the simulation demonstrating that LD can be broken down faster with higher recombination and negative selection.

<a name="figureC"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Diploid-LD-1000.png" width=700>

<sub>Figure (C) Three measures of linkage disequilibrium for different recombination rates. On the left $D$, $D'$ and $r^{2}$ measured per generation are plotted for each simulation, while on the right each LD measured was averaged over all 1,000 simulations.</sub>

<a name="figureD"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Diploid-Selection.png" width=500>

<sub>Figure (D) Bar chart of allele frequency in final generation averaged across 1,000 simulation for different selection coefficients.</sub>
