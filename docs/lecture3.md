# Online Learning and Regret Minimization
(4/9/2025)

Previously, agents had dominant strategies. Now, what should agents do without dominant strategies or even knowledge of the game's rules? Let's explore from a single agent's perspective.

## Regret Minimization

Consider investing in stocks without knowledge of future performance:

- There are \(n\) possible actions (stocks).
- We run an algorithm over \(T\) days.
- On day \(t\), algorithm picks action \(ALG(t)\).
- Reward for action \(i\) on day \(t\) is \(r_{i,t}\), bounded by \(-1 \leq r_{i,t} \leq 1\).

Our goal: Maximize \(\sum r_{ALG(t),t}\).

**Key Idea #1:** Use historical performance to inform decisions.

<div class="definition" markdown="1">
<strong>Algorithm: Follow The Leader (FTL)</strong>

On day \(t\): Take the action with the highest total reward up to day \(t-1\).
</div>

To measure success, we use "regret":

<div class="definition" markdown="1">
<strong>Definition: External Regret</strong>

External Regret = \( \underset{i}{\max} \sum_t r_{i,t} - \sum_t r_{ALG(t),t} \)
</div>

<div class="theorem" markdown="1">
<strong>Claim 1:</strong> For independently, identically distributed (iid) rewards, FTL's expected regret is \(O(\sqrt{T \log(n)})\).
</div>

<div class="theorem" markdown="1">
<strong>Claim 2:</strong> No algorithm can outperform \(\Omega(\sqrt{T \log(n)})\) with iid rewards.
</div>

## Regret Minimization Algorithms

FTL fails under adversarial conditions. Thus, we add randomness:

**Key Idea #4:** Balance randomness with historical performance.

<div class="definition" markdown="1">
<strong>Algorithm: Follow The Regularized Leader (FTRL)</strong>

On day \(t\), choose distribution \(x\) maximizing:
\[\sum_i r_{x,t} - \frac{1}{\eta}\varphi(x)\]
- \(\eta\): Balances randomness and history.
- \(\varphi\): Regularizer penalizing unbalanced distributions.
</div>

**Alternative (equivalent) algorithm: Multiplicative Weight Update (MWU)**

<div class="definition" markdown="1">
<strong>Algorithm: Multiplicative Weight Update (MWU)</strong>

- Initialize weights \(z_{i,0} = 1\).
- At day \(t\):
  - Choose action \(i\) with probability \(\frac{z_{i,t}}{\sum_j z_{j,t}}\).
  - Update weights: \(z_{i,t+1} \leftarrow z_{i,t} e^{\eta r_{i,t}}\).
</div>

MWU and FTRL achieve expected regret \(O(\sqrt{T \log(n)})\) even with adversarial input.

## Swap-Regret Minimization Algorithms

<div class="definition" markdown="1">
<strong>Definition: Swap-Regret (Internal Regret)</strong>

Swap-Regret = \( \underset{\Phi : [n] \to [n]}{\max} \sum_t (r_{\Phi(ALG(t)),t} - r_{ALG(t),t}) \)

where \(\Phi\) maps each action to another action.
</div>

Swap-regret is always at least external regret. Minimizing swap-regret is harder but better.

<div class="definition" markdown="1">
<strong>Algorithm: Swap-Regret Minimization</strong>

- Define meta-actions for each possible swap choice \(\Phi\).
- Run MWU/FTRL on meta-actions.
- At each iteration, solve for distribution \(x_t = \mathbb{E}[\Phi(x_t)]\).

Total Swap-Regret: \(O(\sqrt{T n \log(n)})\)
</div>

## Regret Minimization with Bandit Feedback

With partial (bandit) feedback, we can't observe rewards of actions we didn't take.

<div class="definition" markdown="1">
<strong>Algorithm: UCB1 (Upper Confidence Bound)</strong>

Define: \(UCB_i = \text{avg reward}_i + \sqrt{\frac{2\ln(T)}{\text{# samples of } i}}\).

- On day \(t\), pick arm with max UCB.
</div>

With iid rewards, UCB1 regret is \(O(\sqrt{n T \log(T)})\).

<div class="definition" markdown="1">
<strong>Algorithm: Exp3 (Exponential-weight for Exploration and Exploitation)</strong>

- On day \(t\), MWU chooses an arm.
- Pseudo-rewards:
  - If arm not selected: \(\hat{r}_{i,t}=0\)
  - If arm selected: \(\hat{r}_{i,t}=\frac{r_{i,t}}{Pr[\text{selecting }i]}\) (Inverse Propensity Score)
</div>

Exp3 achieves expected regret \(O(\sqrt{n T \log(n)})\) with adversarial input.

<div class="think-pair-share" markdown="1">
**Think-Pair-Share:** Should UCB or Exp3 be used practically (e.g., news feed editor)? Consider contextual factors, clickbait, user addiction, and fake news.
</div>
