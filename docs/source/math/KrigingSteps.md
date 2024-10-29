(SecSteps)=
# Kriging steps

Kriging models can be used in different steps depending on the goal.

* **Trend estimation** If only the trend parameters $\beta_k$ are
  unknown, these can be estimated by [Generalized Least
  Squares](SecGLS). This step separates the observed response $y_i$
  into a trend and component $\widehat{\mu}(\m{x}_i)$ a non-trend
  component. The non-trend component involves a smooth GP component
  $\widehat{\zeta}(\m{x}_i)$ and, optionally, a nugget or noise
  component $\widehat{\varepsilon}(\m{x}_i)$ or
  $\widehat{\varepsilon}_i$.
  
* **Fit** Find estimates of the parameters, including the covariance
  parameters. Several methods are implemented, all relying on the
  *optimization* of a function of the [covariance
  parameters](SecParam) called the *objective*. This objective can
  relates to frequentist estimation methods:
  [Maximum-Likelihood](SecMLE) (ML) and [Leave-One-Out](SecLOO)
  Cross-Validation. It can also be a Bayesian [Marginal Posterior
  Density](SecBayes), in relation with specific priors, in which case
  the estimate will be a Maximum A Posteriori (MAP). Mind that in
  **libKriging** only *point estimates* will be given for the
  correlation parameters.

* **Update** Update a model object by processing $n'$ new
  observations.  Once this step is achieved, the predictions will be
  based on the full set of $n + n'$ observations. The covariance
  parameters can optionally be updated by using the new observations
  when computing the fitting objective.

* **Predict** Given $n^\star$ "new" inputs $\m{x}^\star_i$
  forming the rows of a matrix $\m{X}^\star$, compute the
  Gaussian distribution of $\m{y}^\star$ conditional on
  $\m{y}$. As long as the covariance parameters are regarded as
  known, the conditional distribution is Gaussian, and is
  characterized by its expectation vector and its covariance
  matrix. These are often called the *Kriging mean* and the *Kriging
  covariance*.

* **Simulate** Given $n^\star$ "new" inputs $\m{x}^{\star}$
  forming the rows of a matrix $\m{X}^\star$, draw a sample of
  $n_{\texttt{sim}}$ vectors $\m{y}^{\star[k]}$, $k=1$, $\dots$,
  $n_{\texttt{sim}}$ from the distribution of $\m{y}^\star$
  conditional on the observations.
  
* **Update simulations**. Given simulations $\m{y}^{\star[k]}$ for a
  simulation design $\m{X}^\star$, assume that the vector of
  conditioning observations can be enriched by some "update"
  observations $\m{y}'$ corresponding to an "update" design
  $\m{X}'$. Update the existing simulations so that they become
  conditional on $\m{y}$ and on $\m{y}'$. 
  See [Updating model objects and simulations](SecUpdate)
  
These steps can be achieved by using a method implemented in
**libKriging**, such as `fit`, `predict`, `update`, ... These methods
are implemented for each of the three classes of [Kriging
models](SecKrigingModels).
  
By "Kriging" one often means the prediction step. The fit step is
generally the most costly one in terms of computation because the fit
objective has to be evaluated repeatedly (say dozens of times) and
each evaluation involves $O(n^3)$ elementary operations.
