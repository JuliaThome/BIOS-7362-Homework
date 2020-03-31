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

$$
\\begin{align\*}
var(\\bar{x}^\*\_1) &= var(\\tfrac{1}{N}\\sum\_{i = 1}^N x\_{1i})\\\\
&= \\tfrac{1}{N^2} var(\\sum\_{i = 1}^N x\_{1i})\\\\
&= \\tfrac{1}{N^2}\\left\[\\sum\_{i = 1}^N \\sum\_{j = 1}^N cov(x\_{1i},x\_{1j})\\right\]\\\\
&= \\tfrac{1}{N^2}\\left\[\\sum\_{i = 1}^N var(x\_{1i})+  \\sum\_{1 \\leq i \\leq j \\leq N} cov(x\_{1i},x\_{1j})\\right\]\\\\
&=\\tfrac{1}{N^2}\\left\[N\\sigma^2 + N(N-1)\\tfrac{\\sigma^2}{N}\\right\]\\\\
&= \\tfrac{1}{N^2}\\left\[N\\sigma^2 + (N-1)\\sigma^2\\right\]\\\\
&= \\tfrac{1}{N^2}\\left\[N\\sigma^2 + N\\sigma^2-\\sigma^2\\right\]\\\\
&= \\frac{\\sigma^2(2n-1)}{N^2}\\\\
\\end{align\*}
$$

Using these two pieces information gives us
$$
\\begin{align\*}
corr(\\bar{x}^\*\_1,\\bar{x}^\*\_2) &= \\frac{cov(\\bar{x}^\*\_1,\\bar{x}^\*\_2)}{\\sqrt{var(\\bar{x}^\*\_1)}\\sqrt{var(\\bar{x}^\*\_2)}}\\\\
&= \\frac{\\sigma^2/N}{\\sigma^2(N-1)/N^2}\\\\
&=  \\frac{1}{2(N-1)/N}\\\\
&= \\frac{N}{2(N-1)}
\\end{align\*}
$$
 Note that when *N* is relatively large,
$corr(\\bar{x}^\*\_1,\\bar{x}^\*\_2) = \\frac{N}{2(N-1)} \\approx 50\\%$.
$$
\\begin{align\*}
var(\\bar{x}\_{bag}) &= var\\left(\\frac{1}{2}(\\bar{x}^\*\_1+ \\bar{x}^\*\_2)\\right)\\\\
&= \\frac{1}{4}\\left\[var(\\bar{x}^\*\_1)+ var(\\bar{x}^\*\_2) + 2cov(\\bar{x}^\*\_1,\\bar{x}^\*\_2)\\right\]\\\\
&= \\frac{1}{4}\\left\[\\frac{\\sigma^2(2N - 1)}{N^2}+ \\frac{\\sigma^2(2N - 1)}{N^2} + 2\\frac{\\sigma^2}{N}\\right\]\\\\
&= \\frac{1}{4}\\left\[\\frac{6\\sigma^2N - 2\\sigma^2}{N^2}\\right\]\\\\
&= \\frac{\\sigma^2(3N-1)}{2N^2}
\\end{align\*}
$$
