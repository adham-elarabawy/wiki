---
description: Approximate solutions to linear systems
---

# Least Squares

## Definition

It is extremely improbable that a fully-defined full-rank system and raw measurements will result in an exact solution. It is often the case that the equations we receive may be corrupted slightly by noise. When we have a large number of equations, the result is an inconsistent system, where no x exists that satisfies all the equations exactly. 

![](../.gitbook/assets/image.png)

Each row in $$A$$represents a constraint equation. 

Each element in $$\vec{b}$$represents the solution \(with noise/error\) for each respective constraint equation. 

The $$\vec{x}$$vector is the _approximate_ solution to the system that will minimize the error of $$A \cdot \vec{x}$$ and $$\vec{b}$$. 

### Limitations

As you can see, the computation of the $$\vec{x}$$vector is dependent on us being able to compute the $$(A^T \cdot A)^{-1}$$term, which means that $$(A^T \cdot A)$$must be invertible. 

#### Intuition behind limitations

* At the end of the day, the limitation above on  $$(A^T \cdot A)$$being full-rank essentially boil down to us having an _over-constrained_ system, and not an _under-constrained_ system. 
* On an ever lower level, this means that $$A$$must have at least as many rows than it has columns.

## Application

Although the use of such system analysis is restricted to linear systems, a key insight is to note that the actual variables are precomputed in the form of the $$A$$ matrix. This means that nonlinear constraint _equations_ are not restrictive of this type of analysis.

### Linear Constraint Equations

Our constraint equations could take on a linear form:

$$
y_i = a_1 \cdot x _i + a_2
$$

The above form of the constraint equations would result in the following:

$$
A = 
\begin{bmatrix}
x_0 & 1\\
x_1 & 1\\
x_2 & 1\\
... & ...
\end{bmatrix}

\vec{b} = 

\begin{bmatrix}
y_0\\
y_1\\
y_2\\
...
\end{bmatrix}

\vec{x}=
\begin{bmatrix}
a_1\\
a_2\\
\end{bmatrix}
$$

Such that the $$a_1 , a_2$$ coefficients function as the slope and y-intercept constants that define the line that maps $$x_i$$to a $$y$$as best as possible. **AKA a best-fit line.** 

### Nonlinear Constraint Equations

Our constraint equations could also take on a nonlinear form:

$$
y_i = a_1 \cdot x _i^2 + a_2\cdot x _i
$$

The above form of the constraint equations would result in the following:

$$
A = 
\begin{bmatrix}
x_0^2 & x_0\\
x_1^2 & x_1\\
x_2^2 & x_2\\
... & ...
\end{bmatrix}

\vec{b} = 

\begin{bmatrix}
y_0\\
y_1\\
y_2\\
...
\end{bmatrix}

\vec{x}=
\begin{bmatrix}
a_1\\
a_2\\
\end{bmatrix}
$$

Such that the $$a_1 , a_2$$ coefficients function as the coefficients that _best_ map the $$x_i$$value to the corresponding $$y$$value.

### Multivariate Constraint Equations

This same analysis can be further applied to multivariate constraint equations, as long as it follows the above pattern.





