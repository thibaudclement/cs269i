# Single-Unit Auctions
(4/23/2025)

Auctions are valuable in settings where price discovery is needed, such as:

- **Monopolies**: Wireless spectrum auctions.
- **Niche products**: Rare items on eBay.
- **Specialized products**: Ad auctions.

Auctions intersect significantly with Computer Science:

- Ad auctions fund many CS researchers.
- Fast auctions necessitate algorithmic bidders.
- Complex auctions require algorithmic auctioneers.

## Case of One Buyer

**Motivation**: Digital goods pricing for maximizing revenue.

- Demand curves derived from users' willingness to pay.
- Revenue = Price × Number of buyers willing to pay that price.
- Roger Myerson (1981): For a demand curve $D$, a formula $p(D)$ exists that maximizes revenue (optimal reserve price).

**Application**: Ad auctions with specialized advertisers (single bidder per spot) using prior beliefs as demand curves.

## Case of Multiple Buyers

**Model:**
1. Set of bidders $I$, each with valuation $v_i$.
2. Seller doesn't know valuations but has prior beliefs.
3. Bidder payoff: $v_i - p_i$ if they win, else $-p_i$.

### First-Price Auction

- Each bidder submits a sealed bid $b_i$.
- Highest bidder wins and pays their bid.

*Note*: Equilibrium bids are below true valuations ($b_i < v_i$).

### All-Pay Auction

- Each bidder submits a sealed bid $b_i$.
- Highest bidder wins the item.
- All bidders pay their bids.

Used for modeling non-auction scenarios (political donations, animal contests). Equilibrium bids are lower than valuations and generally lower than in first-price auctions.

### Second-Price Auction

- Each bidder submits a sealed bid $b_i$.
- Highest bidder wins, paying the second-highest bid.

<div class="theorem" markdown="1">
<strong>Theorem: Equilibrium in Second-Price Auctions</strong>

Second-price auctions are strategyproof: truthful bidding ($b_i = v_i$) is dominant and thus an equilibrium.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Fix other bids $b_j$, let $b^{(-i)} = \max_{j \ne i} b_j$. Two cases:

1. If $v_i < b^{(-i)}$, bidder $i$ prefers losing; bidding truthfully is optimal.
2. If $v_i > b^{(-i)}$, bidder $i$ prefers winning; again, truthful bid is optimal.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Payoffs of Second-Price Auctions</strong>

Second-price auctions are individually rational at equilibrium: $v_i - p_i \geq 0$.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> If bidder doesn't win, payoff = 0. If bidder wins, pays at most their valuation, thus non-negative payoff.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Optimality</strong>

In equilibrium, second-price auctions allocate the good to the highest-valued bidder.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> In equilibrium $b_i = v_i$, thus highest bidder corresponds to highest valuation.
</div>

## Revenue Maximization

<div class="example" markdown="1">
<strong>Example: Full Information Scenario</strong>

- $A$ values item at 1, $B$ values at 2.
- Second-price auction: $B$ wins, pays 1.
- First-price auction: Equilibrium bids near 1, revenue approximately 1.
</div>

To handle uncertainty, we define Bayesian Nash Equilibrium:

<div class="definition" markdown="1">
<strong>Definition: Bayesian Nash Equilibrium</strong>

A strategy profile where each player's strategy maximizes expected payoff given beliefs about others' strategies.
</div>

<div class="example" markdown="1">
<strong>Example: Bayesian Agents</strong>

- $A,B$ values drawn uniformly from [0,1].
- Second-price auction expected revenue: $\frac{1}{3}$.
- First-price auction equilibrium bids: $b_i = \frac{v_i}{2}$, also yielding expected revenue $\frac{1}{3}$.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Revenue Equivalence</strong>

At equilibrium, expected payments depend only on the auction’s allocation rule.
</div>

<div class="corollary" markdown="1">
<strong>Corollary:</strong> First-price, second-price, and all-pay auctions yield identical equilibrium revenue under Bayes-Nash equilibria with standard allocation rules (highest bidder wins).
</div>

### Deviations from Optimal Allocation

Auctions don't always allocate to the highest valuation bidder:

- Overbidding in second-price auctions (highest bidder might bid excessively).
- All-pay auctions may have equilibria not awarding highest value bidder.
- Reserve prices might result in no winner.