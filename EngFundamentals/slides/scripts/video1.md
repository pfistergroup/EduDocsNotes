# Video 1 narration script

This reviewed script maps one narration beat to each rendered overlay page of
`video1.tex`. Slide equations and symbols are written as they should be spoken.
Use `[[pause N]]` for exact internal silence and place `[[seed N]]` immediately
after `Narration:` when a page needs an alternate Qwen take.

## Page 001: Title

Narration:
Welcome to the first flipped class video for ECE 586, Vector-Space Methods. Today, we will discuss the first course topic: propositional logic. We will define the basic logical operations and then use them to build conditional, compound, and meta-level statements.

## Page 002: 1: Logic (overlay 1 of 7)

Narration:
Statements, also called propositions, are the fundamental objects of propositional logic. A statement is a declarative sentence that is true or false, but not both.

## Page 003: 1: Logic (overlay 2 of 7)

Narration:
For example, “This video was recorded for a course at {{univ}}” is a statement, and it is true.

## Page 004: 1: Logic (overlay 3 of 7)

Narration:
The sentence “The real number square root of two is rational” is also a statement, but it is false.

## Page 005: 1: Logic (overlay 4 of 7)

Narration:
In contrast, “Wash your hands before dinner” is not a statement because it does not assert something that is true or false. In English, it is a directive sentence.

## Page 006: 1: Logic (overlay 5 of 7)

Narration:
We can form new statements from existing ones using expressions such as and, or, not, if-then, and if and only if. The first three should be familiar from digital logic.

## Page 007: 1: Logic (overlay 6 of 7)

Pause-after: 2.0

Narration:
Consider the statement: “{{univ}} is located in {{city}}, or all real numbers are rational.” Is this statement true or false? The statement is true because a logical-or is true when at least one of its component statements is true.

## Page 008: 1: Logic (overlay 7 of 7)

Narration:
From now on, we will use capital letters such as P, Q, and R to denote abstract statements. Each letter represents a proposition that has a truth value.

## Page 009: 1.1: Basic Definitions (overlay 1 of 4)

Narration:
The conjunction of P and Q is written P-and-Q in English. It is true only when P and Q are both true and false otherwise. It is denoted symbolically by P wedge Q, where wedge is a symbol that looks like an upside-down V.

## Page 010: 1.1: Basic Definitions (overlay 2 of 4)

Narration:
The disjunction of P and Q is written P-or-Q in English. It is true when at least one of the two statements is true and it is false only when both are false. It is denoted symbolically by P vee Q where vee is a symbol that looks like a V.

## Page 011: 1.1: Basic Definitions (overlay 3 of 4)

Narration:
The negation of P, written not P or symbolically negation P, reverses its truth value. It is true when P is false and false when P is true.

## Page 012: 1.1: Basic Definitions (overlay 4 of 4)

Narration:
Truth tables summarize these definitions. Each row lists one possible assignment of truth values to the input propositions. The conjunction column is true only in the first row, the disjunction column is false only in the last row, and negation exchanges true and false.

## Page 013: 1.2: Conditional Statements (1) (overlay 1 of 4)

Narration:
The conditional statement “if P, then Q” in English is denoted symbolically by P-right-arrow-Q. It is false only in the case where P is true and Q is false; in every other row of the truth table, it is true. P is called the antecedent and Q is called the consequent.

## Page 014: 1.2: Conditional Statements (1) (overlay 2 of 4)

Narration:
The last two rows may initially seem surprising. When P is false, formal logic still assigns the conditional a truth value of true rather than leaving it undefined. These truth values are the standard definition of the conditional connective.

## Page 015: 1.2: Conditional Statements (1) (overlay 3 of 4)

Narration:
One useful interpretation is that the statement "if P, then Q" promises that Q will be true whenever P is true. If P is false, there is no violation of that promise, so the conditional is true by default. This situation is often called vacuous truth.

## Page 016: 1.2: Conditional Statements (1) (overlay 4 of 4)

Narration:
Suppose a friend promises that, “If it is sunny tomorrow, I will ride my bike.” The promise is broken only if tomorrow is sunny and the friend does not ride their bike. If it rains and the friend does not ride their bike, the promise has not been broken, which matches the truth table.

## Page 017: 1.2: Conditional Statements (2) (overlay 1 of 4)

Narration:
The biconditional statement “P if and only if Q” in English is denoted symbolically by P-left-right-arrow-Q. It is true exactly when P and Q have the same truth value. Thus, it is true when both are true and also when both are false.

## Page 018: 1.2: Conditional Statements (2) (overlay 2 of 4)

Narration:
The biconditional has the same truth values as the conjunction of the two directions: If P, then Q; and if Q, then P. Thus, the phrase “if and only if” asserts conditional connectives in both directions.

## Page 019: 1.2: Conditional Statements (2) (overlay 3 of 4)

Narration:
For example, consider the statement “John graduates this term if and only if he passes this class.” As a formal biconditional, it is true when John both graduates and passes, and it is also true when John neither graduates nor passes.

## Page 020: 1.2: Conditional Statements (2) (overlay 4 of 4)

Narration:
Two variations of a conditional have standard names. The converse of P implies Q is Q implies P. The contrapositive is not Q implies not P. A conditional is logically equivalent to its contrapositive, but it is not generally equivalent to its converse.

## Page 021: 1.2: Compound Statements (overlay 1 of 2)

Narration:
Logical connectives can be nested to form compound statements. The expression shown is the conjunction of “if P, then R” with “Q or not R.” Its truth value depends on the three propositions P, Q, and R.

## Page 022: 1.2: Compound Statements (overlay 2 of 2)

Narration:
There is a mechanical, though tedious, way to construct a truth table. First list all eight assignments of truth values to P, Q, and R. Then, continue by filling any column whose values are determined by previously filled entries. The numbers at the bottom show an order in which the displayed columns can be filled.

## Page 023: 1.2: Meta Statements (overlay 1 of 5)

Narration:
A meta statement is a logical statement about logical statements. It describes how the truth of a compound expression behaves across all possible valuations of its propositional variables.

## Page 024: 1.2: Meta Statements (overlay 2 of 5)

Narration:
A tautology is a compound statement that is true for every valuation of its variables. For example, P or not P or Q is always true, because either P or not P must be true, regardless of Q.

## Page 025: 1.2: Meta Statements (overlay 3 of 5)

Narration:
A contradiction is a compound statement that is false for every valuation. The expression P and not-P and Q is always false because P and not-P can never both be true.

## Page 026: 1.2: Meta Statements (overlay 4 of 5)

Narration:
The metastatement R implies S is denoted symbolically by a double-arrow from R to S. It asserts that the ordinary conditional connective "if R, then S" is a tautology. The example given is known by the latin name modus ponens. In English, we say if P-implies-Q is true and P is true, then Q must be true. In contrast to the conditional connective, the double arrow denotes that this reasoning works for every valuation of the compound statements.

## Page 027: 1.2: Meta Statements (overlay 5 of 5)

Narration:
The meta-statement R is equivalent to S is denoted symbolically by the two-sided (or left-right) double-arrow. It asserts that the biconditional between R and S is a tautology. For example, "if P, then Q" is logically equivalent to not-P or Q. In other words, the two compound statements have identical truth values in every row.  More generally, a single arrow forms a statement whose truth depends on other statements whereas a double arrow asserts that a statement is true in all cases.

## Page 028: Next Steps

Narration:
To continue studying after this video, reed Sections 1 through 1.2.2 of the course notes. The optional reading in Sections 1.1 through 2.6 of PAF is also useful. Also, look at the problems in Assignment 1. [[pause 0.5]] This completes the presentation.
