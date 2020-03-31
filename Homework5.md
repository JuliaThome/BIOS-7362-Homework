R Markdown
----------

**Ex. 15.4:** Suppose *x*<sub>*i*</sub>, *i* = 1, …, *N* are iid
(*μ*, *σ*<sup>2</sup>). Let $\\bar{x}^\*\_1$ and $\\bar{x}^\*\_2$ be two
bootstrap realizations of the sample mean. Show that the sampling
correlation
$corr(\\bar{x}^\*\_1,\\bar{x}^\*\_2) = \\frac{n}{2n-1} \\approx 50\\%$.
Along the way, derive $var(\\bar{x}^\*\_1)$ and the variance of the
bagged mean $\\bar{x}\_{bag}$. Here $\\bar{x}$ is a linear statistic;
baggin produces no reduction in variance for linear statistics.

To find $corr(\\bar{x}^\*\_1,\\bar{x}^\*\_2)$ we will need to find
$cov(\\bar{x}^\*\_1,\\bar{x}^\*\_2)$, $var(\\bar{x}^\*\_1)$, and
$var(\\bar{x}^\*\_2)$ using usual properties of covariance and variance.

$$
\\begin{align\*}
cov(\\bar{x}^\*\_1,\\bar{x}^\*\_2) &= cov(\\tfrac{1}{N}\\sum\_{i=1}^Nx\_{1i},\\tfrac{1}{N}\\sum\_{i=1}^Nx\_{2i})\\\\
&= \\tfrac{1}{N}cov(\\sum\_{i=1}^Nx\_{1i},\\sum\_{i=1}^Nx\_{2i})\\\\
&= \\tfrac{1}{N}\\sum\_{i=1}^Ncov(x\_{1i},x\_{2i})\\\\
&= \\tfrac{1}{N}\\sum\_{i=1}^N\\left(\\sigma^2\\times P(x\_{1i} = x\_{2i})\\right)\\\\
&= \\tfrac{1}{N}\\sum\_{i=1}^N\\tfrac{\\sigma^2}{N}\\\\
&= \\tfrac{\\sigma^2}{N}
\\end{align\*}
$$

Using these two pieces information gives us

Note that when *N* is relatively large,
$corr(\\bar{x}^\*\_1,\\bar{x}^\*\_2) = \\frac{N}{2(N-1)} \\approx 50\\%$.
