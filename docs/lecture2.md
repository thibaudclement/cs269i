# Stable Two-Sided Matchings
(4/2/2025)

After medical school, med students start their internship called a "residency." Each (prospective) doctor has preferences over hospitals, and each hospital has preferences over doctors. How should doctors and hospitals be matched?

**Key Nuances:**

- The biggest difference between doctor-residency matching and student-dorm matching is that we now have two-sided preferences (each doctor and hospital have preferences over each other).
- Matching students to dorms is a centralized process; matching doctors to hospitals requires incentivizing participants to use a centralized process to prevent side deals.

## Stable Matching

<div class="definition" markdown="1">
<strong>Definition: Blocking Pair</strong>

Given a match \(M\), the pair (doctor \(i\), hospital \(j\)) forms a blocking pair if they prefer each other to their current assignments in \(M\).
</div>

For example, if Doctor \(n\) prefers Stanford over UCSF and Stanford prefers Doctor \(n\) over Doctor 1, who is currently matched, then (Doctor \(n\), Stanford) form a blocking pair. This results in an **Unstable Matching**.

**Note:** Blocking pairs exist only in two-sided matching markets.

<div class="definition" markdown="1">
<strong>Definition: Stable Matching</strong>

A matching \(M\) is stable if there are no blocking pairs. Equivalently, for every unmatched pair \((i,j)\), either:

- Doctor \(i\) prefers Hospital \(M(i)\) over Hospital \(j\), or;
- Hospital \(j\) prefers Doctor \(M(j)\) over Doctor \(i\).
</div>

**Key Point:** Stability removes incentives to deviate from the centralized matching.

## Deferred Acceptance

**Main idea:** Each doctor proposes to their favorite hospital that hasn't rejected them yet. Hospitals accept the best available candidate.

<div class="definition" markdown="1">
<strong>Mechanism: Deferred Acceptance</strong>

While there's an unmatched doctor \(i\):

1. Doctor \(i\) proposes to their next-favorite hospital \(j\).
2. If hospital \(j\) has no match, they accept doctor \(i\).
3. Else, if hospital \(j\) prefers their current match over doctor \(i\), doctor \(i\) remains unmatched.
4. Else, hospital \(j\) matches with doctor \(i\), releasing their previous match.

The algorithm stops when everyone is matched.
</div>

<div class="example" markdown="1">
<strong>Example</strong>

- **Doctors:** Alice (X, Y, Z), Bob (Y, X, Z), Charlie (Y, Z, X).
- **Hospitals:** X (Bob, Alice, Charlie), Y (Alice, Bob, Charlie), Z (Bob, Charlie, Alice).

Stable matching result: \((Alice, X), (Bob, Y), (Charlie, Z)\).
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Runtime of Deferred Acceptance</strong>

Deferred Acceptance runs in \(O(n^2)\) time.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong>

- There are at most \(n^2\) proposals (each doctor proposes at most \(n\) hospitals).
- Each proposal is \(O(1)\), hence total runtime is \(O(n^2)\).
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Deferred Acceptance is Stable</strong>

Deferred Acceptance outputs a complete stable matching.
</div>

<div class="proof" markdown="1">
<strong>Proof (sketch):</strong> Proven by three claims:

1. Current match stable at each iteration.
2. Once matched, hospitals remain matched.
3. At completion, everyone is matched.

Therefore, no blocking pairs exist.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Efficiency of Stable Matchings</strong>

Every stable matching is Pareto-optimal.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Any deviation from a stable matching worsens at least one participant’s outcome.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Proposing Optimality</strong>

Doctor-proposing Deferred Acceptance yields the doctor-optimal stable matching.
</div>

**Corollary:** Doctor-proposing DA is strategyproof for doctors.

<div class="theorem" markdown="1">
<strong>Theorem: Receiving Non-Optimality</strong>

Doctor-proposing Deferred Acceptance yields the worst stable matching for hospitals.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: Receiving Non-Strategyproofness</strong>

Hospitals can benefit from misreporting preferences.
</div>

**Think-Pair-Share:** How to make DA hospital-optimal? Flip roles (hospital-proposing).

## Deferred Acceptance in Practice

**Why no DA in US undergrad admissions?** Decentralized applications, holistic admission processes, larger applicant pools.

**Historical Doctor-Hospital Matching:**

- 1950s: DA-like algorithms initially used.
- 1960s: Couples complicate preferences.
- 1980s: Negative results—stable matching existence with couples is NP-complete.
- 1990s: Extended DA for couples adopted.

**Practical Doctor Ranking:**

- Interviews (costly)
- Tests (changing role due to USMLE)
- Safety choices (not actually safer)

<div class="theorem" markdown="1">
<strong>Theorem: No Improvements from Safety Choices</strong>

Misranking doctors (safety choices) does not secure a better match.
</div>

<div class="proof" markdown="1">
<strong>Proof:</strong> Misreporting can only worsen or have no effect on outcomes.
</div>

Hospitals use safety choices due to ignorance or prestige metrics ("number needed to fill").

**Other DA Applications:**

- Routing Network Packets: Distributed, truncated preference lists.
- Stanford Marriage Pact: Originally DA-based, now max-weight matching; stability less critical.

**Recap:** DA theoretically optimal but practical challenges (evaluating preferences) remain significant.
