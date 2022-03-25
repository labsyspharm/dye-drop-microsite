---
layout: page
title: Growth rate metrics
nav_order: 10
has_children: true
parent: Overview
---

## GR metrics
<br>
<b>"GR metrics"</b><sup><a href="https://dx.doi.org/10.1038/nmeth.3853">[1]</a><a href="https://dx.doi.org/10.1038/nbt.3882">[2]</a></sup> were recently developed to address the problem that traditional drug sensitivity/resistance metrics (such as IC<sub>50</sub> and E<sub>max</sub>) can be confounded with the number of cell divisions taking place during the response assay. GR metrics use an improved methodology that measures the effect of a perturbation on the <i>growth rate</i> of a cell population rather than on the percent viability. This method creates a transformed "dose-response" curve with new summary metrics (GR<sub>50</sub>, GR<sub>max</sub>, etc.). These new curves and metrics can be used to measure growth rate effects due to drug treatment as well as other perturbations, for example genetic manipulation or changes in seeding density of cells.

The [**GR calculator**](http://www.grcalculator.org){:target="_blank"} provides a web interface for computation of GR metrics.
For offline computation, analysis, and visualization, we provide an R package available on Bioconductor: [**GRmetrics**](https://bioconductor.org/packages/GRmetrics){:target="_blank"}.