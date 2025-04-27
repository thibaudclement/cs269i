# Stable Two-Sided Matchings
_April 2, 2025_

After medical school, med students start their internship called a "residency." Each (prospective) doctor has preferences over hospitals, and each hospital has preferences over doctors. How should doctors and hospitals be matched?

**Key Nuances:**

- The biggest difference between doctor-residency matching and student-dorm matching is that we now have **two-sided** preferences (each doctor and hospital have preferences over each other).
- Matching students to dorms is a _centralized_ process, while matching doctors to hospitals requires incentivizing participants to use a centralized process to prevent side deals.

## Stable Matching

<div class="definition" markdown="1">
<strong>Definition: Blocking Pair</strong>

Given a match \(M\), the pair (doctor \(i\), hospital \(j\)) forms a blocking pair if they prefer each other to their current assignments in \(M\).
</div>

For example, if Doctor \(n\) prefers Stanford over UCSF and Stanford prefers Doctor \(n\) over Doctor 1, who is currently matched, then (Doctor \(n\), Stanford) form a blocking pair. This results in an **Unstable Matching**.

**Note:** Blocking pairs exist only in two-sided matching markets. In a 1-sided matching, we cannot have blocking pairs, because in a blocking pair, both participants need to prefer each other. In the Stanford Undergraduate Housing Problem, even though students have preferences over dorms, dorms do not have preferences over students.

<div class="definition" markdown="1">
<strong>Definition: Stable Matching</strong>

A matching \(M\) is stable if there are no blocking pairs. Equivalently, for every unmatched pair \((i,j)\), either:

- Doctor \(i\) prefers Hospital \(M(i)\) over Hospital \(j\), or;
- Hospital \(j\) prefers Doctor \(M(j)\) over Doctor \(i\).
</div>

**Key Point:** Stability removes incentives to deviate from the centralized matching. For instance, if you have a stable matching between doctors and hospitals, then neither doctors nor hospitals have any incentive to deviate from the matching and match outside of the process. They might as well stay in the centralized matching, because they cannot get anything better outside of the matching process.

## Deferred Acceptance

The Deferred Acceptance Algorithm is an algorithm that finds stable matchings.

**Main idea:** Each doctor proposes to their favorite hospital that hasn't rejected them yet. Hospitals accept the best available candidate. If we discover a blocking pair, we switch the matching.

<div class="definition" markdown="1">
<strong>Mechanism: Deferred Acceptance</strong>

While there's an unmatched doctor \(i\):

- Doctor \(i\) proposes to their next-favorite hospital \(j\).
- If hospital \(j\) has no match, they accept doctor \(i\).
- Else, if hospital \(j\) prefers their current match over doctor \(i\), doctor \(i\) remains unmatched.
- Else, hospital \(j\) matches with doctor \(i\), releasing their previous match.

The algorithm stops when everyone is matched.
</div>

<div class="example" markdown="1">
<strong>Example</strong>

Consider the following agents and their respective preferences:

- **Doctors:** \(Alice (X, Y, Z)\), \(Bob (Y, X, Z)\), \(Charlie (Y, Z, X)\).
- **Hospitals:** \(X (Bob, Alice, Charlie)\), \(Y (Alice, Bob, Charlie)\), \(Z (Bob, Charlie, Alice)\).

Stable matching result: \((Alice, X), (Bob, Y), (Charlie, Z)\).
</div>

**Note:** No matter the order chosen to process the doctors, we always find the stable matching. 

<div class="theorem" markdown="1">
<strong>Theorem: Runtime of Deferred Acceptance</strong>

Deferred Acceptance runs in \(O(n^2)\) time.
</div>

This is important, because when inputs are of non-trivial size, we want to make sure the algorithm is efficient.

<div class="proof" markdown="1">
<strong>Proof:</strong>

- There are at most \(n^2\) proposals (each doctor proposes at most to \(n\) hospitals).
- Each proposal is \(O(1)\).
- So, the total runtime is \(O(n^2)\).
</div>

**Why do we have at most \(n^2\) iterations?** A doctor never proposes to the same hospital twice (we never try to match the same pair of doctor-hospital twice), because we are going down the list of preferences. So, if there are \(n\) doctors and \(n\) hospitals, then there are \(n^2\) possible doctor-hospital pairs. This is why we have at most \(n^2\) iterations (there are instances where it really takes \(n^2\) time).

**Why is each proposal \(O(1)\)?** We assume that doctor \(i\) already has a ranked list of preferences (how we get the preferences is non-trivial but outside of this algorithm). On every iteration, all we do is advance to the next hospital in the list of a doctor’s preferences (for instance, in the case of \(Bob\) above, we moved from Hospital \(Y\) to Hospital \(X\)). When a hospital needs to determine whether it prefers its current match \(i'\) over \(i\) (or not), it can use an array with the preferences of doctors (ranked): this way, it can compare the ranks in \(O(1)\) time.

<div class="theorem" markdown="1">
<strong>Theorem: Deferred Acceptance is Stable</strong>

Given \(n\) doctors and \(n\) hospitals, Deferred Acceptance outputs a complete stable matching.
</div>

<div class="theorem" markdown="1">
<strong>Corollary: A stable matching exists.</strong>

(This is not obvious!)
</div>

<div class="proof" markdown="1">
<strong>Proof (outline):</strong>

We prove that Deferred Acceptance outputs a complete stable matching with three claims:

1. The current match is stable at each iteration.
2. Once matched, hospitals remain matched.
3. At completion, everyone is matched.

Therefore, no blocking pairs exist.
</div>

**How does this proof work?** _Claim 1_ states that we have already matched some doctors and hospitals, and we assume that the matching so far is stable. _Claim 2_ states tgat once a hospital is matched, it may be matched to another doctor, but it never gets unmatched (however, doctors can get unmatched). _Claim 3_ states that no doctor, and no hospital, is unmatched at the end of the matching. Since we know that the matching is stable after each iteration, and there is no one left unmatched at the end, then the matching at the end is stable.

<div class="proof" markdown="1">
<strong>Proof of Claims:</strong>

- **Claim 1:** We assume that doctor \(d\) and hospital \(h\) are currently matched to other matches and they are a blocking pair. This means that \(d\) is matched to a worse hospital, so we must have tried to match \(d\) to \(h\), and we must have gone down the preference list, either because \(h\) refused to match to \(d\), or because \(h\) preferred another doctor. This means that \(h\) must have already matched with someone better than \(d\). This is a contradiction with the fact that \((d,h)\) is a blocking pair.
- **Claim 2:** If you look at the pseudo code of the algorithm, there is simply no command to unmatch a hospital.
- **Claim 3:** If we have a free doctor, then we need to have a free hospital as well. However, if we reach the end of the algorithm, \(d\) already tried to propose to \(h\), but after that step, \(h\) is matched (either because \(d\) matches with \(h\), or because \(h\) is already matched to another doctor). By **Claim 2**, we know that a hospital stays matched until the end of the algorithm, so \(h\) cannot be free. This is a contradiction to \(h\) being free at the end of the algorithm (we cannot have a \((d,h)\) pair free).
</div>

## Deferred Acceptance as a Mechanism

We know that Deferred Acceptance always finds a stable matching. Is it optimal? What does optimality mean?

<div class="theorem" markdown="1">
<strong>Theorem: Efficiency of Stable Matchings</strong>

Every stable matching is Pareto-optimal.
</div>

**Reminder:** An assignment \( A \) is Pareto-optimal if for any other assignment \( B \), there is a participan that (strictly) prefers \( A \) over \( B \).

<div class="proof" markdown="1">
<strong>Proof:</strong> Any deviation from a stable matching worsens at least one participant’s outcome.
</div>

**Comment:** If we take the stable matching, and any other matching (whether it is stable or not), there are going to be some doctors and/or some hospitals that prefer the stable matching over that other matching.

<div class="theorem" markdown="1">
<strong>Theorem: The matching returned by the Deferred Acceptance mechanism is doctor-optimal.</strong>

In other words, every doctor is matched to their favorite hospital possible in any stable matching.
</div>

**If we have multiple stable matchings, which one is the best one?** Doctor-optimality means that every doctor gets the best hospital they can possibly get out of any stable matching. When we talked about the student-dorms 1-sided matching, it was possible that some students were happier, while others were sadder, depending on the matching (we had some trade-offs). However, here, among all stable matchings, the matching that DA outputs is the best for every single doctor simultaneously. An implication of this theorem is that the Deferred Acceptance mechanism is also doctor-strategyproof.

<div class="theorem" markdown="1">
<strong>Corollary: Deferred Acceptance is doctor-strategyproof.</strong>

Doctors cannot gain from misreporting their preferences.
</div>

<div class="theorem" markdown="1">
<strong>Theorem: The matching returned by the Deferred Acceptance mechanism is hospital-worst.</strong>

In other words, every hospital is matched to their least favorite doctor possible in any stable matching.
</div>

<div class="theorem" markdown="1">
<strong>Corollary: Deferred Acceptance is NOT hospital-strategyproof.</strong>

Hospitals can benefit from misreporting their preferences.
</div>

<div class="example" markdown="1">
**Example**

Consider the following agents and their respective preferences:

- **Doctors:** \(Alice (X, Y, Z)\), \(Bob (Y, X, Z)\), \(Charlie (Y, Z, X)\).
- **Hospitals:** \(X (Bob, Alice, Charlie)\), \(Y (Alice, Charlie, Bob)\), \(Z (Bob, Charlie, Alice)\).

Stable matching result: \((Alice, Y), (Bob, X), (Charlie, Z)\).

By changing their preferences over \(Bob\) and \(Charlie\) (compared to the previous example setup), Hospital \(Y\) gets matched to \(Alice\) (their top choice).
</div>

**Question 1: Does a hospital need to know the preferences of the other hospitals over the doctors to game the system?**

Yes, Hospital \(Y\) needs to know the preferences of all other hospitals over all other doctors to game the system, otherwise, it is pretty hard to figure out how to game the system on the hospital side. Aviad does not know of a good strategy for hospitals to game the system.

**Question 2: If a doctor ranks their safety choices higher, does it help them?**

No. For instance, if a doctor prefers Stanford, but understands that their second favorite hospital may be less competitive (i.e. rank them higher as a doctor), it is still not in their best interest to rank that second hospital higher than Stanford in their preference list, because the DA is completely doctor-strategyproof.

**Question 3: Why is the DA mechanism hospital-worst?**

Because we are processing things in order of doctor preferences, and we are only using hospital preferences for tie-breaking purposes.

**Question 4: Does Pareto optimality change if we allow participants to have non-strict preferences?**

In practice, doctors do not rank all possible hospitals, and hospitals do not rank all possible doctors. The theorem statements do not hold exactly in practice (in particular for Pareto optimality if we have non-strict preferences).

**Question 5: As a doctor, if you know that a hospital is misrepresenting their preferences, is it still doctor-stragegyproof?**

From the doctor’s perspective, the hospitals submit some ranked lists of doctors, but they don’t know whether it truthful or not, so this is still doctor-stragegyproof. However, if a doctor can influence how a hospital reports their preferences, then they can game the system.

## Deferred Acceptance in Practice

**Why don’t we use a DA mechanism for undergrad admissions in the US?** 

In the US, the system is very decentralized, and this is a challenge for schools, because they need to admit a number of students without knowing how many are actually going to enroll—unlike hospitals, which generally have 1 or 2 residency positions available, so if none shows up, they don’t have a doctor, and if 5 show up, they cannot pay everyone—and these are generally large numbers.

Also in the US, applications are holistic, which costs money, so application fees limit the number of universities students apply to.

In contrast, in other countries where standardized tests scores are used instead of holistic reviews, DA mechanisms can be used (such as in Brazil, China, Hungary).

**How do doctors rank hospitals?**

- 1950s: DA-like algorithms initially used. At the time, there were very few female doctors (not to mention openly gay doctors).
- 1960s: Couples complicate preferences. More couples want to be near each other, i.e. doctors no longer have a ranked preference over hospitals.
- 1980s: Negative theory results on stable matching with couples. A stable matching may not exist: it is possible that there is no stable matching when you try to match couples to the same hospitals in the same cities. Deciding if a stable matching exists is an NP-complete computational problem (it is, in theory, intractable).
- 1990s: Extended DA for couples adopted.

**How do hospitals rank doctors?**

- Interviews (costly process): hospitals strategize over which doctors to interview ("safety choices").
- Standardized Tests (probably not any more: USMLE switched to pass/fail in January 2022).
- Letters of recommendation, medical school evaluation, personal statement, CV.

<div class="theorem" markdown="1">
<strong>Theorem: In DA, using safety choices is never safer for hospitals.</strong>

Formally, manipulating true ranks to move \(i-th\) doctor ("safety choice") to a higher position cannot help a hospital match with a doctor of rank \(i-or-better\).</div>

Hospitals also use "safety choices" after interviews: they may not rank first the candidates that they evaluate as “too good to come here.” This is particularly interesting since we have seen in doctor-proposing DA that ranking safety choices higher is never safer for hospitals (this is provable).

<div class="proof" markdown="1">
<strong>Proof:</strong>

- Until doctor \(i\) tries to match with a hospital, manipulation has no effect.
- After doctor \(i\) tries to match with a hospital, they can only be replaced by a better doctor.
</div>


**Yet, hospitals still strategically use "safety choices" when ranking doctors post interview. Why?**

- One possible explanation is ignorance of matching mechanisms and their properties (they did not take CS269I).
- Another possible explanation is that they consider their reputation/ego. after the matching is complete, the organization that handles the matching publishes the “number needed to fill” metric, which is the lowest ranking a hospital had to go to fill their positions. This is helpful for doctors the following year to get a sense of how competitive a program is, which is therefore also a signal of how prestigious a program is. For instance, Stanford probably don’t have to be turned down by many doctors, so their number is low, while less prestigious hospitals may need to go through more doctors and have a higher number. If a hospital ranks higher doctors that they think will join them, they can reduce their “number needed to fill” metric and appear more prestigious.

**Other DA Applications:**

- **Routing Network Packets:** Suppose that instead of doctors and hospitals, you want to match packets to servers on the internet. When you own all the servers, you don't have to worry about them matching outside of your algorithm. This would apply to a company like Akamai, who owns a lot of servers—and it actually works better in practice than in theory (because DA is very fact in practice). Packets typically get one of the top servers, so preferences lists are truncated, and the total running time is closer to \(O(n)\). Given the highly distributed nature of packet routing, every packet looks for its own server. 
- **Stanford Marriage Pact:** Matches are made between Stanford students who want to make a pact, i.e. "If we don't get married by time X, we will marry each other." DA is not used anymore (they use something closer to max weight matching instead) because in the 21st century, the graph is not bipartite, due to people having many different preferences. Stability is not a very important part of the requirement, because in practice, Stanford students spend their time looking for a partner outside of the pact/matching.

## Recap

<div class="summary" markdown="1">
<strong>Recap:</strong>

- **In theory:** DA in theory is Pareto-optimal among all matchings, doctor-optimal and hospital-worst among stable matchings, and doctor-strategyproof but not not hospital-strategyproof.
- **In practice:** DA is expensive (collecting preferences is costly, e.g. holistic admissions in US colleges and interview in hospitals) and preferences may not be captured by the model (e.g. matching couples).
</div>
