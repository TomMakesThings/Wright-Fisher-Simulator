<div align="center">
  <h1><b>Haploid and Diploid Wright-Fisher Simulator</b></h1>
  <img src="https://images.weserv.nl/?url=avatars.githubusercontent.com/u/61354833?v=4&h=100&w=100&fit=cover&mask=circle&maxage=7d">
  <p><b>🟢🟢🟢 Code by <a href="https://github.com/TomMakesThings">TomMakesThings</a> 🟢🟢🟢</b></p>
  <p><b><sub>April 2022</sub></b></p>
</div>

---

# About
This repository contains a simulator, implemented in a <a href="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/main/WrightFisher.ipynb">Jupyter notebook</a>, to test the effects of selection, recombination and linkage disequilibrium on haploid and diploid versions of the Wright-Fisher model of genetic drift ([Figure A](#figureA)). For the haploid model, the simulator demonstrates that speed and rate of fixation of an allele in a population can be increased through positive selection. For the diploid model, the simulator demonstrates how LD can be broken down faster with higher recombination and negative selection.

## Wright-Fisher Model Types

<a name="figureA"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Population-Diagrams.png" width=800>

<sub>Figure (A) Diagram demonstrating allele genetic drift over time for the standard Wright-Fisher model (left) and the modified two loci model (right).</sub>

### Haploid Wright-Fisher
The classic Wright-Fisher model simulates a haploid, asexual, panmictic population of size $N$ over $t$ generations for a single loci with two alleles $a$ and $A$.

<ol>
  <li>A population is initialised with an $a$ allele count of $n$.</li>
  <li>For each preceding generation, the number of alleles $n'$ is sampled independently with replacement from a binomial distribution. Selection can be introduced via
  the selection coefficient $s \neq 0$. As alleles $a$ and $A$ have relative fitness $w_{a} = 1 + s$ and $w_{A} = 1$, an $s > 0$ gives allele $a$ a fitness advantage,
  while $s < 0$ means the allele is deleterious and less likely to be passed to the next generation.</li>
  <li>Drift is modelled as a stochastic process in which the variant allele can be lost if its frequency in a generation reaches zero, fixed if its frequency reaches $N$ or fluctuating for any other $n$. If either extreme is encountered, the simulator will end prematurely as only one allele remains.</li>
</ol>


$n' \sim binomial(\frac{n(1 + s)}{n(1 + s) + N - n}, N)$

### Diploid Wright-Fisher with Recombination
A variant of the Wright-Fisher model was created to model genetic drift between two linked loci $A$ and $B$ under both sexual and asexual reproduction. This simulator models a diploid population featuring two alleles in linkage disequilibrium (LD) with partial recombination.

<ol>
  <li>The number of individuals with the $A$ allele is initialised through randomly sampling a distribution $S(n)$, while the rest of the population is set to have the
  $a$ allele.
  <li>Then a singleton variant allele is introduced at random at site $B$ which can occur on either a chromosome with the $A$ allele or the $a$ allele. This is 
  equivalent to introducing a new mutation at $B$.</li>
  <li>For each generation, a new population is filled through selecting haplotypes from the previous generation with probability $1 - r$, and creating recombinant
  haplotypes with probability $r$. In the case of recombination, two alleles are selected at random with probability proportional to the allele frequencies of the
  previous generation. All generations are kept at a constant size $N$ and the simulator iterates until an allele at one loci become fixed.</li>
</ol>

## Linkage Disequilibrium
Linkage disequilibrium (LD) is the non-random association of alleles at different loci. One method to quantify LD between two alleles $A$ and $B$ at different loci is the coefficient of linkage disequilibrium $D$. This is the difference between the frequency of a haplotype for a pair of alleles $A$ and $B$, $p_{AB}$, and the product of the allele frequencies $p_{A} p_{B}$.

$D_{AB} = p_{AB} - p_{A} p_{B}$

The range of potential values for $D_{AB}$ relies on allele frequencies $A$ and $B$, and so it is difficult to compare the level of LD between other pairs of alleles. Therefore it can be normalised to range between -1 to 1, denoted $D'$, by dividing by the maximum difference $D_{max}$ between the observed and expected haplotype frequencies.

$D' = \frac{D}{D_{max}}$

$\text{if D < 0, } D_{max} = max\{p_{A}p_{B}, (1 - p_{A})(1 - p_{B})\}$

$\text{else } D_{max} = min\{p_{A}(1 - p_{A}), (1 - p_{A})p_{B}\}$

Another normalised measure of LD is the genetic correlation $r^{2}$ between pairs of loci. This metric has ranges between 0 and 1.

$r^{2} = \frac{D^{2}}{p_{A}(1 - p_{A}) p_{B}(1 - p_{B})}$

<a name="results"></a>
# Results
## Haploid Wright-Fisher
For the single loci model, the effects of introducing positive/negative selection on genetic drift of an allele with initial frequency $n = 1$ were investigated by running the simulator for 1,000 iterations with selection coefficient $s = 0.02$, $s = 0.005$, $s = 0$, $s = -0.005$ and $s = -0.02$. The number of times the allele fixed or was lost was recorded in [Table A](#tableA), with results showing that higher than average occurrences of fixation occur with positive selection coefficients. This is to be expected as these correspond to situations in which the allele is beneficial and thus confers a positive fitness advantage. By contrast for negative selection coefficients, fixation rate is lower as the allele is deleterious. When comparing fixation and loss times, fixation on average occurs faster for a higher positive $s$, while loss is slightly quicker for a lower negative $s$.

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

## Diploid Wright-Fisher with Recombination
### Comparing LD at Initialisation
For the linked loci model, the initial values for three common linkage disequilibrium metrics $D$, $D'$ and $r^{2}$ were evaluated by repeatedly generating an initial population via random sampling 1,000 times. The haplotype frequencies for the first five runs are recorded in [Table B](#tableB), while the distribution of $r^{2}_{1}$ is plotted in [Figure B](#figureB). This demonstrates that $D$ and $r^{2}$ are highly dependent on the haplotype frequencies in the initial population as these measures are calculated based on the frequency of the background allele $A$. Only $D'$ is consistently initialised as 1 suggesting the population is in complete LD. 

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

### Testing Recombination Rates and Selection
#### Recombination
For each generation in the diploid simulator, recombinant haplotypes are created between two loci with probability $r$. To test the effects of recombination rate on LD, an initial population was randomly generated giving haplotypes frequencies: $\{AB: 1, Ab: 10, aB: 0, ab: 89\}$. In this case, the singleton $B$ allele occurred on a chromosome with the $A$ allele, and so the haplotype $aB$ initially has frequency zero. These initial haplotype frequencies were consistently used to seed the experiments so that results of changing parameters were comparable and averages could be calculated. 

The simulator was run 1,000 times for $r = 0.05$, $r = 0.01$ and $r = 0.02$ and the LD measures over time plotted in [Figure C](#figureC).  Here the results for each simulation per time point, as well as the average over time are depicted. The average across all simulations demonstrate that for higher $r$, fewer generations are required to break down LD. In real populations, higher recombination rate is expected when two loci are further apart. Therefore this simulation implies that a greater distance between loci would speed up LD decay.

<a name="figureC"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Diploid-LD-1000.png" width=700>

<sub>Figure (C) Three measures of linkage disequilibrium for different recombination rates. On the left $D$, $D'$ and $r^{2}$ measured per generation are plotted for each simulation, while on the right each LD measured was averaged over all 1,000 simulations.</sub>

#### Selection
The distribution of average allele frequency after a fixation event occurred for different $s$ is plotted in [Figure D](#figureD). As expected with positive selection towards allele $A$, both its frequency and the frequency of the linked allele $B$ in the final generation is higher than chance. $A$ therefore acts as a driver mutation. Even though the linked allele has no effect on a chromosome's fitness, with a low recombination rate it often hitchhikes when $A$ increases in frequency. This has the effect of increasing LD.

When negative selection is stronger, the $B$ allele frequency is higher than for a weaker negative selection. This can be explained by the occurrence of recombination events forming the haplotype $ab$. As selection is very strong against $AB$ and $Ab$, their frequencies are reduced which has the effect of increasing haplotypes $aB$ and $ab$. The beneficial effect of recombination therefore increases population diversity which explains the reduction of LD with negative selection on allele $A$.

<a name="figureD"></a>
<img src="https://github.com/TomMakesThings/Wright-Fisher-Simulator/blob/assets/Images/Diploid-Selection.png" width=500>

<sub>Figure (D) Bar chart of allele frequency in final generation averaged across 1,000 simulation for different selection coefficients.</sub>
