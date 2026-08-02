# Video 4 narration script

This production script follows the `\note{...}` blocks in `video4.tex`.
`Read.` expands to the matched reveal, notation is rendered as natural spoken
mathematics, and no conceptual explanation is added beyond the source notes.
Where a frame has no spoken note, only its newly revealed slide text is read.

## Page 001: Title

Narration:
Welcome to the fourth video lecture for ECE 586, Vector Space Methods. Today, we’ll discuss equivalence relations and functions.

## Page 002: 1.4: Cartesian Products and Abstract Relations (overlay 1 of 2)

Narration:
Sets of tuples and vectors. For sets A and B, the Cartesian product A cross B is the set of ordered pairs. A cross B is defined as the set of ordered pairs a comma b such that a is in A and b is in B. For n-tuples from the same set, we write A to the n equals A cross A, through n copies of A. Example: For A equal to the set containing a and b, and B equal to the set containing c and d, we have A cross B equals the set containing a c, a d, b c, and b d. A squared equals A cross A, which equals the set containing a a, a b, b a, and b b. A cubed equals the set containing a a a, a a b, a b a, a b b, b a a, b a b, b b a, and b b b.

## Page 003: 1.4: Cartesian Products and Abstract Relations (overlay 2 of 2)

Narration:
A relation, sim, between elements of A is defined by the subset R of A cross A. Specifically, we say the relation x sim y holds if and only if the ordered pair x comma y is in R. Relations are the abstraction of operators like equals, less than or equal to, greater than or equal to, less than, and greater than.

## Page 004: 1.4: Properties of Relations (overlay 1 of 5)

Narration:
The relation sim on A is said to be reflexive if x sim x holds for all x in A. That is, for all x in A, the ordered pair x comma x is in R. It is symmetric if x sim y implies y sim x for all x and y in A. It is transitive if x sim y and y sim z imply x sim z for all x, y, and z in A.

## Page 005: 1.4: Properties of Relations (overlay 2 of 5)

Narration:
It is an equivalence relation if it is reflexive, symmetric, and transitive. Example: Let A be a set of people and P of x y be the statement “x has the same birthday, month and day, as y.” Define relation sim such that x sim y holds if and only if P of x y is true. Then, R equals the set of ordered pairs x comma y in A cross A such that P of x y. Check conditions.

## Page 006: 1.4: Properties of Relations (overlay 3 of 5)

Narration:
An equivalence relation partitions A into disjoint equivalence classes. Bracket a is defined as the set of x in A such that x sim a. Here, the brackets around a, that is, bracket a, represent all elements that are equivalent to a. Notice that every element must be in some equivalence class. Also, no element can be in two different equivalence classes due to transitivity.

## Page 007: 1.4: Properties of Relations (overlay 4 of 5)

Narration:
Example: sim has an equivalence class for each possible day in a year.

## Page 008: 1.4: Properties of Relations (overlay 5 of 5)

Narration:
The set of equivalence classes is called the quotient set. A modulo sim is defined as the set of bracket a for a in A. The quotient set can be seen as the collection of subsets that partition A.

## Page 009: 1.5: Functions (overlay 1 of 7)

Narration:
A function f from X to Y is defined by a subset F of X cross Y such that A sub x, the set of y in Y for which x comma y is in F, has exactly one element for each x in X. The value of f at x in X, denoted f of x, is the unique element in A sub x.

## Page 010: 1.5: Functions (overlay 2 of 7)

Narration:
Unpacking the definition. Function f from X to Y assigns one value f of x in Y to each x in X.

## Page 011: 1.5: Functions (overlay 3 of 7)

Narration:
The notation f from X to Y emphasizes the domain X and the codomain Y.

## Page 012: 1.5: Functions (overlay 4 of 7)

Narration:
The range of f is the subset of Y achieved by f: the set of y in Y such that there exists x in X for which y equals f of x.

## Page 013: 1.5: Functions (overlay 5 of 7)

Narration:
Since the term codomain is uncommon, people sometimes use the term range instead of codomain, either intentionally or unintentionally.

## Page 014: 1.5: Functions (overlay 6 of 7)

Narration:
In basic math, functions are often described by graphs and formulas. This leads students to picture only “nice” functions.

## Page 015: 1.5: Functions (overlay 7 of 7)

Narration:
Example: Cauchy published an incorrect proof of the false assertion: “a sequence of continuous functions converging everywhere has a continuous limit.”

## Page 016: 1.5: Properties of Functions (overlay 1 of 3)

Narration:
Equality. Two functions are equal if they have the same domain, codomain, and value for all elements of the domain.

## Page 017: 1.5: Properties of Functions (overlay 2 of 3)

Narration:
A function f from X to Y is called one-to-one, or injective, if, for all x and x-prime in X, f of x equals f of x-prime implies x equals x-prime. It is onto, or surjective, if its range, the set of f of x for x in X, equals Y. It is a one-to-one correspondence, or bijective, if it is both one-to-one and onto.

## Page 018: 1.5: Properties of Functions (overlay 3 of 3)

Narration:
Inversion. A bijective function has a unique inverse function f-inverse from Y to X satisfying: for all x in X, f-inverse of f of x equals x, and, for all y in Y, f of f-inverse of y equals y. Any one-to-one function f from X to Y defines a bijective function g from X to R, where R is the range of f and g of x equals f of x for all x in X.

## Page 019: 1.5: Applying Functions to Sets (1) (overlay 1 of 3)

Narration:
For f from X to Y and subset A of X, the image of A under f is defined by f of A equals the set of y in Y such that there exists x in A for which f of x equals y, which equals the set of f of x for x in A.

## Page 020: 1.5: Applying Functions to Sets (1) (overlay 2 of 3)

Narration:
Here...

## Page 021: 1.5: Applying Functions to Sets (1) (overlay 3 of 3)

Narration:
This implies that the range of f is simply f of X.

## Page 022: 1.5: Applying Functions to Sets (2) (overlay 1 of 4)

Narration:
The inverse image, or preimage, of a subset C of Y is defined by f-inverse of C equals the set of x in X such that f of x is in C.

## Page 023: 1.5: Applying Functions to Sets (2) (overlay 2 of 4)

Narration:
Here...

## Page 024: 1.5: Applying Functions to Sets (2) (overlay 3 of 4)

Narration:
Allowing set-valued images means the set-valued inverse always exists.

## Page 025: 1.5: Applying Functions to Sets (2) (overlay 4 of 4)

Narration:
For a one-to-one f, the inverse image of a singleton containing f of x is a singleton. f-inverse of the singleton containing f of x equals the singleton containing x.

## Page 026: 1.5: Applying Functions to Sets (3) (overlay 1 of 3)

Narration:
In general, one can show: f-inverse of f of A contains A, and f of f-inverse of B is contained in B. These expressions hold because f compresses sets, that is, it can map different inputs to the same value, while f-inverse expands sets, that is, it can map a singleton to multiple values.

## Page 027: 1.5: Applying Functions to Sets (3) (overlay 2 of 3)

Narration:
Left: For f from the real numbers to the real numbers defined by f of x equals x squared, let A equal the interval from one to two, and notice that B equals f of A equals the interval from one to four. But, f-inverse of B equals the union of the intervals negative two to negative one and one to two, which contains A.

## Page 028: 1.5: Applying Functions to Sets (3) (overlay 3 of 3)

Narration:
Right: For f from the real numbers to the real numbers defined by f of x equals x squared plus one, let B equal the interval from zero to two, and notice that A equals f-inverse of B equals the interval from negative one to one. But, f of A equals f of the interval negative one to one, which equals the interval one to two and is contained in B.

## Page 029: Next Steps

Narration:
Here are some options to continue learning this material.
