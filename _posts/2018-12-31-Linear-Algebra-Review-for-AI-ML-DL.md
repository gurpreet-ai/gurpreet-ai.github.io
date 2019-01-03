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
- [9. Orthogonal Matrices](#9-orthogonal-matrices)
- [10. Symmetric Matrices](#10-symmetric-matrices)
- [11. Inverse](#11-inverse)
- [12. Norms](#12-norms)
- [13. Rank](#13-rank)
- [14. Eigenvalues and Eigenvectors](#14-eigenvalues-eigenvectors)
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

## 8. Eigenvalues and Eigenvectors
Eigenvectors are the **axes** (directions) along which a linear transformation acts simply by **stretching/compressing** and/or **flipping**; eigenvalues give you the factor/magnitude by which it occurs.

Consider a $$N × N$$ matrix A with corresponding eigenvalue $$\lambda$$ and eigenvector $$x$$. Then we can rewrite the matrix equation $$Ax = \lambda x$$ as follows:

## 9. Determinant
Like the trace, the determinant of a matrix is only defined for square matrices. A square matrix whose determinant is zero is called a singular matrix. Otherwise, it is called a non-singular matrix.

## 10. Inverse
The inverse of a square matrix $$A \in R$$ is denoted $$A^{−1}$$ , and is the unique matrix such that:

$$
A^{−1}*A = I = A*A^{-1}
$$

## 11. Norms
A norm of a vector is informally a measure of the **length** of the vector. For example, a commonly-used Euclidean or $$l_2$$ norm. Other examples of norms are the $$l_1$$ norm, and $$l_{\infty}$$ norm.

<!-- $$ l_1 = {\parallel x \parallel}_1 = |x_1| + |x_2| + ... + |x_n| $$
$$ l_2 = {\parallel x \parallel}_2 = \sqrt{|x_1|}^2 + {|x_2|}^2 + ... {|x_n|}^2} $$
$$ l_{\infty} = {\parallel x \parallel}_{\infty} = max |x_i|, i = 1,2,..n $$ -->

$$ 
l_1 = {\parallel x \parallel}_1 = |x_1| + |x_2| + ... + |x_n| 
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