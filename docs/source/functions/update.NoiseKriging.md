# `NoiseKriging::update`


## Description

Update a `NoiseKriging` model object with new points


## Usage

* Python
    ```python
    # k = NoiseKriging(...)
    k.update(newy, newnoise, newX)
    ```
* R
    ```r
    # k = NoiseKriging(...)
    k$update(newy, newnoise, newX)
    ```
* Matlab/Octave
    ```octave
    % k = NoiseKriging(...)
    k.update(newy, newnoise, newX)
    ```


## Arguments

Argument      |Description
------------- |----------------
`newy`     |     Numeric vector of new responses (output).
`newnoise`     |     Numeric vector of new noise variances (output).
`newX`     |     Numeric matrix of new input points.


## Examples

```r
f <- function(x) 1- 1 / 2 * (sin(12 * x) / (1 + x) + 2 * cos(7 * x)*x^5 + 0.7)
plot(f)
set.seed(123)
X <- as.matrix(runif(5))
y <- f(X) + 0.1*rnorm(nrow(X))
points(X, y, col = "blue")
KrigObj <- NoiseKriging(y, rep(0.1^2,5), X, "gauss")
x <- seq(from = 0, to = 1, length.out = 101)
p_x <- predict(KrigObj, x)
lines(x, p_x$mean, col = "blue")
lines(x, p_x$mean - 2 * p_x$stdev, col = "blue")
lines(x, p_x$mean + 2 * p_x$stdev, col = "blue")
newX <- as.matrix(runif(3))
newy <- f(newX) + 0.1*rnorm(nrow(newX))
points(newX, newy, col = "red")

## change the content of the object 'KrigObj'
update(KrigObj, newy, rep(0.1^2,3), newX)
x <- seq(from = 0, to = 1, length.out = 101)
p2_x <- predict(KrigObj, x)
lines(x, p2_x$mean, col = "red")
lines(x, p2_x$mean - 2 * p2_x$stdev, col = "red")
lines(x, p2_x$mean + 2 * p2_x$stdev, col = "red")
```

### Results
```{literalinclude} ../examples/update.NoiseKriging.md.Rout
:language: bash
```
![](../examples/update.NoiseKriging.md.png)