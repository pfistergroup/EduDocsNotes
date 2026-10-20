# Video 12 narration script

This production script is transcribed from the `\note{...}` blocks in
`video12.tex`, following `SCRIPT_TRANSCRIPTION.md`. Each `Read` direction
expands only the newly revealed slide material; all other spoken words preserve
the authored note in source order. Pages 12 through 15 and page 18 use the
documented conservative exact-read fallback for overlays without speaker-note
cues.

## Page 001: Title

Narration:
Welcome to the 12th video lecture for ECE 586, Vector Space Methods. Today, we'll discuss Markov chains as an application of linear transforms.

## Page 002: Chutes and Ladders (overlay 1 of 2)

Narration:
Chutes and Ladders, or Snakes and Ladders, is a boardgame where a single die is rolled to determine how far you move on a gameboard defined by a grid. Some locations contain ladders that let you skip ahead while others contains chutes, or snakes, that set you back. It is based on an ancient game from India that teaches morality by associating ladders with virtues, and snakes with vices.

## Page 003: Chutes and Ladders (overlay 2 of 2)

Narration:
Question: What is the chance a player finishes the game in m or fewer moves?

## Page 004: Markov Chains (overlay 1 of 4)

Narration:
A finite-state Markov chain (or F S M C) with n states is a sequence of random variables X-one, X-two, X-three, and so on. Where X-t is the state at time t. And the probability that X t-plus-one equals j, given X-t equals i and X-one, X-two, through X t-minus-one, equals the probability that X t-plus-one equals j, given X-t equals i. In other words, the event X t-plus-one equals j is conditionally independent of the past given X t.

## Page 005: Markov Chains (overlay 2 of 4)

Narration:
If the probability that X t-plus-one equals j, given X-t equals i, does not depend on t, then the Markov chain is called time invariant. For a time-invariant F S M C, let P in R to the n by n denote the transition probability matrix with entries P sub i j, defined as the probability that X t-plus-one equals j, given X-t equals i.

## Page 006: Markov Chains (overlay 3 of 4)

Narration:
Since each row of P is a probability distribution, P sub i j is greater than or equal to zero, and the sum, from j equals one to n, of P sub i j equals one. Matrices with this property are called stochastic.

## Page 007: Markov Chains (overlay 4 of 4)

Narration:
Here we see a state transition diagram with four states.  The transitions are represented by edges whose labels show the conditional probability of following an edge given the current state.

## Page 008: Properties of Time-Invariant Markov Chains (overlay 1 of 2)

Narration:
[[seed 43]]
Now, we consider the multiple-step transition probability. The probability that X t-plus-two equals j, given X-t equals i, equals the sum, from k equals one to n, of the probability that X t-plus-two equals j, given X t-plus-one equals k, times the probability that X t-plus-one equals k, given X-t equals i. [[pause 0.5]] Replacing these probabilities by elements of the transition probability matrix reveals this as matrix multiplication and the result is the i-j entry of the matrix P squared. By induction, it follows that the probability that X t-plus-m equals j, given X-t equals i, equals the i-j entry of P to the m.

## Page 009: Properties of Time-Invariant Markov Chains (overlay 2 of 2)

Narration:
Now, we look at this in vector notation. Using the notation pie soup-t equals the row vector pie-one soup-t through pie-n soup-t, with pie-i soup-t defined as the probability that X-t equals i, we see that pie-j soup t-plus-one equals the sum, from i equals one to n, of the probability that X t-plus-one equals j and X-t equals i. [[pause 0.3]] This equals the sum, from i equals one to n, of the probability that X t-plus-one equals j, given X-t equals i, times the probability that X-t equals i. Replacing the probabilities by their matrix and vector representations, we see that this equals the sum, from i equals one to n, of P sub i j times pie-i soup t, which equals the j-th entry of pie-soup-t times P. The remaining equalities illustrate the noted induction. ...

## Page 010: Simulating a Markov Chain (overlay 1 of 6)

Narration:
Let X be a random variable with probability, X-equal-to-i, equals p-i, and cumulative distribution function F-X-of-j equals the sum, from i equals one to j, of p-i.

## Page 011: Simulating a Markov Chain (overlay 2 of 6)

Narration:
Goal: Generate a sample of X using a uniform random variable U in the interval from zero to one excluding one.

## Page 012: Simulating a Markov Chain (overlay 3 of 6)

Narration:
For example, let n equal five, and F X of j equal the sum from eye equals 1 to j of p sub eye. Note that F-X-of-j equals the probability that X is at most j.


## Page 013: Simulating a Markov Chain (overlay 4 of 6)

Narration:
To sample X, find the unique p-j interval that contains U and then return j.

## Page 014: Simulating a Markov Chain (overlay 5 of 6)

Narration:
Then, X equals the unique j satisfying U in the interval from F X of j minus one to F X of j  excluding the right endpoint.

## Page 015: Simulating a Markov Chain (overlay 6 of 6)

Narration:
[[seed 43]]
Using this, one can simulate a Markov chain. If X-t equals x, then X t-plus-one equals x-prime is generated according to. the probability that X t-plus-one equals x-prime, given X-t equals x, using the above method.

## Page 016: Hitting Time (overlay 1 of 3)

Narration:
For a Markov chain starting from state i, the first hitting time of state j  is a random variable T sub i j where the probability that T sub i j equals m equals the probability that X m-plus-one equals j, X-m is not equal to j, X m-minus-one is not equal to j, and so on through X-two is not equal to j, given X-one equals i. Thus, X-t equals j for the first time when t equals m-plus-one after starting in state i. [[pause 0.4]] By convention, the probability that T sub i j equals zero equals delta i j, where delta i j is the Kronecker delta function.  [[pause 0.3]] and, if state j is not reachable from state i, then T sub i j equals infinity. Alternatively, we have: probability that T sub i j is at most m equals the probability that there exists t in the set from one through m plus one such that X-t equals j, given X-one equals i. ...

## Page 017: Hitting Time (overlay 2 of 3)

Narration:
If X-t can get stuck in state j, that is, P sub j j equals one, then state j is called absorbing.

## Page 018: Hitting Time (overlay 3 of 3)

Narration:
If j is an absorbing state, then getting to state j means staying in state j, and the probability that T sub i j is at most m equals the probability that X m-plus-one equals j, given X-one equals i, which equals the i j entry of P to the m.

## Page 019: Stationary Probabilities of Recurrent Markov Chains (overlay 1 of 5)

Narration:
A state distribution pie is called stationary if it satisfies pie times P equals pie.

## Page 020: Stationary Probabilities of Recurrent Markov Chains (overlay 2 of 5)

Narration:
State j is reachable from state i if the i j entry of P to the m is greater than zero for some m in the natural numbers. Two states reachable from each other are communicating. A state is recurrent if it is expected to return to itself infinitely many times.

## Page 021: Stationary Probabilities of Recurrent Markov Chains (overlay 3 of 5)

Narration:
Now, we consider purr-own's theorem. If P sub i j is greater than zero for all i and j, then every state is recurrent and the Markov chain has a unique stationary distribution. This also holds if all entries of P to the m are strictly positive for some m greater than or equal to one. The stationary distribution pie equals the expected fraction of time that the process spends in each state.

## Page 022: Stationary Probabilities of Recurrent Markov Chains (overlay 4 of 5)

Narration:
One can find the stationary distribution using row reduction after rewriting pie times P equals pie as the quantity I minus P transpose times pie transpose equals zero.

## Page 023: Stationary Probabilities of Recurrent Markov Chains (overlay 5 of 5)

Pause-after: 1

Narration:
Here we see an example where both states are recurrent.

## Page 024: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: try the required reading, Markov Chains Handout. That's it for today. So, I'll see you next time.
