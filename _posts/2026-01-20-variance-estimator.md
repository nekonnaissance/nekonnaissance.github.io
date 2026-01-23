---

layout: post

title: "An Unbiased Variance Estimator"

---



The formula for the unbiased variance estimator is well known:

$$
\widehat{\sigma}^2 := \frac{1}{n-1} \sum_{i=1}^n \left( X_i - \overline{X} \right)^2 ,
$$

where $X_1,\dots,X_n$ are independent draws from the same distribution and $\overline{X}$ denotes the sample mean.

Every so often, someone in the room eventually asks:

> *Why do we have $n-1$ in the denominator? The expression looks almost like an average of $n$ squared deviations, so why isn't the denominator simply $n$?*

There are two answers one usually hears:

1. Write down the bias $\mathbf{E}[\widehat{\sigma}^2] - \sigma^2$, expand the square, expand $\overline{X}$, expand all the sums, calculate. See? It’s $0$.
2. Because there are only $n-1$ degrees of freedom among the $X_i$, since translating all measurements by the same amount leaves the variance unchanged.

The first answer is formally correct, but it explains little. The second one may feel hand-wavy. Why should degrees of freedom matter at all? Where, exactly, did the missing dimension go?

Since the difference between $\frac{1}{n}$ and $\frac{1}{n-1}$ is most visible for small values of $n$, let us begin by examining what happens in that regime.




## The naive estimator

Define the obvious thing.
Show why it fails.
One equation max.

## The unbiased estimator

State it cleanly.
One boxed equation.
Minimal commentary.

Five Itty Bitty Secrets!
Hahah! Hahah!
