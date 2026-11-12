The simplest interesting player in MIRI's [provability bot prisoner's dilemma tournament](https://arxiv.org/abs/1401.5577) was FairBot, which cooperates if it can prove its opponent cooperates.
It cooperates with another FairBot despite the apparent infinite regress, by Löb's theorem ([some might say magic](https://www.lesswrong.com/w/logical-decision-theories?lens=an-introduction-to-logical-decision-theory-for-everyone-else)).

A related line of work was how to represent statements like "if I take this action, it will have that consequence" in provability logic.
For example there's [these old slides by Vladimir Slepnev](https://web.archive.org/web/20150717031152/https://intelligence.org/wp-content/uploads/2015/05/Slepnev-Models-of-decision-making-based-on-logical-counterfactuals.pdf) that I came across on the MIRI website.

There's 
[a post by James Payor](https://www.lesswrong.com/posts/SBahPHStddcFJnyft/some-constructions-for-proof-based-cooperation-without-loeb), which I think of as alternate FairBots, which look like different formalizations of the consequence of an action.
Like, a bot that cooperates if and only if it can prove its cooperation _results_ in its opponents cooperation.
Such bots are equivalent to FairBot assuming Löb's theorem, but the idea was to cut off the infinite regress without Löb's theorem.

I'm writing this post to share some formula manipulations, simple substitutions really.
It turns out it's very easy to see that these bots are equivalent, assuming Löb's theorem.
But more importantly, we can clearly see the machinery by which Löb's theorem cuts off the infinite regress, and how these alternate formulations accomplish the same thing.

## Substituting in the FairBot formula

I'll start by just showing you the substitutions I have in mind.

FairBot:

$$P \leftrightarrow \Box Q$$

where $P$ means that the bot cooperates, $Q$ that its opponent cooperates.

For the first substitution, we'll need Löb's theorem and its trivial converse:

$$\Box(\Box Q \rightarrow Q) \leftrightarrow \Box Q$$

Substituting:

$$P \leftrightarrow \Box(\Box Q \rightarrow Q)$$

Then, substituting with the FairBot definition:

$$P \leftrightarrow \Box(P \rightarrow Q)$$

This is [Payor's "Idea #1"](https://www.lesswrong.com/posts/SBahPHStddcFJnyft/some-constructions-for-proof-based-cooperation-without-loeb#Idea__1__try_to_prove_A_B).
It's also what you would get by straightforwardly applying the formula in [the Slepnev slides](https://web.archive.org/web/20150717031152/https://intelligence.org/wp-content/uploads/2015/05/Slepnev-Models-of-decision-making-based-on-logical-counterfactuals.pdf) to formalize "I'll cooperate if that results in my opponent's cooperation".

What about Payor's ["Idea #2"](https://www.lesswrong.com/posts/SBahPHStddcFJnyft/some-constructions-for-proof-based-cooperation-without-loeb#Idea__2__try_to_prove__A_B), the subject of [Critch's post](https://www.lesswrong.com/posts/2WpPRrqrFQa6n2x3W/modal-fixpoint-cooperation-without-loeb-s-theorem)?
That says

$$P \leftrightarrow \Box(\Box P \rightarrow Q)$$

As it turns out, this is a consequence of Löb's theorem:

$$\Box(\Box\Box Q \rightarrow Q) \leftrightarrow \Box Q$$

Using this instead of Löb's theorem gets us Idea #2 the same way we got Idea #1.

Substituting:

$$P \leftrightarrow \Box(\Box Q \rightarrow Q)$$

Then, substituting with the FairBot definition:

$$P \leftrightarrow \Box(P \rightarrow Q)$$

This is [Payor's "Idea #1"](https://www.lesswrong.com/posts/SBahPHStddcFJnyft/some-constructions-for-proof-based-cooperation-without-loeb#Idea__1__try_to_prove_A_B).

What about Payor's ["Idea #2"](https://www.lesswrong.com/posts/SBahPHStddcFJnyft/some-constructions-for-proof-based-cooperation-without-loeb#Idea__2__try_to_prove__A_B), the subject of [Critch's post](https://www.lesswrong.com/posts/2WpPRrqrFQa6n2x3W/modal-fixpoint-cooperation-without-loeb-s-theorem)?
That says

$$P \leftrightarrow \Box(\Box P \rightarrow Q)$$

To get that, we use this theorem of provability logic (by which I mean [the system GL](https://plato.stanford.edu/entries/logic-provability/#AxioRule)):

$$\Box (\Box \Box Q \to  Q) \leftrightarrow  \Box Q$$

Using that instead of Löb's theorem, we obtain Idea #2 in the same way as Idea #1.

## Cutting off the infinite regress

In this section, I'm going to consider the consequences of $\lnot P$, that is, that the bot defects.
Assuming the other bot is also a FairBot, we would like this to result in some kind of contradiction, thus proving cooperation.

If I'm FairBot, it seems consistent that I defect because I can't prove you cooperate, but that's just because you defect because you can't prove I cooperate, because...

We'll start by describing this infinite regress in modal logic formulas instead of in English.
Then we'll see how Löb's theorem cuts it off, and how the alternate formulations accomplish the same thing.

### FairBot's infinite regress

FairBot again:

$$P \leftrightarrow  \Box Q$$

Since we're asking "what if I defect?", we'll negate both sides:

$$\neg P \leftrightarrow  \Diamond \neg Q$$

Since the opponent is also a FairBot:

$$\neg Q \leftrightarrow  \Diamond \neg P$$

To see the infinite regress, let's get back to substituting.
Substituting out $\neg Q$ in the first formula using the second formula:

$$\neg P \leftrightarrow  \Diamond \Diamond \neg P$$

And we can keep going:

$$\neg P \leftrightarrow  \Diamond \Diamond \Diamond \Diamond \neg P$$

We defect on each other all the way down in these possible worlds, however deep we want to look.

### Cutting it off with Löb's theorem

Well, let's look at the first substitution we did, using Löb's theorem:

$$\Box(\Box Q \rightarrow Q) \leftrightarrow \Box Q$$

Negating both sides:

$$\neg P \leftrightarrow  \Diamond (\Box Q \wedge  \neg Q)$$

I defect if, what, it's possible that you defect, even though there's a proof you cooperate?

I found this confusing, but youzicha on Tumblr pointed out that in effect, we are saying, consider the _last_ world in which you defect.
It rules out infinite chains.

To see that mechanistically, we can try substituting, using the ordinary FairBot formulas ($\lnot P \leftrightarrow  \Diamond \lnot Q$ and $\lnot Q \leftrightarrow  \Diamond \lnot P$):

$$\neg P \leftrightarrow \Diamond (\Box Q \wedge  \Diamond \neg P)$$

$$\neg P \leftrightarrow \neg \Diamond (\Box Q \wedge  \Diamond \Diamond \neg Q)$$

The right-hand side can be refuted in provability logic (that is, its negation is a theorem GL).
The $\Box Q$ contradicts the $\lnot Q$ two worlds down.
We can't keep substituting forever like we did before; the chain stops here.

$\neg P$ is equivalent to a falsehood, so we've proved cooperation.

### Cooperation in Idea #1

Repeating Idea #1:

$$P \leftrightarrow  \Box(P \rightarrow Q)$$

Negating both sides:

$$\neg P \leftrightarrow  \Diamond(P \wedge  \neg Q)$$

Actually I don't see it.
Really I want to get to the next one,

### Cooperation in Idea #2

which was

$$P \leftrightarrow  \Box(\Box P \rightarrow Q)$$

Negating both sides,

$$\neg P \leftrightarrow  \Diamond(\Box P \wedge  \neg Q)$$

[I've previously called this condition "betrayal"](https://www.lesswrong.com/posts/KRyuwyQiaDPdaHnuk/inside-the-mind-of-a-fair-player-cooperating): I defect if you betray me, that is, defect even though you can prove I cooperate.
That was in my post trying to walk through the reasoning in plain English.

Back to modal logic.
We only need one substitution with $\lnot Q \leftrightarrow  \Diamond \lnot P$:

$$\neg P \leftrightarrow  \Diamond(\Box P \wedge  \Diamond \lnot P)$$

Again, the right-hand side is refutable; $\Box P$ contradicts $\lnot P$ one world down.

## Conclusion

[Idea #2 was exciting to me because this "I imagine you imagnining me" reasoning cuts off after just a few steps](https://www.lesswrong.com/posts/LaCP6WyNzX8kiZn3w/payorian-cooperation-is-easy-with-kripke-frames).
It was my first hint that cooperation in provability logic might not be so mysterious.

Now I get that you can cut off infinite regresses with the contrapositive of Löb's theorem:

$$\Diamond P \rightarrow \Diamond (\Box P \wedge P)$$

In provability logic with Löb's theorem, these reformulations simply follow from there.

Of course the point of the reformulations is that they don't require Löb's theorem.
It's like we "already used" Löb's theorem in rewriting the condition, and now longer need to prove cooperation.

I don't know the ultimate significance of that.
But I've at least shared something of personal significance.
Once I learned why every question "bottoms out" in provability logic, I had to bring it back around, and explain why the "Payorian" approach to cooperation problems works out so nicely.
