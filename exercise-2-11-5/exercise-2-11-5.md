
# Exercise 2.11.5
> Posterior distribution as compromise between information and data:
> let $y$ be the number of heads in $n$ spins of a coin, whose probability of heads is $\theta$.
>
> (a). If your prior distribution for $\theta$ is uniform on the range $[0,1]$, derive your prior predictive distribution for $y$,
>
>$$
Pr(y=k) = \int_0^1 Pr(y=k|\theta)d\theta,
$$
> for each $k=0,1,ldots,n.$
>
> (b) Suppose you assign a $\text{Beta}(\alpha, \beta)$ prior distribution for $\theta$, and then you observe $y$ heads out of $n$ spins. Show algebraically that your posterior mean of $\theta$ always lies between your prior mean, $\frac{\alpha}{\alpha + \beta}$ and the observed relative frequency of heads, $\frac{y}{n}$.
>
> (c) Show that, if the prior distribution on $\theta$ is uniform, the posterior variance of $\theta$ is always less than the prior variance.
>
> (d) Give an example of a $\text{Beta}(\alpha, \beta)$ prior distribution and data $y, n$, in which the posterior variance of $\theta$ is higher than the prior variance.

# Derive prior predictive distribution
From equation 2.5, we know that 

$$
\begin{array}{ll}
Pr(y=k) & = \int_0^1 Pr(y=k|\theta)d\theta \\
        & = \int_0^1 \binom{n}{y} \theta ^ y (1 - \theta)^{n-y}d\theta \\
        & = \frac{1}{n+1}
\end{array}

$$


# Examine simulation for given n over uniform $\theta$
The following simulation agrees with the simulation above.
the simulation 

* draws observations from a binomial distribution over a grid of values of $\theta$ from 0 to 1 for various values of $n$,
* summarises the proportions of each $k$ in the sample,
* compares this to the exact value based on the formula above.



```r
simulate_binom <- function(n) {
    y <- rbinom(1e+06, n, seq(0, 1, length.out = 1000))
    Props <- round(prop.table(table(y)), 3)
    Exact <- round(1/(n + 1), 3)
    list(Props = Props, n = n, Exact = Exact)
}

simulate_binom(4)
```



```
## $Props
## y
##     0     1     2     3     4 
## 0.200 0.199 0.200 0.200 0.200 
## 
## $n
## [1] 4
## 
## $Exact
## [1] 0.2
## 
```



```r
simulate_binom(9)
```



```
## $Props
## y
##     0     1     2     3     4     5     6     7     8     9 
## 0.100 0.100 0.100 0.100 0.100 0.100 0.099 0.100 0.100 0.100 
## 
## $n
## [1] 9
## 
## $Exact
## [1] 0.1
## 
```



```r
simulate_binom(19)
```



```
## $Props
## y
##     0     1     2     3     4     5     6     7     8     9    10    11 
## 0.050 0.050 0.050 0.050 0.050 0.050 0.050 0.050 0.050 0.050 0.050 0.050 
##    12    13    14    15    16    17    18    19 
## 0.050 0.050 0.050 0.050 0.050 0.050 0.050 0.051 
## 
## $n
## [1] 19
## 
## $Exact
## [1] 0.05
## 
```


