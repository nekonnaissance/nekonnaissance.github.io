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


### Some Intuition: Case $n = 1$

Suppose we have only a single random measurement, and we observe $X_1 = 10$.  
There are many pairs $(\mu,\sigma)$ consistent with such an observation, for example:

1. $\mu \approx 10$ and $\sigma$ very small,
2. $\mu \approx 10$ and $\sigma \approx 50$.

There is no way to decide which scenario is closer to the truth. The scale of $\sigma$ can vary by orders of magnitude while remaining compatible with the data. A single observation provides no reliable information about the variance, so an unbiased estimator of $\sigma^2$ cannot exist in this setting.

Now suppose $\mu = 15$ is known and we observe $X_1 = 10$. While we still cannot estimate $\sigma$ precisely, we at least gain information about its order of magnitude. For instance, it is unlikely that $\sigma \ll 1$. This is weak information, but it is no longer nothing.

When the exact value of the mean is known, we are granted a point of reference. For fixed $\mu$, we can construct a slightly different unbiased estimator:

$$
\widehat{\sigma}^2_{\mu\text{ known}} := \frac{1}{n} \sum_{i=1}^n \left( X_i - \mu \right)^2
$$

As we can see, the $-1$ disappears from the denominator. To summarize:

- For $n = 1$, it makes sense that the variance cannot be estimated unless $\mu$ is known.
- Replacing $n$ with $n - 1$ in the denominator can be viewed as a premium paid for not knowing the exact value of $\mu$.

The second point may seem vague for now. In the next section, we make this intuition more precise.





## The unbiased estimator

State it cleanly.
One boxed equation.
Minimal commentary.

Five Itty Bitty Secrets!
Hahah! Hahah!
