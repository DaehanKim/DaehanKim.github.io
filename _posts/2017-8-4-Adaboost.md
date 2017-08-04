---
layout: post
title: Adaboost(Adaptive Boosting)
---

* This post was inspired by Alexander Ihler's Youtube lecture on Adaboost.

### Adaptive Boosting

![boosting1](https://daehankim.github.io/images/boosting.png)


It is Ensemble method. It combines multiple classifiers to make a better one. First, It builds extremely simple classifier like lines.

![boosting2](https://daehankim.github.io/images/boosting2.png)


After running it, it focuses on wrong classified samples and assign high weight to their loss and conversely, grant low weights to those classified correctly. Now build a simple classifier again.

![boosting3](https://daehankim.github.io/images/boosting3.png)


Since we use multiple simple classifiers, many different types of them can be deployed as long as their loss can be weighed.

![boosting4](https://daehankim.github.io/images/boosting4.png)


Finally, ultimate classifier is now just a linear combination of simple classifiers. Then it forms rather complex decision boundary than before. 



This is pseudocode for Adaboost :

![boosting5](https://daehankim.github.io/images/boosting5.png)


Adaboost corresponds to surrogate loss function : 
\\(C_{ada} = \sum_{i} exp(-y^{i}f(x^{i}))\\)

