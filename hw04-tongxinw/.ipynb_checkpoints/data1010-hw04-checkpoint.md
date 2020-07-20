---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.4
  kernelspec:
    display_name: Julia 1.2.0
    language: julia
    name: julia-1.2
---

<style>
@media print
{
h2 {page-break-before:always}
}
</style>

# Homework 04

### Brown University  
### DATA 1010  
### Fall 2019


## Problem 1
 
<img src="dartboard.png" alt="drawing" width="200" align=right>
Suppose that the probability density function for the random point where your dart hits the dartboard $D \subset \mathbb{R}^2$ is given by $$f(x,y) = \frac{1}{\pi} e^{-x^2 - y^2},$$ where the origin is situated at the dartboard’s bull’s eye, and where $x$ and $y$ are measured in inches (this function is positive everywhere in $\mathbb{R}^2$, so the "dartboard" includes the disk shown as well as the (infinite) wall it is mounted on—this is realistic insofar as one can indeed hit the wall with a dart throw). Find the probability of scoring triple 20 on your next throw. 

*(Optional)* Confirm your result using Monte-Carlo simulation.

**Note:** The triple 20 region is the smaller of the two thin red strips in the sector labeled “20”. The inner and outer radii of this thin strip are 3.85 inches and 4.2 inches, respectively. 

```julia
using SymPy
```

```julia

```

## Problem 2
  
Suppose that $X$ and $Y$ have joint PDF $f(x,y) = \frac{3}{2}y$ on the upper unit disk (that is, the set of points which have positive $y$-coordinate and are less than one unit from the origin).

1.  Verify that $f$ is indeed a probability density function.

2.  Find the density of the distribution of $X$.

3.  Find the conditional density of $Y$ given $X = x$.

4.  Find $\mathbb{E}[Y | X]$.





## Problem 3

The *skewness* of a distribution $\nu$ is a measure of its asymmetry about its mean. It is defined to be
$$\mathbb{E}\left[\left(\frac{X-\mu}{\sigma}\right)^3\right],$$ where $X$ is a random variable with distribution $\nu$, $\mu$ is the mean of $X$, and $\sigma$ is the standard deviation of $X$. Find the skewness of the exponential distribution with parameter $1$. You should set up the integrals on your own, but feel free to evaluate them using a symbolic computation system.   




<!-- #region -->
## Problem 4

Let $X$ be the first digit of the number of residents of a randomly selected world city. What would you expect the distribution of $X$ to look like? What about the *last* digit $Y$?

Load the associated world city populations CSV as a DataFrame and check your predictions. Compare to the distribution with probability mass function
$$m(d) = \log_{10}(d+1) - \log_{10}(d) \quad \text{ for }d \in \{1,2,\ldots,9\}.$$

```julia
using StatsBase, Plots, FileIO, DataFrames
D = DataFrame(load("cities.csv"))
D[:Population]
tallydict = # you fill in this part
sticks(1:9,collect(values(tallydict)))
```
<!-- #endregion -->




## Problem 5

A **call option** is a financial contract between two parties which grants the buyer the right, but not the obligation, to purchase a specified security at a specified price (called the **strike price**) at a specified date in the future (called the **expiration date**).

Suppose that you purchase a call option for $10$ shares of AAPL with a strike price of $\$216$ and an expiration $22$ business days from now. Suppose that the daily change in the price of AAPL is normally distributed with mean zero and standard deviation $\$8.44$, and that the changes for different days are independent.

(a) Find a function $f$ such that the call option is worth $f(P)$ dollars to you if the share price in 22 days is $P$. Draw a graph of $f$. Hint: if the price is greater than $\$216$, would you exercise the option and purchase the stock? What if it’s less than $\$216$?

(b) Find the distribution of $P$.

(c) Find the fair price of the call option, based on the above assumptions.

Notes: (1) the data in this problem are real: the current price at time of writing is $\$216$, and the daily fluctuations have had an empirical standard deviation of $\$8.44$ historically. The number of business days in a month is approximately $22$. (2) Although this problem uses finance ideas, all of the finance information you need to solve the problem is in the problem statement.

To help you with the symbolic integration, here's some code for finding the expected value of the Gaussian distribution centered at μ. 

```julia
using SymPy
@vars P σ μ positive=true
I = integrate(P*1/sqrt(2*PI*σ^2)*exp(-(P-μ)^2/(2σ^2)),(P,-oo,oo))
```

## Problem 6

Consider two random variables $X$ and $Y$ whose joint distribution has probability mass of $\frac{1}{n}$ at each of the $n$ points
$\{(x_1, y_1), \ldots, (x_n,y_n)\}$ in $\mathbb{R}^2$. Show that the covariance matrix of $X$ and $Y$ is equal to
  $$
    \frac{1}{n}\sum_{i=1}^{n}\left[\begin{smallmatrix}x_i-\overline{x}
        \\
        y_i-\overline{y}\end{smallmatrix}\right]\left[\begin{smallmatrix}
        x_i-\overline{x}
    \quad y_i-\overline{y}\end{smallmatrix} \right]. 
  $$
where $\overline{x} = (x_1+\cdots+x_n)/n$ and  $\overline{y} = (y_1+\cdots+y_n)/n$. 





## Problem 8

The *Epanechnikov* kernel is defined by
$$
    D(u) = \frac{3}{4}(1-u^2)\boldsymbol{1}_{|u| \leq 1}. 
$$
* Is $D$ continuous? Is it differentiable? Is it twice differentiable?
* Is the tri-cube weight function continuous? Is it differentiable? Is it twice differentiable? 
  
Feel free to use SymPy to perform the symbolic differentiation in this problem. 





## Problem 9

Simulate $n = 1000$ samples from the joint distribution of $X$ and $Y$, given that $X$ is uniform on $[0,1]$ and $Y = 2 + 1.2X + \epsilon$, where $\epsilon \sim \mathcal{N}(0,0.5)$. Record the integrated squared error for the Nadaraya-Watson estimator (with bandwidth selected by cross-validation) and for the line of best fit.

Notes: (1) You can approximate the integrated squared difference between two functions by evaluating the squared difference at the points of a fine-mesh grid. And (2) you'll have to write code for simulating from the joint distribution of $X$ and $Y$, but then the Nadara-Watson part you can mostly get from Data Gymnasia.





## Problem 10

* Find the variance of the uniform distribution on the interval $[0,10]$.
* Generate 10 independent samples from the uniform distribution, calculate the average $\overline{X}$ for those samples, and estimate the variance as $\widehat{V} = \frac{1}{10}\sum_{i=1}^{10} (X_i-\overline{X})^2$. Package this whole process as a function, and call it a million times to find the mean of $\widehat{V}$.
* Which is larger, the answer to (a) or the answer to (b)? Calculate the percent error. 





## Problem 11

The Student’s *t*-distribution with parameter $ν$ is the distribution of the random variable

$$\frac{\bar{X}_{n} - \mu}{S_{n}/\sqrt{n}}$$

where $n = ν + 1$, where $X_{1},...,X{n}$ is a sequence of independent $N(\mu,\sigma^{2})$’s, where $\bar{X} = \frac1n (X_{1} + ... + X_{n})$, and where $S_{n} = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}(X_{i} - \bar{X}_{n})^{2}}$

Estimate the variance of the Student’s *t*-distribution with parameter $ν = 10$ by using the above description to sample
from it $M$ times for some large $M$. Then compute the variance of the distribution which places probability mass $1/M$
at each of the simulated samples.

Look up the exact formula for the variance of the Student’s *t*-distribution on Wikipedia and check that your result is
close to the true value.



