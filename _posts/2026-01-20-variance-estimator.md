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


### Orthogonal Projections

When thinking about $\widehat{\sigma}^2$ geometrically, we may view it as the squared Euclidean norm of an $n$-dimensional vector, normalized by $n-1$. If we define the sample vector

$$
\boldsymbol{X} = [X_1, \dots, X_n]^\top
$$

and the center-of-mass vector

$$
\boldsymbol{C} = \overline{X}\,\mathbf{1}
= [\overline{X}, \dots, \overline{X}]^\top,
$$

where $\mathbf{1}$ stands for the all-ones vector, then

$$
\widehat{\sigma}^2
= \frac{1}{n-1}\,\lVert \boldsymbol{X} - \boldsymbol{C} \rVert_{\ell^2}^2.
$$

Here $\lVert \cdot \rVert_{\ell^2}$ denotes the Euclidean norm, the standard way mathematicians refer to “distance from zero”.

Neat. We are interested in the expected distance from $\boldsymbol{X} - \boldsymbol{C}$ to $\mathbf{0}$. Let us notice a simple but important property of this vector.  
If we define $X_i' = X_i - \overline{X}$ for $i = 1, \dots, n$, then

$$
\langle \boldsymbol{X} - \boldsymbol{C}, \mathbf{1} \rangle
= X_1' + \dots + X_n'
= \left( X_1 - \frac{X_1 + \dots + X_n}{n} \right)
+ \dots
+ \left( X_n - \frac{X_1 + \dots + X_n}{n} \right)
= 0.
$$

This means that the random vectors $\boldsymbol{X} - \boldsymbol{C}$ lie in a subspace orthogonal to the all-ones vector $\mathbf{1}$. Since $\boldsymbol{C}$ itself is a multiple of $\mathbf{1}$, subtracting it removes the component of $\boldsymbol{X}$ in the $\mathbf{1}$ direction. Consequently, $\boldsymbol{X} - \boldsymbol{C}$ is the orthogonal projection of $\boldsymbol{X}$ onto the hyperplane

$$
X_1 + \dots + X_n = 0.
$$

The discussion above shows that subtracting the mean in the definition of $\widehat{\sigma}^2$ removes exactly the component of $\boldsymbol{X}$ in the $\mathbf{1}$ direction. Let us take a look at a simple case in dimension two.

![Orthogonal projection onto $X_1 + X_2 = 0$](/assets/img/variance/projection_single.png)

Even though the scenario depicted above may appear overly simplistic, it still allows for a few useful observations.

- If $\mu = 0$, the squared distance of the blue point from the origin represents $n\,\widehat{\sigma}^2_{\mu\text{ known}}$. Changing $\mu$ simply translates the point along the $[1,1]^\top$ direction, while its projection remains fixed.
- Similarly, the squared distance of the red point from the origin represents $(n-1)\,\widehat{\sigma}^2$, where we pretend that the true value of $\mu$ remains unknown.

Basic trigonometry shows that in the $\mu = 0$ case we have

$$
\lVert \boldsymbol{X} \rVert_{\ell^2}
= \lVert \boldsymbol{X} - \boldsymbol{C} \rVert_{\ell^2} \cos(\alpha),
$$

which implies

$$
n\,\widehat{\sigma}^2_{\mu\text{ known}}
= (n-1)\,\widehat{\sigma}^2 \cos(\alpha).
$$

Now observe that replacing $n-1$ with $n$ in the definition of $\widehat{\sigma}^2$ would lead to the highly dubious identity

$$
\widehat{\sigma}^2_{\mu\text{ known}}
\stackrel{?!}{=}
\widehat{\sigma}^2 \cos(\alpha).
$$

Since $\lvert \cos(\alpha) \rvert \leq 1$, this would systematically push the variance estimate downward.
This is precisely the bias we want to avoid.

At this stage, one might suspect that $\frac{1}{n-1}$ is the correct normalization factor when constructing $\widehat{\sigma}^2$. While this is not yet a proof, it already makes clear that using $\frac{1}{n}$ is the wrong choice.
