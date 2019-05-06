---
layout: post
title: GLM series (1) - Exponential Family
---

Generalized Linear Model(GLM) is like a basic building block in understanding statistical modeling.
First of all, this post introduces exponential family, which is widely used in statistical modeling for its simplicity and many desirable properties.

### Desirable Properties of EF

1. A distribution in EF has conjugate prior.
2. A distribution in EF has sufficient statistics, where those of iid samples are represented as sum of each sample's sufficient statistic.
3. Posterior predictive distribution of response variable with a distribution in EF, can be written in closed-form when the proper conjugate prior was employed.

### General Form of EF

A distribution in EF has a form

\( f_{X}(x;\theta) = h(x)exp(\eta(\theta)^T T(x) - A(\theta) ) \)

And these properties hold : 

- *Support* of \\(X\\) does not depend on the values of \\( \theta \\)
- In case of \\( \eta (\theta) = \theta \\), \\(f_X\\) is called canonical form and any \\(f_X\\) can be reparametrized to be canonical.
- When \\( \vec{\theta} \in R^s \\),  \\(f_X\\) can be defined analogously and \\(f_X\\) is said to be *curved* if \\(dim(\vec{\theta}) < dim(\eta (\vec{\theta})) \\).
- \\(T(x)\\) is a sufficient statistic of a sample x and for another sample \\(x'\\) such that \\(T(x) = T(y)\\), the following holds : 

\( f(x; \theta_1) / f(x ; \theta_2) = f(y; \theta_1) / f(y; \theta_2) \)

- For an iid samples \\( X = \{x_1, x_2, ..., x_n \} \\), we have \\( T(X) = \sum_{i=1}^{n}{T(x_i)} \\)
- \\( \eta \\) is called natural parameter.
- \\( A(\eta) \\) is log-partition function and is determined when \\( T, h, \eta \\) are determined : 

 \( A(\eta) = log(\int_{x}{h(x)exp(\eat^T T(x)) dx}) \)

### Examples

- Normal distribution is in EF : (1) known variance, unknown mean, (2) unknown variance and unknown mean
- Binomial distribution is in EF if number of trials \\(n \\) is fixed constant.
