# Video 11 narration script

This production script is transcribed from the `\note{...}` blocks in
`video11.tex`, following `SCRIPT_TRANSCRIPTION.md`. Each `Read` direction
expands only the newly revealed slide material; all other spoken words preserve
the authored note in source order. Source wording flagged by `\gpt` comments in
the deck is retained pending instructor review.

## Page 001: Title

Narration:
Welcome to the 11th video lecture for ECE 586, Vector Space Methods. Today, we'll finish our discussion of subspaces and bases and then move on to linear transforms.

## Page 002: Sums and Direct Sums (overlay 1 of 4)

Narration:
Sums and Direct Sums allow one to combine subspaces. Let U and W be subsets of a vector space V. The sum of U and W is defined by U plus W and equals the set of v in V formed by u plus w with u in U and w in W.

## Page 003: Sums and Direct Sums (overlay 2 of 4)

Narration:
For a vector space V, subspaces U and W are called disjoint if U intersect W equals the set containing the zero vector. In this case, U and V are said to have trivial intersection because this is the smallest intersection possible since all subspaces contain the zero vector.

## Page 004: Sums and Direct Sums (overlay 3 of 4)

Narration:
For disjoint subspaces U and W in a vector space, their direct sum equals their sum but is denoted by U direct-sum W to emphasize that U and W are disjoint.

## Page 005: Sums and Direct Sums (overlay 4 of 4)

Narration:
An important property of a direct sum is that any vector v in U direct-sum W has a unique decomposition v equals u plus w, where u is in U and w is in W.

## Page 006: 3.3.3 Coordinate Systems and Vectors (overlay 1 of 4)

Narration:
Coordinate systems allow multiple representations of the same vector in different bases. If V is a finite-dimensional vector space, an ordered basis for V is a finite list of vectors that is linearly independent and spans V.

## Page 007: 3.3.3 Coordinate Systems and Vectors (overlay 2 of 4)

Narration:
If B equals v-one through v-n is an ordered basis for V, then the set containing v-one through v-n is a basis for V. But, B defines the set and a specific ordering for the vectors.

## Page 008: 3.3.3 Coordinate Systems and Vectors (overlay 3 of 4)

Narration:
For a finite-dimensional vector space V with ordered basis B equal to v-one through v-n, the coordinate vector of v in V is denoted using brackets as v sub B. It equals the unique vector s in F n such that v equals the sum, from i equals one to n, of s-i v-i.

## Page 009: 3.3.3 Coordinate Systems and Vectors (overlay 4 of 4)

Narration:
Try computing the coordinate vector for the vector one two three four using the given ordered basis. It must exist and be unique because B is a basis.

## Page 010: 3.4: Linear Transforms (overlay 1 of 3)

Narration:
Linear transformations play an important role in linear algebra. Let V and W be vector spaces over a field F. A linear transform from V to W is a function T from V into W such that T of the quantity s v-one plus v-two equals s T v-one plus T v-two, for all vectors v-one and v-two in V, and all scalars s in F; that is, T is linear.

## Page 011: 3.4: Linear Transforms (overlay 2 of 3)

Narration:
Let A be a fixed m by n matrix over F. The function T defined by T of v equals A v is a linear transformation from F to the n by one into F to the m by one. It is a good exercise to identify which properties of which objects imply this.

## Page 012: 3.4: Linear Transforms (overlay 3 of 3)

Narration:
Let V be the space of continuous functions from the closed interval zero to one to the real numbers. Define T by T-f of x equals the integral, from zero to x, of f of t d t. Then, T is a linear transform from V to V because T-f is continuous. [[pause 0.2]] Again, it is good to think how one might show this. ...

## Page 013: 3.4.2: Properties of Linear Transforms (overlay 1 of 3)

Narration:
Each linear transform has a few natural subspaces associated with it. For a linear transformation T from V to W, the range of T is the subspace of vectors w in W such that w equals T v for some v in V. It is denoted by the equation given. [[pause 0.3]] Note that this is the standard range of the function T but linearity implies it is also a subspace. Can you identify why? ...
 
## Page 014: 3.4.2: Properties of Linear Transforms (overlay 2 of 3)

Narration:
For a linear transformation T from V to W, the nullspace of T is the subspace of vectors v in V such that T v equals zero. We denote the nullspace of T by N of T equals the set of v in V such that T v equals zero. Again, how would you prove this is a subspace? ...

## Page 015: 3.4.2: Properties of Linear Transforms (overlay 3 of 3)

Narration:
This theorem describes the most important property of a linear transform. It says that a linear transform is uniquely defined by where it maps a basis. Let V and W be vector spaces over F, and B equal the set of v-alpha such that alpha is in-A be a Hamel basis for V. For each mapping G from B to W, there is a unique linear transformation T from V to W such that T v-alpha equals G of v-alpha for all alpha in-A. This will be shown in the live session.

## Page 016: 3.4.2: Rank and Nullity (overlay 1 of 3)

Narration:
The dimensions of the range and nullspace also have special names. Let V and W be vector spaces over a field F, and let T be a linear transformation from V into W. The rank of T is the dimension of the range of T, and the nullity of T is the dimension of the nullspace of T.

## Page 017: 3.4.2: Rank and Nullity (overlay 2 of 3)

Narration:
Let V and W be vector spaces over the field F, and let T be a linear transformation from V into W. If V is finite-dimensional, then rank of T plus nullity of T equals dimension of V. This will be shown in the live session. It is worth noting here that the range is a subspace of W while the nullspace is a subspace of V. ...

## Page 018: 3.4.2: Rank and Nullity (overlay 3 of 3)

Narration:
This theorem shows that number of linearly independent rows in a matrix equals the number of linearly independent columns. If A is an m by n matrix with entries in the field F, then row rank of A, defined as the dimension of the range of A transpose, equals the dimension of the range of A, which is the rank of A by definition. This will be shown in the live session. ...

## Page 019: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: try the required reading, Course Notes E F 3.3 through 3.4. Or the recommended reading, L A D R Chapter 3 A B C. Also, look at the problems in Assignment 4. That's it for today. So, I'll see you next time. ...
