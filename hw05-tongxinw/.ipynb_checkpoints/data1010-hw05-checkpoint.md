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

# Homework 05

### Brown University  
### DATA 1010  
### Fall 2019


## Problem 1

Label each of the following four estimators as either (i) biased and
  consistent, (ii) biased and inconsistent, (iii) unbiased and
  consistent, or (iv) unbiased and inconsistent.  The matching will be
  one-to-one.

(a) $X_1, X_2, \ldots$ are i.i.d. Bernoulli random variables with
    unknown $p$ and estimator 
    $$\widehat{p} = \frac{1}{n}\sum^n_{i=1}X_i$$

(b) $X_1, X_2, \ldots$ are i.i.d. $\mathcal{N}(\mu,\sigma^2)$, with
    unknown $\mu$ and $\sigma^2$ and estimator 
    $$\widehat{\sigma}^2 = \frac{\displaystyle{\sum^n_{i=1}(X_i-\bar{X})^2}}{n}$$

(c) $X_1, X_2, \ldots$ are i.i.d. uniform random variables on an
    unknown bounded interval. For $n\geq 100$ we estimate the
    mean using
    $$\widehat{\mu} = \frac{\displaystyle{\sum^{100}_{i=1}X_i}}{100}$$
    
(d) $X_1, X_2, \ldots$ are i.i.d. $\mathcal{N}(\mu,\sigma^2)$, with
    unknown $\mu$ and $\sigma^2$. For $n\geq 100$ we estimate the
    standard deviation using
    $$\widehat{\sigma} = \sqrt{\frac{\displaystyle{\sum^{100}_{i=1}(X_i-\overline{X})^2}}{99}}$$


(a) $$\widehat{p}$$ is unbiased and consistant. 

<!-- #region -->
## Problem 2

Suppose that $X_1, \dots, X_n$ are independent
  $\mathrm{Unif}[0, \theta]$ random variables, where $\theta$ is an
  unknown parameter, and consider the
  following estimators for $\theta$: 
  $$\widehat{\theta}_1 = \max(X_1, \dots, X_n),  \qquad \widehat{\theta}_2 = 2 \cdot \frac{X_1 + \cdots + X_n}{n}$$


(a) Find the CDF of $\widehat{\theta}_1$. 

(b) Recall that if $F_{\widehat{\theta}_1}(x)$ and
    $f_{\widehat{\theta}_1}(x)$ are the CDF and PDF of
    $\widehat{\theta}_1$ respectively,
    then $
    \displaystyle{\frac{d}{dx}F_{\widehat{\theta}_1}(x) =
      f_{\widehat{\theta}_1}(x)}$.
    Differentiate your answer to (a) to find the PDF of $\widehat{\theta}_1$. 

(c) Show that $\widehat{\theta}_1$ is consistent. 

(d) Find $\mathbb{E}\left[{\widehat{\theta}_1}\right]$ and
    $\mathbb{E}\left[\widehat{\theta}_2\right].$ Which estimator is biased? 

(e) Find $\operatorname{Var}\left({\widehat{\theta}_1}\right)$ and
    $\operatorname{Var}\left(\widehat{\theta}_2\right).$ Which estimator has lower
    variance? 

(f) Show that the mean squared error of $\widehat{\theta}_1$
    is less than the mean squared error of $\widehat{\theta}_2$
    whenever $n \geq 3$. 
    
Hint: this problem is pretty calculus intensive. SymPy is your friend.
<!-- #endregion -->

## Problem 3

(a) **Hoeffding's inequality** says that if
    $Y_1, Y_2, \ldots$ are independent random variables with the
    property that $\mathbb{E}[Y_i] = 0$ and $a_i \leq Y_i \leq b_i$ for all
    $i$, then for all $\epsilon>0$ and $t > 0$, we have
    $$\mathbb{P}\left(Y_1 + Y_2 + \cdots + Y_n \geq \epsilon \right) \leq
      e^{-t \epsilon} \prod_{i=1}^n e^{t^2(b_i-a_i)^2/8}.$$
    
   Use Hoeffding's inequality to show that if $X_1, X_2, X_3, \ldots$
    is a sequence of independent $\operatorname{Bernoulli}(p)$ random
    variables, then for all $\alpha > 0$, the interval
    $\left(\overline{X}_n - \sqrt{\frac{1}{2n}\log(2/\alpha)},
      \overline{X}_n + \sqrt{\frac{1}{2n}\log(2/\alpha)}\right)$ is a
    confidence interval for $p$ with confidence level $1 -
    \alpha$. Explain what happens to the width of this confidence
    interval if $n$ gets large, and also what happens to the width
    if $\alpha$ is made very small.
    
(b) As above, consider $n$ independent
    $\operatorname{Bernoulli}(p)$'s. Find the normal-approximation
    confidence interval for $p$

(c) As above, consider $n$ independent
    $\operatorname{Bernoulli}(p)$'s. Find the Chebyshev confidence
    interval for $p$. (Chebyshev's inequality says that the probability of any random variable deviating from its mean by more than $k$ standard deviations is no more than $1/k^2$.)

(d) Find the numerical values of the half-widths for each of the
    above confidence intervals when $p = \frac{1}{2}$, $n = 1000$, and
    $\alpha = 0.05$ (approximating $\overline{X}$ as $p$). 


## Problem 4

I drew 6 observations from an undisclosed distribution and obtained the following results:
  `u = [6.19,7.048,6.143,5.459,4.603,4.335]`
  
I also drew 8 observations from another undisclosed distribution and got 
  `v = [8.924,4.698,6.095,4.223,3.643,1.624,1.444,6.309]`
  
(a) Determine whether the Wald hypothesis test (with significance $\alpha = 0.05$) rejects the null hypothesis that the mean of the two distributions are equal. 

(b) Repeat with Welch's t-test in place of the the Wald test. 

<!-- #region -->
## Problem 5

Consider a distribution $\nu$ which is known only via a dozen samples therefrom, the values of which are
```julia
    [8.924,4.698,6.095,4.223,3.643,1.624,1.444,6.309]
```

(a) Obtain a bootstrap estimate of the standard deviation of the
    median of five independent samples from $\nu$.

(b) The actual standard deviation of the median of 5 samples from
    $\nu$ is approximately 2.14. How close is the value you found?
    Could you have gotten as close as desired to this value by
    choosing sufficiently many bootstrap re-samplings?
<!-- #endregion -->

## Problem 6

Consider a population of patients who have had a recent heart attack. A randomized trial is conducted in which each patient is assigned with equal probability (and independently of any attribute of the patient) to either a heart medication regimen or a placebo. Each patient has a unknown genetic attribute $X$ which is uniformly distributed on $[0,1]$.

Suppose that the probability that a patient will comply with the regimen (that is, take the medication as prescribed) is $(1+X)/2$. The conditional probability that they will survive the following decade, given $X$ and given that they take the drug, is $3X/4$. The conditional probability that they will survive the following decade is, given $X$ and given that they do not take the drug, is $(X+1)/4$.

(a) Fill out the following tables, indicating the probability of each outcome. The eight numbers should sum to 1. 

<table>
  <tr>
    <th>Drug condition</th>
    <td>survives</td>
    <td>does not survive</td>
  </tr>
  <tr>
    <td>complaint</td>
    <td>_</td>
    <td>_</td>
  </tr>
  <tr>
    <td>non-compliant</td>
    <td>_</td>
    <td>_</td>
  </tr>
</table>
<table>
  <tr>
    <th>Placebo condition</th>
    <td>survives</td>
    <td>does not survive</td>
  </tr>
  <tr>
    <td>complaint</td>
    <td>_</td>
    <td>_</td>
  </tr>
  <tr>
    <td>non-compliant</td>
    <td>_</td>
    <td>_</td>
  </tr>
</table>

Hint: you want to work out the conditional probabilities of each event given $X$, and then find the expected value of the resulting conditional probability by integrating against the density of $X$. 

(b) Does a randomly selected patient have a higher conditional probability of surviving if they take the drug or if they do not? Does comparing the survival probabilities for the drug and placebo conditions give the correct answer to this question?

(c) Suppose you know yourself well enough to be confident that you'd be relatively unlikely to comply with a prescription regimen if you had participated in this clinical trial. Based on the given probability model, should you take the drug? Would you get the right answer or the wrong answer if you just compared the survival rates for compliant and noncompliant patients?


## Problem 7

(a) Write a function which a distribution `D`, together with an $\alpha$ value and a positive integer $n$ and returns `true` or `false` according to whether the empirical CDF for a random sample of size $n$ obeys the bound in the DKW inequality. 

(b) Run the function many times with `α = 0.05` and check that it returns `true` around 95% of the time. 

```julia
function DKW_check(D, α, n)
end
```

```julia
D = Uniform(0,1)
α = 0.05
n = 1000
mean(DKW_check(D, α, n) for _ in 1:10000)
```

## Problem 8

Consider a family of distributions of the form $\mathrm{Uniform}(\theta, \theta+1)$, where $\theta$ is a parameter. Given a sample $X_1, \ldots, X_n$, show that there isn't a unique maximum likelihood estimator for $\theta$
