---
layout: post
title:  "Linear Algebra Review for Artificial Intelligence, Machine Learning, Deep Learning"
date:   2018-12-31 12:00:00
---

# Topics
- [1. Matrices and Vectors](#1-matrices-and-vectors)
- [2. Addition and Scalar Multiplication](#2-addition-and-scalar-multiplication)
- [3. Matrix Vector Multiplication](#3-matrix-vector-multiplication)
- [4. Matrix-Matrix Multiplication](#4-matrix-matrix-multiplication)
- [5. Matrix Multiplication Properties](#5-matrix-multiplication-properties)
- [6. Trace](#6-trace)
- [7. Transpose](#7-transpose)
- [8. Determinant](#8-determinant)
- [9. Eigenvalues and Eigenvectors](#9-eigenvalues-eigenvectors)
- [10. Orthogonal Matrices](#10-orthogonal-matrices)
- [11. Symmetric Matrices](#11-symmetric-matrices)
- [12. Inverse](#12-inverse)
- [13. Norms](#13-norms)
- [14. Rank](#14-rank)
- [15. Diagonalization](#15-diagonalization)
- [16. Singular Value Decomposition (SVD)](#16-singular-value-decomposition)

## 1. Matrices and Vectors
Matrices are 2-dimensional arrays. The matrix below has four rows and three columns, so it is a 4 x 3 matrix. 

$$
M = \left( \begin{array}{ccc}
 4 &  9 &  8 \\
-1 &  2 & -6 \\
 2 &  5 &  2 \\
 2 & -7 &  3 \\
\end{array} \right)
$$

A vector is a matrix with one column and many rows. The vector below is a 4 x 1 matrix.

$$
M = \left( \begin{array}{ccc}
 4 \\
-1 \\
 2 \\
 2 \\
\end{array} \right)
$$

## 2. Addition and Scalar Multiplication
Addition and subtraction are element-wise, so you simply add or subtract each corresponding element. To add or subtract two matrices, their dimensions must be the same.

$$
\left( \begin{array}{ccc}
a & b \\
c & d \\
\end{array} \right)
+
\left( \begin{array}{ccc}
w & x \\
y & z \\
\end{array} \right)
=
\left( \begin{array}{ccc}
a+w & b+x \\
c+y & d+z \\
\end{array} \right)
$$

Subtracting Matrices:

$$
\left( \begin{array}{ccc}
a & b \\
c & d \\
\end{array} \right)
-
\left( \begin{array}{ccc}
w & x \\
y & z \\
\end{array} \right)
=
\left( \begin{array}{ccc}
a-w & b-x \\
c-y & d-z \\
\end{array} \right)
$$

In scalar multiplication, we simply multiply every element by the scalar value:

$$
\left( \begin{array}{ccc}
a & b \\
c & d \\
\end{array} \right)
*
x
=
\left( \begin{array}{ccc}
a*x & b*x \\
c*y & d*z \\
\end{array} \right)
$$

## 3. Matrix Vector Multiplication
We map the row of the matrix onto the column of the vector, multiplying each element and summing the result. The result is a **vector**. The number of **columns** of the matrix must equal the number of **rows** of the vector. 

An m x n matrix multiplied by an n x 1 vector results in an m x 1 vector.

$$
\left( \begin{array}{ccc}
a & b \\
c & d \\
e & f \\
\end{array} \right)
*
\left( \begin{array}{ccc}
x \\
y \\
\end{array} \right)
=
\left( \begin{array}{ccc}
a*x + b*y \\
c*x + d*y \\
e*x + f*y \\
\end{array} \right)
$$

## 4. Matrix-Matrix Multiplication
To multiply two matrices, the number of **columns** of the first matrix must equal the number of **rows** of the second matrix. 

We multiply two matrices by breaking it into several vector multiplications and concatenating the result.

$$
\left( \begin{array}{ccc}
a & b \\
c & d \\
e & f \\
\end{array} \right)
*
\left( \begin{array}{ccc}
w & x \\
y & z \\
\end{array} \right)
=
\left( \begin{array}{ccc}
a*w + b*y & a*x + b*z \\
c*w + d*y & c*x + d*z \\
e*w + f*y & e*x + f*z \\
\end{array} \right)
$$

An **m x n** matrix multiplied by an **n x o** matrix results in an **m x o** matrix. In the above example, a **3 x 2** matrix times a **2 x 2** matrix resulted in a **3 x 2** matrix.

## 5. Matrix Multiplication Properties
- Matrices are **not commutative**: $$A*B \ne B*A$$
- Matrices are **associative**: $$(A*B)*C = A*(B*C)$$
- The **identity matrix**, when multiplied by any matrix of the same dimensions, results in the original matrix. It's just like multiplying numbers by 1. The identity matrix simply has 1's on the diagonal (upper left to lower right diagonal) and 0's elsewhere.

$$
\left( \begin{array}{ccc}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{array} \right)
$$

## 6. Trace
The trace of a square matrix, denoted **Tr(A)**, is defined as the sum of the diagonal elements of the matrix.

$$
A = \left( \begin{array}{ccc}
-1 & 0 & 3 \\
11 & 5 & 2 \\
6 & 12 & -5
\end{array} \right)
$$

$$
Tr(A) = -1 + 5 + -5 = -1
$$

The trace of a matrix is a linear operation, for example:

$$
Tr(A + B) = Tr(A) + Tr(B)
$$

The trace of the product of matrices is independent of the order of their multiplication:

$$
Tr(AB) = Tr(BA)
$$

## 7. Transpose
The transposition of a matrix is like rotating the matrix 90° in clockwise direction and then reversing it.

$$
A = \left( \begin{array}{ccc}
a & b \\
c & d \\
e & f \\
\end{array} \right)
$$

$$
A^T = \left( \begin{array}{ccc}
a & c & e \\
b & d & f \\
\end{array} \right)
$$

## 8. Determinant
Like the trace, the determinant of a matrix is only defined for square matrices. A square matrix whose determinant is zero is called a **singular matrix**. Otherwise, it is called a **non-singular matrix**.

**Properties**:
- A matrix and its transpose have the same determinant.
- If two rows (columns) of A are interchanged its determinant changes sign but is unaltered in magnitude.

## 9. Eigenvalues and Eigenvectors

Suppose you want to compute a matrix to a large exponent, i.e, $$A^{100}$$. Eigenvalues and eigenvectors allow you do this very nicely without multiplying 100 matrices. 

Suppose $$A$$ is a linear operator. Almost all vectors change direction, when they are multiplied by A. Certain exceptional vectors $$x$$ are in the same direction as $$Ax$$. Those are known as the "eigenvectors".

Multiply an eigenvector by $$A$$. The vector $$Ax$$ is a number $$\lambda$$ times the original $$x$$. The number $$\lambda$$ is an eigenvalue of A. The eigenvalue tells whether the special vector $$x$$ is stretched or shrunk or reversed or left unchanged.

$$Ax = \lambda x$$

$$Ax - \lambda x = 0$$

$$Ax - \lambda I x = 0$$

$$(Ax - \lambda I) x = 0$$

Thus $$x$$ is an eigenvector of $$A$$ corresponding to the eigenvalue $$\lambda$$ if and only if $$x$$ and $$\lambda$$ satisfy $$(Ax - \lambda I)x = 0$$.

The equation $$(Ax - \lambda I)x = 0$$ has a nontrivial solution if and only if the determinant of $$(Ax - \lambda I)$$ is zero.

$$|(Ax - \lambda I)| = 0$$

This is known as the characteristic equation of A. This equation is a ploynomial of degree $$N$$ in $$\lambda$$. The $$N$$ roots of this equation give the eigenvalues $${\lambda}_i$$, $$i = 1, ..., N$$, of $$A$$. Corresponding to each eigenvalue $${\lambda}_i$$ there will be a column vector $$\hat{x}_i$$ which will be the eigenvector of $$A$$. This can be determined from the equation: 

$$A \hat{x}_i = {\lambda}_i \hat{x}_i$$

**Example**: Determine the eigen values and normalized eigenvectors of the following matrix

$$
A = \left( \begin{array}{ccc}
1 &  1 &  3 \\
1 &  1 & -3 \\
3 & -3 & -3 \\
\end{array} \right)
$$

From the characteristic equation we get:

$$
det \left( \begin{array}{ccc}
1-\lambda &  1 &  3 \\
1 &  1-\lambda & -3 \\
3 & -3 & -3-\lambda \\
\end{array} \right) = 0
$$

$$
\Rightarrow (1 − \lambda)\lbrace(1 − \lambda)(−3 − \lambda) −9 \rbrace −1\lbrace−3 − \lambda + 9\rbrace + 3\lbrace−3 − 3(1 − \lambda)\rbrace = 0
$$

Simplifying we get:

$$
\Rightarrow {\lambda}^3 + {\lambda}^2 − 24 \lambda + 36 = {\lambda}^3 +3{\lambda}^2 −2{\lambda}^2 − 6\lambda − 18\lambda + 36 = 0
$$

$$
\Rightarrow (\lambda − 2)(\lambda − 3)(\lambda + 6) = 0
$$

So $$\lambda_1 = 2$$, $$\lambda_2 = 3$$, and $$\lambda_3 = −6$$ are the eigenvalues of A.

Now for eigenvalue $$\lambda_1 = 2$$ we determine the eigen vector **$$x^1$$** with elements $$x_1, x_2, x_3$$. Using the equation $$A\hat{x}_1 = 2\hat{x}_1$$ we get:

$$
x_1 + x_2 + 3x_3 = 2x_1
$$

$$
x_1 + x_2 − 3x_3 = 2x_2
$$

$$
3x_1 − 3x_2 −3x_3 = 2x_3
$$

Solving we get $$x_1 = x_2 = k$$, where $$k$$ in any non-zero number, and $$x_3 = 0$$. A suitable eigenvector is $$\hat{x}_1 = {(k, k, 0)}^T$$.

For normalization we require: 

$$k^2 + k^2 + 0 = 1$$
$$ \Rightarrow k = \frac{1}{\sqrt{2}}$$

So the normalized eigen vector is given by:

$$
\hat{x}_1 = \frac{1}{\sqrt{2}}{(1, 1, 0)}^T
$$

Similarly we can determine:

$$
\hat{x}_2 = \frac{1}{\sqrt{3}}{(1, -1, 1)}^T
$$

$$
\hat{x}_3 = \frac{1}{\sqrt{6}}{(1, -1, -2)}^T
$$

## 12. Inverse
The inverse of a square matrix $$A \in R$$ is denoted $$A^{−1}$$ , and is the unique matrix such that:

$$
A^{−1}*A = I = A*A^{-1}
$$

where $$I$$ is the identity matrix.

Note that not all matrices have inverses. Non-square matrices, for example, do not have inverses by definition. However, for some square matrices $$A$$, it may still be the case that inverses may not exist. $$A$$ is invertible or non-singular if $$A^{−1}$$ exists and non-invertible or singular otherwise.

**Properties**:
- $$(A^{−1})^{-1} = A$$
- $${AB}^{−1} = B^{-1} A^{-1}$$
- $$(A^{−1})^{T} = (A^{T})^{-1}$$

## 13. Norms
A norm of a vector is informally a measure of the **length** of the vector. For example, a commonly-used Euclidean or $$l_2$$ norm. Other examples of norms are the $$l_1$$ norm, and $$l_{\infty}$$ norm.

$$ 
l_1 = {\parallel x \parallel}_1 = |x_1| + |x_2| + ... + |x_n| 
$$

$$
l_2 = {\parallel x \parallel}_2 = \sqrt{|x_1|^2 + |x_2|^2 + ... |x_n|^2}
$$

$$
l_{\infty} = {\parallel x \parallel}_{\infty} = max |x_i|
$$

**Example**: 

$$
x = {[3, -4, 1, 2]}^T
$$

$$ 
l_1 = |3| + |-4| + |1| + |2| = 10 
$$

$$
l_2 = \sqrt{|3|^2 + |-4|^2 + |1|^2 + |2|^2} = \sqrt{30}
$$

$$
l_{\infty} = 4
$$

All three norms presented above are examples of the family of $$l_p$$ norms, which are parameterized by a real number $$p ≥ 1$$.

Norms can also be defined for matrices, such as the **Frobenius norm**.

## 12. Rank
This is where I talk about Rank.

## 13. Diagonalization
This is where I talk about diagonalization.

## 14. Singular Value Decomposition (SVD)
This is where I talk about the SVD.

## 15. Matrix Calculus
This is where I talk about the matrix calculas.