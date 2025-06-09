# P2P File-Sharing Dilemma
_April 14, 2025_

**P2P File-Sharing History:**

- Napster (1999-2001):
    - Major file-sharing network at the time (mostly .mp3 music files).
    - Represented an estimated 40%-60% of college dorms Internet traffic.
    - Network shut down in 2001 due to copyright infringement.
- Gnutella (2000 onwards):
    - Decentralized P2P file-sharing network, harder to shut down.
    - 2010 court order to shut down popular client LimeWire (other clients remain available, but the popularity of the network is in decline).

**Challenge: Free-Riding**

- P2P file-sharing networks rely on users uploading content for sharing.
- Users want to download files for free, but there aren’t really many incentives when uploading files, so some people do not want to contribute back.
- On Gnutella, a large fraction of users only download (66% in 2000, 85% in 2005).

<div class="example" markdown="1">
**A Simplified Game Theory Model of File-Sharing**

Game theorists usually call this the Prisoners' Dilemma.

Consider the following game:

- There are two players: Harry and Marvin.
- Each player has two actions: "upload" and "free-ride".
- Their payoff is \(-1\) for uploading (due to legal risks) and \(+3\) for dowloading, which means:

|               | Upload | Free-ride |
|---------------|--------|-----------|
| **Upload**    | (2,2)  | (-1,3)    |
| **Free-ride** | (3,-1) | (0,0)     |

In other words:

- If Harry free-rides and Marvin uploads, their utility is respectively \(3\) and \(-1\)—and vice versa, if Harry uploads and Marvin free rides, their utility is respectively \(-1\) and \(3\).
- If they are both uploading, they both get \(3\) for downloading and \(-1\) for uploading.
- If they are both free riding, there is nothing happening in the network, so their utility is \(0\).

**What should they do?**

For anything Marv would do, Harry would rather free ride (and vice versa), so the optimal thing for them to do is to free ride. However, if everyone free rides, there are no files available for download, so the social welfare is the worst.

</div>

## Iterated File-Sharing Dilemma

Let's now iterate the file-sharing dilemma game \(n\) times.

<div class="example" markdown="1">
Harry and Marvin now repeat the file-sharing game \(n\) times.

- In each iteration, they play the same file-sharing dilemma game. Their strategy may depend on past iterations.
- Their goal is to maximize their total payoff across all iterations.

**What should they do? How do we model this question?**

</div>

**One consideration:** Can agents commit to a specific strategy or not? If there are two agents sharing files on the internet, it is really hard to enforce commitments towards future rounds of the game.

<div class="definition" markdown="1">
<strong>Definition: Subgame Perfect Equilibrium (SPE)</strong>

- On day \(n\), the agents play a Nash equilibrium.
- On day \(n-1\), the agents evaluate their actions assuming that they will play a Nash equilibrium on day \(n\). Then, they play a Nash equilibrium for this particular game.
- On day \(n-2\), we assume the agents will play an SPE in the future.
- Etc.
</div>

An SPE means that agents cannot commit to playing suboptimal strategies in the future. For instance, if the optimal action for them is to free-ride tomorrow, they cannot commit to uploading tomorrow.

Another way to think about this is that it is like a Nash equilibrium (they are thinking about what happens on the last day), with backward induction (they are thinking back and modeling the future with that thinking).

In a way, this inability to commit is almost like the opposite of the Stackelberg equilibrium where the leader cannot commit to a strategy profile even when the strategy profile is suboptimal given what the follower is doing.

_**Note:** Anything that Harry does will change what Marvin does, and vice versa, and Harry needs to have some model of what Marvin will do in order to determine what will maximize his utility. However, one assumption we can make is that they are never doing something that is suboptimal._

<div class="example" markdown="1">
**Example: SPE for the File-Sharing Dilemma Game Iterated \(n\) Times**

|               | Upload | Free-ride |
|---------------|--------|-----------|
| **Upload**    | (2,2)  | (-1,3)    |
| **Free-ride** | (3,-1) | (0,0)     |

- In the \(n\)-th iteration, free-riding is the dominant strategy. Note that what happened in the past does not change incentives here.
- In the \((n-1)\)-th iteration, free-riding is still strategic. No matter what a player does now, both will free-ride in the next iteration.
- By induction, free-riding is strategic in every iteration.
</div>

## Repeated Games with Discounting

<div class="example" markdown="1">
**Example: \((1-p)\)-Discounted File-Sharing Dilemma**

|               | Upload | Free-ride |
|---------------|--------|-----------|
| **Upload**    | (2,2)  | (-1,3)    |
| **Free-ride** | (3,-1) | (0,0)     |

**Random-stopping assumption:** We are playing—possibly forever when \(p = 0\). At every iteration, we stop playing with probability \(p\) (for instance because another player’s connection defaults, or because there was a lawsuit against the network, etc.).

In other words, Harry and Marvin repeat the file-sharing game:

- In each iteration, they play the same file-sharing dilemma game. Now, their strategy _may_ depend on past iterations.
- At each iteration, they stop with probability \(p\).
- Their goal is to maximize their total payoff across all iterations.

Here, it is less obvious what players should do (due to the random stopping rule).
</div>

_**Note:** This is also a popular model in general (outside of file-sharing) to model interest rates because you would rather have your money today than tomorrow, so every day in the future is worth a little less._

One possible strategy that Harry can choose is called the Grim Trigger Strategy.

<div class="definition" markdown="1">
**Definition: The Grim Trigger Strategy**

- If there was ever a time when Marvin did not upload, do not upload ever again.
- Otherwise, upload.
</div>

Essentially, if there is ever a time when Marvin free-rides, then from that point on, Harry free-rides forever, but until then, he uploads. This is all about making a threat: if Marvin ever stops sharing, then Harry will stop sharing with him. Note however that, on the last day, there is no threat, because there is no future.

Let's analyze Marvin’s optimal strategy, given that Harry is playing the Grim Trigger Strategy. We are assuming that Marvin believes that Harry will actually play Grim Trigger (we will see later why this is a possible assumption). In this scenario, Marvin’s optimal strategy is either to always upload or to never upload, and which one is optimal depends on \(p\).

<div class="example" markdown="1">
**Analysis: Marvin's Strategy When Harry Plays The Grim Trigger**

|               | Upload | Free-ride |
|---------------|--------|-----------|
| **Upload**    | (2,2)  | (-1,3)    |
| **Free-ride** | (3,-1) | (0,0)     |

**Always Uploading:** If Marvin always uploads, Harry also always uploads, so every day they keep playing, Marvin has an expected payoff of \(2\).
This is why the payoff is basically \(2 \cdot the \; geometric \; sequence \; for \; (1-p)\), which comes down to \(\frac{2}{p}\).
In other words, if Marvin always uploads, his expected utility is \(\frac{2}{p}\).

**Never Uploading:** If Marvin never uploads, in the first iteration, Harry uploads, and then Harry sees that Marvin did not upload, so he is never going to upload again. The payoff for Marvin is \(3\) for the first day, and \(0\) for the rest of time, meaning that his utility is \(3\).

**Conclusion:** To decide whether he should always upload or never upload, Marvin should ask when \(3\) is greater than \(\frac{2}{p}\), which means that he should always upload when \(p \leq \frac{2}{3}\).
 
</div>

If Harry is playing the Grim Trigger strategy, then it makes sense for Marvin to always upload whenever \(p \leq \frac{2}{3}\). So, if the game ends every day with probability \(\frac{1}{2}\), then it makes sense for both Harry and Marvin to always upload, which is why this is an SPE.

**Question:** We saw earlier that for any number of iteration \(n\), both players should play the strategy of never uploading. How could it be that it makes sense for Marvin to always upload whenever \(p \leq \frac{2}{3}\), if for any \(n\), the SPE is to never upload?

The point is that, in the random-stopping game, the players do not know in advance when the game is going to end, so any day, they are still doing the same calculations that we just did (on day \(7\), it is still the same as on day \(1\)), which is why there is always an incentive to upload and make their future better, because they don’t know when the future terminates. However, when we analyze the SPE with \(n\) days, we know when the last day is, so we can determine when there is no point uploading (because there is no future).

<div class="theorem" markdown="1">
**Theorem: Folk Theorem (Game Strategy)**

If the players are patient enough, then repeated interaction can result in virtually any average payoff in an SPE equilibrium.

</div>

In other words, the Folk theorem gives general conditions on when Harry can incentivize Marvin to play certain actions (e.g., uploading) using threats like the Grim Trigger strategy.

One issue with the Grim Trigger strategy is that, if for some reason, Marvin's connection goes down one day and he cannot upload, then Harry will never upload again, and Marvin in turn will not upload again, so they get stuck with a utility of \(0\) until the end of the game.

A more practical, robust alternative to the Grim Trigger strategy is called the Tit-for-Tat strategy.

<div class="definition" markdown="1">
**Definition: The Tit-for-Tat Strategy**

- In stage \(1\), upload.
- In stage \(i\), reproduce the action of the other player on stage \(i-1\).
</div>

<div class="example" markdown="1">
**Analysis: Marvin's Choices When Playing Tit-for-Tat**

|               | Upload | Free-ride |
|---------------|--------|-----------|
| **Upload**    | (2,2)  | (-1,3)    |
| **Free-ride** | (3,-1) | (0,0)     |

At stage \(i\), Marvin can:

- Upload on stage \(i\) (utility of \(-1\)), and then download on stage \(i+1\) (utility of \(+3\)) with probability \((1-p)\), because there is the probability that there is no next day.
- Not upload on stage \(i\) (utility of \(0\)), and then not download on stage \(i+1\) (utility of \(0\)).

**Conclusion:** To decide whether he should always upload or never upload, Marvin should ask when \(-1 + 3 \cdot (1-p) \geq 0\), which means that he should always upload whenever \(p \leq \frac{2}{3}\).

</div>

_**Notes:**_

- _The conclusion is the same for Tit-for-Tat as for Grim Trigger, but this is a coincidence: in general, Grim Trigger is a stronger threat._
- _When \(p = \frac{2}{3}\), then both “always upload” and “never upload” are strategic._

<div class="summary" markdown="1">
**Iterated File-Sharing Dilemma Recap**

1. In a one-shot game, free-riding is a strictly dominant strategy, i.e. for any action Marvin takes, Harry is always better off _not_ uploading.
2. With any fixed number of iterations, free-riding is the SPE.
3. With a random number of iterations, a credible threat of future retaliation can lead to cooperation.
</div>

In practice, game theory predicts that:

1. Players do not cooperate in one-round games.
2. Players do not cooperate in \(n\)-round games.
3. Players likely cooperate in games with a random number of rounds.

In fact, in the real world, we frequently observe \((1)\) and \((3)\): in tourist traps, restaurants might as well charge customers as much as they can, because they will only see them once, while in locals’ favorite spots, restaurants expect customers to come over and over, so they have incentives to serve them well.

What about \((2)\)?

<div class="example" markdown="1">
**Experiment: Axelrod Games**

Around 1980, Professor Robert Axelrod invited friends to write computer programs for a tournament of iterated file-sharing dilemma with a fixed number of round \(n = 200\).

Out of 15 submissions, Tit-for-Tat won first place.

**Notes:**

- Tit-for-Tat can never win a head-to-head match, but encouraging cooperation leads to a higher score on average.
- You can always do better than Tit-for-Tat: you can play Tit-for-Tat during \(199\) rounds, and not upload in the last round, but in practice, no participant tried this strategy.

Later on, Professor Axelrod invited his friends to play again. Out of 62 submissions, Tit-for-Tat won first place again.
</div>

_**Note:** Veritasium's _[What Game Theory Reveals About Life, The Universe, and Everything](https://www.youtube.com/watch?v=mScpHTIi-kM)_ YouTube video offers an excellent perspective on this topic._

So, in practice, \((2)\) requires fragile assumptions: Harry assumes in round \(i\) that \(\rightarrow\) Marvin assumes in round \(i+1\) that \(\rightarrow\) Harry assumes in round \(i+2\) that \(\rightarrow\) ... plays optimally in round \(n\).

## BitTorrent Strategies

<div class="example" markdown="1">
**Definition: BitTorrent Overview**

- BitTorrent is currently the main P2P protocol for file-sharing.
- In 2019, BitTorrent accounted for almost 30% of upload traffic (with major spikes after episodes of Game of Thrones).
- Users are organized into swrams sharing the same file.
- A decentralized tracker coordinates active users in a given swarm.
- Each file is broken down into a number of pieces (e.g. 1,000).
- Since users need many (all) pieces, they play the iterated file-sharing dilemma game.
</div>

<div class="definition" markdown="1">
**Definition: The BitTorrent Default Strategy**

This is the strategy most users play because they just download the default BitTorrent client that uses this strategy by default:

- Every 15-30 minutes, a user contacts the tracker, requesting a new random subset of swarm peers. So, their number of known swarm peers grows over time.
- Each user attempts to download from their peers.
- Each user has \(s\) slots and allocates \(\frac{1}{s}\) of upload bandwidth to each slot.
- \(s\) peers receive a slot ("unchoked"), chosen using a variant of the Tit-for-Tat strategy: each user prioritizes peers who sends them the most data. One slot is reserved for "pity uploads" to random peers ("optimistic unchoking"), i.e. a freebee for users who do not have data yet (to give "newbies" a chance).
- For each fixed peer, the priority is given to uploading rare file pieces.
</div>

<div class="definition" markdown="1">
**Definition: The BitThief Strategy**

- Never upload anything.
- Ask tracker for peers much more frequently (to grow the number of peers quickly).

The idea is to maximize the chances of optimistic unchoke. In experiments, though, this strategy is \(5\) times slower than the default BitTorrent strategy. It still completes downloads in reasonable time without any uploads.
</div>

<div class="definition" markdown="1">
**Definition: The BitTyrant Strategy**

In the Tit-for-Tat/BitTorrent strategy, the idea is to upload data to peers who send you the most data.

In contrast, in the BitTyrant strategy, the idea is to upload data to peers who _will_ send you the most data:

- For each peer \(j\), estimate the amount of upload \(u_j\) so that \(j\) unchokes you.
- For each peer \(j\), estimate the speed of dowload \(d_j\) if \(j\) unchockes you.
- Prioritize sending as much data as possible to peer with the maximum \(\frac{d_j}{u_j}\) ratio.

In other words, the rationale is to look for peers who will give you the most data if you give them a little bit of data.

In experiments, this provides \(\approx 70\%\) download speed gains over the standard BitTorrent strategy.
</div>

<div class="summary" markdown="1">
**BitTorrent Strategies Recap**

- **Tit-for-Tat (default):** Prioritize sending data to peers who send you the most data. Reserve one upload slot for new users ("optimistic unchoke").
- **BitThief:** Don't upload anything. Contact as many peers as possible to maximize chances of optimistic unchoke.
- **BitTyrant:** Prioritize sending data to peers who would send you the most data in return.
</div>

## Recap

<div class="summary" markdown="1">
**P2P File-Sharing Recap**

- **Free-riding** Users only download, and don't contribute uploads to others.
- **One-shot file-sharing dilemma:** Free-riding is a dominant strategy.
- **Iterated file-sharing dilemma:** Tit-for-Tat encourages uploads.
- **Subgame Perfect Equilibrium (SPE):** Agents choose today's optimal strategy, assuming they will play an SPE in the future.
- **BitTorrent (decentralized Tit-for-Tat):** Free-riding is possible on optimistic unchokes. Strategizing over which peers give the best return for uploads is also possible.
</div>