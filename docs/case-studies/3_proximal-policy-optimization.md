# Proximal Policy Optimization Algorithms

Alternate between sampling data through interaction with the environment and optimize a 'surrogate' objective function using stochastic gradient ascent.

Leading reinforcement learning methods with nueral netork function approximations:

* deep Q-learning [V. Mnih, K. Kavukcuoglu, D. Silver, A. A. Rusu, J. Veness, M. G. Bellemare, A. Graves, M. Riedmiller, A. K. Fidjeland, G. Ostrovski, et al. “Human-level control through deep reinforcement learning”. In: Nature 518.7540 (2015), pp. 529–533.]
  * fails on many simple problem and  is poorly understood
* "vanilla" policy gradient method [V. Mnih, A. P. Badia, M. Mirza, A. Graves, T. P. Lillicrap, T. Harley, D. Silver, and K. Kavukcuoglu. “Asynchronous methods for deep reinforcement learning”. In: arXiv preprint arXiv:1602.01783 (2016).]
  * poor data effciency and robustness
* trust region / natural policy gradient methods. [J. Schulman, S. Levine, P. Moritz, M. I. Jordan, and P. Abbeel. “Trust region policy optimization”. In: CoRR, abs/1502.05477 (2015).]
  * relatively complicated, not compatible with architecture that include noise (such as dropout) or parameter sharing between policy and value function, or with auxiliary tasks

## Background

### 1 Policy Gradient Method

Policy gradient method: compute estimator of policy gradient and then stochastic gradient ascent. Common gradient estimator:

$$
\hat{g} = \hat{\mathbb{E}}_t \left[ \nabla_{\theta} \log \pi_{\theta}(a_t \mid s_t) \hat{A}_t \right]

$$


| Symbol                                            | Meaning                                                | Intuition                                                                                                                                                                                                                                                     |
| :-------------------------------------------------- | :------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $\hat{g}$                                         | **Estimated policy gradient**                          | The average gradient used to update the policy parameters. It’s what we compute to perform a gradient ascent step in policy optimization.                                                                                                                    |
| $\hat{\mathbb{E}}_t[\cdot]$                       | **Empirical expectation over time steps (or samples)** | The expectation is usually approximated by sampling trajectories from the policy. The hat ( (\hat{}) ) indicates it’s a*sample-based estimate* rather than the true expectation.                                                                             |
| $\nabla_{\theta} \log \pi_{\theta}(a_t \mid s_t)$ | **Score function (policy gradient term)**              | Measures how changing the parameters ( \theta ) would increase or decrease the log-probability of taking action ( a_t ) in state ( s_t ). This is the “direction” in parameter space that increases the likelihood of actions that led to good outcomes.    |
| $\pi_{\theta}(a_t \mid s_t)$                      | **Stochastic policy**                                  | The probability distribution (parameterized by ( \theta )) over possible actions given the state ( s_t ). For example, a Gaussian in continuous control, or a softmax over discrete actions.                                                                  |
| $a_t, s_t$                                        | **Action and state at time ( t )**                     | The agent’s interaction with the environment — ( a_t ) is sampled from ( \pi_\theta(\cdot \mid s_t) ).                                                                                                                                                      |
| $\hat{A}_t $                                      | **Estimated advantage function**                       | Measures how much better an action ( a_t ) was compared to the expected value of the state ( s_t ). It “centers” the returns so that actions better than expected get positive weight and worse ones get negative weight. Commonly estimated as:  A = R - V |

When using automatic differentiaion software (e.g. PyTorch), usually construct a objective function that its differential is the estimator $\hat{g}$, so estimator can be calculated by differentiate:

$$
L^{PG}(\theta) = \hat{\mathbb{E_t}} [ \log \pi_\theta(a_t | s_t) \hat{A}_t ]

$$


| 阶段                         | 做什么                                | 对应概念               |
| :----------------------------- | :-------------------------------------- | :----------------------- |
| ①**Rollout**                | 用当前策略与环境交互，收集 (s, a, r)  | 采样数据               |
| ②**Compute Advantage**      | 从奖励计算 (\hat{A}_t)                | 衡量行动好坏           |
| ③**Policy Gradient Update** | 用 (\nabla_\theta \log \pi_\theta(a_t | s_t)\hat{A}_t) 更新 θ |
| ④**Repeat**                 | 新策略再去环境采样新的 rollouts       | 下一轮迭代             |

### 2 Trust Region method

An objective function ("surrogate" objective) is maximized subject to a constraint on the size of the policy update.

$$
maximize\_{\theta} \; \hat{\mathbb{E}}_t 
\left[
\frac{\pi_{\theta}(a_t \mid s_t)}{\pi_{\theta_{\text{old}}}(a_t \mid s_t)} 
\hat{A}_t
\right]
\\
\text{subject to } 
\hat{\mathbb{E}}_t
\left[
\mathrm{KL}\!\left[\pi_{\theta_{\text{old}}}(\cdot \mid s_t), 
\pi_{\theta}(\cdot \mid s_t)\right]
\right]
\le \delta
\tag{4}
$$

here $\theta_{old}$ is the vector of policy parameter before the update. Can be efficiently solved using conjugate gradient algorithm, with a linear approximation to objective and quadratic approximation to constraint. 

> 基本上就是对 policy gradient 做了 first order approximation, 然后为了防止 update 太大加了个每次 update 的 step 大小限制. 

## 3 Proximal Policy Optimzation - Clipped Surrogate Objective


## References

> J. Schulman, F. Wolski, P. Dhariwal, A. Radford, and O. Klimov. Proximal policy optimization algorithms. arXiv preprint arXiv:1707.06347, 2017.
> J. Schulman. Approximating kl divergence, 2020. URL http://joschu.net/blog/kl-app rox.html.
> J. Schulman, P. Moritz, S. Levine, M. Jordan, and P. Abbeel. High-dimensional continuous control using generalized advantage estimation. arXiv preprint arXiv:1506.02438, 2015.

## Keywords

Scalable: scalable to large models and parallel implementations
data efficient:
robustness: i.e., successful on a variety of problems without hyperparameter tuning
