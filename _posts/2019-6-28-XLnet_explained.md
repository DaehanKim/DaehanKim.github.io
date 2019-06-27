---
layout: post
title: XLnet explained (1) - autoregressive and autoencoding language model
---

Recently, Yang has uploaded his paper on arxiv, which proposed a model that outperforms in 20 benchmark NLP tasks to BERT. Let's dig into some basic ideas of this model.  

### Auto-regressive language model

Auto-regressive model refers to models that *predicts the variable with itself used as input.* In this case, usually the target variable is changing over time, so many time-series-prediction tasks are innately auto-regressive. Language models(in the classic formulation) can be viewed as a type of auto-regressive modeling, since the target variable is defined by the word that'll come up next and input is a sequence of words that precede the target word. 
Formally, 

$$ P(x_{1:n}|\theta) = \Pi_{i=1}^{n}{P(x_{i}|x_{< i}, \theta)} $$

where \\( x_i \\) is i-th token in the text. Above equation holds by bayes rule without any assumption on distribution on words.


### BERT as a denoising auto-encoder

BERT efficiently utilize contexts from both directions, by adopting denoising auto-encoding strategy. To build the training corpus, BERT randomly masks 15% of the whole corpus with [mask] token, and train the model to correctly fill in the blank! (Actually, there are some more. For details, read [this paper](https://arxiv.org/abs/1810.04805)) This can be viewed as injecting noise into the corpus since this hides some possibly relavant information. BERT is then trained to *denoise* this corrupted corpus. Furthermore, BERT can be seen as auto-encoder since it encodes the input sequence and finally decodes into the same sequence(which is denoised). 

Formally, BERT is optimized over this objective:


$$ {\mathcal{L}}_{bert} = \sum_{x \in \mathcal{T}} log P(x|\mathcal{C},\theta) + \alpha \mathcal{L}_{nsp} $$


where \\(T \\) is masked tokens(targets), \\(C\\) is context(tokens not included in \\(T \\)) and \\(\mathcal{L}_{nsp}\\) stands for next sentence prediction loss(see the paper for details). \\( \alpha \\) is a mixing constant.

This strategy was kinda unique in language modeling(since almost all language model was trained in an auto-regressive fashion) and was extremely effective. There are some drawbacks, however, in this approach. First, This method assumes that probability distribution of each masked token is independent to each other given the context \\( \mathcal{C} \\). This assumption is purely for the convinience of computation so rarely applys to real-world language structure, since masked tokens usually correlate to each other. Plus, context can be limited because several tokens can be masked in the same sentence. For instance, when there is a sentence, "I go to school" and suppose that both 'to' and 'school' were masked. When BERT tries to figure out what is in the masked 'to', it cannot use the context of 'school', which can be crutial in training. (This can be alleviated - but not solved clearly - by randomly masking corpus several times and training the model on newly masked corpora)

XLnet tries to tackle these two problems by redesigning auto-regressive formulation of language model.

*This post is based on the paper [XLNet: Generalized Autoregressive Pretraining for Language Understanding](https://arxiv.org/abs/1906.08237).*
