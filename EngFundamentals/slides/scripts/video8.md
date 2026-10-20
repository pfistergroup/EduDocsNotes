# Video 8 narration script

This production script is transcribed from the `\note{...}` blocks in
`video8.tex`, following `SCRIPT_TRANSCRIPTION.md`. Each `Read` direction expands
only the newly revealed slide material; all other spoken words preserve the
authored note in source order. Page 18 retains both final proof cues on the
same rendered overlay.

## Page 001: Title

Narration:
Welcome to the eighth video lecture for ECE 586, Vector Space Methods. Today, we'll discuss the idea of compactness and its applications.

## Page 002: 2.1.4: Compactness (overlay 1 of 7)

Narration:
Compactness is a very useful property in analysis that identifies when an arbitrary metric space behaves, in some sense, like a closed and bounded subset of real numbers. A metric space, X comma d, is totally bounded if, for any epsilon greater than zero, there exists a finite set S of radius-epsilon balls that cover X. That is, the union, over x in S, of B sub d of x comma epsilon, equals X. ...

## Page 003: 2.1.4: Compactness (overlay 2 of 7)

Narration:
For example, let X be this subset of R squared.

## Page 004: 2.1.4: Compactness (overlay 3 of 7)

Narration:
For some positive epsilon, we can cover this set by a finite number of radius-epsilon balls.

## Page 005: 2.1.4: Compactness (overlay 4 of 7)

Narration:
Reducing epsilon, we can repeat this. In fact, we can do this for any epsilon greater than zero. Thus, X is totally bounded.

## Page 006: 2.1.4: Compactness (overlay 5 of 7)

Narration:
A metric space is compact if it is complete and totally bounded. We will see that compactness plays an important role in the convergence of sequences.

## Page 007: 2.1.4: Compactness (overlay 6 of 7)

Narration:
[[seed 43]]
Examples. The closed real interval from zero to one is compact. [[pause 0.2]] A subset of Euclidean R n is compact if and only if it is closed and bounded. [[pause 0.2]] But, the standard metric space of real numbers is not compact because it is not totally bounded. This is because N balls of radius epsilon can cover a width of at most two N epsilon.

## Page 008: 2.1.4: Compactness (overlay 7 of 7)

Pause-after: 2

Narration:
A closed subset A of a compact space X is itself a compact space. As an exercise, think about how you might prove this.

## Page 009: 2.1.4: Compactness and Sequences (overlay 1 of 3)

Narration:
[[seed 43]]
Let x-one, x-two, and so on, in X be a sequence; and let n-one, n-two, and so on, in the natural numbers be a strictly increasing sequence. Then, x n sub k, equal to x n sub  one, x n sub two, and so on, is a subsequence of x n.

## Page 010: 2.1.4: Compactness and Sequences (overlay 2 of 3)

Narration:
A sequence in a compact metric space has a subsequence that converges. This property is used somewhat regularly in analysis.

## Page 011: 2.1.4: Compactness and Sequences (overlay 3 of 3)

Pause-after: 2

Narration:
[[seed 43]]
For the compact metric space X equal to the closed real interval from negative two to two with absolute distance, let x n equal negative one to the n plus one over n. Then, the subsequence x-two, x-four, x-six, and so on, converges to one. This is because negative one to an even power equals one, and one over n vanishes as n tends to infinity. [[pause 0.3]] Does the sequence x n have any other limit points? Consider the subsequence x-one, x-three, x-five, and so on. Does this converge?

## Page 012: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 1 of 7)

Narration:
Now, we will outline a proof of the Bolzano--Weierstrass Theorem.  Let X equal to the closed real interval from a-naught to b-naught with the distance between x and y equal to the absolute value of x minus y. Let x n soup zero be the sequence of interest represented by the red dots.  [[pause 0.3]] We will proceed recursively by identifying subintervals I sub k equal to the closed real interval from a-k to b-k starting from I naught equal to X.  At each step, the red dots will indicate elements of the current subsequence that fall into the interval of interest.

## Page 013: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 2 of 7)

Narration:
Observe that the cardinality of the set of n in the natural numbers such that x n soup zero is in I-naught equals infinity, and split the interval I-naught in half at a-naught plus b-naught, over two.

## Page 014: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 3 of 7)

Narration:
Of the two halves, infinitely many elements of x n soup zero must lie in one of them. In the example, this is the right half and it is highlighted.

## Page 015: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 4 of 7)

Narration:
Call it I-one, and let x n soup one be the subsequence of x n soup zero in I-one. Then, the cardinality of the set of n in the natural numbers such that x n soup one is in I-one equals infinity.

## Page 016: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 5 of 7)

Narration:
Split eye-one into halves and let eye-two be a half containing infinitely many elements of x n soup one.

## Page 017: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 6 of 7)

Pause-after: 1

Narration:
Now, we can see the pattern. [[pause 0.2]] After k steps, induction shows the length of I sub k is the absolute value of b k minus a-k, equal to two to the negative k times the absolute value of b-naught minus a-naught. [[pause 0.3]]  Thus, the k-th subsequence, x n soup k in I sub k, has all elements within distance two to the negative k times the absolute value of b-naught minus a-naught from each other.

## Page 018: 2.1.4: Bolzano--Weierstrass for a Closed Real Interval (overlay 7 of 7)

Pause-after: 3

Narration:
From this, it follows that the diagonal subsequence x k soup k of x n is Cauchy. [[pause 0.2]] To understand why we need the diagonal sequence, think about why the sequence x n soup k might not converge.  Likewise, consider the sequence and x 1 soup n.

## Page 019: 2.1.5: Two Important Consequences (overlay 1 of 3)

Narration:
Let X be a metric space, and f mapping X to the real numbers be a continuous function from X to the real numbers. If A is a compact subset of X, then there exists x in A such that f of x equals the supremum of f of A; that is, f achieves a maximum on A. This result is often summarized as, "A continuous function on a compact set achieves a maximum value."

## Page 020: 2.1.5: Two Important Consequences (overlay 2 of 3)

Narration:
[[seed 43]]
The previous result allows one to define a complete metric space of functions. Let X comma d be a compact metric space, and C of X be the set of continuous functions mapping X to the real numbers. This set of functions, with the metric d infinity of f comma g, defined as the supremum over x in X of, the absolute value of, "f of x" minus "g of x", which equals the maximum over x in X of, the absolute value of "f of x" minus "g of x", defines a complete metric space.

## Page 021: 2.1.5: Two Important Consequences (overlay 3 of 3)

Narration:
We say that a metric "metrizes" a topology (which defines a type of convergence) if the two topologies have the same open sets.  In that case, convergence in the topology is equivalent to convergence under the metric.

## Page 022: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: try the suggested reading, Course Notes E F 2.1.4 through 2.1.5. Or the optional reading, M M A 2.1. Also, look at the problems in Assignment 3. That's it for today. So, I'll see you next time.

