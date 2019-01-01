---
layout: post
title:  "Linear Algebra Review for Artificial Intelligence, Machine Learning"
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
- [9. Inverse](#9-inverse)
- [10. Norms](#10-norms)
- [11. Rank](#11-rank)
- [12. Eigenvalues and Eigenvectors](#12-eigenvalues-eigenvectors)
- [13. Diagonalization](#13-diagonalization)
- [14. Singular Value Decomposition (SVD)](#14-singular-value-decomposition)

## 6. Trace

## 7. Transpose

## 8. Determinant

## 9. Inverse
This is where I talk about Determinant, Inverse, Transpose, and Trace.

## 10. Norms
This is where I talk about Norms.

## 11. Rank
This is where I talk about Rank.

## 12. Eigenvalues and Eigenvectors
This is where I talk about Eigenvalues and Eigenvectors.

## 13. Diagonalization
This is where I talk about Matrix-Matrix Multiplication.

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
This is where I talk about Trace.

## 7. Transpose
This is where I talk about Transpose.

## 8. Determinant
This is where I talk about Determinant.

## 9. Inverse
This is where I talk about Inverse.

## 10. Norms
This is where I talk about Norms.

## 11. Rank
This is where I talk about Rank.

## 12. Eigenvalues and Eigenvectors
This is where I talk about Eigenvalues and Eigenvectors.

## 13. Diagonalization
This is where I talk about Diagonalization.

## 14. Singular Value Decomposition (SVD)
This is where I talk about the SVD.