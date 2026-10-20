# Video 9 narration script

This production script is transcribed from the `\note{...}` blocks in
`video9.tex`, following `SCRIPT_TRANSCRIPTION.md`. Each `Read` direction expands
only the newly revealed slide material; all other spoken words preserve the
authored note in source order. Pages 19 and 20 use the documented conservative
exact-read fallback for the two overlays without speaker-note cues, and page 24
retains the extra final cue on its final visual state.

## Page 001: Title

Narration:
Welcome to the ninth video lecture for ECE 586, Vector Space Methods. Today, we'll discuss fields and matrices.

## Page 002: 3.1: Linear Algebra and Abstraction (overlay 1 of 2)

Narration:
Linear algebra is the foundation of engineering mathematics. [[pause 0.2]] This chapter will review and extend your knowledge of linear algebra. [[pause 0.2]] Abstraction allows the application of similar ideas to many different areas. [[pause 0.2]] Your prior experience with real vector spaces makes this possible.

## Page 003: 3.1: Linear Algebra and Abstraction (overlay 2 of 2)

Narration:
Abstraction is an important part of this class. Metric spaces provide abstract notions of distance and closeness. Fields provide abstract notions for arithmetic of scalars: addition, subtraction, multiplication, and division. Vector spaces abstract the additive properties of real vectors. Building the abstraction up slowly allows one to discover what elements are important for each result.

## Page 004: 3.1: Fields (overlay 1 of 2)

Narration:
Consider a set F with binary operations: "addition" and "multiplication." For every pair of elements s and t in F, we require s plus t to be in F. For every pair of elements s and t in F, we require s t to be in F, where multiplication is denoted here by placing the elements next to each other.

## Page 005: 3.1: Fields (overlay 2 of 2)

Pause-after: 3

Narration:
A field satisfies all the standard multiplicative and additive properties of the real numbers. Pause and take a moment to read through them. They are listed here for your review, but you do not need to memorize them.

## Page 006: 3.1: Examples of Arithmetic Fields

Narration:
The rational numbers with standard addition and multiplication form a field. The real numbers with standard addition and multiplication form a field. The complex numbers with standard addition and multiplication form a field. The set of integers with standard addition and multiplication is not a field. For prime p, the set from zero to p minus one, with addition and multiplication modulo p, is a field. The last example is known as a finite field and such fields are useful in communications and computing.

## Page 007: 3.2: Matrices (overlay 1 of 2)

Pause-after: 3
Narration:
Consider finding n scalars x-one, through x n, in F that satisfy the following conditions.

## Page 008: 3.2: Matrices (overlay 2 of 2)

Narration:
They define a system of m linear equations in n unknowns, A x equals y, where x equals x-one through x n; y equals y-one through y m; and A is the matrix given by the following equation. Thus, matrices can be used to define systems of linear equations. In addition, they are also used to represent linear transformations.

## Page 009: 3.2: Matrix Multiplication (overlay 1 of 2)

Pause-after: 1

Narration:
Let A be an m by n matrix over F, that is, A in F m times n; and let B be an n by p matrix over F. The matrix product A B is the m by p matrix C whose i j entry is c sub i j, equal to the sum, from r equal to one to n, of a-sub i r times b sub r j. This is standard matrix multiplication, which I expect you've all seen before.

## Page 010: 3.2: Matrix Multiplication (overlay 2 of 2)

Pause-after: 3

Narration:
If we interpret a matrix as a list of column vectors, then matrix multiplication also gets a different interpretation.  Similarly, writing a matrix as a list of row vectors provides another interpretation. Please pause and take a moment to review these.

## Page 011: 3.2: Echelon Forms (overlay 1 of 2)

Narration:
A matrix A in F m times n is in row echelon form if: any all-zero row is below all rows with non-zero entries; and, for all rows with non-zero entries, the leading coefficient, that is, the first non-zero element from the left, is strictly to the right of the leading coefficient of the row above it. Thus, the entries below the leading coefficient in a column are zero. Also, A is in column echelon form if A transposed is in row echelon form. [[pause 0.2]] For example, the matrix A on the right is in reduced row echelon form.

## Page 012: 3.2: Echelon Forms (overlay 2 of 2)

Narration:
A matrix B in F m times n is in reduced row echelon form if it is: in row echelon form with every leading coefficient equal to one; and every leading coefficient is the only non-zero element in its column. Also, B is in reduced column echelon form if B transposed is in reduced row echelon form. This form allows one to easily find vectors in the null space of the matrix. For example, the matrix B on the right is in reduced row echelon form.

## Page 013: 3.2: Elementary Row Operations (overlay 1 of 3)

Narration:
An elementary row operation on an m by n matrix consists of: multiplying a row by a non-zero scalar; swapping two rows; or adding a scalar multiple of one row to another row. An elementary column operation is the same, but applied to columns.

## Page 014: 3.2: Elementary Row Operations (overlay 2 of 3)

Narration:
A square matrix A in F m times m is invertible if there is a square matrix B in F m times m such that A times B equals B times A equals I, where I is the m by m identity. In that case, A inverse equals B.

## Page 015: 3.2: Elementary Row Operations (overlay 3 of 3)

Narration:
Elementary row operations on A in F m times n are realized, for an invertible matrix E in F m times m, by matrix multiplication as E times A. [[pause 0.3]] They can be used in a sequence to induce row reduced echelon form. For example, one approach is Gaussian elimination.

## Page 016: 3.2: Elementary Row Operations (overlay 1 of 5)

Narration:
For any m by n matrix A over F, there is an invertible m by m matrix P over F such that R equals P times A is in reduced row echelon form.  This follows from applying row operations on A to perform Gaussian elimination and collecting the transforms into the matrix P.

## Page 017: 3.2: Elementary Row Operations (overlay 2 of 5)

Narration:
For A in F m times n, define the augmented matrix A prime equal to the block matrix with an m times m identity appended to A on the right.

## Page 018: 3.2: Elementary Row Operations (overlay 3 of 5)

Narration:
Use elementary row operations to transform A-prime into row reduced echelon form as R prime.

## Page 019: 3.2: Elementary Row Operations (overlay 4 of 5)

Narration:
Elementary row operations imply that R prime equals P times A prime for some invertible P.

## Page 020: 3.2: Elementary Row Operations (overlay 5 of 5)

Narration:
Then, R prime equals P times the block matrix formed by appending I on the right of A. Since this equals the block matrix formed by appending P on the right of R, it follows that R equals to P times A and is in row reduced echelon form.

## Page 021: 3.2: Foundation of Dimension (overlay 1 of 4)

Narration:
Let A be an m by n matrix over F with m less than n. Then, there exists a length-n column vector x not equal to the zero vector, over F, such that A x equals zero.

## Page 022: 3.2: Foundation of Dimension (overlay 2 of 4)

Narration:
Use row reduction to compute the reduced row echelon form of-A giving R equals P times-A, where P is invertible by the previous lemma.

## Page 023: 3.2: Foundation of Dimension (overlay 3 of 4)

Narration:
Observe that the columns of R containing leading elements can be combined in linear combination to cancel any other column of R.

## Page 024: 3.2: Foundation of Dimension (overlay 4 of 4)

Narration:
Thus, one can construct a vector x satisfying R x equals zero, and observe that A x equals P inverse R x equals zero. [[pause 0.3]] A concrete example of this process will be given in class.

## Page 025: Next Steps

Narration:
Here are some options to continue learning this material. To continue studying after this video: try the suggested reading, Course Notes E F 3.1 through 3.2. Or the optional reading, M M A 3.1. Also, look at the problems in Assignment 4. That's it for today. So, I'll see you next time.
