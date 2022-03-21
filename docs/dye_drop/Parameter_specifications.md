---
layout: default
nav_order: 4
title: Parameter specifications
parent: Deep Dye Drop
---

# Parameter specifications

The master function `run_cell_cycle_gating.run` contains a number of arguments and parameters that can be adjusted. 

```
run(data, ndict, dfm=None,
    ph3_channel=True, ldr_channel=True,
    px_edu=None, x_ldr=None, control_based_gating=False,
    control_gates=None, fudge_gates=np.array([0, 0, 0, 0]),
    header=7, ldr_gates=None,
    nuclei_population_name="Nuclei Selected")
```


## Arguments

- **data** - The name or path to the input object level data. data can either be a file (.txt, .csv, .tsv) or a folder containing one .txt file per well
- **ndict** - ndict is a python dict required to be specified in order to map column names in the input data to a fixed format required by the script. 
- **dfm** - (optional) Default is None. This is a dataframe that should contain metadata mapping plates (barcode) and wells to specific experimental conditions such as cell line, drug, and concentration.
- **control_based_gating** - Default is False. If True, the script will run automated gating only on those wells that are DMSO controls. Note, a metadata table has to be provided for the script to know which wells are control wells.
- **control_gates** - This is a dataframe that contains control-based (i.e prior) estimates of gating values. <!-- See example#2 for further clarity -->
- **fudge_gates** - This argument enables you to offset the automated DNA gates by the provided values. The four inputs correspond respectively to: 1) the outer left gate, 2) the inner left gate, 3) the inner right gate, and 4) the outer right gate. 
    - For example, setting *fudge_gates* to np.array([0, 0.1, -0.2, 0]) will offset the inner 2 gates by 0.1 to the right an 0.2 to the left 
- **ph3_channel** - Default is True. Set to False in case the 4th channel is not used
- **ldr_channel** - Default is True. Set to False in case LDR is not used in the assay