# Linear Algebra

## Scope
Vectors, matrices, eigenvalues, decompositions (SVD, QR, Cholesky), and geometric intuition for linear transformations.

## Core principles
- A matrix A as a linear transformation: Ax stretches, rotates, or shears vectors x; understanding this geometrically prevents algebra from feeling like symbol-pushing.
- Rank is the dimension of the output space; full rank means invertible, rank-deficient means information loss or redundancy in columns/rows.
- Eigenvalues and eigenvectors capture the "directions that don't change direction" under transformation; λ tells you the stretch factor. This is why they matter in stability, vibration, and spectral clustering.
- Singular value decomposition (SVD: A = UΣV^T) separates the transformation into rotation-scale-rotation; it always exists and is the most numerically stable decomposition.
- Norms (L2, L1) measure vector magnitude and control regularization; they're not just abstract—they change optimization landscapes and solution behavior.

## Apex practices
- Use SVD for dimensionality reduction (truncate small singular values), matrix inversion (in ill-conditioned systems), and low-rank approximation.
- Think of QR decomposition (A = QR) as orthogonalizing columns; it's numerically more stable than normal equations for solving least-squares.
- Understand matrix conditioning: condition number = largest/smallest singular value; high conditioning means small perturbations produce large output changes (numerical instability).
- Exploit structure: sparse, banded, symmetric matrices admit specialized algorithms (Cholesky for positive definite, iterative solvers for large sparse systems).

## Pitfalls
- Inverting matrices explicitly (A^-1) is slower and less accurate than solving Ax = b via LU or QR; matrix inverse should be rare in production code.
- Ignoring ill-conditioning; even correct algebra fails numerically when condition number is huge.
- Using eigenvalues for statistical inference without understanding that small perturbations can shuffle them; robustness requires repeated evaluation or SVD.

## Tools & references
Strang's "Introduction to Linear Algebra," Boyd's "Introduction to Applied Linear Algebra," LAPACK/BLAS, numpy.linalg documentation.
