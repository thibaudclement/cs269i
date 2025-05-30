<div class="summary" markdown="1">
**Blockchain Recap (So Far)**

Main goal: Maintain a ledger (i.e. a history of events that we all/mostly agree on) that is:

- Decentralized: Messages are delayed/dropped (no uniform time)
- Permissionless: Users join, leave, come back at any time

Risks of Sybil attacks require alternatives to “majority”:

- Vanilla Proof-of-Stake (PoS) protocol: At each iteration:
    - (1) Sample a random coin;
    - (2) Ask its owner to create the next block.
- Proof-of-Work (PoW): At each iteration:
    - (1) Miners compete to invert a hash function;
    - (2) First miner to succeed creates new block
</div>

<div class="summary" markdown="1">
**Market Failures Recap**

A **market failure** occurs when a market fails to converge to an optimal outcome.

We have seen five types of market failures:

1. Externalities (side effects on other parties)
2. Transaction costs
3. Thinness (flow of buyers/sellers too small)
4. Timing issues
5. Information asymmetry

</div>

<div class="summary" markdown="1">
**No-Trade Theorems Recap**

**Public information no-trade theorem:** If the market already aggregated all available public information, there is no point in trading.

**Public+Private information no-trade theorem:** Alice will only want to buy at current price if she has private information:

- If Alice wants to buy, she probably has private information.
- Bob doesn’t want to sell Alice.
- Even if Alice learns private information, she can’t use it.

</div>

## Flashboys 1.0

<div class="example" markdown="1">
**Example: The High-Frequency Trading (HFT) Speed Arms Race**

In 2010, Spread Networks opened new $300M fiber optics from NY to Chicago. Why? Because it is (almost) a straight line, which brings latency down from 16ms to 13ms.

Who needs 3ms saving in latency? In comparison, a blink of the eye is less than 100ms. Answer: Low latency High Frequency Traders (HFT) race to beat each other.

There was a joke at the time saying that Spread Networks's fiber optics would soon be obsolete, when someone digs a tunnel, thus “avoiding the pesky curvature of the earth.”

Ironically, in 2011, latency time down to 10ms using microwaves! It turns out that air refracts slightly better than glass.

</div>

**Is Spread Networks a market failure?**

A hypothesis may be that investing \(\$300\)M for saving 3ms (for only one year) represents social waste, because someone is paying this \(\$300\)M, yet no one is much happier.

Maybe Spread Networks made so much money that they were happy, but they would have been happier to take the same money from HFTs without paying \(\$300\)M for new fiber optics.

Here are some externalities to consider:

- When the first HFT buys bandwidth from Spread Networks, they’re happy because they expect to make a lot of money by being faster than their competitors. Spread Networks is also happy because they sold bandwidth.
- However, the other HFTs are sad because they’re now slower than 1st HFT.
- We reach a market equilibrium when all HFTs buy bandwidth.
- As a result, none of them are happy.
- The total negative externality is greater than or equal to \(\$300\)M.

**Should we consider an even larger market failure?**

HFTs make a lot more than $300M a year. Yet, they just buy and sell stocks (securities) and make money out of it! Does anyone else benefit from having them?

## A Stock Market Model

<div class="remark" markdown="1">

We will slowly build up an increasingly elaborate model. Yet, even at the end of this lecture, we will still abstract out many important aspects.

</div>

<div class="definition" markdown="1">

Let's model a market for fungible (i.e. interchangeable) shares of one company.

Main model points:

- Stock exchange rules: continuous limit order book.
- Players:
    - Naïve investors
    - Liquidity providers
    - Snipers
- Stock “value” (and how it changes)

</div>

<div class="summary" markdown="1">
**Continuous Limit Order Book Recap**

Definitions:

- Bid: highest buy order
- Ask: lowest sell order

Rules:

- Buy/sell orders can arrive at any time.
- Trading happens whenever a new buy order is greater than the ask (or a new sell order less than the bid).

Two kinds of orders:

- Marketable orders already have a match in the book.
- Resting (non-marketable) orders are waiting to be matched.

</div>

<div class="definition" markdown="1">
**Definition: Naïve Investors**

Homer just received his paycheck. He wants to buy 1 stock to save for retirement.
Abe is retired. He wants to sell 1 stock to pay for health insurance.
Homer can buy 1 stock from Abe!

Problem (Market thinness): Homer gets his paycheck on the 10th, while Abe’s insurance fees due on the 1st.

we need liquidity providers!

_**Note:** No-trade theorems don’t apply with naïve investors (Investing for retirement doesn’t make sense for prediction markets)._

</div>

<div class="summary" markdown="1">
**Liquidity Providers Recap**

Liquidity providers buy low now and sell high later (or: sell high now and buy low later).

Liquidity providers leave bid/ask resting orders on the order book.

</div>

Naïve investors can buy/sell at any time by trading with liquidity providers. When they buy+sell, liquidity providers earn the spread. That means that the naïve investors lose this spread. Spread is the part of naïve investors transaction costs.

<div class="definition" markdown="1">
**Definition: Stock Value**

The “true” value of the stock represents investors’ aggregate belief of how much it would pay in the future, e.g., how much dividends it will ever pay, discounting for risk and time.

At equilibrium, the true value is between the bid and the ask. Otherwise, investors could buy/sell more stocks.

</div>

Various events can change the stock’s value (i.e. change investors’ aggregate belief):

1. **Correlated stocks (securities):**
    - If someone buys gold in Chicago, the price of gold in NYC goes up.
    - ES and SPY are two ways to invest in S&P 500.
2. **The 2013 Fed Robbery:** The Federal Reserve frequently announces changes in monetary policy. On 2013, September 18th, 2:00:00 PM, when the Fed made an exciting announcement, more than \(\$5\) billion traded within 100 milliseconds. This was controversial, as it means that markets in NYC and Chicago reacted faster than speed of light.
3. **Twitter (now X):** The timing of tweets is much less regulated than Fed Reserve's announcements. For instance, the stock market moved when Trump tweeted "covfefe" in 2017. Are NLP models robust enough to make this kind of call in a few microseconds?
4. **Reddit:** The timing of posts is also much less regulated than Fed Reserve's announcements, as suggested by the impact of `r/wallstreetbets` on the GameStop stock price in 2021.
5. **Hacks:** In 2024, The @SECGov X account was compromised, and an unauthorized tweet was posted, falsely announing that the SEC had approved the listing and trading of spot Bitcoin exchange-traded products, which moved the price of Bitcoin.

<div class="definition" markdown="1">
**Definition: Snipers**

Snipers wait for a change in a stock value and rush to trade with liquidity providers’ resting orders.

When a stock value changes, liquidity providers rush to cancel (or update) their resting orders before getting sniped.

Being slightly faster than a competitor is worth a lot of money. Many races are won by a margin of less than 10 μs.

Luck also helps: sometimes, a slower order is accepted due to randomness in the stock exchange’s computer!

</div>

<div class="summary" markdown="1">
Putting it all together:

- Naïve investors rely on trading with resting orders by liquidity providers (especially in thin markets).
- When a stock value changes, snipers and liquidity providers race to update/snipe resting orders. This is risky and costly for liquidity providers.
- Liquidity providers increase the spread to make up for sniping risk.
- An increased spread means increased transaction costs for naïve investors.

</div>

## Fixes for These Market Failures?

Can the following speed bumps resolve speed arm races and reduce risk for liquidity providers?

Naïve attempts do not work:

- Symmetric speed bumps (i.e. all orders get delayed by the same amount):
    - Don’t solve speed arm races.
    - Don’t solve sniping risk for liquidity providers.
- Random speed bumps (i.e. each order gets delayed by some random amount):
    - Mostly solve speed arm races (when the random delay is greater than the speed difference).
    - Make sniping risk worse, as one liquidity provider may compete with many snipe attempts.

Better proposals exist:

- Sniper-only speed bumps (i.e. only delay sniping orders, which is technically a speed bonus to cancelling resting orders):
    - Give liquidity providers time to react to value-changing events.
    - Solve speed arm races.
    - Solve liquidity providers’ sniping risk.
        - Reduce their expected cost.
        - Liquidity providers can afford a smaller spread.
        - Reduce transaction costs for naïve investors.
- Frequent batch auctions:
    - We batch orders for some short interval (e.g. 100 ms).
    - For each batch, we find the market clearing price.
    - Advantage: everyone has time to react to value-changing-events.
    - Orders are prioritized by price instead of arrival time.    

## Flashboys 2.0

Things get even wackier on the blockchain.

<div class="definition" markdown="1">
**Definition: Smart Contracts**

So far we talked about blockchains that record payments (“transactions”).Ethereum and other blockchains (but not Bitcoin) support smart contracts:

- Smart: Can run complex computer code (ideally Turing-complete).
- Contract: Both parties agree to terms (and sign).

</div>

<div class="example" markdown="1">
**Example: Loan**

1. Alice pays Bob \(\$1\).
2. 300 blocks from now, Bob will pay Alice \(\$1.1\).

</div>

<div class="example" markdown="1">
**Example: Collateralized Loan**

This is more realistic:

1. Alice pays Bob \(\$1\) and Bob sends the contract a collateral.
2. 300 blocks from now, if Bob hasn’t paid yet, Alice can take the collateral.

</div>

In practice, some concreate instances of smart contracts include:

- Non-Fungible Tokens (NFTs).
- Shareholders votes: Once a month, every stock owner can cast a vote to decide on the next dividend.
- Gambling.
- Games (e.g., CryptoKitties).

In the collateralized loan example, it is crucial that "Alice pays Bob \(\$1\)" and "Bob sends the contract a collateral" happen simultaneously. Otherwise, Bob could abort after receiving the money. These are atomic transactions.

<div class="definition" markdown="1">
**Definition: Atomic Transactions**

Either all steps of the transaction are executed successfully, or all steps are cancelled.

</div>

<div class="example" markdown="1">
**Example: Flash Loan**

No collateral is needed when:

1. Alice pays Bob \(\$1\).
2. Bob pays Alice \(\$1.1\) back in the same block.

</div>

<div class="definition" markdown="1">
**Definition: Decentralized Finance (DeFi)**:

- Supports trading of cryptocurrencies, stocks, contracts, derivatives, etc.
- Is a popular application of smart contracts

</div>

Some variants, such as limit order book (IDEX, Paradex, Etherdelta, ...) and Automated market makers (Uniswap, Bancor) can be automated as decentralized smart contracts.

**Punchline:** Extreme sniping opportunities for decentralized finance.

## Sniping++ on DeFi

## Miners’ Extractable Value (MEV) 

## Fee sniping, selfish tie-breaking, and undercutting

## “Flashboys 0.0”

## Recap