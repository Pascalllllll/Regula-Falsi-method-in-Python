# Regula Falsi method in Python

This project implements the **Regula Falsi method** (also known as the **False Position Method**) in Python to find the root of a real-valued function. It also includes a simple plot to visualize the function and the approximated root.

### What is Regula Falsi?

The **Regula Falsi** method is a numerical technique used to find the root of a nonlinear equation $f(x) = 0$. It is similar to the bisection method, but instead of using the midpoint, it uses a linear interpolation between two points to better estimate the root.

Given two initial guesses $x_1$ and $x_2$ such that $f(x_1) \cdot f(x_2) < 0$, the method iteratively finds the point:

$$
x_3 = x_2 - f(x_2) \cdot \frac{x_1 - x_2}{f(x_1) - f(x_2)}
$$

### ✅ Example Output

```text
i        x1           x2           x3           f(x3)
1        0.400000     0.500000     0.494982     0.000107
2        0.494982     0.500000     0.495008     0.000000

Root found at x = 0.495008
```

A graph will also be shown with the function curve and vertical line at the root approximation.

### 🛠 How to Use

1. Clone this repository or copy the code into a Python file.
2. Install Matplotlib if needed:

   ```bash
   pip install matplotlib
   ```
3. Run the script using any Python environment.
4. Modify the `f(x)` function and initial guesses `x1` and `x2` to experiment with different equations.

---

### Example Functions

```python
# Example 1:
# return math.sin(x) - 5*x + 2
# x1 = 0.4
# x2 = 0.5

# Example 2:
# return math.exp(x) - 2*x - 21
# x1 = 3
# x2 = 4

# Example 3:
# return math.cos(x) - 3*x
# x1 = 0.3
# x2 = 0.4

# Example 4:
# return x**3 - 100
# x1 = 4
# x2 = 5
```

---

### 📌 Notes

* Make sure that `f(x1)` and `f(x2)` have opposite signs to guarantee the method works.
* This script assumes you are using functions that are continuous in the interval $[x1, x2]$.

---

just copy the code below!


```python
import matplotlib.pyplot as plt
import numpy as np
import math

def f(x):
    return math.sin(x) - 5*x + 2
x1 = 0.4
x2 = 0.5

    # Example 1:
    # return math.sin(x) - 5*x + 2
    # x1 = 0.4
    # x2 = 0.5

    # Example 2:
    # return math.exp(x) - 2*x - 21
    # x1 = 3
    # x2 = 4

    # Example 3:
    # return math.cos(x) - 3*x
    # x1 = 0.3
    # x2 = 0.4

    # Example 4:
    # return x**3 - 100
    # x1 = 4
    # x2 = 5


tol = 1e-5
max_iter = 100

def regula_falsi(f, x1, x2, tol=1e-5, max_iter=100):
    if f(x1) * f(x2) >= 0:
        print(f"Failed: f({x1}) = {f(x1):.6f}, f({x2}) = {f(x2):.6f}")
        print("f(x1) and f(x2) must have a different sign.")
        return None

    print("{:<8} {:<12} {:<12} {:<12} {:<12}".format("i", "x1", "x2", "x3", "f(x3)"))
    for i in range(max_iter):
        f1 = f(x1)
        f2 = f(x2)
        x3 = x2 - f2 * (x1 - x2) / (f1 - f2)
        f3 = f(x3)
        print("{:<8} {:<12.6f} {:<12.6f} {:<12.6f} {:<12.6f}".format(i + 1, x1, x2, x3, f3))

        if abs(f3) < tol:
            return x3

        if f1 * f3 < 0:
            x2 = x3
        else:
            x1 = x3

    return x3

root = regula_falsi(f, x1, x2, tol, max_iter)
if root is not None:
    print("\nRoot found at x = {:.6f}".format(root))

    x_vals = np.linspace(x1 - 0.5, x2 + 0.5, 400)
    y_vals = [f(x) for x in x_vals]

    plt.plot(x_vals, y_vals, label="f(x)", color='blue')
    plt.axhline(0, color='black', linewidth=0.5)
    plt.axvline(root, color='red', linestyle='--', label=f"Akar ≈ {root:.5f}")
    plt.title("Regula Falsi Method")
    plt.xlabel("x")
    plt.ylabel("f(x)")
    plt.grid(True)
    plt.legend()
    plt.show()

```
