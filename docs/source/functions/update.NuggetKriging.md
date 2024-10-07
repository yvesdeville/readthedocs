# `NuggetKriging::update`


## Description

Update a `NuggetKriging` model object with new points


## Usage

* Python
    ```python
    # k = NuggetKriging(...)
    k.update(y_u, X_u)
    ```
* R
    ```r
    # k = NuggetKriging(...)
    k$update(y_u, X_u)
    ```
* Matlab/Octave
    ```octave
    % k = NuggetKriging(...)
    k.update(y_u, X_u)
    ```


## Arguments

Argument      |Description
------------- |----------------
`y_u`     |     Numeric vector of new responses (output).
`X_u`     |     Numeric matrix of new input points.


## Examples

```r
f <- function(x) 1- 1 / 2 * (sin(12 * x) / (1 + x) + 2 * cos(7 * x)*x^5 + 0.7)
plot(f)
set.seed(123)
X <- as.matrix(runif(10))
y <- f(X) + 0.1 * rnorm(nrow(X))
points(X, y, col = "blue")

k <- NuggetKriging(y, X, "matern3_2")

x <- sort(c(X,seq(from = 0, to = 1, length.out = 101))) # include design points to see interpolation
p <- k$predict(x)
lines(x, p$mean, col = "blue")
polygon(c(x, rev(x)), c(p$mean - 2 * p$stdev, rev(p$mean + 2 * p$stdev)), border = NA, col = rgb(0, 0, 1, 0.2))

X_u <- as.matrix(runif(3))
y_u <- f(X_u) + 0.1 * rnorm(nrow(X_u))
points(X_u, y_u, col = "red")

## change the content of the object 'k'
k$update(y_u, X_u)

x <- sort(c(X,X_u,seq(from = 0, to = 1, length.out = 101))) # include design points to see interpolation
p2 <- k$predict(x)
lines(x, p2$mean, col = "red")
polygon(c(x, rev(x)), c(p2$mean - 2 * p2$stdev, rev(p2$mean + 2 * p2$stdev)), border = NA, col = rgb(1, 0, 0, 0.2))
```

### Results
```{literalinclude} ../functions/examples/update.NuggetKriging.md.Rout
:language: bash
```
![](../functions/examples/update.NuggetKriging.md.png)
