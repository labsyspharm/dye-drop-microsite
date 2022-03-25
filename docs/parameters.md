---
layout: default
nav_order: 5
title: Parameter reference

---

# Parameter reference

## Description
This code takes in data from a deep dye drop experiment, determines the number of alive or dead cells, then classifies the alive cells into G1, G2, S, or M phase.

## Input 
**Deep Dye Drop requires two inputs:**

1. The name or path to the input object level data. The input `data` can either be a file (.txt, .csv, .tsv) or a folder containing one .txt file for each well.

2. A python dict `ndict` that maps column names in the input data into a format compatible with the script.

### Formatting
**Please add relevant information about how these input files need to be formatted. Are certain columns required? Is each row a different well? How are start and end points indicated.** What do these look like? 

## Output
**Please describe the output format** 

Something like: 
"After running deep dye drop, you get two .csv files as an output. 

1. This .csv file contains X columns of information that give the cell cycle averages per well 
2. This file contains live and dead cells per well "

## Usage

The master function `run_cell_cycle_gating.run` contains a number of arguments and parameters that can be adjusted. 

```
run(data, ndict, dfm=None,
    ph3_channel=True, ldr_channel=True,
    px_edu=None, x_ldr=None, control_based_gating=False,
    control_gates=None, fudge_gates=np.array([0, 0, 0, 0]),
    header=7, ldr_gates=None,
    nuclei_population_name="Nuclei Selected")
```



## Required arguments

{: .text-center}
| Name | Description |
|---|---|
| ```data``` | The name or path to the input object level data. |
| `ndict` |  A python dict used to map column names in the input data into a format compatible with the script|


## Optional arguments
*Additional details for some arguments are shown below the table.*
{: .fs-3}

{: .text-center}
|  Name | Default | Description |
|---|---|---|
| `dfm` | None | A [dataframe](./parameters.html#dfm) that should contain metadata mapping plates (barcode) and wells to specific experimental conditions such as cell line, drug, and concentration. |
| `control_based_gating` |False |If True, the script will run automated gating only on those wells that are DMSO controls. Note, a metadata table has to be provided for the script to know which wells are control wells.|
| `control_gates` | |A [dataframe](./parameters.html#control_gates) that contains control-based (i.e prior) estimates of gating values.|
| `fudge_gates` | | This [argument](./parameters.html#fudge_gates) enables you to offset the automated DNA gates by the provided values. |
| `ph3_channel` | True | Set to False if the 4th color channel is not used |
| `ldr_channel` | True| Set to False if LDR is not used in the assay |

<br>

### dfm

This dataframe can be used to map specific experimental plates to specific experimental conditions. To do this, the dfm input should contain **these elements** formatted **this way**.

{: .fs-3}
**For example:**
```
paste a dfm here
```

<br>

### control\_gates

Contains control-based (i.e prior) estimates of gating values in the format `______`

{: .fs-3}
**For example:** setting `control_gates` to `______` will `do this thing`.

<br>

### fudge\_gates
The four inputs to `fudge_gates` correspond respectively to: 
>1) the outer left gate
>2) the inner left gate
>3) the inner right gate
>4) the outer right gate

{: .fs-3}
**For example:** setting `fudge_gates` to np.array([0, 0.1, -0.2, 0]) will offset the inner gates by 0.1 to the right an 0.2 to the left. 