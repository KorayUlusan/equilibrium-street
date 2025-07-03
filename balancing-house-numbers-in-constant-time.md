# The Balancing House Number Problem in Constant Time

## From Pell Recurrence to Closed Form

Recall we showed that

$$X^2 - 8Y^2 = 1,$$

and that the sequence $\{Y_k\}$ (with $Y_k=m_k$) satisfies the matrix recurrence

$$
\begin{pmatrix}
X_{k+1} \\
Y_{k+1}
\end{pmatrix} = \begin{pmatrix}3&8 \\
1&3 \end{pmatrix} \begin{pmatrix}X_k \\
Y_k\end{pmatrix}
$$

with $(X_1,Y_1)=(3,1)$.


### 1. Induced scalar recurrence for $m_k$

From the matrix, one can eliminate $X_k$ to get a second‑order recurrence for $Y_k$.  In fact

$$
Y_{k+1} = X_k + 3Y_k,
\quad
X_k = 3Y_k + 8Y_{k-1}
$$

so

$$
Y_{k+1} = (3Y_k + 8Y_{k-1}) + 3Y_k = 6Y_k + 8Y_{k-1}.
$$

But since $8Y_{k-1} = Y_k - X_{k-1}$, one finds more cleanly

$$\boxed{Y_{k+1} = 6Y_k - Y_{k-1},}$$

with initial values

$$
Y_0 = 0,\quad Y_1 = 1.
$$


### 2. Characteristic equation

The recurrence $Y_{k+1} - 6Y_k + Y_{k-1} = 0$ has **characteristic polynomial** $r^2 - 6r + 1 = 0$ whose two roots are $r = 3 \pm \sqrt{8}$.

Call them 

$$
\alpha = 3 + \sqrt{8},\quad \beta = 3 - \sqrt{8}.
$$


### 3. Binet‑style formula

By the theory of linear recurrences, the general term is

$$
Y_k = A\alpha^k + B\beta^k.
$$

Use the initial conditions:

$$
Y_0 = A + B = 0,
\qquad
Y_1 = A\alpha + B\beta = 1.
$$

Solving gives

$$
A = \frac{1}{\alpha - \beta},\quad B = -\frac{1}{\alpha - \beta},
\quad
\alpha - \beta = 2\sqrt{8}.
$$

Hence

$$
\boxed{
m_k = Y_k
= \frac{\alpha^k - \beta^k}{\alpha - \beta}
= \frac{(3+\sqrt8)^k - (3-\sqrt8)^k}{2\sqrt8}
}.
$$


### 4. Final $O(1)$ formula

Therefore, for $k\ge1$,

$$
\boxed{
f(k) = m_k 
= \frac{(3+\sqrt8)^k - (3-\sqrt8)^k}{2\sqrt8}
}
$$

computes the $k$-th balancing house number in **constant time**.


## In Code

```py
import math

def balancing_house_number_closedform(k):
    sqrt8 = math.sqrt(8)
    a = 3 + sqrt8
    b = 3 - sqrt8
    # Use the closed form for the k-th solution of Pell:
    m_k = (a**k - b**k) / (2 * sqrt8)
    return round(m_k)

# Example usage:
for i in range(1, 11):
    print(f"f({i}) = {balancing_house_number_closedform(i)}")
```
