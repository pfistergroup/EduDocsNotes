# Video 10 narration script

This production script is transcribed from the `\note{...}` blocks in
`video10.tex`, following `SCRIPT_TRANSCRIPTION.md`. Each `Read` direction
expands only the newly revealed slide material; all other spoken words preserve
the authored note in source order. Source wording flagged by `\gpt` comments in
the deck is retained pending instructor review.

## Page 001: Title

Narration:
Welcome to the 10th video lecture for ECE 586, Vector Space Methods. Today, we'll discuss vector spaces.

## Page 002: 3.3: Vector Spaces (overlay 1 of 4)

Narration:
Let's start by defining a vector space. A vector space consists of the following: a field F of scalars, where zero and one in F denote the additive and multiplicative identities.

## Page 003: 3.3: Vector Spaces (overlay 2 of 4)

Narration:
A set V of vectors, which are decorated by an underline in these notes.

## Page 004: 3.3: Vector Spaces (overlay 3 of 4)

Narration:
[[seed 43]]
A binary operation called vector addition, which maps any pair of vectors v and w in V to a vector v plus w in V satisfying four conditions: [[pause 0.3]] vector addition is commutative, v plus w equals w plus v; [[pause 0.3]] vector addition is associative, u plus the quantity v plus w equals the quantity u plus v plus w; [[pause 0.3]] there is a unique vector zero in V such that v plus zero equals v, for all v in V; [[pause 0.3]] and, to each v in V, there is a unique vector negative v in V such that v plus negative v equals zero.

## Page 005: 3.3: Vector Spaces (overlay 4 of 4)

Narration:
A binary operation called scalar multiplication, which maps any s in F and v in V to a vector s-v in V satisfying four conditions: [[pause 0.3]] the multiplicative identity of the field, one, is the identity and one times v equals v, for all v in V; [[pause 0.3]] scalar multiplication is associative, the quantity s-one s-two times v equals s-one times the quantity s-two v; [[pause 0.3]] scalar multiplication distributes over vector addition, s times the quantity v plus w equals s v plus s w; [[pause 0.3]] and scalar addition distributes over scalar multiplication, the quantity s-one plus s-two times v equals s-one v plus s-two v. [[pause 0.3]] Please review these rules once carefully.

## Page 006: 3.3: Vector Space Examples (overlay 1 of 2)

Narration:
A vector space is defined by choosing a set and rules for vector addition and scalar multiplication which satisfy the requirements. Consider the standard vector space for F to the n. Let F be a field, and let V equal F to the n be the set of n-tuples v equal to v-one through v-n. For w equal to w-one through w-n in F to the n, the sum of v and w is defined by element-wise addition and equals the n-tuple v-one plus w-one through v-n plus w-n. The scalar product of s in F and v in V is defined by s-v equals the n-tuple s v-one through s v-n.

## Page 007: 3.3: Vector Space Examples (overlay 2 of 2)

Narration:
Let x be a non-empty set and let y be a vector space over f.  Consider the set V of all functions mapping x to y. Define vector addition of two functions f and g in V to be the function f plus g that, when evaluated at x, equals f of x plus g of x, for all x in X, where addition on the right-hand side is defined by vector addition in Y. Define the scalar product of s in F and the function f in V to be the function s-f that, when evaluated at x, equals s times f of x for all x in X, where the multiplication on the right-hand side is defined by scalar multiplication in Y.

## Page 008: 3.3.1: Subspaces (overlay 1 of 3)

Narration:
Let V be a vector space over F. Uh subspace of V is a subset W of V which is itself a vector space over F. Subspaces play an important role in vector spaces.

## Page 009: 3.3.1: Subspaces (overlay 2 of 3)

Narration:
A subset of a vector space is a subspace if and only if it is closed under vector addition and scalar multiplication. This lemma states this principle formally. A non-empty subset W of V is a subspace of V if and only if, for every pair w-one and w-two in W and every scalar s in F, the vector s w-one plus w-two is in W. [[pause 0.3]] This lemma also makes it easy to determine when a subset is a subspace.

## Page 010: 3.3.1: Subspaces (overlay 3 of 3)

Narration:
Let A be an m by n matrix over F. Then, the subset V of F-to-the-n-by-one of vectors satisfying A v equals zero forms a subspace. Try using the Lemma to prove this.

## Page 011: 3.3: Linear Combinations (overlay 1 of 3)

Narration:
A vector w in V is said to be a linear combination of the vectors v-one through v-n in V, provided that there exist scalars s-one through s-n in F such that w equals the sum, from i equals one to n, of s-i v-i. [[pause 0.3]] For real vectors, it's likely you've all heard this term before.

## Page 012: 3.3: Linear Combinations (overlay 2 of 3)

Narration:
Let U be a list, or set, of vectors in V. The span of U, denoted span of U, is defined to be the set of all finite linear combinations of vectors in U. Note that we only consider finite linear combinations at this point because we don't yet have a topology that allows us to discuss convergence of an infinite linear combination.

## Page 013: 3.3: Linear Combinations (overlay 3 of 3)

Narration:
For a vector space V, the span of any list, or set, of vectors in V forms a subspace. This also follows easily from the lemma on the previous slide.

## Page 014: 3.3.2: Linear Dependence and Independence (overlay 1 of 2)

Narration:
[[seed 43]]
Let V be a vector space over F. Uh list of vectors u-one through u-n in V is called linearly dependent if there are scalars s-one through s-n in F, not all equal to zero, such that the sum, from i equals one to n, of s-i u-i equals zero. A list that is not linearly dependent is called linearly independent. [[pause 0.3]] Similarly, a subset U of V is called linearly dependent if there is a finite list u-one through u-n-in-U of distinct vectors that is linearly dependent. Otherwise, it is called linearly independent.

## Page 015: 3.3.2: Linear Dependence and Independence (overlay 2 of 2)

Pause-after: 2

Narration:
For V equal to R to the fourth, vectors v-one equal to "one one zero zero", v-two equal to "zero one one zero", and v-three equal to "zero zero one one", are linearly independent because u equal to s-one v-one plus s-two v-two plus s-three v-three is not equal to the zero vector unless s-one s-two and s-three are all zero.  Thus, these three vectors are linearly independent.  You can pause and read the argument in parentheses.

## Page 016: 3.3.2: Basis (overlay 1 of 2)

Narration:
Let V be a vector space over F. Let B equal the set of v-alpha such that alpha is in-A be a subset of linearly independent vectors from V such that every vector v in V can be written as a finite linear combination of vectors from B. Then, the set B is a Hamel basis for V. If V has a finite basis, it is called finite-dimensional. From this, a basis decomposition v equal to the sum, from i equals one to n, of s-i v-alpha-i, must be unique. This is because the difference between any two distinct decompositions produces a finite linear dependency in the basis and, hence, a contradiction. Thus, in vector spaces, uniqueness of representation follows from the linear independence of the basis vectors.

## Page 017: 3.3.2: Basis (overlay 2 of 2)

Narration:
Every vector space has a Hamel basis. In finite dimensions, a Hamel basis is exactly what you've seen called a basis in past linear algebra courses. For infinite dimensions, things will be different once we have a topology defined.

## Page 018: 3.3.2: Standard Basis

Narration:
Let F be a field and let a subset U of F-n be the list of vectors e-one through e-n defined to be the canonical basis. For any vector v in F to the n, define the vector v to be the sum of the canonical basis elements weighted by v-one through v-n. This shows that the collection U spans F to the n. Since U is linearly independent, v equals zero in equation one if and only if v-one through v-n all equal zero. Accordingly, the set U is a basis for F to the n. This basis is called the standard basis for F to the n.

## Page 019: 3.3.2: Dimension (overlay 1 of 2)

Narration:
The following theorem says that, if a space is spanned by n vectors then it can contain at most n linearly independent vectors. Specifically: let V be a finite-dimensional vector space that is spanned by a finite set of vectors W equal to the set containing w-one through w-n. If U equal to the set containing u-one through u-m, a subset of V, is a linearly independent set of vectors, then m is less than or equal to n. We can prove this theorem using our lemma from the last lecture based on the row-reduced echelon form.

## Page 020: 3.3.2: Dimension (overlay 2 of 2)

Narration:
Thus, all bases have the same number of vectors. The dimension of a finite-dimensional vector space is the number of elements in any basis for V. It is denoted by dimension V. [[pause 0.3]] To see this, suppose two bases have a different number of vectors. Then, if we let W be the smaller basis and U be the larger basis, we can apply the Theorem to get a contradiction.

## Page 021: 3.3.2: Invertibility (overlay 1 of 2)

Narration:
Let A in F to the n by n be an invertible matrix. Then, the columns of A form a basis for F to the n. Similarly, the rows of A will also form a basis for F to the n. [[pause 0.3]]  This shows that invertible matrices have linearly independent rows and columns.

## Page 022: 3.3.2: Invertibility (overlay 2 of 2)

Narration:
Let A be an n by n matrix over F whose columns, denoted by a-one through a-n, form a linearly independent set of vectors in F to the n. Then A is invertible. This shows a matrix is invertible if and only if its rows and columns are linearly independent.

## Page 023: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: try the required reading, Course Notes E F 3.1 through 3.3. Or the recommended reading, L A D R Chapters 1 and 2. Also, look at the problems in Assignment 4. That's it for today. So, I'll see you next time.
