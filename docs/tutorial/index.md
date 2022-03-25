---
layout: default
nav_order: 2
title: Tutorial
has_children: true
---

# Quick start

1. Install the package from the [github repository](https://github.com/datarail/DrugResponse) as explained in the [Installation](/dye_drop/Installation.html) page
2. cd into the example folder: `cd DrugResponse/python/cell_cycle_gating/examples/`
3. Open the jupyter notebook `DDR_example.ipynb` on your machine and execute the steps in the notebook. 
    - Alternatively, you can use your preffered python environment i.e sypder or ipython and follow the steps shown in the example page.
4. The code takes roughly 2-4 minutes to run. Two output files will be generated upon successful completion of your run:
     - `EX_01[78956].csv` - A table containing rows corresponding to wells in the 96 well plate. Each well (row) will contain well-level summary of the number of live/dead cells and fraction of cells in each phase of the cell cycle.
     - `EX_01[78956].pdf` - The script saves a pdf showing multiple figures; one for each well. Each figure shows the gating on each DNA v EDU scatter plot for review.
    
<!--
 Table of contents
 
 1. Computation pipeline overview
 2. Install
 3. Parameter specifications
 4. Running the pipeline. An Example
-->
 
