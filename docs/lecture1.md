# One-Sided Matching and Serial Dictatorship
(3/31/2025)

**The Stanford Undergrad Housing Problem:**

- There are \( n \) students, each with some preference over dorms.
- There are \( m \) dorms, each with some capacity (for simplicity, assume capacity is 1 for every dorm).

How can we assign students to dorms?

## Max Weight Matching

One possible solution is to maximize total happiness:

<div class="definition" markdown="1">
<strong>Mechanism: Happiness Maximization</strong>

1. Create a bipartite graph where:
    - One side represents students.
    - The other side represents dorms.
    - Each edge from a student to a dorm represents how much that student likes that dorm.
2. Determine the max-weight matching (i.e., Hungarian Algorithm).
</div>

**Key question:** How does the algorithm determine how much each student likes each residency? Only the students themselves know how much they like each dorm, so we need to rely on students to tell the algorithm.

**Challenge:** Each student has an *incentive* to exaggerate how much they like their favorite dorm and undercut how much they like other dorms (using a "0" or "negative infinity" weight for those dorms). In other words: max-weight bipartite matching allows students to game the system.

This occurs because finding the matching that maximizes total happiness is conceptually right, but this naive max-weight matching fails to take incentives into account. Another possible algorithm is Serial Dictatorship.

## Serial Dictatorship

This is how Stanford actually assigns dorms to students.

<div class="definition" markdown="1">
<strong>Mechanism: Serial Dictatorship</strong>

1. Sort students in some fixed order (random, seniority, alphabetically, etc.).
2. Go through the list in *that* order and allow each student (the "dictator") to select their most preferred available dorm.
</div>

How is this better? There can still be students unhappy with their result. Indeed, a common complaint about Serial Dictatorship is unfairness: the first student chooses whichever dorm they want, while the last student gets only the last pick.

When sorting is random, Serial Dictatorship guarantees **ex-ante fairness**: *before* the random sorting, all students have equal chances. However, *after* the sorting happens (even randomly), Serial Dictatorship loses fairness: there's no guarantee of **ex-post fairness**.

<div class="definition" markdown="1">
<strong>Definition: Mechanism</strong>

A mechanism consists of three things:

1. A method of collecting inputs from agents,
2. An algorithm that acts on the inputs,
3. An action taken based on the output of the algorithm.
</div>

In our context (Stanford Undergrad Housing Problem), based on inputs (dorm preferences) and the algorithm (available dorm after each student's pick), the mechanism takes actions (it assigns dorms).

**Note:** All three components matter because there's a feedback loop: how we use inputs impacts what students report as preferences. The naive bipartite matching approach encourages students to game the system by misreporting their preferences.

Thus, when designing a mechanism, we must consider:

- The algorithm itself,
- How/where inputs come from,
- Actions taken based on inputs,
- How promised actions affect reported inputs.

<div class="definition" markdown="1">
<strong>Definition: Strategyproofness/Truthfulness</strong>

A mechanism is strategyproof if it's in every agent's best interest to act truthfully, i.e., to report true preferences.
</div>

Even more formally, game theorists somtimes use the term **Dominant Strategy Incentive Compatible**:

<div class="definition" markdown="1">
<strong>Definition: Dominant Strategy Incentive Compatible - DSIC</strong>

A mechanism is dominant strategy incentive compatible if truthfulness is a dominant strategy for each participant. That is, being truthful is a best response regardless of other players' actions.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: You Cannot Game Serial Dictatorship</strong>

It is in every student's best interest to choose their favorite available dorm in their turn. Formally, we say that Serial Dictatorship is **strategyproof** or **truthful**.
</div>

<div class="proof" markdown="1">
**Proof:**

- Your room choice doesn't affect room availability before your turn.
- When your turn arrives, your best action is choosing your favorite available room.
</div>

Why does this prove that Serial Dictatorship is strategyproof? Until your turn comes, it is other students who are bidding, and there is nothing you can do to affect it. However, when comes your turn, you choose what you get, so you should choose the best thing for you.

<div class="definition" markdown="1">
<strong>Definition: Pareto Optimality</strong>

An assignment \( A \) is Pareto optimal if, for any other assignment \( B \), there's at least one participant strictly preferring \( A \) over \( B \).
</div>

<div class="theorem" markdown="1">
<strong>Theorem: You Cannot Make Everyone Happier Without Making Someone Sadder</strong>

Serial Dictatorship assignments are Pareto Optimal.
</div>

<div class="proof" markdown="1">
**Proof:**

Assume, for the sake of contradiction, that a different assignment exists making everyone as happy or happier.

Consider the first student assigned differently: all better dorms are already assigned identically to students before them.

Thus, the first differing student gets a worse dorm and becomes less happy—we have reached a contradiction.

Therefore, Serial Dictatorship is Pareto Optimal.
</div>

## Additional Discussion

**Why is truthfulness good?** It prevents corruption and ensures fairness by removing any insider advantage.

**When is truthfulness important?** When optimizing happiness, truthful inputs ensure correct objectives.

**When is relaxing truthfulness acceptable?**  In contexts with social norms where truthfulness isn't expected (e.g., poker games), strategyproofness isn't crucial.

**Fairness/equity issues with Serial Dictatorship:** Fairness depends on sorting order. Seniority or randomness provide fairness ex-ante but not necessarily ex-post.

**Is there any other flaws in Serial Dictatorship?** A dictator's seemingly insignificant decision may have huge impact on other agents. For instance, by the time my turn arrive, only my 9th and 10th choices are available. Since I am almost indifferent between them, I break ties and take my 9th choice. However, it is possible that my 9th choice was in fact someone else's top choice and they _really_ wanted it. This may be even worse if their 2nd-10th choices happen to be already taken.

## Recap

<div class="summary" markdown="1">

- **Definition: Mechanism.** A mechanism meaning soliciting inputs, running an algorithm, and taking actions.
- **Definition: Strategyproof/truthful.** A mechanism is strategyproof/truthful is misreporting preferences can never make a participant better off.
- **Defintion: Pareto-optimal.** An assignment \( A \) is Pareto-optimal if for any other assignment \( B \), there is a participan that (strictly) prefers \( A \) over \( B \).
</div>