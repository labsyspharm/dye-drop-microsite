---
layout: default
nav_order: 13
title: Static/Toxic GR
parent: Growth rate metrics
---

## GR static and GR toxic
<br>
The original GR method detailed in <a href="https://dx.doi.org/10.1038/nmeth.3853">Hafner et al. (2016)</a> only takes into account living cells. However, when toxicity and cell death occurs, it may be informative to model this as well. To take this into account, we have extended our method for situations in which one has estimates of the number of dead cells as well as living cells. We separate the "GR" into two components: a static component <font color="light blue"><b>GR<sub>static</sub></b></font>, which measures the how much <font color="light blue"><b>viable cell growth rate is slowed compared to control</b></font>, and a toxic component <font color="red"><b>GR<sub>toxic</sub></b></font>, which measures how much <font color="red"><b>cell death rate is increased compared to control</b></font>.

### Definitions:

|Variable| Definition | Column title |
|---|---|---|
|**_x(c,t)_**|the amount of **_viable cells_** at time _t_ at drug concentration _c_|_**cell_count**_|
|**_d(c,t)_**| the amount of **_dead cells_** at time _t_ at drug concentration _c_|_**dead_cell_count**_|
|**_x<sub>0</sub>_** = _x(0,0)_| the starting amount of **_viable cells_** |_**cell_count__time0**_|
|**_d<sub>0</sub>_** = _d(0,0)_| starting amount of **_dead cells_** |_**dead_cell_count__time0**_|
|**_x<sub>ctrl</sub>_** = _x(0,t)_| amount of **_un-treated viable cells_** at time _t_| _**cell_count__ctrl**_|
|**_d<sub>ctrl</sub>_** = _d(0,t)_| amount of **_dead un-treated cells_** at time _t_| _**dead_cell_count__ctrl**_|
|**_k<sub>s</sub>(c,t)_**| the "cytostatic" growth-rate of the cell population, i.e. the rate of change of viable cells, for treatment concentration _c_ at time _t_| |
|**_k<sub>d</sub>(c,t)_**| the "cytotoxic" growth-rate of the cell population, i.e. the rate of change of dead cells, for treatment concentration _c_ at time _t_| |
|**_k(c,t)_** = **_k<sub>s</sub>(c,t)_** + **_k<sub>d</sub>(c,t)_**| the overall growth-rate of the cell population for treatment concentration _c_ at time _t_| |
|**_t_**| the duration of the assay in hours| |

### Overview:

In order to differentiate between the effects of slowed growth and toxicity, we introduce the static and toxic GR. We start by modifying our model of cell population growth to separate total population growth into two parts, a growth rate <b><i>k<sub>s</sub></i></b> and a death rate <b><i>k<sub>d</sub></i></b>.

{: .text-center}
<img src="{{ site.baseurl }}/assets/images/gr/gr_statictoxic/gr_models.png" style="width:70%;margin:20px 20px">
	
<p>
  To derive these, we describe the rates of change with a system of ordinary differential equations (ODEs):
<img src="{{ site.baseurl }}/assets/images/gr/gr_statictoxic/gr_diffeq.png" style="width:70%;margin:20px 20px">
</p>
<p>
  Using the initial conditions for the population of live cells <b><i>x<sub>0</sub> = x(0,0)</i></b> and dead cells <b><i>d<sub>0</sub> = d(0,0)</i></b>, we solve this system for <b><i>k<sub>s</sub></i></b> and <b><i>k<sub>d</sub></i></b>.
</p>
<center><img src="{{ site.baseurl }}/assets/images/gr/gr_statictoxic/gr_diffeq_sol.png" style="width:80%;margin:20px 20px"></center>
<p>
  For <font color="light blue"><b>GR<sub>static</sub></b></font>, the cytostatic part of growth-rate inhibition, we consider the ratio of the treated growth-rate among viable cells to the un-treated growth rate <b><i>k<sub>s</sub>(c)/k<sub>s</sub>(0)</i></b>. Again, we exponentiate it and subtract 1 to bound our values for the curve. Since <font color="light blue"><b>GR<sub>static</sub></b></font> only characterizes slowed population growth and not cell death, it is bounded between 1 and 0.
</p>
<p>
  For <font color="red"><b>GR<sub>toxic</sub></b></font>, we expect the un-treated death rate <b><i>k<sub>d</sub>(0)</i></b> to be close to zero, so to make a more robust measure we use the difference of the death rates <b><i>k<sub>d</sub>(c) - k<sub>d</sub>(0)</i></b> rather than their ratio. As with <font color="light blue"><b>GR<sub>static</sub></b></font>, we exponentiate and subtract 1. This makes it so that <font color="red"><b>GR<sub>toxic</sub></b></font> is bounded between 0 and -1.
</p>
<center><img src="{{ site.baseurl }}/assets/images/gr/gr_statictoxic/gr_vs_gr_sd.png" style="width:80%;margin:20px 20px"></center>
<p>
  As with the original GR method, we fit logistic curves to model the <font color="light blue"><b>GR<sub>static</sub></b></font> and <font color="red"><b>GR<sub>toxic</sub></b></font> values as a function of the log treatment concentration.
</p>
<center><img src="{{ site.baseurl }}/assets/images/gr/gr_statictoxic/GR_static_toxic_growth.png" style="width:70%;margin:20px 20px"></center>
<center><img src="{{ site.baseurl }}/assets/images/gr/gr_statictoxic/GR_static_toxic_fitted_curves.png" style="width:70%;margin:20px 20px"></center>
<p>
  As with the original GR curves, we extract summary metrics from the <font color="light blue"><b>GR<sub>static</sub></b></font> and <font color="red"><b>GR<sub>toxic</sub></b></font> curves such as <b><i>GR<sub>50</sub></i></b>, <b><i>GR<sub>inf</sub></i></b>, <b><i>GR<sub>AOC</sub></i></b>, etc. These metrics summarize the growth response of the viable and dead cell populations, respectively.
</p>
<p>
  All of these parameters are defined in the same was as for the original GR curves, with a few small changes. Since the <font color="red"><b>GR<sub>toxic</sub></b></font> curve is bounded between 0 and -1, its <b><i>GR<sub>50</sub></i></b> is defined as the concentration at which it crosses the y = -0.5 line. Similarly, it's <b><i>GR<sub>AOC</sub></i></b> value is defined as the area above the curve, but below zero.
</p>

---