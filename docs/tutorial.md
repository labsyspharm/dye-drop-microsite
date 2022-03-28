---
layout: default
title: Dye Drop tutorial
nav_order: 3
last_modified_date: 2022-03-28
---

# Dye Drop tutorial

## Installation
1. Open a terminal of your choice.
2. Clone the [github repository](https://github.com/datarail/DrugResponse)
  ```
  $ git clone https://github.com/datarail/DrugResponse.git
  ```
3. Install the dependencies:
  ```
  $ cd DrugResponse/python
  $ pip install -e .
  ```

## Cell-gating example

1. cd into the example folder: `cd DrugResponse/python/cell_cycle_gating/examples/`
  - The example directory (located in `DrugResponse/python/cell_cycle_gating/examples/`) contains a Raw data folder `EX_01[78956]`.
    - This folder contains 10 .txt files, each corresponding to single cell data from a given well (wells C3 to C12).
2. Type `python` to open a python terminal or open the Jupyter notebook `DDR_example.ipynb` and execute the steps in the notebook.
  - The code is reproduced below with a summary of each step.
  - The example script will: 1) read the contents of the folder, 2) perform automated gating, and 3) output a .csv file and .pdf file that contain well-level summaries of number of live/dead cells and fraction of cells in diferent phases of the cell cycle. In addition, a pdf file containing figures that show the gating per well is available for review.
  - This example dataset contains 10 wells and should run within a minute. An entire plate with ~300 wells is expected to run in 10-15 minutes.

## Running the example

1. Import required dependencies
  ```
  from cell_cycle_gating import run_cell_cycle_gating as rccg ## main cell-gating functions
  import pandas as pd     
  import warnings
  warnings.filterwarnings('ignore')
  ```
2. Import the metadata file that containg mapping between the well name and conditions (i.e cell line, drug, concentration etc).
  <br> - Note: a metadata file in not required for succesfully running the script but is highly recommended.
  ```
  dfm = pd.read_csv('EX_01_metadata.csv')
  ```
3. Specify the name of the folder containing the object level data.
  <br> - Note: If your data is saved in a single file, provide the name  of the file (or entire path).
  ```
  obj = 'EX_01[78956]'
  ```
4. Map user-defined channel names to standarized names required by the script.
  <br> - Note: The column names in your input dataset may vary based on your software or personal preferences. However, the script expects a set of standard column names for DNA content, LDR, EDU features.
  ```
  ndict = {'Nuclei Selected - EdUINT': 'edu',
          'Nuclei Selected - DNAcontent': 'dna',
          'Nuclei Selected - LDRTXT SER Spot 8 px': 'ldrint',
          'Nuclei Selected - pH3INT': 'ph3'}
  ```
5. Run automated gating on the example dataset. (Run time ~1 minute)
  ```
  dfs = rccg.run(obj, ndict, dfm)
  ```

- `dfs` is data frame that will be returned containing well-level summary of live/dead and fraction of cells in S, G1, G2 M, etc.
- Two files `EX_01[78956].csv` and `EX_01[78956].pdf` will be saved in your local directory.
  - `EX_01[78956].csv` - A comma-separated text file with a table containing rows corresponding to wells in the 96 well plate.
  <br>Each row contains a well-level summary of the number of live/dead cells and fraction of cells in each phase of the cell cycle for one well.
  <figure>
      <img src="{{ site.baseurl }}/assets/images/dye_drop/example_result_csv.png" class="center">
      <figcaption align = "center"><b>Example output table</b></figcaption>
  </figure>
  - `EX_01[78956].pdf` - a pdf with DNA v EDU scatterplots and gating for each well
  <figure>
    <img src="{{ site.baseurl }}/assets/images/dye_drop/example_result_pdf.png" class="center">
    <figcaption align = "center"><b>Example output figures</b></figcaption>
  </figure>
