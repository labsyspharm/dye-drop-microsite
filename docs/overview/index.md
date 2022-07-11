---
layout: page
title: Overview
nav_order: 2
has_children: true
---

# Overview

The “Dye Drop” and “Deep Dye Drop” assays [(Mills et al., 2021)](https://doi.org/10.1101/2021.08.27.457854){:target="_blank"} are minimally disruptive, customizable assays that use sequential density displacement to collect multiplexed data at low-cost with high reproducibility.

*Dye drop consists of:*  

[1. Wet-lab experiment](/protocol.html){: .btn .btn-outline } [2. Imaging samples](./#resulting-images){: .btn .btn-green } [3. Extracting image data](./#extracting-cell-cycle-information){: .btn .btn-outline }

<br>

*We describe several different ways to implement Dye Drop assays to obtain detailed cell viability and cell cycle phenotypes that are often obscured by population-average assays.*

{: .text-center}
[View example data](./#applying-dye-drop){: .btn .btn-green}  

<br>

## Experimental Methods
### Dye Drop
Dye drop uses a sequence of solutions where each solution is made slightly denser than the last by addition of iodixanol (OptiPrep<sup>TM</sup>), an inert liquid used in radiology. The denser solutions flow to the bottom of the well, displacing the previous solution with high efficiency and minimal mixing. This eliminates the need for pre-fixation mix and wash steps, where most of the experimental variability and uneven cell loss occurs.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Dye Drop protocol overview]({{ site.baseurl }}/assets/images/figures/1-exp.png)
Cells plated in 384-well plates (a single well is depicted) are exposed to different perturbagens for a set amount of time and then stained with Hoechst (to label all nuclei) and a LIVE/DEAD dye (to label dead cells) prepared in solution with OptiPrep<sup>TM</sup>. Cells are then fixed by layering in a denser solution containing formaldehyde and more OptiPrep<sup>TM</sup> to the wells. 

### Deep dye drop

Deep Dye Drop incorporates EdU and antibody-based staining to gain detailed cell cycle data.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Deep Dye Drop protocol overview]({{ site.baseurl }}/assets/images/figures/2-exp.png)
Cells are plated and treated as above, they are then incubated with a LIVE/DEAD dye and EdU (incorporated into newly synthesized DNA by cells in S-phase) prepared in solution with OptiPrep<sup>TM</sup>, and fixed as above. Cells are then permeabilized to facilitate antibody staining, blocked to prevent non-specific antibody binding, EdU is labeled with a fluorescent dye, cells are stained with a phospho-histone H3 antibody (to identify M-phase cells) and Hoechst (to label all nuclei and measure DNA content) overnight.

{: .text-center }
{: .fw-500 }
{: .fs-5}
*See the [Experimental Protocol]({{site.baseurl}}/protocol.html) section for more details.*

<br>

## Resulting Images

The stained cells are then imaged on a fluorescent microscope. 


![example fluorescence image]({{ site.baseurl }}/assets/images/figures/3-images-cm.png)

This sample was stained with 4 common markers:

{: .fs-3 }
{: .fw-300 }
>1. Hoechst, a molecule that binds the minor groove of double stranded DNA is used to visualize nuclei and measure DNA content
>2. EdU, a molecule that is incorporated into newly synthesized DNA while cells are in S-phase
>3. LIVE/DEAD red (LDR), a stain that penetrates the disrupted cell membrane and binds intracellular amines in dead cells
>4. pH3 (phospho-histone H3), a protein that is phosphorylated during the chromosomal condensation of M-phase

{: .text-center}
{: .fs-5}
*Deep dye drop can also be combined with multiplexed imaging methods like [CyCIF](https://www.cycif.org/){:target="_blank"} to yield detailed molecular and spatial information.*

<br>

## Extracting cell cycle information

### Live / Dead cells  
Using Hoechst and LDR, cells that have high LDR signal and/or low DNA content are counted as dead cells.

### M-Phase
Cells that have high pH3 signal are counted as M-phase cells.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Image depicting the gating that classifies cells as alive/dead or as M-phase]({{ site.baseurl }}/assets/images/figures/4-comp.png)
Examples of how cells are classified as live or dead (left) or in M-phase (right).


### S-Phase
Cells in S-phase have high EdU signal.

### G1/G2
EdU negative cells are classified as G1, G2 or S-phase dropout (S_dropout) based on their DNA content (integrated Hoechst intensity). G2 cells have duplicated DNA content relative to G1 cells, and cells with intermediate DNA content are classified as S_dropout.

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![Image depicting the gating that classifies cells as G1, G2, or S-phase]({{ site.baseurl }}/assets/images/figures/5-comp.png)
Example of how cells are classified into G1-, G2-, or S-phases.

{: .text-center}
{: .fs-5}
*See the [Computational Method]({{site.baseurl}}/overview/dye-drop/ddd-comp.html) section for more details.*

### Growth Rate Metrics

Dye Drop methods are an ideal complement to the growth-rate (GR) inhibition method of computing dose responses that allows for the comparison of drug effects across cell lines with varied doubling times. 

Cell viability data obtained from Dye Drop can be fed into the [GR calculator](http://www.grcalculator.org/) to determine the GR value for a given treatment compared to an untreated control. 

{: .text-center }
{: .fs-3 }
{: .fw-300 }
![The GR value relates naturally to a treatment's effects on cell population growth. For partially cytostatic treatments (where growth is slowed, but not completely halted) GR values fall between 1 and 0. A GR value of zero represents cytostasis, or completely halted population growth. Cytotoxic treatments (where cell population declines) produce GR values between 0 and -1. Finally, a GR value of greater than one signifies a treatment that promotes growth.]({{ site.baseurl }}/assets/images/figures/6-gr.png)
Graph depicting how growth rate values correspond to cell growth metrics.


### Growth Rate Metrics - Cytostatic and Cytotoxic Components

{: .text-center}
{: .fs-5}
*See [GR Metrics]({{site.baseurl}}/overview/gr_metrics/) for more details on calculating GR values and metrics.*

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




