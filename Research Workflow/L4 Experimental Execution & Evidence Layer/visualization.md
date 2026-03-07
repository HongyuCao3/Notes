# Five-Dimensional Visual Encoding Cheat Sheet (for Scientific Figures)

When designing a figure, map information to visual channels **by data type and perceptual strength**.

## 1. Position (X, Y) — **Primary quantitative axes**

* **Best for:** Ordered, quantitative, continuous variables
* **Why:** Highest precision; humans perceive position most accurately
* **Typical use:**

  * X: independent variable (time, steps, epochs, sample size)
  * Y: dependent variable (performance, loss, accuracy)

> Rule: If a variable is *important and ordered*, try to put it on X or Y first.

---

## 2. Color

### 2.1 Color Lightness / Intensity — **Ordered quantitative**

* **Best for:** Ordered or continuous quantitative values
* **Examples:**

  * Dark → light for magnitude
  * Low → high uncertainty, density, or confidence
* **Use when:** X/Y are already occupied

> Rule: Use **one hue, varying lightness** for ordered data.

### 2.2 Color Hue — **Categorical**

* **Best for:** Discrete, unordered categories
* **Examples:**

  * Model types
  * Methods / algorithms
  * Experimental conditions

> Rule: Different hues = different categories (avoid ordering implications).

---

## 3. Shape — **Categorical (secondary)**

* **Best for:** Discrete categories (especially when color is already used)
* **Examples:**

  * Circle / triangle / square for different methods
* **Limitations:**

  * Perceptual capacity is small (≈ 4–6 shapes max)

> Rule: Use shape for **few, high-level categories**, not fine-grained distinctions.

---

## 4. Size — **Ordered quantitative (coarse)**

* **Best for:** Ordered quantitative variables with **low precision requirement**
* **Examples:**

  * Sample size
  * Frequency / count
  * Importance / weight

> Rule: Size conveys order, **not exact value**. Use sparingly.

---

## Practical Mapping Priority (Recommended Order)

1. **X, Y** → most important quantitative variables
2. **Color lightness** → secondary quantitative
3. **Color hue** → main categorical grouping
4. **Shape** → additional categorical distinction
5. **Size** → coarse quantitative or emphasis

---

## Common Anti-Patterns (Avoid)

* Using **color hue** to imply order
* Encoding **precise values** with size
* Using too many shapes or colors
* Encoding the same variable redundantly unless intentional (e.g., highlight)

---

## Mental Checklist Before Plotting

* What are my **quantitative vs categorical** variables?
* Which variable is **most important to read accurately**?
* Have I reserved **position** for the most critical information?
* Is each visual channel used **consistently and unambiguously**?


