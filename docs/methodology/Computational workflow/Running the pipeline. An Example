---
layout: default
nav_order: 8
title: Running the pipeline. An Example
parent: Computational workflow
---

# An example of running the automated gating script

1. Install the package as explained in the Installation page
2. The example directory (located in `DrugResponse/python/cell_cycle_gating/examples/`) contains a Raw data folder `EX_01[78956]`
3. This folder contains 10 .txt files, each corresponding to single cell data from a given well (wells C3 to C12)
4. The example script below will read the contents of the folder, perform automate gating and output a .csv file that contains a well level summary of number of live/dead cells and fraction of cells in diferent phases of the cell cycle.
5. In addition, pdf file containing figures that show the gating per well is also available for review.
6. The example can either be run in a Jupyter notebook or on your preferred python session
7. This example dataset contains 10 wells and should run within a minute. An entire plate with ~300 wells is expected to run in 10-15 minutes

## Running the example

1. Import required dependencies

```
import pandas as pd     
import warnings
warnings.filterwarnings('ignore')
from cell_cycle_gating import run_cell_cycle_gating as rccg. # The main functions for automated gating are imported
```

2. Import the metadata file that containg mapping between the well name and conditions (i.e cell line, drug, concentration etc). A metadata file in not required for succesfully running the script but is highly recommended.

```
# Load metadata file (OPTIONAL)
dfm = pd.read_csv('EX_01_metadata.csv')
```

3. Specify the name of the folder containing the object level data. Note: If your data is saved in a single file, provide the name  of the file (or entire path)
```
obj = 'EX_01[78956]'. # name of  folder containing example data
```

4. The column names in your input dataset may vary based on your software or personal preferences. However, the script expects a set of standard column names for DNA content, LDR, EDU features. Map column names in the input data to the standard names expected by the script
```
# Name of object level directory
obj = 'EX_01[78956]'

# Load metadata file (OPTIONAL)
dfm = pd.read_csv('EX_01_metadata.csv')

5. Map user defined channel names to standarized names required by the script
```
ndict = {'Nuclei Selected - EdUINT': 'edu',
        'Nuclei Selected - DNAcontent': 'dna',
        'Nuclei Selected - LDRTXT SER Spot 8 px' : 'ldrint',
        'Nuclei Selected - pH3INT': 'ph3'}
``` 

6. Run automated gating on the example dataset. (Run time ~1 minute)
```
dfs = rccg.run(obj, ndict, dfm). # dfs is data frame that will be returned containing well level summary of live/dead and fraction of cells in S, G1, G2 M, etc
```

7. Two files `EX_01[78956].csv` and `EX_01[78956].pdf` will be saved in your local directory



