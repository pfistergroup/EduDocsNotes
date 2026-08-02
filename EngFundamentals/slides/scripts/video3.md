# Video 3 narration script

This production script follows the `\note{...}` blocks in `video3.tex`.
`Read.` expands to the matched reveal, notation is rendered as natural spoken
mathematics, and no conceptual explanation is added beyond the source notes.

## Page 001: Title

Narration:
Welcome to the third video lecture for ECE 586, Vector Space Methods. Today, we’ll discuss set theory.

## Page 002: 1.4: Set Theory (overlay 1 of 9)

Narration:
Set theory is the foundation, along with logic, of all modern mathematics.

## Page 003: 1.4: Set Theory (overlay 2 of 9)

Narration:
Numbers, relations, functions, and so on, are all defined using set theory.

## Page 004: 1.4: Set Theory (overlay 3 of 9)

Narration:
But, it’s not as simple as one would hope because naive approaches are inconsistent. That is, for some P, the definitions imply P and not P.

## Page 005: 1.4: Set Theory (overlay 4 of 9)

Narration:
Axiomatic approaches avoid contradictions but are overly complicated.

## Page 006: 1.4: Set Theory (overlay 5 of 9)

Narration:
Thus, we use naive set theory, which defines the operations of set theory without worrying about paradoxes. This is sufficient for engineering math.

## Page 007: 1.4: Set Theory (overlay 6 of 9)

Narration:
Naive set theory. A set is defined as “any collection of objects, mathematical or otherwise.” For example, consider “the set of all books published in 2007.”

## Page 008: 1.4: Set Theory (overlay 7 of 9)

Narration:
Objects in a set are called elements or members of the set.

## Page 009: 1.4: Set Theory (overlay 8 of 9)

Narration:
The logical statement “a is a member of the set capital A” is denoted “a in capital A”.

## Page 010: 1.4: Set Theory (overlay 9 of 9)

Narration:
Its negation, “a is not a member of the set A,” is denoted “a not in A.”

## Page 011: 1.4: Using Set Theory (overlay 1 of 7)

Narration:
Now, we consider howone defines sets. First, one can present a set by listing elements. For the standard English vowels, A equals the set containing a, e, i, o, and u.

## Page 012: 1.4: Using Set Theory (overlay 2 of 7)

Narration:
A key property of sets is that element order is irrelevant: the set containing i, o, u, a, and e is the same as A. Also, repeated elements have no effect: the set containing a, e, i, o, u, e, and o is the same as A.

## Page 013: 1.4: Using Set Theory (overlay 3 of 7)

Pause-after: 0.3

Narration:
A singleton is a set containing exactly one element, such as the set containing a.

## Page 014: 1.4: Using Set Theory (overlay 4 of 7)

Narration:
The following blackboard bold symbols are used denote some standard sets: the integers by Z; the real numbers by R; and the complex numbers by C.

## Page 015: 1.4: Using Set Theory (overlay 5 of 7)

Narration:
We can also build new sets from old sets. For example, set-builder notation defines, for a logical predicate P of x, defined on x in X, “A is the set of elements in X such that P of x is true” is denoted by A equals x-in-X such that P of x.

## Page 016: 1.4: Using Set Theory (overlay 6 of 7)

Narration:
If no x in X satisfies P of x, then the result is the empty set.

## Page 017: 1.4: Using Set Theory (overlay 7 of 7)

Narration:
For example, consider the natural numbers, N, and the positive prime integers, P. N equals the set of x in the integers such that x is greater than or equal to one, which equals the set containing one, two, three, four, and so on.; P equals the set of x in the integers such that x is greater than or equal to one and x is prime, which equals the set containing two, three, five, seven, eleven, and so on.

## Page 018: 1.4: Set Properties (overlay 1 of 5)

Narration:
For a set A, its cardinality, denoted by absolute value of A, is the number of elements in A. The cardinality of the set containing a, e, i, o, and u equals five.

## Page 019: 1.4: Set Properties (overlay 2 of 5)

Narration:
If there is a one-to-one correspondence between A and the natural numbers, then A is called countably infinite and the cardinality of A equals infinity.

## Page 020: 1.4: Set Properties (overlay 3 of 5)

Narration:
For example, the set of rational numbers, Q, is defined as the set of q in the real numbers such that there exists a natural number n such that n times q is an integer.  This set is countably infinite. For example, we can sequenitally all list rationals m over n with the absolute value of m less than or equal to n squared.

## Page 021: 1.4: Set Properties (overlay 4 of 5)

Narration:
If the cardinality of A equals infinity but A is not countably infinite, then A is uncountably infinite.

## Page 022: 1.4: Set Properties (overlay 5 of 5)

Narration:
Example: real numbers are uncountably infinite by Cantor’s diagonal argument. This is not covered in this class but is worth googling if you haven’t seen it.

## Page 023: 1.4: Venn Diagrams

Narration:
Here, we see Venn diagrams for some standard set operations. The sets A and B are represented by overlapping circles. Starting at the top left diagram, we see the union of A and B, which contains all elements in either A or B.; Next, in the top right diagram, we see the intersection of A and B, which contains elements that are in both A and B.; Moving to the bottom right diagram, we see the set difference, A minus B, which contains all elements that are in A and not in B.; Finally, in the bottom left diagram, we see the complement of A, which contains all elements in the universal set U except those in A.

## Page 024: 1.4: From Logic to Set Theory (overlay 1 of 4)

Narration:
Now, we will consider operations on sets A and B more formally. The union of A and B, denoted as shown, is the set of elements in either A or B. Logically, that means x is in A union B if and only if x is in A or x is in B.; Here and below, we use the notation for equivalence because this biconditional holds for all x, A, and B.

## Page 025: 1.4: From Logic to Set Theory (overlay 2 of 4)

Narration:
The intersection of A and B, denoted as shown, is the set of elements in both A and B. Logically, that means x is in A intersect B if and only if x is in A and x is in B.

## Page 026: 1.4: From Logic to Set Theory (overlay 3 of 4)

Narration:
The set difference A minus B, or A backslash B, is the set of elements in A but not in B. Logically, that means x is in A minus B if and only if x is in A and x is not in B.

## Page 027: 1.4: From Logic to Set Theory (overlay 4 of 4)

Narration:
The set A complement, denoted as shown, relative to an implied universal set U, is defined by U minus A. Logically, that means x is in A complement if and only if x is not in A.

## Page 028: 1.4: Relationships Between Sets (overlay 1 of 4)

Narration:
Now, we discuss relationships between sets.; We say A equals B if both sets have the same elements. Logically, “A equals B” if and only if, for all x, x in A if and only if x in B. The “for all x” refers to all x in the implied universal set. However, for this operation, we could also write “for all x in A” without changing the meaning.

## Page 029: 1.4: Relationships Between Sets (overlay 2 of 4)

Narration:
A is a subset of B, denoted A subset-or-equal B, if all elements in A are also in B. “A subset-or-equal B” if and only if, for all x, if x is in A, then x is in B. The “for all x” refers to all x in the implied universal set. Again, writing “for all x in A” wouldn’t change the meaning.

## Page 030: 1.4: Relationships Between Sets (overlay 3 of 4)

Narration:
A is a proper subset of B, denoted A proper-subset B, if A is a subset of B and A is not equal to B. In this case, there must be some element in B that is not in A.

## Page 031: 1.4: Relationships Between Sets (overlay 4 of 4)

Narration:
Two sets are called disjoint if A intersect B equals the empty set.

## Page 032: 1.4: De Morgan, Infinite Operations, and Negation (overlay 1 of 3)

Narration:
De Morgan’s: the negation of “P or Q” equals “not P and not Q.” With P and Q equal to “x is in A” and “x is in B,” this implies that the complement of A union B equals A superscript c intersect B superscript c. This is because membership in the complement of a set is logically the same as negation of membership in that set.

## Page 033: 1.4: De Morgan, Infinite Operations, and Negation (overlay 2 of 3)

Narration:
Now, we see that infinite unions and intersections have rather intuitive and direct definitions. Let S sub alpha denote a collection of sets indexed by alpha in I. The first equation says the infinite union of the collection contains x if there is some alpha in I such that x is in S sub alpha. This matches our intuition that the union contains all elements in all the sets. Similarly, the second equation says the infinite intersection of the collection contains x only if x is in S sub alpha for all alpha in I. This matches our intuition that the intersection contains an element if and only if it is in all the sets.

## Page 034: 1.4: De Morgan, Infinite Operations, and Negation (overlay 3 of 3)

Narration:
Now, we can apply De Morgan’s identity by translating to logic, negating, and mapping back to set theory. First, we see that x is in the infinite union if and only if there exists alpha in I such that x is in S sub alpha. Since the logical negation of this statement is, for all alpha in I, x is not in S sub alpha, it follows that x is in the complement of the infinite union if and only if it is in the infinite intersection of the complements of the sets in the collection.

## Page 035: 1.4: Foundations of Set Theory (overlay 1 of 4)

Narration:
Naive set theory allows one to define any set described by a sentence. Russell’s paradox is a famous example that exposed a major problem with naive set theory. Let R equal the set of all sets S such that S is not in S. That is, the set of all sets that do not contain themselves. This set exists in naive set theory, though it may be empty, simply because it is described by the above sentence. The paradox arises from the fact that this definition leads to the logical contradiction: R is not in R if and only if R is in R. In particular, the set-builder construction implies that, if a set does not contain itself, then it must be in R. Alternatively, it must be in R.

## Page 036: 1.4: Foundations of Set Theory (overlay 2 of 4)

Narration:
In naive set theory, there are sets that contain themselves. For example, consider the “set of all sets” or the “set of abstract ideas.” But, this is not allowed in axiomatic set theory.

## Page 037: 1.4: Foundations of Set Theory (overlay 3 of 4)

Narration:
What does Russell’s paradox show? It shows that naive set theory is not consistent because it allows constructions leading to contradictions. It is avoided in axiomatic formulations by restricting constructions. It also implies that R cannot exist in any consistent set theory.

## Page 038: 1.4: Foundations of Set Theory (overlay 4 of 4)

Narration:
This class will use naive set theory but avoid problematic statements.

## Page 039: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: Try the suggested reading: Course Notes E F 1.4. Or the optional reading: P A F 3.1 through 3.5. Also, look at the problems in Assignment 2. That’s it for today. So, I’ll see you next time.
