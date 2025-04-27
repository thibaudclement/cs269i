# Equilibria in Games
(4/14/2025)

Last time, we explored what selfish agents should do when the mechanism is not strategyproof, and possibly not fully specified, from a single agent's perspective. Now, let's analyze systems with multiple agents. This serves as an introduction to game theory.

<div class="example" markdown="1">
<strong>Example: The Penalty Kick Game</strong>

Consider the scenario of a penalty kick between Messi (kicker) and Lloris (goalie), where the probability of goal is defined as follows:

|                | Kick Left | Kick Right |
|----------------|-----------|------------|
| **Jump Left**  | 0.5       | 0.8        |
| **Jump Right** | 0.9       | 0.2        |

**Questions:**

- Where should Messi kick?
- Where should Lloris jump?

</div>

Lloris does not know which direction Messi is going to kick—and needs to think about it. Messi does not know which direction Lloris is going to jump—and needs to think about it.

The answer is not obvious, but Game Theory tells us:

- Messi should kick left with probability 0.6 and right with probability 0.4.
- Lloris should jump left with probability 0.7 and right with probability 0.3.
- The probability of goal is 0.62.

More specifically:

- When Messi kicks left, there is a \(0.5 \cdot 0.7 + 0.9 \cdot 0.3 = 0.62\)  probability of goal.
- When Messi kicks right, there is a \(0.8 \cdot 0.7 + 0.2 \cdot 0.3 = 0.62\) probability of goal, too.
- When Lloris jumps left, there is a \(0.5 \cdot 06 + 0.8 \cdot 0.4 = 0.62\) probability of goal.
- When Lloris jumps right, there is a \(0.9 \cdot 0.6 + 0.2 \cdot 0.4 = 0.62\) probability of goal, too.

This is called a Nash Equilibrium:

- If Lloris jumps with these probabilities, Messi is indifferent when kicking left or kicking right.
- If Mess kicks with these probabilities, Lloris is indifferent when jumping left or jumping right.
- When both are kicking/jumping with these probabilities, neither has an incentive to deviate from these probabilities.

<div class="definition" markdown="1">
<strong>Definition: Nash Equilibrium</strong>

A pair of (possibly randomized) strategies, such that no player has an incentive to deviate. 
</div>

**Question: How do we come up with these probabilities?**

There is an algorithm that comes up with those.

**Question: Do Messi and Lloris know each other’s probabilities?**

No, they don’t. They are deciding in the moment.

**Question: Are both Messi and Lloris’s decisions happening at the same time or is one reacting to the other?**

Lloris does not have time to see what Messi does, so both are happening at the same time.

## Equilibrium in 2-Player Zero-Sum Games

Assumptions:
- There are 2 players (Lloris and Messi).
- This is a Zero-sum game, meaning that their incentives are perfectly misaligned: what Lloris wants is exactly the opposite of what Messi wants.

Messi wants to optimize the probability of goal, i.e. he wants to maximize over all his possible kick strategies, assuming the worst possible jumping strategy for Lloris:

\[
  Messi's \; opt: \underset{kick-stratregy}{max} \underset{jump-stratregy}{min} Pr[goal]
\]

Lloris has the opposite optimization problem: he wants to figure out how to jump, he knows Messi is going to kick in the direction that makes it as hard as possible for him, and he wants to minimize the probability of goal:

\[
  Lloris's \; opt: \underset{jump-stratregy}{min} \underset{kick-stratregy}{max}  Pr[goal]
\]

<div class="theorem" markdown="1">
**Theorem:** Messi’s max-min = Nash equilibrium = Lloris’s min-max.
</div>

In other words: In a 2-player zero-sum game, even with more than 2 strategies per player, Messi’s max-min optimization problem is the same as the Nash Equilibrium (which tells us that the Nash Equilibrium is unique), which is going to be the same as Lloris’ min-max optimization problem.

**Where did these probabilities come from?**

One way to compute them is to use Linear Programming (LP), which generalizes the \(s-t \; Max-Flow\), which is the same as the \(s-t \; Min-Cut\), and this duality is the same reason why Messi’s problem is equivalent to Lloris’s problem. This gives us an efficient algorithm to compute these probabilities.

## Mini Case Study: Poker Algorithms

<div class="example" markdown="1">
<strong>Case Study: "Heads Up" (2-Player) Poker</strong>

Rough rules of Poker:

- Every player is dealt 2 cards (private information)
- Players bet during betting round
- There are some open cards on the table (public information)
- We determine which player's private cards are a better match to the cards on the table

**Can we use Linear Programming to compute the Nash Equilibrium strategy?**

Linear Programming is fast, but Poker is a _very_ large game. How large? Large enough that someone write a research paper about it—actually, about an _algorithm_ for _estimating_ how large it is.

In fact, there 56 trillion possible card combinations. However, this is not the only thing to consider: we also need to take into account how the other player is betting. Then, the number of possible combinations of what could happen becomes \(10^{160}\). Efficient Linear Programming algorithms are not fast enough.
</div>

Poker is an extensive-form game, because there are turns. In game theory, an extensive-form game represents a strategic interaction where players make decisions sequentially, and the order of moves is explicitly modeled using a game tree.

<div class="theorem" markdown="1">
**Definitions: Game Theory Terminology Overload**

- **Game Node:** State of the game (i.e. all cards dealt, and all bets made, so far)
- **Game Tree:** Graph representing which game nodes are reachable from which game node (i.e. there is an edge if we can go from \(A\) to \(B\) by calling another bet)
- **Information Set:** All the game nodes consistent with a player's information.
</div>

The most important part is the _Information Set_, which represents all the games nodes consistent with a player’s information, i.e. there are different states of the game that correspond to different cards that other players could be holding.

**Why should we worry about all the possible game states? Why can't we just solve the current state/information ste in real time?**

What a player wants to do at a given state of the the game depends on what they know (what they see), but it also depends on what the other players are going to do, which in turns depends on what they think that original player is going to do, and what they think that player is going to do depends on the cards they have now, but also what they might do with other cards.

<div class="definition" markdown="1">
**Algorithmic Insight #1: Use the Blueprint strategy.**

1. Blueprint solves a corase approximation of Poker ("only" \(10^13\) states, i.e. \(50TB\) to store 1 strategy).
2. During live play: we can use Blueprint to solve the actual information set, i.e. to estimate what the other player thinks we would do if we had their informations set.
</div>

<div class="definition" markdown="1">
**Algorithmic Insight #2:** Use regret-minimizing algorithms, e.g., MWU/FTRL.
</div>

<div class="theorem" markdown="1">
**Theorem:** If two players play a zero-sum game, and both use a regret-minimization algorithm, they will converge towards a Nash equilibrium.
</div>

<div class="example" markdown="1">
<strong>Case Study: "Heads Up" (2-Player) Poker (Cont'd)</strong>

In 2017, CMU's Poker bot beat top human Poker players for the first time.
</div>

<div class="summary" markdown="1">
<strong>Recap: 2-Player 0-Sum Game</strong>

At Nash equilibirum:

- Both players choose actions randomly
- Neither player can gain from changing distribution
- Theorem: max-min = Nash equilibrium = min-max

Algorithms for computing Nash equilibrium:

- Linear programming
- Regret minimization
</div>

## Nash Equilibrium in Non-Zero-Sum Games

<div class="example" markdown="1">
<strong>The Penalty Kick Game, Revisited</strong>

Lloris's incentives:

- Lloris wants to win the World Cup (he already did in 2018).
- Lloris also wants to be the goalie who stopped Messi's penalty kick (to earn more fame and sponsorship opportunities).

| Pr[goal]               | Messi kicks Left | Messi kicks Right |
|------------------------|------------------|-------------------|
| **Lloris jumps Left**  | 0.5              | 0.8               |
| **Lloris jumps Right** | 0.9              | 0.2               |

| Pr[save]               | Messi kicks Left | Messi kicks Right |
|------------------------|------------------|-------------------|
| **Lloris jumps Left**  | 0.4              | 0                 |
| **Lloris jumps Right** | 0                | 0.6               |

Therefore: \(Lloris's utility = Pr[save] - Pr[goal]\).

| U_{Messi}              | Messi kicks Left | Messi kicks Right |
|------------------------|------------------|-------------------|
| **Lloris jumps Left**  | 0.5              | 0.8               |
| **Lloris jumps Right** | 0.9              | 0.2               |

| U_{Lloris}             | Messi kicks Left | Messi kicks Right |
|------------------------|------------------|-------------------|
| **Lloris jumps Left**  | -0.1             | -0.8              |
| **Lloris jumps Right** | -0.9             | 0.4               |

This is what Lloris is really maximizing (while Messi is only optimizing the probability of goal).

**Where should Messi kick now? Where should Lloris jump now?**

It is no longer a zero-sum game, because the incentives of Messi and Lloris are neither perfectly aligned not perfectly misaligned. Messi does not care whether he misses or Lloris saves, but Lloris does (he would rather save).
</div>

**How should we model this question?**

We can use a Nash equilibrium, which always exists in a finite game, even if it is not a zero-sum game.

<div class="theorem" markdown="1">
<strong>Theorem: Nash's Existence Theorem (1951)</strong>

Every finite game has at least one Nash equilibrium (possibly mixed strategies). If players play the Nash equilibrium, neither wants to deviate.
</div>

**Caveats:** The Nash equilibrium...

- ... is no longer unique.
- ... is no longer equal to the max-min and the min-max.
- ... is not approached by Regret Minimization.
- ... is intractable to compute, even approximately.
- ... sometimes does not make sense (see below).

<div class="example" markdown="1">
<strong>Example: The CS269I Grade Game</strong>

You and your partner submitted a wonderful project, but the instructor is not sure how much each of you contributed to it. So, they will assign your grades using the following game:

1. You send the instructor \(x \in \{2, ..., 99\}\), and your partner sends the instructor \(y \in \{2, ..., 99\}\).
2. Then the instructor assigns you grade as follows:

    - If \(x = y\), then your grade is \(x\).
    - If \(x < y\), then your grade is \(min\{x,y\}+2\).
    - If \(x > y\), then your grade is \(min\{x,y\}-2\).

**Which grade should you send to the instructor?**

If you know your partner is going to put 99, then you put 98 so you get 100, and your friend get 96. So, maybe, you are going to put 97 and get 99, but if your friend it doing 97, you would rather put 96 and get 98. But then your friend is doing 96, so you would rather put 95, etc. It turns out that the unique Nash equilibrium in this game is when both players play 2 (x = y = 2), which is not expected in practice with real players.
</div>

So, we have this theorem that says that a Nash equilibrium always exists, but it has all these caveats. Let's consider alternative solution concepts that have emerged in game theory which, sometimes, may be a better model for this kind of games or strategic situations.

## Correlated Equilibrium

<div class="example" markdown="1">
<strong>Example: The Intersection Game</strong>

This is similar to the "Chicken" and the "Hawk-Dove" games. Essentially, you arrive at an intersection, where another car arrives as well, and you need to decide what to do:

|           | Go        | Wait  |
|-----------|-----------|-------|
| **Go**    | (-99,-99) | (1,0) |
| **Wait**  | (0,1)     | (0,0) |

What does this mean?

- If we both wait, we both get 0, nobody is moving.
- If we go and other person waits, we get 1 and they get 0.
- If we wait and the other person goes, we get 0 and they get 1.
- If we both go, we are very happy, we get a very negative utility, we have an accident.

This implies the following equilibria:

- **Asymmmetric equilibria:** (Go, Wait), (Wait, Go), i.e. if they go, we want to wait, and vice versa.
- **Symmetric equilibria:** Go with a probability of \(1\%\) and Wait with a probability of \(99\%\), i.e. we each independently go with a probability of \(1\%\) and wait with a probability of \(99\%\)—which is not great, since there is still a \(1/10000\) probability of colliding.
- **Correlated Equilibrium**: (Go, Wait) with a probability of \(50\%\) and (Wait, Go) with a probability of \(50\%\), i.e. we go and they wait with a probability of \(50\%\), and we wait and they go with a probability of \(50\%\). This is a correlated distribution: it is not independent. To implement this, we need a correlating device, i.e. something that is going to help us correlate our choices, such as a spotlight. For instance, the spotlight, with a probability of \(50\%\) is going to show us red and show them green, or vice versa, but it is never going to show us both green (hopefully).
</div>

<div class="definition" markdown="1">
<strong>Definition: Correlated Equilibrium</strong>

A correlating device sends each player a secret recommended action ("signal") from a pubicly-known correlated distribution. No player can gain from deviating from the recommended action.
</div>

In other words, when we have a correlated distribution over actions that gives a signal/recommended action, if the other player follows their recommended action, it is in our best interest to follow our own recommended action.

For instance, if the spotlight shows us red, it is probably because someone else has green, so we don’t want to go, but if the spotlight shows us green, then we know everyone must have red, so we might as well go.

**Note:** Every Nash equilibrium is an (un)correlated equilibrium.

**Good news:**

- A correlated equilibrium can be computed efficiently (e.g. with Linear Programming).
- If every player runs a Swap-Regret-minimizing algorithm, then the play converges towards the set of correlated equilibria. It is not really an equilibrium, though, as players will continue to cycle around the set of correlated equilibria forever.
- If every player runs an External-Regret-minimizing algorithm, then the play converges towards the set of coarse correlated equilibria.

## Coarse Correlated Equilibrium

What is the difference between a correlated equilibrium and a coarse correlated equilibrium?

Both types of equilibria rely on a correlating device to send each player a secret recommended action ("signal") from a publicly-known correlated distribution. However:

- In the **correlated equilibrium:** Players choose to follow the recommended action _after_ seeing it.
- In the **coarse correlated equilibrium:** Players want to follow their average recommended action, byt may not like some recommendations.

**Question: How do we know which algorithm and the equilibrium are appropriate?**

One way to think about it is to remember that agents are going to do what is good for them. If you think players are going to use the simplest algorithm, it is probably external regret minimizing, they will like end up at the coarse correlated equilibrium. If you expect them to use a more sophisticated swap-regret algorithm (which has other game theory advantages), you expect them to end up at the correlated algorithm.

**Bad News:**

- Just like the Nash equilibrium, the correlated equilibrium is not unique, and sometimes, it does not even make sense (cf. the CS269I Grade Game).
- Without a correlating device, we are not in an equilibrium: players have an incentive to deviate.

## Stackelberg Equilibrium

<div class="example" markdown="1">
<strong>Example: The Intersection Game, Revisited</strong>

As a reminder:

|           | Go        | Wait  |
|-----------|-----------|-------|
| **Go**    | (-99,-99) | (1,0) |
| **Wait**  | (0,1)     | (0,0) |

However, suppose now that you are playing against a "dog driver":

- You don't trust the dog to be rational.
- You don't trust the dog to follow the correlating device (the spotlight signal).
- You wait... so the dog can go.

**Conclusion:** The dog is better than you at the Intersection Game. More generally, committing to a strategy gives power.
</div>

This is what we call a Stackelberg equilibrium.

<div class="definition" markdown="1">
<strong>Definition: Stackelberg Equilibrium</strong>

A Stackelberg equilibrium is a pair of strategies (Leader's strategy, Follower's strategy) such that:

1. The Follower's strategy is optimal given the Leader's strategy.
2. The Leader's commitment is optimal, i.e. the payoff is optimal for the Leader among all pairs satisfying #1.
</div>

In other words, the Follower's strategy is a best response to what the strategy chosen by the Leader, and the Leader chooses the optimal strategy for them assuming that the Follower is going to pick a best response.

<div class="theorem" markdown="1">
The Leader’s utility, in the optimal Stackerlberg equilibrium, is at least what they can get in any possible equilibrium.
</div>

**Note:** If we think about the games we talked about so far, we talked about mixed strategies. For instance, Messi did not want to tell Lloris which side he was going to kick. However, in the Stackelberg equilibrium, without loss of generality, the follower is using a deterministic action, because the leader is already committed to a strategy, and the fact that the follower is using a deterministic action gives us an efficient algorithm using Linear Programming agin (it is something that we can compute efficiently).

<div class="example" markdown="1">
<strong>Mini Case Study: Security Games</strong>

A Stackelberg equilibrium may be used to model how security games where:

- The goal for defense forces (i.e. security checks, patrols, etc.) is to choose the optimal strategy.
- The assumption is that attackers can observe the defense strategy.

In practice, this is deployed in a variety of domains:

- Infrastructure (airport security)
- Nature (wildlife protection)
- Urban crime (LA Metro)
- Cybersecurity (honeypots, audits)

Challenges in real-world applications include:

- **Algorithmic difficulty:** How to deal with the combinatorial number of possible actions (e.g. a route in a large road network)?
- **Uncertainty:** What are the attacker's payoffs? Is the attacker rational? Will the defender be able to executed their strategy as planned?
- **Collagoration with human defenders:** Will patrol teams follow, or feel "micro-managed" by, the algorithm?
</div>

## Recap

<div class="summary" markdown="1">
<strong>Three Solution Concepts</strong>

- **Nash Equilibrium:** Each player samples independently from a distribution. Nobody has an incentive to deviate from the distribution.

    - Cleanest game theory assumption.
    - May not be achievable in complex environments.

- **Correlated Equilibrium:** A correlated distribution of actions that every player would rather follow. This may arise when agents independently run ML algorithms.

- **Stackelberg Equilibrium:** The Follower's strategy is optimal given the Leader's strategy, and the Leader's commitment is optimal.

    - Applies when one player has commitment power.
    - It is unclear how to generalize for more than two players.
</div>

<div class="example" markdown="1">
<strong>Example: The Penalty Kick Game—What Really Happened (Spoiler Alert)</strong>

Messi kicked left. Lloris jumped left. Messi scored.
</div>