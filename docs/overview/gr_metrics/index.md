---
layout: page
title: Growth rate metrics
nav_order: 10
has_children: true
parent: Overview
---

# Growth rate metrics
<b>"Growth rate (GR) metrics"</b><sup><a href="https://dx.doi.org/10.1038/nmeth.3853">[1]</a><a href="https://dx.doi.org/10.1038/nbt.3882">[2]</a></sup>  were developed as an alternative to traditional drug sensitivity/resistance metrics (such as IC<sub>50</sub> and E<sub>max</sub>), which can be confounded when cells continued to grow during the assay. 

GR metrics measure the effect of a perturbation on the <i>growth rate</i> of a cell population rather than on the percent viability. This creates a transformed "dose-response" curve with new summary metrics (GR<sub>50</sub>, GR<sub>max</sub>, etc.). These new curves and metrics can measure growth rate effects due to drug treatment and can be applied to other perturbations, for example on genetic manipulation or on cells plated at different densities.

<br>

{: .text-center }
{: .fw-500 }
{: .fs-5}
On the following pages, you can learn more about the computational methdos used in the classical [GR method](./GRmetrics_overview.html) and the new addition of [static and toxic](GRstatic_toxic.html) growth rate metrics. 

<br> 

**Growth rate metrics can be calculated in two ways:**
1. The [**GR calculator**](http://www.grcalculator.org){:target="_blank"} provides a web interface for computation of GR metrics.
2. For offline computation, analysis, and visualization, we provide an R package available on Bioconductor: [**GRmetrics**](https://bioconductor.org/packages/GRmetrics){:target="_blank"}.