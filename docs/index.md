---
layout: default
title: My Page
---

# RL: Lecture 3

Backup diagram

**DIAGRAM HERE**

### IV - Optimal policies and optimal state and action value functions

A policy $\pi$ is better than a policy $\pi'$ if $\forall s$, $v_{\pi}(s) \geq v_{\pi'}(s)$

The optimal state-value function is

$$
v_{*}(s) = \max_{\pi} v_{\pi}(s), \, \forall s \in \mathcal{S}
$$

This optimal **state value** function is unique …, and there is no unique **optimal policy**

An optimal policy is such that:

$$
\pi^* \in \argmax_{\pi} v_{\pi}(s), \,\, \forall s \in \mathcal{S}
$$

The optimal action value function is:

$$
q_*(s, a) \in \argmax_{\pi} q_{\pi}(s, a), \,\, \forall s \in \mathcal{S}, \, \forall a \in \mathcal{A(s)}
$$

### ***Bellman equation for the optimal state value function***

$$
v_*(s) = \max_{a \in \mathcal{A(s)}} q_*(s, a)
$$

$$
= \max_{a \in \mathcal{A(s)}} E_{\pi^*}(G_t |S_t=s, A_t=a)
$$

$$
= \max_{a \in \mathcal{A(s)}} E_{\pi^*}(R_{t+1}+\gamma G_{t+1} |S_t=s, A_t=a)
$$

$$
= \max_{a \in \mathcal{A(s)}} E_{\pi^*}(R_{t+1}+\gamma v^*(s_{t+1}) |S_t=s, A_t=a)
$$

$$
v_*(s) = \max_{a\in \mathcal{A(s)}} \sum_{r, s'} P(s', r | s, a)(r+\gamma v_*(s)), \,\, \forall s \in \mathcal{S}
$$

**Dynamic of the Environment:**

$$
P(s', r | s, a) = P_r(s_{t+1} = s', R_{t+1}=r|S_t=s, A_t=a)
$$

### ***Bellman equation for the optimal action value function***

$$
q_*(s, a) = \sum_{s', r} P(s', r | s, a)(r+ \gamma \max_{a' \in \mathcal{A(s')}} q_*(s', a')), \,\, \forall s \in \mathcal{S}, \forall a \in \mathcal{A(s)}
$$

For the optimal state-value function, we get a system of nonlinear equations - $|\mathcal{S}|$ nonlinear equations for the action value function have $|\mathcal{S}|, |\mathcal{A}|$ nonlinear equations

Backup diagrams

**THERE IS A DIAGRAM HERE, 2 DIAGRAMS HERE.**

Assume that $q_*(s, a)$ is available. An optimal policy can be deduced from $q_*(s, a)$:

$$
\pi(s) \in \argmax_{a \in \mathcal{A(s})} q_*(s, a), \,\, \forall s \in \mathcal{S}
$$

To interact in an optimal way with the environment, one simply has to behave greedily considering $q_*(s, a)$

## Lesson 4: Tabular methods

Remember that for a policy $\pi$

$$
v_{\pi}(s) = \sum_a \pi(a|s) \sum_{s', s} P(s', r | s,a)(r + \gamma v_{\pi}(s')), \,\, \forall s
$$

$$
q_{\pi}(s, a) = \sum_{s', r} P(s', r|s, a)(r+\gamma \sum_{a'}( \pi(a'|s')q_{\pi}(s', a')) )
$$

Fixed point equation is

$$
x \in R^n, \,\,\, f: R^n \to R^n
$$

contractive function

if $f$ is contractive, i.e, $\forall x, y$

$$
|| f(x) - f(y) || < \alpha|| x-y ||, \,\, \alpha < 1
$$

Bellman equation for $v_{\pi}$ can be written as:

$$
v_{\pi} = f(v_{\pi})
$$

Where

$$
v_{\pi} = (v_{\pi}(1), \dots, v_{\pi}(|\mathcal{S}|))^T
$$

and can be shown to be contractive if $\gamma < 1$

more contractive $f$ i.e smaller $\alpha$ the faster the convergence

Then, according to **Banach fixed-point theorem**, $v_{\pi} = f(v_{\pi})$ admits a qunique solution which can be evaluated iteratively.

for evaluating $v_{\pi}(s)$ for a given policy, ew use

$$
v_{k}(s) = \sum_a \pi(a|s) \sum_{s', r}P(s', r|s, a)(r+\gamma v_{k-1}(s')), \forall s \in \mathcal{S}
$$

with $v_0(s)$ initialized arbitrary, $\forall s \in \mathcal{S}$

Policy evaluation Algorithm

```julia
v(s) arbitrary initialized, except v(terminal) = 0

```