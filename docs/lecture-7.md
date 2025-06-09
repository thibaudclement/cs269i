# Market Failures
_April 21, 2025_

The vanilla assumption at the foundation of classical microeconomics is that a free market ("invisible hand") naturally converges to an optimal outcome.

<div class="definition" markdown="1">
**Definition: Market Failure**

When the market fails to converge to an optimal outcome.
</div>

It is important to understand what can go wrong in market design and which strategies exist for mitigating these issues. In this lecture, we focus on five types of market failures:

1. Externalities and public goods.
2. Transaction costs.
3. Market thinness/monopolies.
4. Timing issues.
5. Information asymmetry.

## Externalities and Public Goods

This is probably the most important market failure.

<div class="definition" markdown="1">
**Definition: Externality**

A side-effect on someone other than the seller/buyer.
</div>

In other words, an externality is the net effect a transaction has on everyone else. For instance, if you are watching a lecture online, as a side-effect, your roommate's Wi-Fi is congested.

An externality is a market failure when market participants don't have incentives to reduce negative externalities and increase positive externalities.

<div class="definition" markdown="1">
**Definition: Public Good**

Something that belongs to everybody but is owned by nobody.
</div>

A market failure occurs when market participants are under-incentivized to invest in public goods.

Ecological damage is considered as "the biggest market failure of all time." It is a side-effect of many economic activities, from hunting, to farming, and Bitcoin mining.

The environment is a public good. Whose it it? Who is vested enough to protect it? When we pollute and hurt nature, it hurts everyone (it has a lot of externality on other people, with a large total effect), and we cannot just let the free market take care of the environment.

What can we do about it?

<div class="remark" markdown="1">
**Ecological Damage Mitigation Strategies**

- **Pigouvian Tax:** Named after British economist Arthur Cecil Pigou, the idea is to tax proportionally to the externality. An example of this is a carbon tax: if you pollute, you have to pay for how much you pollute, which incentivizes you to pollute less. Similarly, if you smoke, there are externalities for other people (such as second-hand smoking and more expensive health care), so it makes sense to tax you.
- **Coasian bargaining:** Named after British economist Ronald Coase, the idea is to auction off public goods. Everyone can throw their pollution into the air because no one owns it, but if someone owned all the air, they would charge you for polluting it. However, is it a great idea that someone owns all the air? 
</div>

**Question: Is a library an example of a public good?**

Yes, it is a great example of a public good.

**Question: Can the government be a participant in the market, given that libraries and national parks are public goods, but on government land?**

We usually think of those as public goods and we think of the government not as a participant in the market but like an organization that is formed to take care of those public goods.

**Key point:** Environmental impact is a huge example of market failure, even though it is a fairly simple one.

## Transaction Costs

_**Note:** Computer science really kicks in to address this market failure._

<div class="definition" markdown="1">
**Definition: Transaction Costs**

Transaction costs are costs associated with making transactions that prevent beneficial trades.
</div>

<div class="example" markdown="1">
**Example**

I would be willing to pay \(\$10,000\) for a boat. You are happy at home, so you would rather have \(\$9,900\) than your boat. Should you sell me your boat?

- In theory: Yes! Regardless of price, we would be \(\$100\) happier in total.
- In practice: Probably not, considering a \(9\%\) sales tax.
</div>

What can we do about it? Legally, not much:

> "nothing is certain except death and taxes."

<div class="example" markdown="1">
**Example**

I am hungry and willing to pay \(\$10\) for an apple. Someone out there would rather have \(\$0.99\) than their apple. Should I buy the apple from them?

- In theory: Yes!
- In practice: How would I find them? How would I send them the money?
</div>

Finding someone with an apple might cost more than \(\$10\), even though they are out there. There is another form of transaction cost (distinct from taxes), associated with search, finding matches, and payment.

<div class="remark" markdown="1">
**Transaction Costs Mitigation Strategies**

Facilitating transactions matters because, even if in theory I would rather have an apple, and someone would rather have \(\$0.99\), finding them and paying them is hard.

Lots of companies facilitate transactions: dating apps, Couchsurfing, Airbnb, ride-hailing apps, Craigslist, eBay, Amazon, TaskRabbit, StubHub, Mechanical Turk, etc.
</div>

## Market Thickness

Market thinness is actually one _reason_ for high transaction costs.

<div class="definition" markdown="1">
**Definition: Thick Market**

We say that a market is thick if there are many buyers and many sellers.
</div>

In a thick market:

- Sellers and buyers have a lot of options.
- Prices are at (or close to) market equilibrium.
- The outcome is welfare-maximizing.

<div class="example" markdown="1">
**Example of a Thick Market:** A market in Lagos, Nigeria. There are lots of people with lots of options to go from, and a lot of competition, so we expect the price to be at or close to market equilibrium.
</div>

<div class="definition" markdown="1">
**Definition: Thin Market**

We say that a market is thin if there are few buyers and not many sellers.
</div>

In a thin market:

- There are no buyers in sight.
- If somes buyers do come, sellers monopolize.
- The outcome is sub-optimal.

<div class="example" markdown="1">
**Example of a Thin Market:** One motorcycle selling ice cream in the Faysoum Desert, Egypt. There is one seller, and zero buyer. If a buyer shows up in the middle of the desert and really wants ice cream, the seller will hike up the price and take advantage of the fact that there is only one ice cream seller in the desert.
</div>

**Why are monopolies a problem?**

When we consider sellers' incentives, the First Welfare Theorem extends to goods with reserve prices to cover costs. For example, an Airbnb host should never rent a room below the total of their cleaning cost, insurance, and hotel tax.

However, sellers setting reserve prices is _not_ strategyproof (like hospitals in DA). Moreover, sellers have simple, obvious manipulations (unlike hospitals, who had to know what other hospitals and doctors were bidding, sellers do not need that information).

<div class="example" markdown="1">
**Example: Monopoly** 

Let's consider a scenario with 1 seller (\(true \; cost = 0\)) and 1 buyer (\(value = 100\)):

- Any price between \(0\) and \(100\) would be a competitive equilibrium.
- DA-with-prices would suggest \(p = 0\) (buyer-optimal).
- The seller wants to set the reserve price to \(100\).

On Airbnb, hosts set prices: nobody is actually running DA-with-prices. Let's recall that DA-with-prices is buyer-strategyproof but _super not_ seller-strategyproof anyway.
</div>

This is why monopolies are a real problem, especially in a thin market.

However, there are ways to get around it:

- **Thick(er) market:** As a market becomes very thick (it is far from a monopoly), then it approaches seller-strategyproofness. We say that it is _strategyproof-in-the-large_.
- **Information limitation:** Sellers still need to know the buyer’s value to set a good reserve price, so if they don’t really have a lot of information, even with a monopoly, then they cannot set a very high reserve price, so information limitation helps.

What can we do about it?

<div class="remark" markdown="1">
**Market Thinness Mitigation Strategies**

If monopolies and thin markets are a problem, then one solution is to build a thick market (or make a market thicker).

Solutions include:

- Spend a lot of resources on **recruiting** a lot of early adopters to get a thick market, and then **retaining** them.
- **Scale markets**, for instance by merging existing markets (see example of kidney exchange programs).
- **Batch transactions**:
    - Every once in a while, there is a new patient and a kidney that are available for a match, and we may wonder when we should try to clear the market. In many countries, they wait 3-4 months to have a batch and try to find matches, while in the US, the frequency is much higher, i.e. around 1 week. One reason for this is that there is competition between markets, so if one market is matching every few months, and another is matching every few weeks, then you can match quicker in the latter, but it may not be an optimal match, so there is a trade-off.
    - In the context of ride-sharing/ride-hailing, when you order an Uber ride, it might wait for a couple of minutes to pool you with other people who are ordering a car to find the best matches between drivers and riders.
</div>

## Timing Issues

<div class="example" markdown="1">
**Timing Issue #1: Committing to Contracts Too Early (Market Unravelling)**

In the medical residency (doctor-hospitals) job market pre-NRMP:

- 1900's-1940's: The market was decentralized, and hospitals were racing to make offers earlier.
- If other hospitals were making offers in December, then you had to make offers in November (slightly more uncertainty, but much less competition).
- If other hospitals were making offers in Novenber, ...
- ... by 1945, hospitals were making job offers to first-year students.

This is a market failure because commitments were made too early: first-year students don’t know which speciality they want and how good they really are. There was a lot of uncertainty, it was hard to tell whether doctors were a good match, yet _because of_ uncertainty, hospitals were sending offers too early.

However, now, with the centralized system, offers are sent during the final year of study, so doctors know better what they want.
</div>

<div class="example" markdown="1">
**Timing Issue #2: Exploding Offers**

An exploding offer is like a job offer that requires a very short response.

One reason why one wants to give exploding offers is that, if a job offer is turned down, an employer needs to scramble to find someone else to fill the position.

This type of constraint is amplified when:

- There is a limited time window for making offers, since you don’t have more time to turn around.
- An employer is constrained to only hire exactly one person. If you hire 10 people, you can make 20 offers, but if you hire 1 person, you need to know very fast if they are going to accept the offer or not, so you put the pressure on the candidate.
</div>

<div class="example" markdown="1">
**The de Gea transfer**

- 24 hours is a short time window to make a goalie transfer decision worth millions of euros.
- The reason of this is that FIFA has a limited time window for when you are allowed to transfer soccer players.
- Each team has exactly one starting goalie, so they cannot make offers to three goalies (they don’t want to have 2 and they don’t want to have 0).

_**Note:** David de Gea's transfer to Real Madrid from Manchester United in 2015 failed due to administrative issues, specifically the late submission of paperwork. The deal was agreed upon, including a part-exchange deal with Real Madrid's Keylor Navas. However, the paperwork was not submitted in time for the La Liga deadline, leading to the transfer collapse._
</div>

<div class="example" markdown="1">
**An Extreme Case**

According to a 2005 applicant for federal judicial clerkships:

> "I received the offer via voicemail while I was in flight to my second interview. The judge actually left 3 messages: the first to make the offer, the second to tell me that I should respond soon, and the third to rescind the offer. It was a 35-minute flight."
</div>

<div class="example" markdown="1">
**Timing Issue #3: Not Waiting For The Market To Clear**

This is related to hiring psychologists:

- Starting at 9am, employers can call psychologists to offer them a position.
- They may say yes, and then call back and decline because they got a better offer.
- Then employers had to go back to the next psychologist on their preference list.

_You would hope that this was an employer-optimal DA mechanism._

In practice:

- Employers were worried that psychologists would reject them at 3:59pm, right before the 4:00pm deadline, so they asked that candidates commit to an accepted offer and do not switch.
- Candidates started accepting offers that may have been their safety choices rather than their favorite choice.
- Then, employers started making commitments earlier and earlier.

This resulted in a suboptimal matching and it was far from being strategyproof because psychologists started to strategize and think about whether they should commit to an employer that was a safety choice even though they may like another employer better, and therefore, it was not stable.

This is another example of market unraveling.
</div>

What can we do about it?

<div class="remark" markdown="1">
**Timing Issues Mitigation Strategies**

Solutions to deal with timing issues include:

- Use **centralized matching systems** to prevent this type of market unraveling, like we have seen for doctors and hospitals.
- Set **rules that do not allow agents to make offers before certain dates**, but in practice, these rules tend to fail, because there are incentives to bend the rules and still make early offers and ask for early commitments
- In practice, what does seem to work better is to have **rules that allow candidates to accept and then cancel exploding offers**, because if that is the norm, then it takes the kick out of exploding offers (what is the point of exploding offers if candidates can say yes immediately and then back out?).
</div>

**Question: Why does eliminating exploding offers solve this issue?**

For example, in the US, PhD candidates must accept or decline offers by April 15, and everyone know this is the rule. If Stanford says that candidate need to respond by April 1st, then the market unravels.

But if the norm is that everyone knows that students can accept Stanford by April 1st, but then still change their mind and go to Berkeley by April 14th, then there is no point for Stanford to even ask candidates to accept by April 1st.

By eliminating the ability for candidates to commit to exploding offers, it takes away the ability from universities to make exploding offers in the first place, and prevents the market from unraveling.

## Information Asymmetries

<div class="example" markdown="1">
**Cr/NC vs. Letter Grade Game (In Class)**

At LovesFun University, students can choose between Cr/NC (Pass/Fail) and a letter grade _after_ seeing their final grade for a class. It always counts for their major.

In this in-class game, groups were asked to pick a random mock grade and discuss whether they wanted to opt for Cr/NC or a letter grade.

Then, the following discussion questions were asked:

1. **When you see an internship applicant with a Cr/NC on their transcript, what do you think their letter grade must have been?** Answer: Probably a B or a C.

2. **What is the equilibrium of this game?** Answer: The equilibrium of this game is when only people who got a C- take the credit instead of the letter grade. One caveat though is that employers do not really read transcripts, they care about the GPA, so a credit can be more favorable than a grade that lowers the GPA.

**Question: What if a team that has a C- wants to show a letter grade?**

In practice, it does not make sense, because they would prefer to be mixed with people who got a B or a C on average rather than show a worse grade.
</div>

<div class="example" markdown="1">
**Example: Market for Lemons**

Suppose that you want to buy a used car. You are willing to payer more for a car in good condition. Sellers are willing to sell bad cars for less (they are eager to replace their car).

| Car Condition  | Buyer's Value | Seller's Value |
|----------------|---------------|----------------|
| **Good**       | 12            | 10             |
| **Bad**        | 6             | 4              |

Regardless of whether a car is good or bad, there is a positive **gain from trade**, i.e. the seller and the buyer are happier if they transact. This is why in an optimal market, you buy some car.

Here, we say that there is information asymmetry, because the seller knows the car condition, but the buyer doesn't.

Let \(g \in [0,1]\) be the fraction of cars in the market that are in good condition. Let \(h \leq g\) be the fraction of cars in good condition also available for sale.

What do we expect at market equilibrium?

**Possible bad equilibrium:**

- \(h = 0\), i.e. only bad cars are for sale.
- \(Price \leq 6\) since buyers assume that cars for sale are in bad condition (i. the price has to be between \(4\)—how much sellers want for their bad cars—and \(6\)—how much sellers are willing to pay for bad cars).
- Good sellers don't want to sell their cars (which is why \(h = 0\) is indeed an equilibrium).

**Possible good equilibrium:**

- \(h = g\), i.e. all sellers are trying to sell their cars.
- The buyers' willingness to pay is: \(12g + 6 \cdot (1-g) = 6 + 6g\) (i.e. \(12\) times the fraction of good cars, plus \(6\) times the fraction of bad cars).
- For good sellers to stay in the market, we need to have \(6 + 6g \geq 10\), i.e. \(g \geq \frac{2}{3}\) (the value that buyers are willing to pay for a car in an unknown condition must at least be the value that sellers of good cars are expecting to create an expectation of a good deal.)
</div>

This is not great, but it can get worse.

<div class="example" markdown="1">
**Example: Market for Lemons (Even Worse)**

Let's assume that the market is split \(\frac{1}{3}\), \(\frac{1}{3}\), \(\frac{1}{3}\) between good cars, bad cars, and lemons:

| Car Condition  | Buyer's Value | Seller's Value |
|----------------|---------------|----------------|
| **Good**       | 12            | 10             |
| **Bad**        | 6             | 4              |
| **Lemons**     | 0             | 0              |

If everyone sells, the buyer's value is at most \(\frac{1}{3} \cdot (12 + 6 + 0) = 6\). So, good sellers exit the market.

This means that the buyer's value becomes \(\frac{1}{2} \cdot (6 + 0) = 3\). So, bad sellers also exit the market.
</div>

<div class="example" markdown="1">
**Example: Market for Health Insurance**

The **good equilibrium** is that everyone buys a reasonably priced health insurance and everyone who has health insurance is taken car of.

The **problem** is that insurance companies have an incentive to sell only/mostly to healthy people. For instance, selling health insurance to college students is probably a good deal (they are younger and in better health than the average person).

If companies can sell health insurance targeted at healthier individuals/demographics, then competitors are left with less healthy people who may be more expensive to insure, which drives the prices up.

However, healthy people do not want to buy health insurance when the prices are high, only people who have higher health costs are going to buy when prices are high.

That means that health insurance companies have to raise their prices even more. In the extreme, perhaps no one has health insurance, which is a very bad equilibrium, because only unhealthy people buy very expensive health insurance and no one else is insured because it’s too expensive.
</div>

<div class="example" markdown="1">
**Example: Clickbait Content**

Content creators know whether their content is actually good content or not.

In the good equilibrium, we mostly have interesting content and a lot of audience.

However, there is the something called moral hazard, which is that it is easier and cheaper to create bad content with a clickbait-y title.

So, if the number of clicks remains the same, then creators are incentivized to resort to clickbait. As a consequence, perhaps the good creators who do not do this go bankrupt because they cannot meet the market prices (given all the clickbait creators who flood the market).

This results in a bad equilibrium, where we have mostly clickbait and users are not interested in it, so they don’t click it.
</div>

<div class="definition" markdown="1">
**Definition: Adverse Selection**

Only lemons stay in the market due to information asymmetry.
</div>

What can we do about it?

<div class="remark" markdown="1">
**Adverse Selection Mitigation Strategies**

- **Provide more information to both sides of the market**
    - For example, if you sell your car, there are mandatory disclosures (you are required by law in many states to say if you have problems with your car).
    - Before Obamacare, by law, you had to declare pre-existing health conditions, and that could hike up health insurance prices.
    - You can invest in reputation systems (rating on Yelp, Amazon), which comes with lots of great incentives in CS questions.
- **Disallow the use of information on both sides of the market**
    - For instance, with universal healthcare, you have to give health insurance to everyone, which does not allow health insurance companies to use information to pick and choose college students.
    - In the stock market, there are regulations about insider trading, where if you have insider information about whether a stock is going to go up or down, you cannot use this information to invest.
- **Disincentivize lemons**
    - For example, if a dealer has to give a guarantee over a car, they do not have an incentive to sell lemon cars (this is why many states disallow selling cars “as is”).
    - In online ads, ad platforms may not only consider the price of the ads, but also the perceived quality of the ads, for instance if it is for a better product, which incentivizes advertisers to create higher quality content (ads).
</div>

**Question: Why do we prefer providing more information for cars and less information for health insurance?**

One perspective is that, when people buy used cars, the side with the least information (the buyer) is an individual, while when people buy health insurance, the side with the most information (the buyer) is an individual, and maybe we want to side with and protect individuals, rather than larger companies.

There may also be a notion of luxury (for a car) vs. necessity (for healthy insurance), all the more since, with a car, some things will break based on how you drive (so you have incentives to drive well), while you cannot prevent yourself from getting sick (even though you still have incentives to eat well and exercise).

## Recap

<div class="summary" markdown="1">
**Market Failures Recap**

A market failure occurs when a market fails to converge to an optimal outcome.

We have seen five types of market failures:

1. Externalities and public goods.
2. Transaction costs.
3. Market thinness.
4. Timing issues.
5. Information asymmetry.

Mitigation strategies exist for all five types of market failures.
</div>

