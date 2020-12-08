---
layout: page
title: Model Comparison
permalink: comparison
sidebar: true
interactive: comparison.html
---
---

## Does the successive Poisson or Gamma model better represent our data?

Here, we investigated microtubule catastrophe using labeled tubulin for different concentrations of total tubulin. We found that there is not very significant variance in the data between the different tubulin concentrations, but there is a very slight trend for greater time between catastrophes as the tubulin concentration increases.

We have the most data points for a tubulin concentration of 12 µM tubulin, so we will use the data for this concentration to compare the two models.

### Gamma Model
The MLEs for the Gamma distribution were $\alpha = 2.91$ and $\beta = 0.0076$, with confidence intervals of [$2.62949722, 3.2073774$] and [$0.00686769, 0.00850854$], respectively.

We then compared these confidence intervals to the plug-in estimates of the data. For the Gamma distribution, $\mu = \alpha / \beta$ and $\sigma^2 = \alpha / \beta^2$, which we can manipulate to obtain $\alpha = \mu * \beta$ and $\alpha = \sigma^2 * \beta^2$ to solve for $\beta$ and get $\beta = \mu / \sigma^2$ and $\alpha = \mu^2 / \sigma^2$. Using the Gamma distribution hypothesis, the percent error calculated between the expected and actual $\alpha$ and $\beta$ values were about 7% for both.

### Successive Poisson Model
The MLEs for this model were $\beta_1 = 0.005255456835288156$, $\Delta\beta = 6.141225700561563\times10^{-12}$, and $\beta_2 = 0.00525545682914693$.

The confidence intervals were [$4.99397589\times 10^{-3},5.52957558\times 10^{-3}$], [$5.73834899\times 10^{-12},6.39502758\times 10^{-7}$], and [$4.99343182\times 10^{-3},5.52957538\times 10^{-3}$], respectively.

## Model Comparison
To see which model works better, we generated sample values from the two distribution models. For the Gamma model, we used the Gamma generator with the $\alpha$ and $\beta$ values gotten from the MLE. For the multiple Poisson event model, we generate two separate samples from the Exponential distribution with the $\beta_1$ and $\beta_2$ MLE parameters, and return them added. These are similar to the generative functions used in the bootstrapping process.

We plotted these sample values against the ECDF for the actual data. We saw that the Gamma distribution was more similar to the actual data than the multiple Poisson event distribution, although they were very close. We also plotted the differences between the actual ECDF and ECDFs for the two models to more clearly show that the Gamma distribution model was more similar to the actual data than the multiple Poisson event distribution model.

## Maximum Likelihood Estimation for Other Tubulin Concentrations

We obtained parameter estimates for the other tubulin concentrations using the Gamma model:

| Tubulin Concentration| $\alpha$ | $\beta$ |
|-------|--------|---------|
| 7 µM | 2.4438576181986615 | 0.00755037294885461 |
| 9 µM | 2.6797160735581533 | 0.008779371023383385 |
| 10 µM | 3.2107972394074356 | 0.009029890255519896 |
| 12 µM | 2.9149398724567774 | 0.00766122805656492 |
| 14 µM | 3.3614626885951777 | 0.007174992802876018 |

Looking at the MLE of the $\alpha$ and $\beta$ parameters for each of the different tubulin concentrations, we can see that there was a slight upward trend (although between 10 and 12 it swapped) of the alpha values. In this model, the alpha parameter represents the minimum number of steps to produce a catastrophe. The data implies that as the concentration of tubulin increases, the number of steps to produce a catastrophe also increases. One possible explanation of this is that when there are more tubulin available in the environment, the less likely it is for an interrupting component to come in to the growth of the microtubule and induce a catastrophe. When we consider the beta parameter values, it peaks at 10 µM and decreases at higher or lower concentrations of tubulin. In this model the beta parameter represents the rate of occurrence of each step. It appears that at higher or lower tubulin concentrations, the rate of occurence of steps is lower, possible due to either interference of tubulin at higher concentrations, or the lack of tubulin to induce a step at lower concentrations. 10 µM tubulin concentration has the highest rate of step occurrence and the second highest number of steps required to induce a catastrophe.

As a sanity check, we also plotted ECDFs for each of the tubulin concentrations by using the MLE parameters to generate samples from the Gamma distribution. This results in a graph that looks very similar to the plotting of the original data.

<!-- The below line includes the interactive figure. Do not change! -->
<center>

{% include_relative interactives/{{page.interactive}} %}

</center>
