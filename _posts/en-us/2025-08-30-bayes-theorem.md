---
layout: post
title: Bayes’ Theorem — from idea to impact (Test post by Codex)
date: 2025-08-30 09:00:00 -0400
description: Origin of Bayesian thinking, comparison with frequentists, interpretations of Bayes’ theorem, practical applications, and connections to other fields
tags: bayes probability statistics inference machine-learning
categories: statistics
related_posts: false
---

Bayes’ theorem is a compact rule for learning from data. It ties together prior beliefs, how data are generated (the likelihood), and what we should believe after seeing evidence (the posterior). Beyond the formula, it is a way to reason and decide under uncertainty.

## Where the idea came from

- Thomas Bayes and Pierre-Simon Laplace formalized “inverse probability”: inferring causes from observations.
- Frequentism later emphasized long-run frequencies and procedures with repeated-sampling guarantees.
- Modern Bayesian statistics combines subjective or structured priors with computational tools (MCMC, variational inference) to analyze rich models.

## Frequentist vs Bayesian (in one minute)

- Probability:
  - Frequentist: long-run frequency of events.
  - Bayesian: degree of belief consistent with probability axioms.
- Parameters:
  - Frequentist: fixed but unknown; only data are random.
  - Bayesian: random, with a prior that is updated by data.
- Inference targets:
  - Frequentist: estimators, confidence intervals, hypothesis tests.
  - Bayesian: posterior distributions, credible intervals, posterior predictive checks.

## The theorem and its forms

In parameter form with data D and parameter θ:

$$
p(\theta\mid D) = \frac{p(D\mid \theta)\,p(\theta)}{p(D)} \propto p(D\mid \theta)\,p(\theta).
$$

The denominator is the evidence (marginal likelihood):

\begin{equation}
\label{eq:evidence}
p(D) = \int p(D\mid \theta)\,p(\theta)\,d\theta.
\end{equation}

Odds form with hypothesis H against H^c and evidence E:

$$
\frac{p(H\mid E)}{p(H^c\mid E)} = \underbrace{\frac{p(E\mid H)}{p(E\mid H^c)}}_{\text{Bayes factor}} \cdot \frac{p(H)}{p(H^c)}.
$$

Interpretations:

- Posterior ∝ Likelihood × Prior: data update beliefs.
- Evidence balances fit and complexity; it penalizes overly flexible models.
- With a flat prior, the MAP estimate approaches the MLE; non-flat priors act like regularizers (e.g., Gaussian prior ≈ L2, Laplace prior ≈ L1).

## Conjugate examples

1) Beta–Binomial (coin bias). Prior \(\theta\sim \mathrm{Beta}(\alpha,\beta)\); observe k successes in n trials.

$$
\theta\mid D \sim \mathrm{Beta}(\alpha+k,\,\beta+n-k),\quad 
\mathbb E[\theta\mid D]=\frac{\alpha+k}{\alpha+\beta+n}.
$$

2) Gaussian–Gaussian (unknown mean, known variance). Prior \(\mu\sim\mathcal N(\mu_0,\tau_0^2)\); data \(x_i\stackrel{iid}{\sim}\mathcal N(\mu,\sigma^2)\).

\begin{equation}
\label{eq:gauss}
\mu\mid D\;\sim\;\mathcal N\!\left(\frac{\frac{\mu_0}{\tau_0^2}+\frac{n\bar x}{\sigma^2}}{\frac{1}{\tau_0^2}+\frac{n}{\sigma^2}},\;\;\frac{1}{\frac{1}{\tau_0^2}+\frac{n}{\sigma^2}}\right).
\end{equation}

## Computation in practice

- Analytic: conjugacy and small models.
- Approximate: Laplace approximation, expectation propagation.
- Sampling: MCMC (Metropolis–Hastings, HMC/NUTS) for general posteriors.
- Optimization: variational inference turns inference into ELBO maximization.

## Applications you meet every day

- A/B testing: compare conversion rates with Beta–Binomial posteriors; stop when a decision is confident.
- Medical diagnosis: update disease odds with test likelihood ratios (Bayes factors).
- Spam filtering: Naive Bayes combines token likelihoods to score emails.
- Recommenders: hierarchical Bayes pools information across users/items.
- Tracking and control: Kalman filters are linear–Gaussian Bayes in real time.
- Bayesian optimization: pick experiments via a GP posterior and acquisition rules.

## Connections to other fields

- Information theory: evidence decomposes into fit and complexity; MDL and Bayes are closely related.
- Machine learning: priors as regularizers; Bayesian neural nets quantify uncertainty; dropout approximates a Bayesian ensemble.
- Causality: encode structural knowledge as priors over DAGs or effects.
- Decision theory: minimize expected loss with respect to the posterior.
- Finance and risk: update beliefs about returns and volatilities as data arrive.

## Takeaways

- Bayes’ theorem is a principle for learning from data.
- Priors let you express constraints and share strength across groups.
- The posterior quantifies uncertainty and drives principled decisions.

For reference, here is the law of total probability used in Eq. \eqref{eq:evidence}:

$$
p(D) = \int p(D,\theta)\,d\theta = \int p(D\mid\theta)\,p(\theta)\,d\theta.
$$

