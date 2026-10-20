# Video 13 narration script

This production script is transcribed from the `\note{...}` blocks in
`video13.tex`, following `SCRIPT_TRANSCRIPTION.md`. Each `Read` direction
expands only the newly revealed slide material; all other spoken words preserve
the authored note in source order. Slide wording flagged by `\gpt` comments in
the deck is read as displayed pending instructor review.

## Page 001: Title

Narration:
Welcome to the 13th video lecture for ECE 586, Vector Space Methods. Today, we'll combine vector spaces with metric spaces by discussing normed vector spaces and Banach spaces.

## Page 002: 3.5: Normed Vector Spaces (overlay 1 of 2)

Narration:
We continue our abstract exploration of vector spaces by defining a norm, which generalizes the idea of length in vector spaces. [[pause 0.4]] Let V be a vector space over a scalar field of real and complex numbers. [[pause 0.2]] A norm on the vector space V is a real-valued function mapping V to R, that satisfies the following properties. [[pause 0.4]] For all v in v, the norm of v is greater than or equal to zero with equality if and only if v equals the zero vector. [[pause 0.3]] For any scalar s and vector v, the norm of s v equals the absolute value of s times the norm of v. The norm of v plus w is less than or equal to the norm of v plus the norm of w, for all v and w in V. The third property is called the triangle inequality.

## Page 003: 3.5: Normed Vector Spaces (overlay 2 of 2)

Narration:
The concept of a norm is closely related to that of a metric. For instance, a metric can be defined from any norm. For a norm on the vector space V, the induced metric, d of v-comma-w, equals the norm of v minus w. Thus, every normed vector space is also a metric space and all of our earlier results for metric spaces also apply. ...

## Page 004: 3.5: Examples of Normed Vector Spaces (overlay 1 of 2)

Narration:
The following functions are examples of norms for R to the n and C to the n. The ell-one norm of v equals the sum, from i equals one to n, of the absolute value of v-i. The ell-p norm of v equals the sum, from i equals one to n, of the absolute value of v-i to the p, all to the power one over p, for p strictly between one and infinity. The ell-infinity norm of v equals the maximum, over i from one to n, of the absolute value of v-i. The ell-two norm is the standard Euclidean length of a vector.

## Page 005: 3.5: Examples of Normed Vector Spaces (overlay 2 of 2)

Narration:
The same vector may have different lengths under different norms. For v equal to three comma negative four comma twelve, the one norm is nineteen, the two norm is thirteen, and the infinity norm is twelve. For v equal to one comma i comma one, the one norm is three, the two norm is the square root of three, and the infinity norm is one. For v equal to zero comma zero comma two, all three norms equal two. In the second row, i is the imaginary unit and its absolute value is one. The third row shows that these norms may also give the same length.

## Page 006: 3.5: Norms for Function Spaces (overlay 1 of 3)

Narration:
For real or complex functions on the interval from a to b, replace sums by integrals. The L-one norm of f of t equals the integral, from a to b, of the absolute value of f of t, d t. The L-p norm of f of t equals the integral, from a to b, of the absolute value of f of t to the p, d t, all to the power one over p, for p strictly between one and infinity. The L-infinity norm of f of t equals the essential supremum, over the interval from a to b, of the absolute value of f of t. The essential supremum ignores changes on sets of zero length. For continuous functions on this interval, it equals the ordinary supremum.

## Page 007: 3.5: Norms for Function Spaces (overlay 2 of 3)

Narration:
Initially, these expressions define seminorms: the p-seminorm of f equals zero if and only if f equals zero almost everywhere, abbreviated a.e. The functions that are zero a.e. form a closed subspace in the topology induced by the seminorm. Identifying f equivalent to g when the p-seminorm of f minus g equals zero makes L-p a normed space of equivalence classes. For each p, we start with measurable functions for which the displayed expression is finite. A seminorm satisfies the norm axioms except that a nonzero function may have seminorm zero. Almost everywhere means except on a set of zero length. For example, changing a function at a single point does not change its equivalence class. The entire closed subspace of zero-a.e. functions becomes the zero vector, and the induced norm is well-defined on the equivalence classes. The standard construction uses the Lebesgue integral, but we will keep the usual function notation.

## Page 008: 3.5: Norms for Function Spaces (overlay 3 of 3)

Narration:
These spaces are infinite dimensional; retain only functions with finite norm. Otherwise, the norm would not be a real-valued function. An infinite-dimensional space does not mean that every vector has infinite norm; it means that no finite list spans the whole space.

## Page 009: 3.5: Norms Versus Metrics (overlay 1 of 3)

Narration:
We have seen that every norm induces a metric. But, does every metric define a norm? Consider vectors in R to the n with the euclidean metric: d of v-comma-w equals the square root of the sum, from i equals one to n, of v-i minus w-i squared. [[pause 0.3]] Recall the bounded metric given by d-bar of v-comma-w equal to the minimum of d of v-comma-w, and one. [[pause 0.3]] Define f, from R to the n to R, by f of v equals d-bar of v-comma-zero. Is the function f uh norm?

## Page 010: 3.5: Norms Versus Metrics (overlay 2 of 3)

Narration:
By the properties of d-bar, we have: d-bar of v-comma-zero is greater than or equal to zero, for all v in R to the n; equality holds if and only if v equals zero. [[pause 0.3]] And, d-bar of v plus w-comma-zero equals d-bar of v-comma-negative-w, which is less than or equal to d-bar of v-comma-zero, plus d-bar of w-comma-zero, for all v-comma-w in R to the n. [[pause 0.3]] So, the function f satisfies the first and third properties of a norm.

## Page 011: 3.5: Norms Versus Metrics (overlay 3 of 3)

Narration:
However, d-bar of s-v comma-zero is not always equal to the absolute value of s times d-bar of v-comma-zero. For instance, d-bar of two e-one comma-zero equals one, which is less than two times d-bar of e-one comma-zero. Thus, the function f of v equal to d-bar of v-comma-zero is not a norm. Hence, not every metric is induced by a norm.

## Page 012: 3.5: Properties of Normed Vector Spaces (overlay 1 of 3)

Narration:
Now, we consider some properties of normed vector spaces. [[pause 0.3]]
A vector v in V is called normalized if the norm of v equals one. For any v not equal to zero, consider u equal to v divided by the norm of v, so that the norm of u equals one. This follows from the second property of a norm. A normalized vector is called a unit vector.

## Page 013: 3.5: Properties of Normed Vector Spaces (overlay 2 of 3)

Narration:
For a vector space V over R or C, two norms, denoted norm sub V and norm sub V-prime, are called equivalent if there are positive reals m and capital M such that, for all v in V, m times the V-prime norm of v is less than or equal to the V norm of v, which is less than or equal to capital M times the V-prime norm of v. Equivalent norms define the same open sets and hence the same notion of convergence.

## Page 014: 3.5: Properties of Normed Vector Spaces (overlay 3 of 3)

Narration:
For finite-dimensional normed spaces, all norms are equivalent. Thus, in finite dimensions, the choice of norm does not affect whether a sequence converges. This is not true in infinite dimensions.

## Page 015: 3.5: Complete Normed Spaces (overlay 1 of 4)

Narration:
A complete normed vector space is called a Banach space.  Recall that a metric space is complete if every Cauchy sequence converges to a point in the space. And completeness is defined here using the induced metric.

## Page 016: 3.5: Complete Normed Spaces (overlay 2 of 4)

Narration:
For example, the vector space R to the n, or C to the n, with any well-defined norm is a Banach space. This follows from the completeness of the real numbers and the equivalence of all norms in finite dimensions.

## Page 017: 3.5: Complete Normed Spaces (overlay 3 of 4)

Narration:
For all p from one to infinity, let V equal ell-p be the Banach space of real sequences, v-one, v-two, v-three, and so on, with finite ell-p norm. As we mentioned earlier, only sequences with finite norm are included.

## Page 018: 3.5: Complete Normed Spaces (overlay 4 of 4)

Narration:
We also note that the vector space of continuous functions f, from the closed interval from a to b, is a Banach space under the supremum norm where the norm of f equals the supremum, over t in the domain, of the absolute value of f of t. This works because the uniform limit of continuous functions is continuous.

## Page 019: 3.5: Schauder Basis (overlay 1 of 2)

Narration:
Recall that a Hamel basis only allows finite linear combinations. Now that we have a topology, we can also consider infinite linear combinations. A Banach space V has a Schauder basis, v-one, v-two, and so on, if every v in V can be written uniquely as the sum, from i equals one to infinity, of s-i v-i, where convergence is determined by the norm topology. For example, let V equal ell-p be the vector space of real sequences with finite p-norm. Then, the standard Schauder basis is the countably infinite extension, e-one, e-two, and so on, of the standard basis.

## Page 020: 3.5: Schauder Basis (overlay 2 of 2)

Narration:
There is one caveat. A Banach space need not have a Schauder basis. Thus, this cannot be assumed in general-proofs for Banach spaces.

## Page 021: 3.5: Convergence of Sums (overlay 1 of 5)

Narration:
Now, we consider the convergence of sums in a Banach space.  Convergence is defined via the induced metric: d of v-comma-w equals the norm of v minus w. [[pause 0.4]] If the sum, from i equals one to infinity, of the norm of v-i equals the finite constant a, then the sum, from i equals one to n, of v-i converges as n goes to infinity and the norm of the limit is upper bounded by a. [[pause 0.4]] This is the Banach space analog of the fact that absolutely convergent sum of real numbers converge.

## Page 022: 3.5: Convergence of Sums (overlay 2 of 5)

Narration:
For a proof, Let a-n equal the sum, from i equals one to n, of the norm of v-i. Observe that, for n greater than m, the first equation shows that the absolute difference of the partial sums of the norms equals the sum of the intermediate terms. [[pause 0.4]] The second equation shows that the norm of the difference of the vector partial sums is upper bounded by the sum of the norms of the intermediate terms. [[pause 0.4]] The inequality follows from the triangle inequality.

## Page 023: 3.5: Convergence of Sums (overlay 3 of 5)

Narration:
Since the sum, from i equals one to infinity, of the norm of v-i converges, a-n must be a Cauchy sequence.

## Page 024: 3.5: Convergence of Sums (overlay 4 of 5)

Narration:
Since the norm of u-n minus u-m is less than or equal to the absolute value of a-n minus a-m, u-n is also a Cauchy sequence. Since a Banach space is complete, this Cauchy sequence converges to some vector u.

## Page 025: 3.5: Convergence of Sums (overlay 5 of 5)

Narration:
Once u-n converges, the norm bound is given by the triangle inequality. That is, the norm of u-n is at-most-a for all n, and this bound also holds in the limit.

## Page 026: 3.5: Open and Closed Subspaces (overlay 1 of 3)

Narration:
Uh closed subspace of a Banach space is a subspace that is a closed set in the topology generated by the norm. Recall that a closed set contains all of its limit points.

## Page 027: 3.5: Open and Closed Subspaces (overlay 2 of 3)

Narration:
All finite dimensional subspaces of a Banach space are closed. This is because every finite-dimensional normed space is complete.

## Page 028: 3.5: Open and Closed Subspaces (overlay 3 of 3)

Narration:
Now, we consider the subspace of ell-p vectors with finite support. Let W equal the set, e-one, e-two, and so on, be the standard Schauder basis of ell-p. The span of W only includes finite linear combinations. However, a sequence of finite linear combinations, like u-n equals the sum, from i equals one to n, of one over i squared times e-i, converges to the limit, as n goes to infinity, of u-n, with infinite support. This limit is not a finite linear combination of the basis vectors. Thus, the span of W is not closed. Convergence will be shown in the live session.

## Page 029: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: try the required reading, Course Notes E F 3.5. Or the recommended reading, L A D R Chapter 6 A. Also, look at the problems in Assignment 5. That's it for today. So, I'll see you next time.
