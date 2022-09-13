# `NuggetKriging::logLikelihood`


## Description

Get logLikelihood of NuggetKriging Model


## Usage

* Python
    ```python
    # k = NuggetKriging(...)
    k.logLikelihood()
    ```
* R
    ```rlibKriging
    k$logLikelihood()
    ```
* Matlab/Octave
    ```octave
    % k = NuggetKriging(...)
    k.logLikelihood()
    ```


## Value

The logLikelihood computed for fitted
  $theta$.


## Examples

```r
f <- function(x) 1 - 1 / 2 * (sin(12 * x) / (1 + x) + 2 * cos(7 * x) * x^5 + 0.7)
set.seed(123)
X <- as.matrix(runif(5))
y <- f(X) + 0.01*rnorm(nrow(X))
r <- NuggetKriging(y, X, kernel = "gauss")
print(r)
logLikelihood(r)
```

### Results
```{literalinclude} ../examples/logLikelihood.NuggetKriging.md.Rout
:language: bash
```
![](../examples/logLikelihood.NuggetKriging.md.png)


## Reference

* Code: <https://github.com/libKriging/libKriging/blob/master/src/lib/NuggetKriging.cpp#L94>