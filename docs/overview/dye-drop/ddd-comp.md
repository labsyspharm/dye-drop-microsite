---
layout: default
nav_order: 3
title: Computational method
parent: Overview
---

Dye Drop Computational Protocol 
{: .fs-8}
{: .fw-400}
{: .text-blue-200}

{: .fs-5}
{: .fw-500}
{: .text-green-200}
Automated gating of single cell Deep Dye Drop data

Dye drop analyzes single-cell feature data automatically with custom scripts. Cell cycle states, such as cell death, G1, G2, S, and M-phase, are determined based on LDR, DNA content, EdU, and pH3 levels using the heuristics described below.

<br>

{: .fs-5}
{: .fw-500}
{: .text-blue-100}
1.)	Classification of dead versus live cells based on LDR signal intensity

* LDR intensity values were log transformed [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L54){:target="_blank"}
* A kernel density estimate smoothing function was applied to the log transformed data (`seabon.kdeplot`)[[code]](https://github.com/datarail/DrugResponse/blob/master/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L40){:target="_blank"}
* Using the additive inverse of the smoothened data, the peak of the signal was identified. (`scipy.signal.find_peaks`). The corresponding location of the peak on the x-axis corresponds to the LDR intensity cutoff above which cells were considered LDR positive. [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L42){:target="_blank"}
* Based on empirical data, any peaks at log<sub>10</sub>LDR < 1.2 were excluded as erroneous peak detections [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L45){:target="_blank"}

{: .text-center}
<img src="{{ site.baseurl }}/assets/images/dye_drop/ddd_overview_1.png" style="width:70%;margin:20px 20px">
<br>

{: .fs-5}
{: .fw-500}
{: .text-blue-100}
2.)	Classification of cells with normal DNA content

* DNA content values were log transformed [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L54){:target="_blank"}
* Cells identified as LDR positive in step 1 were excluded (dead cells)  and a kernel density smoothing function was applied to log-transformed data.[[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L255){:target="_blank"}
* A peak finding algorithm was applied to identify all peaks that had a minimal amplitude/height of greater than 10% of maximum 
* If only 2 peaks were detected, the minimum of their corresponding x-axis locations (i.e. DNA content) was defined as the approximate G1 peak location. The maximum was defined as the G2 peak location. [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L82){:target="_blank"}
* If more than 2 peaks were identified, the peak with the most surrounding DNA density was chosen as the G1 peak location (G1<sub>loc</sub>).
* To find the location of the G2 peak, the cells with DNA content <= G1 peak location were excluded and the remaining signal was used to identify the local maxima as corresponding to the G1 peak (G2<sub>loc</sub>)[[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L126){:target="_blank"}
* Based on empirical assessment, the inner and outer boundaries or gates (dg<sub>1</sub> to dg<sub>4</sub>) were applied [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L264){:target="_blank"} as follows:
<p style="margin-left: 200px">
dg<sub>1</sub> = G1<sub>loc</sub> – 1.5 * (G1<sub>loc</sub>  – G2<sub>loc</sub>) <br>
dg<sub>2</sub> = G1<sub>loc</sub>  – 0.9 * (G1<sub>loc</sub>  – G2<sub>loc</sub> ) <br>
dg<sub>3</sub> = G2<sub>loc</sub>  + 1.3 * (G1<sub>loc</sub>  – G2<sub>loc</sub> ) <br>
dg<sub>4</sub> = G2<sub>loc</sub>  + 2.2 * (G1<sub>loc</sub>  – G2<sub>loc</sub>) <br></p>

* Cells within the inner gates (dg<sub>2</sub> < DNA content < dg<sub>3</sub>) were defined as having normal DNA content. Cells with DNA content between inner and outer left gate are subG1 (dg<sub>1</sub> < DNA content < dg<sub>2</sub>) , cells with DNA content beyond inner right are defined as beyond G2 (DNA content > dg<sub>3</sub>). Cells with LDR positive status or with DNA content below inner left gate (DNA content < dg<sub>1</sub>) are defined as dead cells [[code]](https://github.com/datarail/DrugResponse/blob/399c25da761196cf6cc435c1aeaeeb74d917d2d1/python/cell_cycle_gating/dead_cell_filter_ldrint.py#L280){:target="_blank"}
<br>

{: .fs-5}
{: .fw-500}
{: .text-blue-100}
3.)	Classification of cells with high EdU as S-phase cells [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L24){:target="_blank"}

* EdU intensity values were log transformed
* A kernel density estimate smoothing function was applied to the log transformed data (`seabon.kdeplot`).
* Using the additive inverse of the smoothened data, the peak of the signal was identified. (`scipy.signal.find_peaks`). The corresponding location of the peak on the x-axis corresponded to the LDR intensity cutoff above which cells were considered EdU high positive. 

{: .fs-5}
{: .fw-500}
{: .text-blue-100}
4.) Using DNA content and EDU signal to identify location of G1, G2 and S phase peak

* EdU intensity values an DNA content were log-transformed
* A 2D histogram EdU and DNA content was computed. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L366){:target="_blank"}
* MATLAB’s `imregional` function was used to identify regional maximas on the 2D plate [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L348){:target="_blank"}
* The regional maximas were used to define a set of candidate peaks for G1, S, and G2 phases. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L473){:target="_blank"}
* Using the individual signal intensity values from EdU and DNA content, the position of G1, S, and G2 peaks were identified using scipy’s peak detection algorithm on the smoothed log values. In the event of multiple peaks identified, the peak which overlapped with the candidate peaks identified in step 4d was selected as the most likely position of the G1, S and G2 foci. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L561){:target="_blank"}

{: .text-center}
<img src="{{ site.baseurl }}/assets/images/dye_drop/ddd_overview_2.png" style="width:60%;margin:20px 20px">
<br>

{: .fs-5}
{: .fw-500}
{: .text-blue-100}
5.)	Classification of cells in G1, G2, and S phase

* Cells with EdU content above EdU cutoff were categorized as being in the S-phase
* The remaining cells were carried forward for further classification in G1/G2 phase
* A normal distribution was fit to all cells within the local neighborhood of G1 location identified in Step 4. The boundary between G1 and G2 cells (or S-phase dropout) was defined as X-axis point which lies at the 99% significance interval of the standard distribution. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L973){:target="_blank"}
* Similarly, a normal distribution was fit to all cells within the local neighborhood of G2 location (identified in Step 4). The boundary between G2 and G1 cells (or S-phase dropout) was defined as the X-axis point point which lies at the 1% significance interval of the standard normal distribution.[[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L986){:target="_blank"}
* Cells whose DNA content fell between the boundaries defined in step 5c & d  (if any) were identified as `S-phase dropout` cells. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/cellcycle_phases.py#L1060){:target="_blank"}
<br>

{: .fs-5}
{: .fw-500}
{: .text-blue-100}
6.)	Classification of cells with high pH3 as M-phase cells

* pH3 intensity values were log transformed for all cells evaluated as alive in Step 3h.
* A kernel density estimate smoothing function was applied to the log transformed data. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/ph3_filter.py#L46){:target="_blank"}
* Using the additive inverse of the smoothened data, the peak of the signal was identified. (`scipy.signal.find_peaks`). The corresponding location of the peak on the x-axis corresponded to the pH3 intensity cutoff above which cells were considered pH3 high positive. 
* Cells were reclassified as M-phase cells if they passed the criterion in Step 6c. If not, they retained their classification as evaluated in Step 5d-e. [[code]](https://github.com/datarail/DrugResponse/blob/da03b5e14f25021e250ea462d1cd98a9a609911f/python/cell_cycle_gating/ph3_filter.py#L121){:target="_blank"}

{: .text-center}
<img src="{{ site.baseurl }}/assets/images/dye_drop/ddd_overview_3.png" style="width:50%;margin:20px 20px">
<br>