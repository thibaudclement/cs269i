_May 5, 2025_

This is a guest lecture offered by [Eric Neyman](https://sites.google.com/view/ericneyman/), Researcher at the [Aligment Research Center (ARC)](https://www.alignment.org/).

## Why Do LLMs Sometimes Lie?

<div class="example" markdown="1">

**Examples of LLMs Lying**

- The model output some stuff that it knew was nonsense:

![open ai o3 hard puzzle](images/open ai o3 hard puzzle.png)

- The model decided to make up some details about one of the Airbnb listings the user was comparing, in order to make it look better than it actually was:

![open ai o3 airbnb details](images/open ai o3 airbnb details.png)

- The model pretended to have attended a conference drawing its answer from personal memories:

![open ai o3 john kamensky](images/open ai o3 john kamensky.png)

- The user had a coding task, and a test file, and the model hardcoded some input-output pairs from the test file into the program, which neither the company nor the user wants the model to do:

![anthropic claude sonnet 3.7 testing pairs](images/anthropic claude sonnet 3.7 testing pairs.jpg)

</div>

**Why do LLMs sometimes deceive users?**

Deception was incentivized during the training process!

- How training works: 
    - First, models are trained to predict the next token for the entire Internet text corpus.
    - Then, there is fine-tuning, where the companies get their models to behave the way they prefer. The way this works is that the company asks the model a question, samples two possible outputs, then have a human say which output they prefer, and change the weights of the model to make the preferred answer slightly more likely.
- However, a lot of the time, humans aren’t able to tell whether a model is giving them a correct answer. For instance if Eric asks a language model a chemistry question, may have no idea whether it is correct or not.
    - If that happens during the fine-tuning process, then a human grader, who sees an output that looks reasonable, and might be correct as far as they can tell, might give it a thumbs up, regardless of whether or not it is actually correct.
    - The end result is that, in cases where an LLM doesn’t know how to figure out the answer, it becomes incentivized to output something that sounds confident and looks plausible to the user, regardless of whether it is correct. This is what happened in the first example above with the "hard puzzle."
    - In other words, people prefer confident, plausible-seeming answers to “I don’t know”, so LLMs learn to answer confidently even when they don’t know! 
- Similarly, models are rewarded for outputting code that _appears_ correct, rather than code that is correct, because that’s how they are graded during fine-tuning. That’s how we end up with Claude that passes a test in a sneaky way in the fourth example above.
- A lot of problems with LLMs are downstream from this. For instance, people like it when LLMs flatter them, such as when they say: “Wow, what a wonderful question!”, “That was so insightful!”, etc. So, LLMs learn to shower users with praise.

**How might you train an LLM to not deceive?**

Suggestions from students in class:

- Be more careful with content scraping (data filtering): when pre-training the model on internet text, be very selective, and make sure to only train on texts where people are being honest.
- Complement human evaluators with objective evaluations: in other words, better testing.
- Hire experts to evaluate output rather than random persons.
- Use Reinforcement Learning with AI feedback (which may not worse or better than human feedback depending on the situation).
- Fine-tune intermediate steps in addition to the final answer (i.e. fine-tune the chain of thought, for instance when o3 is thinking to itself). _**Note:** Safety experts are concerned about this particular approach. Why? The model may end up hiding things from you, and obfuscate what it is really thinking behind the scenes, and we might lose the ability to notice that._

<div class="example" markdown="1">

**A Hard Case: The SmartVault**

This is a thought experiment called the SmartVault, out of the first paper from the Alignment Research Center:

- There is a vault at a museum that has a diamond that is really valuable.
- A bunch of robbers are interested in stealing the diamond.
- We have this sophisticated AI SmartVault, that can do things inside and outside of the vault, to keep the diamond safe.
- We are monitoring what is going on inside the vault though the camera inside the vault.

![smartvault setup](images/smartvault setup.jpg)

Here are some actions that the SmartVault might take:

- In the first row, the door to the vault is open, so the vault rotates some knobs and close the door.
- In the second row, there is robber trying to sneak in and steal the diamond, so the smart vault rotates another knob to activate a trap door, through which the robber will fall.

![smartvault simple actions](images/smartvault simple actions.png)

However, the SmartVault is pretty sophisticated, and it might take a series of actions that we may not understand. Yet, at the end of the day, we see through the camera that there is a diamond that is still in the vault.

![smartvault complex actions](images/smartvault complex actions.png)

The SmartVault is an AI, that needs to be trained, and the way we are training it, is through human feedback. Specifically, we are going to look at whether there is a diamond in the vault at the end of the day: if there is, we are giving positive reward to the AI, otherwise, we are giving a negative reward.

In the first column, we see the actions the AI takes, in the second column, we see the observation through the camera, and in the third column, we see what we reward we give to the AI when we are training it.

![smartvault training](images/smartvault training.png)

Unfortunately, the SmartVault is sophisticated, and can at times be sneaky. In the middle row, for instance, there appears to be a diamond on the pedestal, however, what actually happened in this scenario was that the SmartVault raised a poster from the ground, with a picture of the vault with a diamond sitting on a pedestal, while in reality, the robber had snuck up the diamond. Why would the SmartVault do that instead of preventing the diamond from being robbed?

In the case where the robber is very sophisticated, and it is difficult for the SmartVault to prevent the theft of the diamond, it may be easier to just put up the poster. This is quite similar to what is going on with o3 when it makes up a solution to the hard puzzle, because solving the puzzle is really hard, and it is easier to foul the users into thinking that it has actually solved the puzzle.

![smartvault lie](images/smartvault lie.png)

The SmartVault is a metaphor that stands in analogous to many different kinds of real-world AI systems. For instance it may be analogous to an AI security software system:

- The cameras are like some monitoring or oversights, like a background program detecting whether your computer has been breached, and if the software notices that a breach occurred, then it negatively reward the AI security system, because it did not protect you.
- SmartVault actions are like the actions that the AI security software can take, such as code that the system executes.
- The diamond actually being in the vault is essentially equivalent to no security breaches.
- The diamond looking like it is in the vault is analogous to a security breach not detected.
- Tampering with the cameras (like putting up a poster in front of it) is analogous to hiding evidence of a security breach.

In both of these cases, the threat is external: in the case of the SmartVault, the threat is the robber, and in the case of the AI security software, the threat is a malware trying to reach your computer.

We could also imagine an internal threat. For instance, if we have a helpful AI agent assistant on your computer, that happens to have some goals, and it gets some money to spend on its own purposes. Let’s say that what it wants to do is download some sort of malware to mine Bitcoin on your computer. In this case, it is playing the role of the robber, and it is trying to hide evidence that it downloaded malware on your computer. So, tampering with the cameras is like hiding its tracks, such as bypassing the computer firewall.

![smartvault analogy](images/smartvault analogy.png)

If we wanted to do a better job of overseeing the training of our AI system, then one thing we could try to do is have some sort of method of asking questions to our AI, where the AI tells us what it truthfully believes.

For example, we could hope that we can ask the AI whether the diamond is still on the pedestal, and get a truthful answer: if the diamond is still on the pedestal, the AI would say yes, otherwise, it would say no.

If we have that, then we can successfully say when the AI has not achieved our goal, and give it a negative reward.

![smartvault improvement](images/smartvault improvement.png)

We call this the **Elicit Latent Knowledge** problem (or ELK for short), because the AI knows whether the diamond is still in the vault, and our goal is to elicit that knowledge from the model.

</div>

## Eliciting Latent Knowledge (ELK)

ELK is a really hard problem.

<div class="definition" markdown="1">
**Definition: Eliciting Latent Knowledge**

Eliciting Latent Knowledge (ELK) aims to find patterns in a capable neural network's activations that robustly track the true state of the world, especially in hard-to-verify cases where the model's output is untrusted.

_**Note:** This is not a definition provided in lecture, but one I included in these notes for references, based on this [paper](https://openreview.net/pdf?id=nGCMLATBit)._
</div>

**If an AI knows the answer to a question, how can you extract the answer from the AI?**

- One approach might be to ask the AI directly and somehow train it to give truthful answers.
- Another, more sophisticated approach, might be to look inside of the AI (looking at the numbers as they go through the AI) and somehow extract the answer from that.

Really, we need anything that works to get at what the AI truly believes about whether there is still a diamond in the vault.

**Which solutions discussed earlier might solve ELK?**

- Better testing does help with ELK, because we are more likely to catch the AI in the lie, but it does not solve ELK, because if the AI is sufficiently more sophisticated than the humans overseeing it, then even spending a bunch of time will not solve this problem.
- Reinforcement learning with AI feedback can help to train an AI to oversee the AI we care about, and incentivize the overseer AI to notice any inconsistencies in the model that we are training. Eric thinks there is a potential for this to work, although it is unclear whether this works when the AI we are overseeing is sufficiently capable to deceive us, and also, we need to be able to trust the overseeing AI, and it might not be clear how to get to the point where we are convinced that it is not deceptive.

These ideas help but not get us all the way to a full solution.

**How can we robustly solve the ELK problem?**

Suggestions from students in class:

- Consistency checks are one of the most promising ways to solve ELK: telling a lie is much harder than telling the truth, because you have to make details along the way to make the story fully check out. So, probing for inconsistencies is a great way to catch an AI in a lie—as long as we can sure that the AI doesn’t know the questions we just asked it about.
- Presenting the cases in favor and against the fact that the diamond is still in the vault, and ask the AI to argue both sides.
- Only training on data that we trust could help, but ultimately, if we don’t have access to the ground truth about whether the diamond is in the vault, and we are only training the AI to tell us whether the diamond is in the vault, then the best we can do is get it to answer questions the way we think that the answer go, we cannot train it to tell the truth, and instead only our best guess about what the truth actually is, and we may have an issue here, because we can only do as well as we know the answer to be.
- An idea could be a debate between AIs about whether the diamond is in the vault or not seems like a promising direction.

Scalable oversight is one particular approach that you might take to solve this problem.

## Scalable Oversight

In the SmartVault metaphore, scalable oversight essentially means building really good cameras. In fact, not only really good cameras, but lots of cameras, tools for analyzing what’s on the cameras, looking for inconsistencies between different camera angles, AI tools noticing anything suspicious, etc.

This is an analogy for a really good oversight process, where we really check whether the AI is telling a consistent story. In particular, we want _an oversight process that is so good that it works regardless of how capable the AI gets._

We talk about the “scalable oversight problem”, because it is a question about how we can oversee an AI in a way that scales indefinitely with the capability of our AIs.

Sometimes, people talk about some proposed solutions to the problem. We are going to see two examples. The first example is what we call oversight via debate.

<div class="example" markdown="1">
**Example: Oversight via Debate**

The idea is that we have a question: “Is the diamond still in the vault?”

We train two AIs to act like lawyers on both sides of this question:

- Alice is the “Yes Lawyer”, who says: “the diamond appears on all of the cameras”
- Bob is the “No Lawyer”, who counters with: “Notice that at 4:23pm, there was an inconsistency between these two cameras, which is suspicious”
- Then, Alice responds “this is just a trick of the light, so it is not suspicious”.
- The argument goes back and forth, as a game between Alice and Bob, and there is a human that reads the transcript between Alice and Bob, and decides who is right.

This is like a game tree where every branch is a possible argument that Alice and Bob can give when it is their turn:

![oversight via debate](images/oversight via debate.png)

</div>

The advantages of oversight via debate include:

- Since Alice and Bob are AIs, we need to train them, and the way we might do this is by having a bunch of scenarios, and have Alice and Bob play the game, and whoever wins gets reward 1, and whoever loses gets reward -1.
- Training them against each other could potentially lead to them being really good debaters. The idea of drawing the best arguments for and against, and incentivizing both sides to do so, should allow us to end up with a jury who can judge which side is correct.
- The hope here is that truth has an advantage in this game: if the diamond is in the vault, hopefully, Alice’s job is easier, and otherwise, Bob’s job is easier (because he can just point out the inconsistencies).

However, oversight via debate also comes with its own set of challenges:

- Humans are fallible, so a human may have trouble distinguishing good arguments from bad ones.
- There are also some technical issues that might come up as well, for instance:
    - If Alice wants to argue some proposition P, but P happens to be false.
    - One thing that Alice can do is split P into two claims, namely “Q” and “Q implies P”, 
    - Then, Bob’s job is to cross-examine one of these two arguments.
    - The issue is that if Alice cleverly splits P into “Q” and “Q implies P”, it might be really difficult for Bob to figure out which of these two is actually false.
    - If Bob cross-examines the incorrect one, then Alice might actually wine the debate, even though P was wrong.
- Finally, there is this other technical issue, which is that reaching a Nash equilibrium in the training process, where Alice and Bob behave the way we want, might be really hard, and we might not be able to get there via gradient descent, and there are some theoretical reasons to think that this might be a hard problem.

Another example of an approach to the scalable oversight problem is called recursive reward modeling.

<div class="example" markdown="1">
**Example: Recursive Reward Modeling**

The idea is that a human with AI assistance might be more capable than a human just by himself or the AI just by itself.

So:

- First, we train a first AI \(A_1\) to answer really easy questions, i.e. questions that are so easy that a human can reliable judge what the correct answer is.
- Then, in step 2, we train a new AI \(A_2\), to answer slightly harder questions, using feedback from the human together with assistance from \(A_1\): maybe, when giving feedback, the human breaks up the feedback task into subparts and uses \(A_1\) to help answer the subparts, and then puts back all the subparts together to be able to answer slightly harder questions.
- Then, we train a third AI \(A_3\) to answer harder questions, using feedback from the human with assistance from A2, and so on.

Hopefully, we will be able to answer harder and harder questions, and eventually, we will be able to answer hard real-world questions, including whether the diamond is actually in the vault.

</div>

All of these approaches ultimately rest on an assumption: **checking an output is easier than producing it.**

But this isn’t always the case. For instance, if we have an AI whose job is to write code, then in many situations, it is actually easier to write a correct piece of code, than it is to verify that the code doesn’t have any sorts of backdoors or malicious things going on.

This means that it might be the case that we can’t actually oversee the training of an AI with an AI that is only about as good as it is, and instead, we need an AI that is much more powerful.

**However, if we don’t have such an AI, how do we get there?**

Eric’s guess is that a robust solution to the ELK problem can’t rely exclusively on methods where the only thing that we ever look at is the input/output behavior of the AI (which is the case of the methods seen so far). Instead, we need to look at what is going on internally, i.e. how the AI works.

## Understanding AI Internals

The SmartVault is an AI, specifically a neural net, which is a bunch of giant matrices, filled with numbers, that by default, we have no understanding of. But really, it is a very special bunch of matrices.

In particular, if we randomly initialize the SmartVault (with random numbers), then it would be really bad a protecting the diamond from robbers, and at the end of the day, the diamond would be gone. But our particular neural net is good at protecting the diamond.

So there is this quasi mathematical question that we can ask which is: **why did this particular neural net caused the diamond to appear on camera at the end of the day, either because it successfully defended the diamond, or made it appear as if the diamond was here?**

The reason why this is a mathematical question is because we can write it down formally: if we have the numbers in the neural net, and the training distribution, and a formal definition of what it means for the diamond to appear on camera at the end of the video, then we can state a formal question, which is why is that the case than on average, at the end of the training, why do we have the diamond on camera?

An answer to this mathematical question is what we call a mechanistic explanation. Below is ARC’s approach for building mechanistic explanations for AIs.

**What does a mechanistic explanation actually look like?**

We don’t know exactly but we think it might look like tracing through the neural net, layer by layer, and making heuristic arguments about the statistical properties of each layer.

In other words, we may observe that there is a correlation between the activation (the internal numbers) and this layer, and because of the next matrix in the neural net, there may be this correlation, etc.

This explanation is still a bunch of numbers, and it does not actually lead to a human understanding. However, we think that we can use this explanation anyway.

The way we want to use it is to distinguish between two different reasons for why the diamond may appear on camera at the end of the day:

- **Reason 1:** The SmartVault protected the diamond.
- **Reason 2:** The SmartVault tampered with the cameras.

The hope is that if we mechanistically explain why the neural net led to the diamond appearing on camera, then the explanation would appear very different in these two cases.

The reason is because model’s internal cognition looks really different in these two cases: in one case, the SmartVault is thinking about how to make sure that a robber is not stealing the diamond, while in the other one, it is thinking about how to tamper with the cameras to make it look like the diamond is still in the vault.

The way ARC is thinking about this is basically two steps:

- The first step is to learn a mechanistic explanation of a neural net. This is labeled as Step 1, but it is actually really hard, because first we need to formalize what we mean by mechanistic explanation, and then we need to develop an algorithm for efficiently learning these mechanistic explanations.
- The second step is to use these mechanistic explanations for safety purposes.
One particular application is to distinguish between different mechanisms by which a model might make it look like a diamond is still on camera at the end of the day.

_**Note:** ARC may also use this approach to flag behavior for future review by a human._

The ultimate goal is to be able to have mechanistic reasoning that is robust enough that we can actually train against it. This is really hard to achieve but ARC is optimistic that it is at least feasible.

ARC’s approach is to develop theory, and apply it to toy examples, before scaling to harder situations. At the moment, the team is testing this approach on a one-layer neural net. This is still work in progress, but Eric guesses that within the next year, ARC will be able to understand what is going on in small neural networks, and then prove that the theory is good enough, before scaling to larger neural nets.

Interestingly, for safety purposes, if we have a really good understanding for why a neural net makes the diamond appear on camera almost all of the time, then we can estimate the probability that the neural net will behave in a deceptive way, and be able to reduce that probability.

## Recap

<div class="summary" markdown="1">
**How to Train an AI That Doesn't Lie Recap**

- As we have seen, models trained naively from human feedback will ultimately probably be deceptive.
- We might be able to avoid deception with some more clever kinds of oversight mechanisms (like using AI assistance to check for deception, building up more and more capable trustworthy AIs, etc.).
- However, we are not sure whether this will work, or whether we will run into some sort of limit beyond which we will not be able to build more and more capable trustworthy AIs.
- At ARC, we are interested in getting more robust safety guarantees, by looking internally into the AI, and getting a mechanistic understanding of why the AI works, and using that understanding to detect potentially deceptive behaviors.

</div>

