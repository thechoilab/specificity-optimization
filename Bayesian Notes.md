# Bayesian Notes

## Lecture 1

### Overall Goals of Statistical Inference:

1. point estimation (single best value for an unknown parameter
2.  probability estimation (interval of likely values for an unknown parameter)
3. probabilty of specific hypothesis/hypothesis testing
4. prediction of future events/unobserved data

### Classical approach to statistical inference

Assume a statistical model that links observed data to a set of unknown parameters (e.g. normal model: yi (iid) ~ N(mu,sigma_squared).

-yi = observed data, mu and sigma_squared unknown parameters

theta_tilda = (nu,sigma_squared) -> theta is a set of unknown parameters (as denoted by tilda)

#### In classical statistics:

unknown parameters are **fixed values (vs bayesian = random variables)**

- With theta as fixed values, there is a natural emphasis on point estimation

How is this typically done?

Based on a probbility density function p(yi(theta))

If we have observations yi to yn, then likelihood: p(y|theta) = product from i=1 to n of p(yi|theta)

We want parameter values theta that make our observed data as likely as possible

Theta_hat = argmax(p(y|theta))

However, there is uncdrtainty in our estimated theta_hat_mle that comes from the fact that our data is a single sample out of many possible samples. How much do our point estimates change from sample to sample?

-> why "sampling distributions" are such a key concept

Classical procedures are designed to have good "long run frequency properties" (ie) procedures that do well on average across all possible samples

Of course, we typically only get to see one sample, so we need to rely on: a) asymptotic result (eg Central Limit Theorem) and b) bootstrap: simulate the sampling distribution using just a single sample

#### Disadvantages of classical approach

1. Since unknown parameters are fixed values, we cannot make direct probability statements about them
   - 95% confidence interval does NOT mean that probability of theta in the confidence interval equals .95 -- since it is a constant and not a distribution like a random variable
   - Theta is a fixed value so it either is or isn't

2. Sampling distributions are not always easy to calculate
   - Asymptotic results rely on large sample sizes, and bootstrapping doesn't save us with small smaples

### Bayesian approach to statistical inference

The fundamental concept underlying the Bayesian approach is that unknown parameters theta do not have fixed values. Rather theta_tilda are also considered random variables that each have their own probability distribution.

- Point estimation is clearly less important because we need to estimate the entire distribution of values for theta

How do we estimate the distribution of unknown theta_tilda given whatever data we have observed?

1. Our data are random variables with distribution given by our model: p(y|theta)

2. Our parameters are random variables themselves as well. So now we also need an assumed distribution for them (denote as p_theta)

With the 2 pieces above, we can use Bayes' rule to calculate the distribution of theta given data y:

Two ways to write it:

1. P(theta|y) = p(y|theta)*p(theta)/p(y)

2. P(theta|y) is proportional to p(theta)*p(y|theta)
   - (assuming p(y) is a constant) -> here p(theta) is a prior distribution
   - fixed hyperparameters govern the distribution of theta itself

We can view Bayes' rule as an updating function: we posit a prior distribution for theta (create out of thin air) and then we observe data that makes certain values of theta_tilda more likely than others.

Posterior distribution is the prior distribution but weighted by the likelihood.

- this posterior distribution can be continuously updated (it becomes the new prior in future iterations)

#### Consequences of the Bayesian Approach

1. Variability in the theta_tilda is automatically incorporated into the psoterior distribution and since theta_tilda is a random variable, we can make direct probability statements about it (e.g. P(mu is an element of (a,b)|y_tilda) = 0.95)

(eg) theta = treatment effect for a drug

Classical: hypothesis test of theta = 0 vs theta != 0

vs

Bayesian: calculates P(theta > 0|y)

2. Bayesian approach is less reliant on asymptotic results
   - no need for sample size to be large enough
   - if sample size is small, then posterior distribution just has high variance (but there could also be an issue of bias if our prior sucks)

#### Disadvantages of the Bayesian Approach

1. We need to make additional model assumptions by specifying prior distribution p(theta) in addition to our likelihood p(y|theta)
   - Having to specify a prior is a good thing in some cases when we really have prior information we want to build into our analysis
   - prior is not a big deal if we have lots of data since in this case the likelihood completely washes out the prior
   - p(theta|y) is proportional to p(y|theta)p(theta) is proportional to (productfrom i=1 to n of p(yi|theta) * p(theta)-> p(y|theta) completely dominates the function with large amounts of data

Danger zone for priors is when we don't have a lot of data and we don't have real prior information - since prior will still have quite a bit of weight here. In this case a poorly specified prior has the potential to bias our inference.

2. Estimating full posterior distribution instead of just a single set of optimal values is more difficult
   - Good computational schemes for estimating the posterior distribution

## Lecture 2

Both Bayesian and classical models use probability densities to connect observed data y_tilda to a set of unknown parameters theta_tilda. The big difference is:

Classical: theta_tilda are fixed (but unknown) values

Bayesian: theta_tilda are random variables

Considering theta_Tidlda as random variables, inference in a Bayesian analysis is based on the posterior distribution:

P(theta_tilda|y_tilda): distribution of likely parameter values given the data we've observed.

We calculate this posterior distribution using Bayes rule:

P(theta_tilda|y_tilda) = P(y_tilda|theta_tilda)*p(theta_tilda)/P(y_tilda)

P(theta) is the prior distribution: our prior belief about the relative frequency of different theta_tilda values

P(y_tilda|theta_tilda) is the likelihood: measure of how likely our observed data is for a partciular set of parameter values

P(y_tilda) is the marginal distribution of the data. (it's a function of observed data, not interesting w.r.t inference for theta_tilda)

So we often just refer to P(y_tilda) as a normalizing constant and write Bayes rule as P(theta_tilda|y) is porportional to p(y|theta)*p(theta_tilda)

Next couple classes we will be exploring simple enough models where we can calculate P(theta|y) analytically. For most Bayesian models we need to use simulation to calculate P(theta_tilda|y_tilda)

### Once we have a posterior distribution, what do we do with it?

1) Point Estimation: posterior mean: E(theta|y_tilda) = the integral of theta_tilda * p(theta_tilda|y_tilda) * d_theta

posterior mean: theta_med s.t the integral from -inf to theta_median p(theta|y) * d_theta = 0.5

posterior mode: theta_mode = argmax of theta for p(theta_tilda|y_tilda)

Variability Estimation: 

(C1,C2) is a 95% posterior interval if P(theta as an element of (c1,c2)|y_tilda) >= 0.95

- this interval conttains >= 95% of the mass of the distribution

- AKA 95% credible intervals -> the shortest interval that contains 95% of posterior probability

Var(theta_tilda|y_tilda) or SD(theta_tilda|y_tilda) is also very useful.

3. Probabilities of specific hypohteses:

   - e.g. theta = effect of a new drug

   $P(\theta>0|\tilde{y})$

4. Prediction of unobserved data y*

   - $P(\tilde{y}^{*}|\tilde{y})$ = $\int P(\tilde{y}^{*}|\tilde{\theta})*P(\tilde{\theta}|\tilde{y})* d\theta$

   - Posterior predictive distribution: takes into account variability in boh the data and unknown parameters

     vs.

   - $P(\underset{\sim}{y}^{*}|\hat{\underset{\sim}{\theta}})$
   - Does not account for variability in theta_tilda

### With these goals in mind, let's look at some simple single parameter models, where a key step is how we come up with a prior distribution.

#### Binomial Data

Connecticut vs Teal (1982):

Supreme Court case about evidence of discrimination within a particular company based on an internal test

|       | <u>Pass</u> | <u>Fail</u> | <u>Total</u> |
| ----- | ----------- | ----------- | ------------ |
| White | 206         | 53          | 259          |
| Black | 26          | 22          | 48           |

Let's focus, for now, on just modeling the success rate for Blacks

- $y_B$ = observed passes among Blacks

- $n_B$ = total test takers " "

- $\theta_B$ = probability of pass " "

Likelihood:

$y_B \sim Binomial(n_B,\theta_B)$

$p(y_B|\theta_B)$ = $n_B \choose y_B$ * ${\theta_B}^{y_B}$ * $(1-\theta_b) ^ {n_b-y_b}$

How do we specify a prior for $\theta_B$? We need a distribution with same domain as $\theta_B$ which is $(0,1)$.

One candidate is the bea distribution: $\theta_B \sim Beta(\alpha,\beta)$  -> fixed value that we have to input "hyper-parameters"

$P(\theta_B) = \cfrac{p(\alpha)p(\beta)}{p(\alpha+\beta)} * \theta_B^{\alpha-1} * (1-\theta_b)^{\beta-1}$

A particular example of hyperparameter choice would be $\alpha = \beta = 1 \Rightarrow p(\theta_\beta) = 1 \Rightarrow$ uniform $(0,1)$ density

$P(\theta_\beta|y_\beta) \propto P(y_\beta|theta_\beta)p(\theta_\beta)$

$\propto {n_\beta \choose y_\beta} *{\theta_\beta}^{y_\beta}*(1-\theta_\beta)^{n_\beta-y_\beta} * \cfrac{p(\alpha)p(\beta)}{P(\alpha+\beta)}*\theta_\beta^{\alpha-1}*(1-\theta_\beta)^{\beta-1}$

$\propto \theta_\beta^{y_\beta+\alpha-1}*(1-\theta_\beta)^{n_\beta-y_\beta+\beta-1}$

Recognize this as the same functional form as a beta distribution:

$y_\beta \sim Beta(y_\beta+\alpha,n+\beta-y_\beta+\beta)$

First example of a **conjugate prior**

### Conjugate Prior