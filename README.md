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

As it turns out, this is also a theorem of provability logic:


