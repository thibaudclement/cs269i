# Online Learning and Regret Minimization
(4/9/2025)

So far in this class, agents had dominant strategies, such as doctor reporting their true preferences in DA, so we had a good guess of what they should do. However, what should agents do without dominant strategies or even knowledge of the game's rules? In other words, what should selfish agents do when the mechanism is not strategyproof, and possibly not fully specified? Let's explore this question from a single agent's perspective.

## Regret Minimization

If we know which stocks are going to go up and down, we should buy the stocks that are going to go up and sell them before they are going to go down. But what do we do when we don’t know that? We want an algorithm that will explain how to invest well in the stock market First, we will try to use historical performance of stocks to determine what to do tomorrow.

<div class="example" markdown="1">
**Scenario 1:** Consider investing in stocks without knowledge of future performance:

- There are \(n\) possible actions (stocks).
- We run an algorithm over \(T\) days.
- On day \(t\), the algorithm picks action \(ALG(t)\).
- Reward for action \(i\) on day \(t\) is \(r_{i,t}\), bounded by \(-1 \leq r_{i,t} \leq 1\).

Our goal is to maximize the sum of the rewards of the actions the algorithm chooses, namely \(\sum r_{ALG(t),t}\).
</div>

<div class="remark" markdown="1">
**Key Idea #1:** Use historical performance to inform decisions.
</div>

A pretty natural guess is to try a greedy algorithm, called **Follow The Leader**, where on every day, we just take the action that has generated the most reward so far.

<div class="definition" markdown="1">
<strong>Algorithm: Follow The Leader (FTL)</strong>

On day \(t\): Take the action with the highest total reward up to day \(t-1\). Break ties arbitrarily.
</div>

How can we reason about whether this first idea is a good idea or not? We measure the success of online learning algorithms in terms of **regret**. Our benchmark is a fixed action over time: we are comparing with the best stock overall, not the best stock every single day. The intuition is that, if the algorithm has low regret, then we are doing almost as well as the best stock.

<div class="definition" markdown="1">
<strong>Definition: External Regret</strong>

External Regret = \( \underset{i}{\max} \underset{t}{\sum} r_{i,t} - \underset{t}{\sum} r_{ALG(t),t} \)
</div>

**Question: Can regret be negative?** Yes! That is a fantastic case, when we are doing better than the best stock.

So, is FTL (i.e. the greedy algorithm that takes the best action every time) a good idea?

<div class="theorem" markdown="1">
<strong>Claim 1:</strong> For independently, identically distributed (iid) rewards, FTL's expected regret is \(O(\sqrt{T \log(n)})\).
</div>

In other words, if, for each action, the rewards on different days are **independently, identically distributed**, aka **iid** (i.e. every day, the rewards are drawn from the same distribution—some stocks tend to do better, some stocks tend to do worse), then FTL has an expected regret in the order of \(O(\sqrt{T \log(n)})\).

**What does this mean?** It means that, as long as \(T\) is much bigger than \(\log(n)\), the whole thing inside the square root is going to be less than \(T^2\) (because \(\log(n)\) is less than \(T\), so \(T \log(n)\) is less than \(T \cdot T\), so the whole thing is less than \(T^2\).

Regret is less than 1 on average, so regret is less than the number of days, and regret per day is diminishing (going to 0).

For instance, the NYSE only lists 2,000 companies, and \(\log(2000) \approx 11\), so it takes about \(11\) days to start doing as well as the best stock on the NYSE (we can replace \(11\) days with \(11\) seconds if we are trading really fast).

<div class="theorem" markdown="1">
<strong>Claim 2:</strong> No algorithm can outperform \(\Omega(\sqrt{T \log(n)})\) with iid rewards.
</div>

**Why is this claim true?**

Let’s assume that the reward for every action, every day, is just a random coin flip (\(+1\) or \(-1\)), completely independently at random. So, in any algorithm based on history, the next choice is going to be a random coin flip.

However, if we have \(n\) actions, one of them is going to do a little bit better than average (each one has a \(50/50\) expectation, but one of them is going to be a little bit better than average). If we do the math of how much better than average it is going to be, it comes out to roughly this magic number of \(O(\sqrt{T \log(n)})\).

The number \(O(\sqrt{T \log(n)})\) itself is not super important. However, the intuition is that it is the right bound: \(O(\sqrt{T \log(n)})\) converges very fast, and as long as \(T\) is much bigger than \(\log(n)\). Since \(\log(n)\) is a tiny number, the algorithm is doing really well.

<div class="remark" markdown="1">
**Key Idea #2:** External regret is the difference between the algorithm's total reward and the reward from the single best-in-hindsight action, i.e. 

External Regret = \( \underset{i}{\max} \underset{t}{\sum} r_{i,t} - \underset{t}{\sum} r_{ALG(t),t} \).
</div>

## Regret Minimization Algorithms

So, we are doing almost as well as the best stock. The catch is that the stock market is not iid: the stocks may go up one day, two days, three days, but they can only go up so much.

In an adversarial context, it is as if someone is trying to make it hard for us. FTL does not do well with adversarial input. In fact, no deterministic algorithm does well with adversarial input.

<div class="remark" markdown="1">
**Key Idea #3:** To minimize regret in an adversarial context, we introduce randomness in the algorithm.
</div>

However, choosing actions uniformly at random may also be a bad idea, because some actions are consistently worse than others.

<div class="remark" markdown="1">
**Key Idea #4:** We need an algorithm with a good balance between having enough randomness and paying attention to historical performance.
</div>

One idea to minimize regret is to pick a distribution of actions rather than a pure action.

<div class="definition" markdown="1">
<strong>Algorithm: Follow The Regularized Leader (FTRL)</strong>

On day \(t\), choose distribution \(x\) maximizing \(\underset{t}{\sum} (r_{x,t} - \frac{1}{\eta}\varphi(x))\) where:

- \(r_{x,t}\) provides the historical performance,
- \(\eta\) balances randomness and history,
- \(\varphi\) is the regularizer, which penalizes unbalanced distributions.
</div>

**How does \(\varphi\) work?** \(\varphi\) is a (usually convex) function that “penalizes” unbalanced distributions. For instance, if we have a distribution that puts all the weight on one stock, then \(\varphi\) is going to determine that it is a bad distribution and give it a bad score. We can pick different functions that are going to give different performance.

Now, let's consider another famous algorithm.

<div class="definition" markdown="1">
<strong>Algorithm: Multiplicative Weight Update (MWU)</strong>

- Initialize weights \(z_{i,0} = 1\) for all \(i\).
- At day \(t\):
    - Choose action \(i\) with probability \(\frac{z_{i,t}}{\underset{j}{\sum} z_{j,t}}\).
    - Update weights: \(z_{i,t+1} \leftarrow z_{i,t} e^{\eta r_{i,t}}\).
</div>

The idea is that, at the beginning, all the weights are going to be 1. Each day, we are going to choose an action with a probability proportional to the weight. Then, there are updates: we multiply the weight of each action by the reward the the action got. If an action got a big positive reward, we are multiplying its weight by a big number, and its weight next time is going to be bigger. If an action got a small or negative reward, we are multiplying its weight by a small number, and its weight next time is going to be smaller.

\(\eta\) is called “learning rate”. It is a parameter that balances between randomness and FTRL:

- If we have a higher \(\eta\), it is putting a lot of weight into learning really fast (fitting to historical performance).
- If we have a smaller \(\eta\), we are staying very close for a long time to the original distribution, which is uniform over all actions, so it is more random.

Although we are not going to prove this claim in lecture, it turns out that this Multiplicative weight update (MWU) algorithm is the same as FTL when using the entropy regularizer.

<div class="theorem" markdown="1">
<strong>Claim:</strong> MWU = FTRL with entropy regularizer \(\varphi(x) = - \sum x_i \log(x_i) \).
</div>

The point is that these are two ways to look at the same algorithm, trying to balance randomness and historical performance to avoid an adversarial example.

<div class="theorem" markdown="1">
<strong>Theorem:</strong> MWU and FTRL achieve expected regret \(O(\sqrt{T \log(n)})\).
</div>

This is optimal, even against adversarial input. As long as the adversary does not know the inside randomness of the algorithm, this algorithm is completely adversary proof.

## Swap-Regret Minimization Algorithms

So far, we have formalized the idea of measuring online algorithms with regret, and we have seen actual optimal algorithms that minimize regret even against very adversarial input. However, what happens if there is an adversary who can look at our algorithm’s choices, and use that to do better than us? This is embarrassing: how can avoid that?

In Judo, winning is not about our own strength, but about using our opponent’s strength to make them fall over. Similarly, in the stock market, winning is not about knowing the market ourselves, but instead using oour opponent’s power to beat them.

<div class="definition" markdown="1">
<strong>Definition: Swap-Regret (Internal Regret)</strong>

Swap-Regret = \( \underset{\Phi : [n] \to [n]}{\max} \underset{t}{\sum} (r_{\Phi(ALG(t)),t} - r_{ALG(t),t}) \) where \(\Phi\) maps each action to another action.
</div>

In the context of external regret, our algorithm was just competing with the best single action (i.e. the best stock). In the context of swap regret, our algorithm has to compete with a friend, who is seeing what our algorithm is recommending, and using that to do something else.

**How is the swap function determined?** We are taking the best of all possible swap functions?

**Between external regret and swap regret, which one is higher?** The swap regret is always at least as high as the external regret.

**Which kind of regret is it better to minimize?** It is better to minimize swap regret.

One way to see this is that we can have everything mapping to the same action (i.e. the best action in hindsight) in the swap function. So, if we can minimize the swap regret, it is better, although it is also much harder because the benchmark is more complex.

**Why don’t we use the best possible scenario to calculate regret?** Indeed, another benchmark we can use is the best action each day (rather than the best action overall). The benchmark is just too high. For instance, if everyday we are playing a game where we flip a coin, and we need to determine whether it is going to be head or tail, there is no good algorithm for this, it is helpless.

We saw that, for external regret, there is an algorithm that can do as well as the best stock, even with adversarial input. It turns out that with swap regret, there is also a pretty good algorithm.

<div class="definition" markdown="1">
<strong>Algorithm: Swap-Regret Minimization</strong>

- Define meta-actions for each possible swap choice \(\Phi\).
- Run MWU/FTRL on meta-actions.
- At each iteration, solve for distribution \(x_t = \mathbb{E}[\Phi(x_t)]\).
</div>

<div class="theorem" markdown="1">
<strong>Claim:</strong> The Total Swap-Regret is in the order of \(O(\sqrt{T n \log(n)})\)\).
</div>

The total swap regret looks like the external regret, except that instead of \(n\) action, we have to take the \(\log\) of \(n^n\) actions. This is a higher regret, so it is going to take more time to achieve vanishing regret.

For instance, if we think about the NYSE, with 2,000 actions, instead of \(\log(2000) \approx 11\), it is going to be \(\log(2000^{2000})\), which is \(\log(2000) \cdot 2000 \approx 11 \cdot 2000 \approx 22000\).

So, for instance, if \(T\) is in days, it is going to take \(60\) years for the swap to beat the entire stock exchange, but if we are talking in seconds, then \(22000\) seconds is not very long (about \(6\) hours).

## Regret Minimization with Bandit Feedback

<div class="example" markdown="1">
**Scenario 2:** Consider a new portal/feed editor:

- We run an algorithm over \(T\) days.
- There are \(n\) possible "arms" (i.e. actions), where an "arm" is a news category or a reporter, for instance.
- On the \(t\)-th day, a user comes, and we can show them one news item.
- The reward \(r_{i,t}\) measures how long the user engaged with the news item.

Our goal is to minimize regret, namely \(\underset{i}{max} \underset{t}{\sum}(r_{i,t} - r_{ALG(t),t})\).
</div>

**Challenge:** With partial (bandit) feedback, we see how long a user engaged with what we showed them, but we don’t know long the user would have engaged with the content we did not show them. Yet, we still have to compete with all the other actions.

**Solution:** We need to arbitrate how much we want to learn about how each arm is doing (i.e. exploration) and how much we want to extract reward from the best arm (i.e. exploitation).

<div class="remark" markdown="1">
<strong>Key Idea #5:</strong> To account for bandit/partial feedback, we may apply a similar regret minimization framework, with a trade-off between exploration and exploitation.
</div>

<div class="definition" markdown="1">
<strong>Mechanism: Multi-Armed Bandit Model Warm-Up Algorithm</strong>

- Try all possible arms to see which one yields the best reward.
- Keep pulling on the best arm identified.
</div>

This approach works well if rewards are fixed (e.g., one arm consistently rewards highly). However, it struggles with randomness, leading to potential overfitting.

How much exploration is needed? By the **Law of Large Numbers**, the average reward converges to the expectation over time. **Concentration Inequalities** quantify this convergence rate.

Using the Hoeffding Inequality:

\[
Pr\left[\text{expectation} > \text{average of samples} + \sqrt{\frac{X}{\text{number of samples}}}\right] < e^{-2X}
\]

To ensure confidence across $T$ iterations:

\[
Pr\left[\text{expectation} > \text{average of samples} + \sqrt{\frac{2\ln(T)}{\text{number of samples}}}\right] < \frac{1}{T^4}
\]

By setting $X = 2\ln(T)$, we derive an **Upper Confidence Bound (UCB)**. This ensures minimal mistakes over the algorithm's runtime.

<div class="definition" markdown="1">
<strong>Mechanism: UCB1 Algorithm</strong>

Let \(\text{UCB}_i = \text{(average of $i$'s samples)} + \sqrt{\frac{2\ln(T)}{\text{number of $i$'s samples}}}\).

On day \(t\):

- Compute UCB for each arm.
- Pull the arm with the maximum UCB (breaking ties randomly).
</div>

This greedy algorithm balances exploration and exploitation:

- **Under-explored arms** (few samples) have a high exploration incentive.
- **High-performing arms** (high averages) encourage exploitation.

The expected regret under iid rewards (between -1 and 1) is in the order of \(O(\sqrt{nT\log(T)})\) as long as \(T > n\log(n)\), which is not as good as full feedback scenarios remains but reasonable for bandit feedback.

In other words:

- **Good:** Regret per day approaches 0 if \(T > n\log(n)\).
- **Bad:** Not as optimal as full feedback.
- **Ugly:** Requires iid rewards.

**Caveat:** Because UCB1 is a greedy, deterministic algorithm (with no randomness), we can construct an adversarial input.

Let's explore another algorithm that works for bandit feedback AND against an adversarial input. The idea is to use MWU again. The challenge is that in MWU, every time we want to update the weights of the actions, we need to know the rewards, but we don’t have the rewards. Instead, we are going to feed the algorithm pseudo-rewards, something that is going to replace the reward and hopefully work as well as the reward.

<div class="definition" markdown="1">
<strong>Mechanism: Exp3 Algorithm</strong>

On day \(t\):

- MWU selects an arm.
- Define pseudo-rewards:
    - If arm \(i\) is not selected: \(\hat{r}_{i,t} = 0\).
    - If arm \(i\) is selected: \(\hat{r}_{i,t} = \frac{r_{i,t}}{Pr[\text{selecting } i]}\).
</div>

**Pseudo-reward rationale:**

- Unselected actions yield zero (unknown) rewards.
- Selected actions are scaled to compensate selection probability, ensuring unbiased estimates (**Inverse Propensity Score**).

<div class="remark" markdown="1">
**Key Idea #6:** The Inverse Propensity Score means that \(\hat{r}_{i,t}\) is an unbiased estimator, i.e. \(\mathbb{E}[\hat{r}_{i,t}] = \mathbb{E}[{r}_{i,t}]\).
</div>

The expected regret for Exp3 is \(O(\sqrt{nT\log(n)})\), slightly worse than MWU with full feedback (i.e. \(O(\sqrt{T\log(n)})\), though better algorithms exist to reduce variance.

## Recap

<div class="summary" markdown="1">
<strong>Key Ideas</strong>

- **Key Idea #1:** Use historical performance to forecast the future.
- **Key Idea #2:** Use regret to measure the success of algorithms.
- **Key Idea #3:** Use randomness as safety against adversarial inputs.
- **Key Idea #4:** Balance randomness and optimization.
- **Key Idea #5:** Balance exploration and exploitation.
- **Key Idea #6:** Use unbiased estimates of rewards.
</div>
