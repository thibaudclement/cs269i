# P2P File-sharing Dilemma
(4/14/2025)

**Historical Context:** Napster (1999-2001), Gnutella (2000 onwards). Issue: Free-riding.

|            | Upload | Free-ride |
|------------|--------|-----------|
| **Upload** | (2,2)  | (-1,3)    |
| **Free-ride** | (3,-1) | (0,0)     |

Dominant Nash equilibrium: both free-ride (socially worst outcome).

## Repeated Games

Iterating game \(n\) times. What happens?

<div class="definition" markdown="1">
<strong>Definition: Subgame Perfect Nash Equilibrium (SPNE)</strong>

A Nash equilibrium valid in every subgame.
</div>

Repeated free-riding emerges by backward induction.

## Repeated Games with Discounting

Probability \(p\) that the game stops each round (discount future payoffs).

**Grim Trigger Strategy:** Free-ride forever if opponent ever free-rides.

- Always uploading payoff: \(\frac{2}{p}\)
- Always free-riding payoff: \(3\)

Equilibrium if \(p < 2/3\).

**Tit-for-Tat:** Initially upload, then match opponent’s previous action. Robust and stable.

## BitTorrent Strategies

BitTorrent is a popular P2P protocol (~30% upload traffic).

**Default Strategy:**
- Tracker coordinates peers.
- Tit-for-tat-based uploads, optimistic unchoking for random peers.

**BitThief:** Never upload, frequent peer querying.

**BitTyrant:** Upload strategically to maximize future downloads (ratio-based).
