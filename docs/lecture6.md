# Market Equilibrium
_April 16, 2025_

Previously, we examined scenarios without monetary transfers. Introducing money changes market dynamics substantially:

- Stanford housing would differ if rooms were auctioned.
- Buying organs is illegal in most countries.
- Hospitals-student monetary matches face legal restrictions.

**Issues with non-monetary markets:**
1. Limited to ordinal rather than cardinal preferences.
2. Emergence of underground markets.
3. Potential exploitation (bots manipulating donor lists).

<div class="definition" markdown="1">
<strong>Definition: Cardinal vs Ordinal Utilities</strong>

- **Cardinal**: Assign numeric values to preferences.
- **Ordinal**: Only ranks preferences by order.

Cardinal utilities convey richer information (ordinal can be derived from cardinal), are intuitive in economic analysis, and typically monetarily measurable.
</div>

<div class="definition" markdown="1">
<strong>Definition: Fungible vs Idiosyncratic Goods</strong>

- **Fungible goods**: Interchangeable units.
- **Idiosyncratic goods**: Unique goods.

Many real-world goods blend these traits (e.g., ridesharing).
</div>

<div class="definition" markdown="1">
<strong>Definition: Supply and Demand Curves</strong>

- **Demand curve**: Quantity consumers buy at each price.
- **Supply curve**: Quantity firms sell at each price.

Typically:

- Price is vertical ($y$-axis).
- Quantity is horizontal ($x$-axis).
</div>

<div class="remark" markdown="1">
Usually, demand slopes downward and supply upward. However, exceptions (monopoly markets, certain special goods) exist.
</div>

<div class="definition" markdown="1">
<strong>Definition: Market Clearing Price</strong>

The price where supply equals demand. All buyers and sellers transact, "clearing" the market.
</div>

## Unit-Demand Market Model

**Setup:**

- $m$ idiosyncratic goods.
- $n$ buyers (each buys at most one good).
- Buyer $i$ values good $j$ at $v_{i,j}$.
- Buyer $i$'s payoff for good $j$: $U_{i,j} = v_{i,j} - p_j$.
- Utility without buying: $U_{i,\varnothing} = 0$.

<div class="definition" markdown="1">
<strong>Definition: Competitive Equilibrium</strong>

A price vector $p = (p_1,\dots,p_m)$ and matching $M:\{1,\dots,n\}\to\{1,\dots,m\}$ satisfying:

1. Buyers get their preferred good at price $p$:
   $$v_{i,M(i)} - p_{M(i)} \geq v_{i,j} - p_j \quad \forall i,j.$$
2. Unmatched goods have price zero.
3. Buyers are unmatched only if $v_{i,j}-p_j<0$ for all goods $j$.
</div>

<div class="remark" markdown="1">
This implies individual rationality, ensuring buyers never choose negatively valued outcomes.
</div>

<div class="definition" markdown="1">
<strong>Definition: Social Welfare</strong>

Sum of buyers' values:
$$U(M)=\sum_i v_{i,M(i)}.$$

Prices excluded as buyer costs equal seller profits.
</div>

## Properties of Competitive Equilibrium

<div class="theorem" markdown="1">
<strong>Theorem: First Welfare Theorem</strong>

Competitive equilibrium allocation maximizes social welfare:
$$\sum_i v_{i,M(i)} \geq \sum_i v_{i,M'(i)} \quad \forall M'.$$
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> By competitive equilibrium definition, for any alternative matching $M'$:
$$\sum_i(v_{i,M(i)}-p_{M(i)})\geq \sum_i(v_{i,M'(i)}-p_{M'(i)}).$$
Since total prices paid are equal, we get welfare optimality.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Existence of Competitive Equilibrium</strong>

Competitive equilibrium always exists in finite unit-demand markets with discrete prices.
</div>

<div class="remark" markdown="1">
In more complex markets, equilibrium existence isn't guaranteed.
</div>

<div class="proof" markdown="1">
<strong>Proof (via Deferred Acceptance with Prices):</strong>

Construct ranked lists of (good, price) pairs for each buyer (discarding negative options). Buyers iteratively propose to their next-best option; goods tentatively accept highest offers. Termination guaranteed (similar to deferred acceptance).

Resulting allocation meets competitive equilibrium conditions:

- Buyers matched to best possible option.
- Unmatched goods priced zero.
</div>

<div class="proposition" markdown="1">
<strong>Proposition: Deferred Acceptance with Prices</strong>

The deferred acceptance with prices algorithm is strategyproof and buyer-optimal.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Direct from standard deferred acceptance reasoning.
</div>