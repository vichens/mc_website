---
layout: page
title: Successive Poisson Model
permalink: poisson
sidebar: true
interactive: poisson.html
---
---

## Developing a model for catastrophe: successive Poisson processes

We investigated two possible models for microtubule catastrophe.

In our first model, we assert that catastrophe is triggered by two biochemical processes happening in succession. We model both as a Poisson process, with $$\beta_1$$ being the rate of arrivals for the first process and $$\beta_2$$ being the rate of arrivals for the second.

To explore how the ratio $$\beta_2/\beta_1$$ affects the time to catastrophe, we used random number generation to simulate a typical experiment consisting of 150 catastrophe events using our successive Poisson model for several values of $$\beta_1$$ and $$\beta_2$$. ECDFs were plotted for each, and we saw that the greater the ratio between $$\beta_2$$:$$\beta_1$$, the greater the time * $$\beta_1$$ values.

Below, we derive the PDF and CDF for the distribution for the time to catastrophe analytically. 

The joint PDF is $$f(t, t_1) = f(t-t_1)\,f(t_1)$$.

$$f(t, t_1) = \beta_2\mathrm{e}^{-\beta_2(t-t_1)}\,\beta_1\mathrm{e}^{-\beta_1 t_1}$$.

$$f(t) = \int_0^t\mathrm{d}t_1\,f(t, t_1) \\[1em]
=  \int_0^t \mathrm{d}t_1\,\beta_2\mathrm{e}^{-\beta_2(t-t_1)}\,\beta_1\mathrm{e}^{-\beta_1 t_1} \\[1em]
= \beta_1\beta_2\mathrm{e}^{-\beta_2 t} \int_0^t \mathrm{d}t_1\,\mathrm{e}^{-(\beta_1 - \beta_2)t_1} \\[1em]
= \frac{\beta_1\beta_2\,\mathrm{e}^{-\beta_2 t}}{\beta_1-\beta_2}\left(1 - \mathrm{e}^{-(\beta_1 - \beta_2)t}\right) \\[1em]
= \frac{\beta_1\beta_2}{\beta_2-\beta_1}\left(\mathrm{e}^{-\beta_1 t} - \mathrm{e}^{-\beta_2 t}\right)$$.

$$F(t; \beta_1, \beta_2) = 
\frac{\beta_1 \beta_2}{\beta_2-\beta_1}\left[
\frac{1}{\beta_1}\left(1-\mathrm{e}^{- \beta_1 t}\right)- \frac{1}{\beta_2}\left(1-\mathrm{e}^{-\beta_2 t}\right)
\right]$$.

This was verified by overlaying the analytical CDF with an ECDF from our simulation.

<!-- The below line includes the interactive figure. Do not change! -->
<center>

{% include_relative interactives/{{page.interactive}} %}

</center>

## Maximum Likelihood Estimation

We obtained a maximum likelihood estimate for the parameters of this model for the labeled tubulin, since we have previously shown that there is little difference between labeled and unlabeled tubulin.

We started by noting that if we flip $\beta_1$ and $\beta_2$, we see that the PDF will return the same value, so we can rewrite this PDF and the parameters in terms of $\beta_1$ and $\Delta \beta$ where $\Delta \beta = \beta_2 - \beta_1$ and $\beta_2 = \Delta \beta + \beta_1$ to get the following PDF
$$f(t; \beta_1, \Delta \beta) = \frac{\beta_1 (\beta_1 + \Delta \beta)}{\Delta \beta} e^{-\beta_1 t} (1 - e^{-\Delta \beta t}) $$.

This is also a good approach because from the original PDF, when we take the log of the PDF to get the log likelihood, we would get 
$$L(t; \beta_1, \beta_2) = \ln(\frac{\beta_1 \beta_2}{\beta_2 + \beta_1}) + \ln(e^{-\beta_1 t} - e^{-\beta_2 t}) $$.

The term $$\ln((e^{-\beta_1 t} - e^{-\beta_2 t}))$$ would be the logarithm of an extremely small number, and given the numerical inaccuracies of computation, this is risky. With the factored PDF with the different parameters, the log likelihood function would be 
$$L(t; \beta_1, \Delta \beta) = \ln(\frac{\beta_1 (\beta_1 + \Delta \beta)}{\Delta \beta}) + \ln(e^{-\beta_1 t}) + \ln(1 - e^{-\Delta \beta t})$$.

where the $$\ln( (1 - e^{-\Delta \beta t}))$$ component will be a reasonable value. 

So we will go forward using the PDF 
$$f(t; \beta_1, \Delta \beta) = \frac{\beta_1 (\beta_1 + \Delta \beta)}{\Delta \beta} e^{-\beta_1 t} (1 - e^{-\Delta \beta t}) $$,

and the log likelihood function
$$L(t; \beta_1, \Delta \beta) = \ln(\frac{\beta_1 (\beta_1 + \Delta \beta)}{\Delta \beta}) + -\beta_1 t + \ln(1 - e^{-\Delta \beta t}) $$,

with the limits of the parameters being $$\beta_1 \ge 0$$ and $$\Delta \beta \ge 0$$.

We then used Powell's method to calculate maximum likelihood estimates for parameters for the microtubule time to catastrophe measurements, parametrized by $$\beta_1, \delta_\beta$$. We also used parametric bootstrapping to obtain 95% confidence intervals.

The MLE for $$\beta_1$$ was $$4.54 \times 10^-3$$, and for $$\Delta \beta$$ was $$1.48 \times 10^-7$$.

Since this model is close to a Gamma distribution with $\alpha = 2$, we use the fact that for a Gamma distribution, $$\mu = \alpha / \beta$$ to get that $$\beta = \alpha / \mu = 2 / 440.7 = 0.0045$$ which fits into our confidence interval for $$\beta_1$$, [$$0.0041, 0.0050$$].

For the $\Delta \beta$ parameter, we know that $\beta_1$ and $\beta_2$ are close in value (or at least of similar order of magnitude). This is because if one $\beta$ value was much larger than the other, then the observed times will approach a single-arrival event dependent on the smaller $\beta$ value, and thus the $\alpha$ value would be expected to be around 1. However, we know that our gamma distribution has an $\alpha$ that is around 2, so the $\beta$ values are not very different from each other. As a result, the $\Delta \beta$ value is expected to be very small, which we can see in the confidence interval for the $\Delta \beta$ parameter, [$$4.01 \times 10^-12, 4.58 \times 10^-7$$].