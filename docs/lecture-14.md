_May 28, 2025_

In week 1, we discussed matching problems modeled with ordinal utilities. In most lectures since, we looked into markets/auctions with money.

The basic assumption for mechanism design with money is "How much I want something = how much I’m willing to pay for it." However, an obvious caveat to keep in mind is that "How much I’m willing to pay also depends on how much money I have."

Today, we are going to discuss fair allocation without monetary transfers (w/ cardinal utilities).

## I-Cut-You-Choose Mechanism

Alice and Bob want to split a cake. Each has different preferences over strawberries, blueberries, cheese, etc. 

<div class="definition" markdown="1">
**Definition: I-Cut-You-Choose mechanism**

1. Alice cuts the cake into two equal-for-her pieces.
2. Bob chooses his favorite of the two pieces

</div>

This mechanism is a long-time favorite, even used to divide land in the Bible:

> “And Abram said unto Lot, "Let there be no strife, I pray thee, between me and between thee and between my herdmen and between thy herdmen, for we be brethren. Is not the whole land before thee? Separate thyself, I pray thee; if thou wilt take the left hand, then I will go to the right; or if thou depart to the right hand, I will go to the left.“ – Genesis 13:8-9

This mechanism is also very simple: Aviad uses it often at home with his kids.

Yet, is I-cut-you-choose strategyproof?

<div class="theorem" markdown="1">
**Claim:** I-cut-you-choose is _not_ strategyproof.

</div>

<div class="proof" markdown="1">
**Proof:**

Suppose Alice just wants to get as much cake as possible:

- If Bob really likes blueberries, Alice could cut a small piece of cake with 51% of blueberries. Bob would choose it, and Alice gets the rest of the cake.
- If Bob really likes strawberries, small piece with 51% of strawberries…

To cut optimally, Alice wants to know Bob’s preferences—and Bob probably doesn’t want to tell her in advance.

</div>

In other words, I-cut-you-choose is not strategyproof for the cutter (but it is strategyproof for the chooser).

<div class="definition" markdown="1">
**Definition: Envy-Freeness (1/2)**

An allocation is envy-free if no agent envies another agent’s allocation (i.e. no agent would rather have the other’s allocation over their own).

</div>

<div class="theorem" markdown="1">
**Claim:** If Alice cuts the cake into 2 pieces that are equal for her (and Bob picks his favorite), the resulting allocation is envy-free.

</div>

Note that envy-freeness is a stronger property than stability: for example, giving the entire cake to Alice is stable (because Alice wouldn’t want to switch allocation), but not envy-free (because Bob would).

It’s pretty satisfying that I-cut-you-choose is envy-free! However, maybe some envy-free allocations still seem unfair (e.g. think of Bob getting a small piece with 51% of blueberries).

How can we analyze mechanisms from a fairness perspective?

## Fairness Criteria and Objectives

<div class="remark" markdown="1">
We’re about to see a lot of definitions. Aviad doesn't expect us to remember all of them by the end of lecture. The point is to give us (a) a sense of the complexity of this question, and (b) a taste of major approaches to tackling it.

</div>

Formalizing fair allocations:

- Our goal is to choose an allocation \(A = (A_1, ..., A_n)\) to \(n\) agents.
- Each agent \(i\) has a valuation function \(v_i()\).

For this part of lecture, we can just think about additive valuations: If \(x,y\) are disjoint, then \(v_i(x \cup y) = v(x) + v(y)\).

<div class="definition" markdown="1">
**Definition: Envy-Freeness (2/2)**

We may re-define envy-free allocations as:

\[
  \forall i,j \; v_i(A_i) \geq v_i(A_j).
\]

</div>

There exists a lot of ways to define fair allocations.

<div class="definition" markdown="1">
**Definition: Proportional**

We may define proportional allocations as:

\[
  \forall i \; v_i(A_i) \geq \frac{v_i(A)}{n}.
\]

In other words: my happiness guarantee doesn’t depend on others’ allocation.
</div>

<div class="definition" markdown="1">
**Definition: Perfect**

We may define perfect allocations as:

\[
  \forall i \; v_i(A_i) = \frac{v_i(A)}{n}.
\]

This is similar to proportional, but also making sure that no one is too happy (we may want to think about why this may be helpful).
</div>

<div class="definition" markdown="1">
**Definition: Equitable**

We may define equitable allocations as:

\[
  \forall i,j \; v_i(A_i) = v_j(A_j).
\]

This a little funny because we have to compare \(i\)’s happiness to \(j\)’s happiness (we may want to think about how to achieve this).
</div>

<div class="definition" markdown="1">
**Definition: Competitive equilibrium from equal incomes (CEEI)**

- Give each agent a budget of 1 (fake money).
- Find prices (for pieces of cake) and an allocation such that:
    - The entire cake is allocated (unless there is a zero-priced unwanted leftover piece).
    - Every agent is allocated the favorite piece they can afford given their budget constraint.

_**Note:** With fake money, agents maximize value subject to budget constraint. This is different from Lecture 6 where they maximized utility based on value-price._

</div>

With indivisible goods, often none of these can be satisfied! For example, if we want to allocate 1 hat, then both Alice and Bob want it.

Notice that for this example we would have a competitive equilibrium with real money: Alice gets the hat and pays for it, Bob gets nothing and keeps his money. But with fake money Bob isn’t satisfied with keeping his fake money.

<div class="definition" markdown="1">
**Definition: Maximin Share (MMS)**

Each agent \(i\) proposes (cuts) allocation \(A^i\) to \(n\) agents.

(\(A\) still denotes the real allocation.)


MMS condition:

\[
  v_i(A_i) \geq \underset{A^i}{max} \; \underset{j}{min} \; v_i(A_j^i)
\]

</div>

Some unfairness is inevitable (for instance if we think of the hat example). MMS tries to capture the minimal necessary unfairness. It is a little bit like saying to agent \(i\), “Even if you cut the cake any way you wanted to, you wouldn’t guarantee more than you got in this allocation”. This is why we say that MMS is “no worse than worst-case I-cut-you-choose."

Surprisingly, sometimes, even MMS cannot be satisfied.

One idea is to approximately-fairly dividing indivisible items.

<div class="definition" markdown="1">
**Definition: Envy-Free-Up-to-1-Item (EF1)**

\[
  v_i(A_i) \geq v_i(\frac{A_j}{"best" \; item}).
\]

EF1 in equations:

\[
  \forall i,j \; \exists g \in A_j \; v_i(A_i) \geq v_i (\frac{A_j}{g}).
\]

EF1 in words: 

- \(v_i(A_j)\) = the value agent \(i\) would have for agent \(j\)’s allocation \(A_j\).
- A weaker benchmark is: \(v_i(\frac{A_j}{"best" \; item})\) = the same as \(v_i(A_j)\), but we discard \(i\)’s favorite item.

</div>

EF1 can always be satisfied, e.g., agents taking turns selecting one item at a time (“round robin”). However, EF1 is sometimes not very fair. For example, Alice and Bob are splitting 2 cars and 10 chairs:

- Fair allocation: each gets one car + 5 chairs.
- Also EF1: each gets one car, and Alice gets all the chairs.

<div class="definition" markdown="1">
**Definition: Envy-Free-Up-to-Any-Item (EFX)**

\[
  v_i(A_i) \geq v_i(\frac{A_j}{"worst" \; item}).
\]

</div>

Can EFX always be satisfied? This is an open problem.

<div class="definition" markdown="1">
**Definition: \(\alpha\)-Maximin Share (MMS)**

“Only a bit \((\alpha)\) worse than worst-case I-cut-you-choose.”

\(\alpha\)-MMS condition:

\[
  v_i(A_i) \geq \alpha \; \underset{A^i}{max} \; \underset{j}{min} \; v_i(A_j^i)
\]

</div>

<div class="theorem" markdown="1">
**Theorem:** A \(\frac{3}{4}\)-MMS allocation always exists.

</div>

Is more-than-\(\frac{3}{4}\)-MMS always impossible? This is another open problem.

<div class="definition" markdown="1">
**Definition: _Approximate_ Competitive equilibrium from equal incomes (A-CEEI)**

- Give each agent a budget of _approximately_ 1 (fake money).
- The allocation is only required to _approximately_ clear markets.

</div>

An A-CEEI always exists, although with some tradeoff in approximations of equal incomes vs. market clearing.

However, this is computationally intractable: the computational complexity of finding an A-CEEI was one of Aviad's first research projects in PhD, and he still works on it.

What do we mean by approximately market clearing? We have to allocate non-existing goods.

Another approach is to look for an allocation that maximizes **fair objective functions**.

<div class="definition" markdown="1">
**Definition: Utilitarian/Social Welfare**

“Maximum total happiness”:

\[
  \underset{A_1, ..., A_n}{max} \sum_i v_i(A_i)
\]

</div>

<div class="definition" markdown="1">
**Definition: Egalitarian/Maximin**

“Maximum happiness of the saddest person”:


\[
  \underset{A_1, ..., A_n}{max} \; \underset{j}{min} \; v_i(A_i)
\]

</div>

<div class="definition" markdown="1">
**Definition: Nash Social Welfare**

Middle ground between utilitarian and egalitarian:

- Emphasis on increasing lower \(𝑣_𝑖\) (we can think of the extreme case where one \(v_i\) is close to zero).
- Yet, it doesn’t completely ignore higher \(v_i\) like egalitarian.

\[
  \underset{A_1, ..., A_n}{max} \; \prod_i \; v_i(A_i)
\]

</div>

The Nash Social Welfare is scale-invariant, which makes it easier to compare different agents without money.

<div class="theorem" markdown="1">
**Theorem:** CEEI allocation maximizes Nash Social Welfare.

</div>

<div class="example" markdown="1">
**Examples:** Some fair allocations in practice.

- Allocating goods:
    - Spliddit used to maximize social welfare subject to MMS/proportionality/EF. 
    - They decided that NSW is better.
- Allocating classes:
    - Approximate-CEEI.
    - Combinatorial demand.
    - The number of students must significantly exceed the number of classes.
- Allocating chores:
    - Spliddit used to assign chores by assuming they’re divisible (we can use randomized rounding to assign fractional chores) and drawing new chores each week to guarantee approximate “ex-post” fairness.
    - Then they looked for an equitable solution, and optimized over all equitable solutions using Linear Programming.
- Allocating computing (see upcoming example from Databricks).

</div>

## Dominant Resource Fairness (DRF)

<div class="definition" markdown="1">
**Definition: Leontieff Utility**

I want to make as much cake as possible, so I need fixed ratios of \(flour : oil : sugar\).

</div>

<div class="example" markdown="1">
**Example**

Consider the following computational resource sharing model:

- We have \(m\) resources (CPU, memory, I/O, …) with fixed capacities.
- There are \(n\) users:
    - Each user wants to run as many identical tasks as possible.
    - Each task demands a fixed vector of resources (2 GPU, 3 TB RAM).
    - For now, tasks are infinitesimally small (2\(\epsilon\) GPU, 3\(\epsilon\) TB RAM).

How can we allocate these resources to these users? In particular, we want to:

- Ensure fairness, efficiency.
- Avoid monetary transfers (e.g. allocation inside a given organization).

</div>

Incentives are important in compute allocation:

- “For example, one of Yahoo!’s Hadoop MapReduce datacenters has different numbers of slots for map and reduce tasks. A user discovered that the map slots were contended, and therefore launched all his jobs as long reduce phases, which would manually do the work that MapReduce does in its map phase.”
- “A big search company provided dedicated machines for jobs only if the users could guarantee high utilization. The company soon found that users would sprinkle their code with infinite loops to artificially inflate utilization levels.”

<div class="definition" markdown="1">
**Definition: Dominant Resource Fairness**

Fix an allocation of resources to users:

- User \(i\) has some share (fraction) of the total capacity of each resource.
- User \(i\)’s dominant resource is the resource with the largest share.

**Dominant resource fairness means** equal shares of dominant resources across users.

</div>

<div class="example" markdown="1">
**Example:** _Not_ Dominant Resource Fairness

Consider the following scenario:

- Total capacity = 10 GPU, 20 TB
- Ali received 4 GPU, 16 TB
- Ali’s GPU share \(= \frac{2}{5}\)
- Ali’s memory share \(= \frac{4}{5}\)
- Beth’s GPU share \(\leq \frac{3}{5}\)
- Beth’s memory share \(\leq \frac{1}{5}\)

Ali’s dominant resource is memory: this is _not_ DRF.

</div>

<div class="example" markdown="1">
**Example:** Dominant Resource Fairness

Consider the following scenario:

- Total capacity = 10 GPU, 20 TB
- Ali received 2 GPU, 16 TB
- Ali’s GPU share \(= \frac{1}{5}\)
- Ali’s memory share \(= \frac{4}{5}\)
- Beth’s GPU share \(= \frac{4}{5}\)
- Beth’s memory share \(= \frac{1}{10}\)
- \(\frac{1}{10}\) of memory remains unused

Ali’s dominant resource is memory and Beth's dominant resource is GPU: this is DRF.

</div>

<div class="definition" markdown="1">
**Definition: Dominant Resource Fairness Mechanism**

- Every user submits their ratio of demands (e.g. 2 GPU : 1 TB).
- The algorithm computes the (unique) maximal allocation subject to DRF.

</div>

<div class="theorem" markdown="1">
**Theorem:** Every user prefers the DRF allocation to \(\frac{1}{n}\) of each resource.

</div>

In other words, every user prefers DRF over naïve resource allocation. This property is called sharing incentives and it is related to individual rationality.

<div class="proof" markdown="1">
**Proof:** Allocation is maximal

\(\rightarrow\) Some resource \(j^\star\) is exhausted.

\(\rightarrow\) Some user \(i^\star\) gets \(\geq \frac{1}{n}\) of \(j^\star\).

\(\rightarrow\) \(i^\star\) has \(\geq \frac{1}{n}\) of her dominant resource.

\(\rightarrow\) every user has \(\geq \frac{1}{n}\) of their dominant resource.

</div>

<div class="theorem" markdown="1">
**Theorem:** The DRF allocation is envy-free.

</div>

<div class="proof" markdown="1">
**Proof:** Assume by contradiction that Ali envies Beth.

\(\rightarrow\) Beth has more of every resource–including Ali’s dominant resource.

\(\rightarrow\) This is a contradiction to DRF.

</div>

<div class="theorem" markdown="1">
**Theorem:** DRF is Pareto-optimal.

</div>

<div class="proof" markdown="1">
**Proof:** Allocation is maximal

\(\rightarrow\) Some resource \(j^\star\) is exhausted.

\(\rightarrow\) By simplifying assumption, we can’t make someone happier without taking some \(j^\star\) from someone else.

</div>

<div class="theorem" markdown="1">
**Theorem:** The DRF mechanism is strategyproof.

</div>

<div class="proof" markdown="1">
**Proof:** Let \(A_T\) denote the allocation of DRF with true preferences.

Assume by contradiction that Ali can misreport to get a better allocation \(\widehat{A}\).

By Pareto-optimality of \(A_T\), Beth has a smaller allocation in \(\widehat{A}\) than in \(A_T\).


\(\rightarrow\) Beth receives less of her dominant resource in \(\widehat{A}\).

\(\rightarrow\) Ali receives less of his dominant resource in \(\widehat{A}\)-this is a contradiction.

</div>

## (Beyond) DRF in Practice

Let's revisit our example from earlier:

<div class="example" markdown="1">
**Example**

Recall the following vanilla assumptions:

- We have \(m\) resources (CPU, memory, I/O, …) with fixed capacities.
- There are \(n\) users:
    - Each user wants to run as many identical tasks as possible.
    - Each task demands a fixed vector of resources (2 GPU, 3 TB RAM).
    - Simplifying assumption: demand \(>0\) for every resource.
    - For now, tasks are infinitesimally small (2\(\epsilon\) GPU, 3\(\epsilon\) TB RAM).

</div>

In practice:

- Tasks are not identical, and they arrive and depart over time \(\rightarrow\) This is a hard problem, both in theory and in practice, which requires **Practical DRF** (While resources are not exhausted, select user \(i\) with the minimum dominant share, and add their next feasible task).
- Some tasks have flexibility in resource use (e.g., map vs. reduce manipulation example).
- Some tasks have more specific desiderata (e.g., specific hardware, specific location).
- Tasks are not infinitesimally small \(\rightarrow\) \(\rightarrow\) This is a hard problem, both in theory and in practice, which requires **Practical DRF** (While resources are not exhausted, select user \(i\) with the minimum dominant share, and add their next feasible task).
- Some users have higher priority \(\rightarrow\) This requires **Weighted DRF**.
- Some tasks have zero demand for some resource \(\rightarrow\) This requires **Extended DRF** (Find the maximal DRF allocation, and then recurse on remaining feasible tasks).

## Recap

<div class="summary" markdown="1">
**Envy and Fairness Recap**

- Envy-free Cake Cutting:
    - I-cut-you-choose mechanism: 1. Alice cuts the cake into two equal-for-her pieces, and then 2. Bob chooses his favorite of the two pieces.
    - I-cut-you-choose is not strategyproof for the cutter (but it is strategyproof for the chooser).
    - Definition: An allocation is envy-free if no agent envies another agent’s allocation (i.e. no agent would rather have the other’s allocation over their own).
    - Claim: If Alice cuts the cake into 2 pieces that are equal for her (and Bob picks his favorite), the resulting allocation is envy-free.

- A lot of different ways to define fair allocations:
    - Envy-Free (EF1/EFX): \(v_i(A_i) \geq v_i(A_j)\).
    - Proportional: \(v_i(A_i) \geq \frac{v_i(A)}{n}\).
    - Equitable: \(v_i(A_i) = v_j(A_j)\).
    - Perfect: \(v_i(A_i) = \frac{v_i(A)}{n}\).
    - \(\alpha\)-Maximin Share (MMS): \(v_i(A_i) \geq \alpha \; \underset{A^i}{max} \; \underset{j}{min} \; v_i(A_j^i)\).
    - (Approximate) Competitive equilibrium from equal incomes (A-CEEI).
    - Utilitarian/Social Welfare: \(\underset{A_1, ..., A_n}{max} \sum_i v_i(A_i)\).
    - Nash Social Welfare: \(\underset{A_1, ..., A_n}{max} \; \prod_i \; v_i(A_i)\).
    - Egalitarian/Maximin: \(\underset{A_1, ..., A_n}{max} \; \underset{j}{min} \; v_i(A_i)\).

- Which definition to use depends on the application:
    - Allocating goods:
        - Spliddit used to maximize social welfare subject to MMS/proportionality/EF. 
        - They decided that NSW is better.
    - Allocating classes:
        - Approximate-CEEI
        - Combinatorial demand
        - The number of students must significantly exceed the number of classes
    - Allocating chores:
        - Spliddit used to assign chores by assuming they’re divisible (we can use randomized rounding to assign fractional chores) and drawing new chores each week to guarantee approximate “ex-post” fairness.
        - Then they looked for an equitable solution, and optimized over all equitable solutions using Linear Programming.
      - Allocating computing (see example from Databrick).

- Dominant Resource Fairness:
    - Fix an allocation of resources to users:
        - User \(i\) has some share (fraction) of the total capacity of each resource.
        - User \(i\)’s dominant resource is the resource with the largest share.
    - Theorems: DRF satisfies sharing incentives, envy-free, Pareto-optimal, strategyproof.
    - Extended DRF: Find the maximal DRF allocation, and recurse on the remaining feasible tasks.
    - Practical DRF: While resources are not exhausted, select user \(i\) with the minimum dominant share, and add their next feasible task.    

</div>
