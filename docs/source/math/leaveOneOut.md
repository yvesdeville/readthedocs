(SecLOO)=
# Leave-one-out

Consider $n$ observations $y_i$ from a Kriging model corresponding to
the "`Kriging`" case with no nugget or noise.  For $i=1$, $\dots$, $n$
let $\widehat{y}_{i|-i}$ be the prediction of $y_i$ based on the
vector $\m{y}_{-i}$ obtained by omitting the observation $i$ in
$\m{y}$. The vector of *leave-one-out* (LOO) predictions is
defined by

$$
  \widehat{\m{y}}_{\mathtt{LOO}} :=
  [ \widehat{y}_{1|-1}, \dots, \,  \widehat{y}_{n|-n} ]^\top,
$$

and the leave-one-out Sum of Square Errors criterion is defined by

$$
  \texttt{SSE}_{\texttt{LOO}} :=
  \sum_{i=1}^n \{ y_i - \widehat{y}_{i|-i} \}^2 =
  \| \m{y} - \widehat{\m{y}}_{\texttt{LOO}} \|^2.
$$

It can be shown that

$$ 
\m{y} - \widehat{\m{y}}_{\texttt{LOO}} =
\m{D}_{\m{B}}^{-1}\m{B}\,\m{y} 
$$ 

where $\m{B}$ is the [Bending Energy Matrix](SecBending) (BEM)
and $\m{D}_{\m{B}}$ is the diagonal matrix with the same
diagonal as $\m{B}$.

By minimizing $\texttt{SSE}_{\texttt{LOO}}$ with respect to the
covariance parameters $\theta_\ell$ we get estimates of these. Note
that similarly to the profile likelihood, the LOO MSE does not depend
on the vector $\bs{\beta}$ of trend parameters.

An estimate of the GP variance $\sigma^2$ is given by

$$
   \widehat{\sigma}^2_{\texttt{LOO}} = 
   \frac{1}{n} \, \m{y}^\top \mathring{\m{B}} 
   \m{D}_{\mathring{\m{B}}}^{-1} 
   \mathring{\m{B}} \m{y}
$$

where $\mathring{\m{B}}:= \sigma^2 \m{B}$ does not depend on
$\sigma^2$ and $\m{D}_{\mathring{\m{B}}}$ is the diagonal
matrix having the same diagonal as $\mathring{\m{B}}$.

The LOO estimation can be preferable to the maximum-likelihood
estimation when the covariance kernel is mispecified, see
{cite:t}`Bachoc_ParametricCov` who provides many details on the
criterion $\texttt{SSE}_{\texttt{LOO}}$, including its derivatives.
