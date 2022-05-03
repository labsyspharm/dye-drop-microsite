---
layout: page
title: Overview
nav_order: 2
has_children: true
---

# Overview

The “Dye Drop” and “Deep Dye Drop” assays [(Mills et al., 2021)](https://doi.org/10.1101/2021.08.27.457854){:target="_blank"} are minimally disruptive, customizable assays that use sequential density displacement to collect multiplexed data at low-cost with high reproducibility.

*Dye drop consists of:*  

[1. Wet-lab experiment](/protocol.html){: .btn .btn-outline .btn-arrow } [2. Imaging samples](./#resulting-images){: .btn .btn-green .btn-arrow } [3. Extracting image data](./#extracting-cell-cycle-information){: .btn .btn-outline .btn-arrow }

<br>

*We describe several different ways to implement Dye Drop assays to obtain detailed cell cycle information and to quantify single-cell phenotypes that are often obscured by population-average assays.*

{: .text-center}
[View example data](./#applying-dye-drop){: .btn .btn-green}  

<br>

## Experimental Methods
### Dye Drop
Dye drop uses a sequence of solutions where each solution is made slightly denser than the last by addition of iodixanol (OptiPrep<sup>TM</sup>), an inert liquid used in radiology. The denser solutions flow to the bottom of the well, displacing the previous solution with high efficiency and minimal mixing. This eliminates the need for mix and wash steps, where most of the experimental variability and uneven cell loss occurs.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Dye drop experiment overview]({{ site.baseurl }}/assets/images/figures/1-exp.png)
For example, cells can be plated into a 384-well plate, then a cell cycle dye (mixed with OptiPrep<sup>TM</sup>) can be added to each well and stains the target cells. The experiment is eventually halted by adding an even more dense fixing solution (such as paraformaldehyde + OptiPrep<sup>TM</sup>) to the wells. From here, the contents of the well can be aspirated and rinsed as normal.

### Deep dye drop

Deep Dye Drop incorporates antibody-based staining to gain even more valuable information about cell behavior.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Deep dye drop experiment overview]({{ site.baseurl }}/assets/images/figures/2-exp.png)
The cells are cultured, stained, and fixed with a method identical to the dye drop protocol above. In this example, Edu is used as a cell cycle dye. EdU is incorporated into newly synthesized DNA during chromosome replication and must be activated after fixing in order to visualize the stain. Afterwards the wells are rinsed, blocked to prevent non-specific antibody binding, and incubated with antibodies that specifically bind a molecule or protein within the sample.

{: .text-center }
{: .fw-500 }
{: .fs-5}
*A detailed protocol for both Dye Drop and Deep Dye Drop is available in [Experimental Method]({{site.baseurl}}/protocol.html).*

<br>

## Resulting Images

The stained cells are then imaged on a fluorescent microscope. 


![example fluorescence image]({{ site.baseurl }}/assets/images/figures/3-images.png)

This sample was stained with 4 common markers:

{: .fs-3 }
{: .fw-300 }
>1. Hoechst, a molecule that specifically binds the minor groove of double stranded DNA and can be used to visualize DNA content within a nucleus
>2. EdU, a molecule that is incorporated into newly synthesized DNA and indicates cells in the S-phase
>3. Live/dead red, a stain that binds free amines (The dye can bind free-amines on the surface of both live and dead cells, but in dead cells, the dye penetrates the disrupted cell membrane and binds intracellular amines, resulting in a much brighter signal.)
>4. pH3 (phospho-histone H3), a protein that is phosphorylated during the chromosomal condensation of M-phase

{: .text-center}
{: .fs-5}
*Deep dye drop can also be combined with multiplexed imaging methods like [CyCIF](https://www.cycif.org/){:target="_blank"} to yield detailed molecular and spatial information.*

<br>

## Extracting cell cycle information

### Live / Dead cells  
Using Hoechst and the live/dead stain, cells that have low Hoechst signal and high live/dead signal are quantified as dead cells.

### M-Phase
Cells that are stained with pH3 are counted as cells within M-phase and actively undergoing mitosis.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Image depicting the gating that classifies cells as alive/dead or as M-phase]({{ site.baseurl }}/assets/images/figures/4-comp.png)
Example of how cells are classified as being alive/dead (left) or in M-phase (right).


### S-Phase
Cells in S-phase are stained brightly with EdU.

### G1/G2
By plotting Edu intensity versus DNA content (Hoechst intensity), the cells can further be classified into the G1 or G2 phases. Cells that are negative for EdU can be classified as G1 or G2 based on the quantity of DNA within the cells, where less DNA indicates G1 and duplicated DNA content indicates G2 phase, and DNA content in intermediate ranges indicates cells entering or leaving these stages.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Image depicting the gating that classifies cells as G1, G2, or S-phase]({{ site.baseurl }}/assets/images/figures/5-comp.png)
Example of how cells are classified into G1-, G2-, or S-phases.

{: .text-center}
{: .fs-5}
*More detailed about the computational methods used to classify cells into the cell cycle phases can be found in [Computational Method]({{site.baseurl}}/overview/dye-drop/ddd-comp.html).*

### Growth Rate Metrics

Dye Drop methods are an ideal complement to the growth-rate (GR) inhibition method of computing dose responses and when combined, greatly improve the depth and accuracy of data while only slightly increasing cost. 

Cell viability data obtained from Dye Drop can be fed into the [GR calculator](http://www.grcalculator.org/) to determine the GR value for a given treatment compared to an untreated control. 

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![The GR value relates naturally to a treatment's effects on cell population growth. For partially cytostatic treatments (where growth is slowed, but not completely halted) GR values fall between 1 and 0. A GR value of zero represents cytostasis, or completely halted population growth. Cytotoxic treatments (where cell population declines) produce GR values between 0 and -1. Finally, a GR value of greater than one signifies a treatment that promotes growth.]({{ site.baseurl }}/assets/images/figures/6-gr.png)
Graph depicting how growth rate values correspond to cell growth metrics.

{: .text-center}
{: .fs-5}
*More detailed about the computational methods used to calculate these values can be found in [GR Metrics]({{site.baseurl}}/overview/gr_metrics/).*

<br>

## Applying Dye Drop

{: .text-center}
{: .fs-5}
This example is part of a large-scale dataset generated by using Dye Drop on a panel of breast cancer cells and a kinase inhibitor library - **read more in [(Mills et al., 2021)](https://doi.org/10.1101/2021.08.27.457854){:target="_blank"}.**

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Image depicting example application of dye drop for cancer]({{ site.baseurl }}/assets/images/figures/7-examp.png)
In this example, Dye Drop methods tracked the response of breast cancer cell lines to drug Palbociclib at a range of concentrations over 3 days. For each concentration and timepoint, the EdU intensity versus DNA content plots can be generated – each plot indicates the percentage of cells in S-phase at this timepoint (upper panels). In addition, antibody staining of the sample revealed changes in cell morphology (indicated by actin staining) after drug treatment (lower panels).

<br>




