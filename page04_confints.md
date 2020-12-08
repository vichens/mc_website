---
layout: page
title: Confidence Intervals
permalink: confints
sidebar: true
interactive: confints.html
---
---

## Is the distribution of catastrophe times for microtubules with labeled tubulin the same as that for unlabeled tubulin?
In order to investigate if the catastrophe times for microtubules with labeled tubulin and for those with unlabeled tubulin could be identically distributed, we plotted their ECDFs along with a confidence interval using bootstrapping. Looking at the confidence intervals of the ECDFs, the distributions of the labeled and unlabeled observations is largely overlapping, and the points follow a very similar trend. The confidence interval of the unlabeled times appears to be larger than those of the labeled times, which is most likely due to the labeled dataset having 211 data points, while the unlabeled dataset having only 95 data points, thus increasing the confidence interval.

As a second check, we plotted the upper and lower bounds for the 95% confidence interval as computed from the DKW inequality for the microtubule catastrophe data. We saw that the upper and lower bounds for the confidence intervals for both the labeled and unlabeled datasets functioned as expected, and there was no overlap between the upper and lower bounds and the confidence intervals. The bounds were much closer for the first half of the data, when the ECDF values were increasing, but for the second half of the data, the bounds were much larger than the actual confidence interval of the ECDFs.

For statistical testing, we used the Mann-Whitney U test. Our null hypothesis was that the distributions of the two datasets are similar. Since we obtained a p-value of 0.149, above the 0.05 level of significance, we could not reject the null hypothesis. This test concluded that the two datasets, between the labeled and unlabeled tubulin, had similar distributions.


<!-- The below line includes the interactive figure. Do not change! -->
<center>

{% include_relative interactives/{{page.interactive}} %}

</center>



