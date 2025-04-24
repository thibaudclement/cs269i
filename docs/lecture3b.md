# Top Trading Cycles
(1/18/2023)

<div class="remark" markdown="1">
_**Note:** This lecture was skipped during the Spring 2025 quarter. Below are notes from the Winter 2023 quarter._
</div>

Previously, we studied:

- **Random Serial Dictatorship** (one-sided matching)
- **Deferred Acceptance** (two-sided matching)

**This lecture:** What happens when participants are already endowed with goods?

Example: Stanford PhD housing renewal—students face tradeoffs between renewal and lottery entry.

**Problem Setup:**

- \(n\) students, \(n\) rooms
- Each student has a current room and preference over all rooms

<div class="definition" markdown="1">
<strong>Mechanism: Top Trading Cycles (TTC)</strong>

While there are unmatched students/rooms:

1. Create a graph with unmatched rooms and students as nodes.
2. Draw edges:
   - from each room to its current owner.
   - from each student to their most preferred available room.
3. Identify cycles, remove them, and execute the trades indicated by cycles.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Runtime of TTC</strong>

Top Trading Cycles runs in \(O(n^2)\) time.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Constructing graph and edges is \(O(n)\). Finding cycles via directed edges visits at most \(2n+1\) nodes (pigeonhole principle), thus \(O(n)\). Each iteration removes at least one student; thus, overall complexity is \(O(n^2)\).
</div>

<div class="remark" markdown="1">
Input size is \(n^2\) (preference lists of length \(n\)), so TTC is linear relative to input size.
</div>

<div class="definition" markdown="1">
<strong>Definition: Individual Rationality (IR)</strong>

A mechanism is individually rational if no agent is worse off after participating.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: TTC is Individually Rational</strong>
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Students trade rooms only if they prefer the new room.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Strategyproofness of TTC</strong>

Top Trading Cycles is strategyproof.
</div>

<div class="remark" markdown="1">
This proof was noted as flawed; a corrected proof was expected.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Efficiency of TTC</strong>

TTC allocation is Pareto-optimal.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Equivalent to serial dictatorship in order cycles formed. Serial dictatorship is Pareto-optimal, thus TTC is Pareto-optimal.
</div>

## Top Trading Cycles and Chains (TTCC)

Graduating students and new students (without rooms) require modifications:

<div class="definition" markdown="1">
<strong>Mechanism: Top Trading Cycles with Chains (TTCC)</strong>

1. Process students in random order.
2. Mark student \(i\) visited:

   - If \(i\)'s top room is unoccupied, assign room, release previous.
   - If room occupied by unvisited student \(j\), move \(j\) ahead of \(i\).
   - If room occupied by visited student \(j\), cycle identified.
</div>

TTCC maintains strategyproofness, Pareto-optimality, individual rationality, and efficiency.

## TTC(C) in Practice

**Why isn't TTCC common?**

- Running TTCC repeatedly can break strategyproofness over multiple years.
- Increased strategic behavior over "popular" rooms.

**Application:** School choice (New Orleans, 2011-12) used TTC but switched to DA (Deferred Acceptance) due to simplicity in explanation.

**College Admissions:** Universities prefer specific applicants; direct trades don't apply.

**Kidney Transplants:** Kidney exchange involves patient-donor compatibility issues and logistical constraints.

**Considerations in Kidney Exchange:**

- Strategyproofness less critical (compatibility-based).
- Priority considerations (health urgency).
- Stability and central mechanism incentivization.
- Logistical challenge: Long cycles require simultaneous transplants; chains manageable.
- Dynamic arrivals/departures.
- Strategic hospitals may internally match.
- High failure probability (93% matches fail).
- Ethical issues and multi-organ exchange possibilities.
