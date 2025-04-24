# Equilibria in Games
(1/23/2023)

Previously, agents had dominant strategies. Now, we consider what happens when no dominant strategy exists.

<div class="example" markdown="1">
<strong>Example: Penalty Kicks</strong>

|            | Kick Left | Kick Right |
|------------|-----------|------------|
| Jump Left  | 0.5       | 0.8        |
| Jump Right | 0.9       | 0.2        |

No pure-strategy equilibrium exists because each player has an incentive to deviate.
</div>

**Solution:** Mixed strategies—kicker left/right (0.6, 0.4), goalie left/right (0.7, 0.3). Expected scoring probability becomes equal (0.62), providing no incentive to deviate.

<div class="definition" markdown="1">
<strong>Definition: Mixed Strategy</strong>

A probability distribution over pure strategies.
</div>

<div class="definition" markdown="1">
<strong>Definition: Nash Equilibrium</strong>

A strategy profile where no player benefits from deviating unilaterally.
</div>

## Equilibrium in 2-Player Zero-Sum Games

**Assumptions:**
- Exactly 2 players.
- Sum of payoffs is zero.

Player one aims: \(\max_{s_1} \min_{s_2} u(s_1,s_2)\)

Player two aims: \(\min_{s_2} \max_{s_1} -u(s_1,s_2)\)

<div class="theorem" markdown="1">
<strong>Theorem: Min-Max Payoffs</strong>

In two-player zero-sum games, the max-min payoff equals Nash equilibrium payoff equals min-max payoff.
</div>

<div class="definition" markdown="1">
<strong>Definition: Game Theory Terminology</strong>

- **Game Node**: State in the game.
- **Game Tree**: Graph showing reachable game nodes.
- **Information Set**: Game nodes indistinguishable given player's information.
</div>

<div class="example" markdown="1">
<strong>Example: Poker</strong>

"Heads Up" poker has \(10^{161}\) states. Approximate strategies (blueprints) and regret minimization algorithms enable practical computation.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Regret Minimization Convergence</strong>

In two-player zero-sum games, regret minimization converges to Nash equilibrium.
</div>

## Nash Equilibrium in Non-Zero-Sum Games

<div class="theorem" markdown="1">
<strong>Theorem: Nash's Existence Theorem (1951)</strong>

Every finite game has at least one Nash equilibrium (possibly mixed strategies).
</div>

**Issues:**
- Equilibria not unique.
- Hard to compute.
- May not make practical sense.

<div class="example" markdown="1">
<strong>Example: Grade Game</strong>

Two students choose grades \(x, y \in \{2,...,99\}\). Equilibrium: \(x = y = 2\).
</div>

<div class="example" markdown="1">
<strong>Example: Intersection Game</strong>

|           | Go        | Wait  |
|-----------|-----------|-------|
| **Go**    | (-99,-99) | (1,0) |
| **Wait**  | (0,1)     | (0,0) |

- Pure equilibria: (Go, Wait), (Wait, Go)
- Mixed equilibrium: small probability for simultaneous Go.
- **Correlated Equilibrium**: Randomize between (Go, Wait) and (Wait, Go).
</div>

<div class="definition" markdown="1">
<strong>Definition: Correlated Equilibrium</strong>

Players follow a correlated distribution of recommended actions. No player benefits from deviating given the recommendation.
</div>

Correlated equilibria can be efficiently computed.

<div class="definition" markdown="1">
<strong>Definition: Stackelberg Equilibrium</strong>

Strategy profile with leader committing first, follower optimally responds, and leader optimally chooses commitment.
</div>

<div class="remark" markdown="1">
Leader commitment can result in higher payoffs than correlated equilibria.
</div>

<div class="example" markdown="1">
<strong>Example: Security Games</strong>

- Airport security
- Infrastructure defense
- Cybersecurity
- Anti-poaching
</div>