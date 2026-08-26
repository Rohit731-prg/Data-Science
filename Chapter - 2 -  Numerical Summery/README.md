Absolutely bro. Let's make **Day 2 notes as a proper revision sheet**, not a teaching conversation. You should be able to read this once before practical and recover the whole topic. 🧠🐼

# Day 2: Descriptive Statistics & Statistical Measures

## 1. What is Descriptive Statistics?

**Descriptive statistics** means describing a dataset using numbers.

For example, if we have students' marks:

```text
50, 60, 70, 80, 90
```

We want to know:

* What is the average?
* What is the middle value?
* How spread out are the values?
* What is the minimum/maximum?
* How much variation is there?

These are answered using **descriptive statistics**.

---

# 2. Select the numerical data

Suppose your dataset is:

```python
import pandas as pd

data = pd.read_csv("data.csv")
```

And your numerical column is `Data_value`.

```python
x = data["Data_value"]
```

Now `x` contains only the values from that column.

---

# 3. Count

Number of non-empty observations.

```python
x.count()
```

Example:

```text
10
20
30
40
```

Count = `4`

---

# 4. Mean

### Meaning

The **average** of all values.

### Formula

```text
Mean = Sum of all values / Number of values
```

### Python

```python
x.mean()
```

Example:

```text
10, 20, 30

Mean = (10 + 20 + 30) / 3
     = 20
```

---

# 5. Median

### Meaning

The **middle value** after arranging the data in ascending order.

```python
x.median()
```

Example:

```text
10, 20, 30, 40, 50
```

Median = `30`

### If there are even numbers

```text
10, 20, 30, 40
```

Middle values = `20, 30`

```text
Median = (20 + 30) / 2 = 25
```

### Important

**Median is less affected by outliers than mean.**

---

# 6. Mode

### Meaning

The value that occurs **most frequently**.

```python
x.mode()
```

Example:

```text
10, 20, 20, 30, 40
```

Mode = `20`

### Why does `mode()` sometimes return multiple values?

Because there can be more than one most-frequent value.

For example:

```text
10, 10, 20, 20, 30
```

Both `10` and `20` are modes.

If you need only the first result:

```python
x.mode().iloc[0]
```

---

# 7. Minimum and Maximum

### Minimum

Smallest value:

```python
x.min()
```

### Maximum

Largest value:

```python
x.max()
```

Example:

```text
10, 20, 30, 40
```

```text
Minimum = 10
Maximum = 40
```

---

# 8. Range

### Meaning

The difference between the maximum and minimum.

### Formula

```text
Range = Maximum - Minimum
```

### Python

```python
data_range = x.max() - x.min()
```

Example:

```text
10, 20, 30, 40

Range = 40 - 10
      = 30
```

### Remember

Range tells us the **overall spread** from the smallest to largest value.

---

# 9. Quartiles

Quartiles divide ordered data into parts.

The three important quartiles are:

```text
Q1 → 25th percentile
Q2 → 50th percentile
Q3 → 75th percentile
```

And:

```text
Q2 = Median
```

### Python

```python
Q1 = x.quantile(0.25)
Q2 = x.quantile(0.50)
Q3 = x.quantile(0.75)
```

You can print:

```python
print("Q1:", Q1)
print("Q2:", Q2)
print("Q3:", Q3)
```

### Simple understanding

```text
0%        25%        50%        75%        100%
│----------│----------│----------│-----------│
           Q1         Q2         Q3
                      ↑
                   Median
```

---

# 10. Interquartile Range (IQR)

### Meaning

IQR measures the spread of the **middle 50%** of the data.

### Formula

```text
IQR = Q3 - Q1
```

### Python

```python
Q1 = x.quantile(0.25)
Q3 = x.quantile(0.75)

IQR = Q3 - Q1

print("IQR:", IQR)
```

Example:

```text
Q1 = 20
Q3 = 50

IQR = 50 - 20
    = 30
```

### ⭐ Important

IQR is especially useful for **detecting outliers**.

You'll use it in Day 3.

---

# 11. Variance

### Meaning

Variance tells us **how spread out the values are around the mean**.

Small variance:

```text
50, 51, 49, 50
```

Values are close together.

Large variance:

```text
10, 50, 90, 20
```

Values are more spread out.

### Python

```python
x.var()
```

### Concept

Variance is based on the squared difference from the mean:

```text
Variance = average of squared deviations from mean
```

Don't worry about manually calculating it for the practical unless asked.

---

# 12. Standard Deviation

### Meaning

Standard deviation tells us approximately **how much the values vary around the mean**.

### Relationship

```text
Standard Deviation = √Variance
```

### Python

```python
x.std()
```

Example:

```python
variance = x.var()
standard_deviation = x.std()
```

### Easy understanding

```text
Small SD → values are close together

Large SD → values are spread out
```

---

# 13. Mean Absolute Deviation (MAD)

### Meaning

MAD is the **average distance of each value from the mean**, ignoring whether the distance is positive or negative.

### Formula

```text
MAD = average(|Xi - Mean|)
```

### Python

```python
mean = x.mean()

MAD = (x - mean).abs().mean()

print("MAD:", MAD)
```

### Understand the code

```python
x - x.mean()
```

Gives the deviation from mean.

```python
(x - x.mean()).abs()
```

Makes all deviations positive.

```python
(x - x.mean()).abs().mean()
```

Finds the average deviation.

Therefore:

```text
x
 ↓
subtract mean
 ↓
absolute value
 ↓
average
 ↓
MAD
```

### Why do we get ONE number?

Because the final `.mean()` calculates the average of all individual deviations.

---

# 14. `describe()` ⭐

Pandas can automatically give you many descriptive statistics:

```python
x.describe()
```

Or for the whole dataset:

```python
data.describe()
```

Typical output:

```text
count
mean
std
min
25%
50%
75%
max
```

Meaning:

| Output  | Meaning                |
| ------- | ---------------------- |
| `count` | Number of observations |
| `mean`  | Average                |
| `std`   | Standard deviation     |
| `min`   | Minimum                |
| `25%`   | Q1                     |
| `50%`   | Q2 / Median            |
| `75%`   | Q3                     |
| `max`   | Maximum                |

⚠️ `describe()` **doesn't directly give you everything in your syllabus**.

It doesn't directly give:

* Range
* MAD
* IQR

So calculate those yourself.

---

# 🧪 Complete Day 2 Program

This is the program you should practice writing yourself:

```python
import pandas as pd

# Load dataset
data = pd.read_csv("data.csv")

# Select numerical column
x = data["Data_value"]

# Basic statistics
print("Count:", x.count())
print("Mean:", x.mean())
print("Median:", x.median())
print("Mode:", x.mode().iloc[0])
print("Minimum:", x.min())
print("Maximum:", x.max())

# Range
data_range = x.max() - x.min()
print("Range:", data_range)

# Quartiles
Q1 = x.quantile(0.25)
Q2 = x.quantile(0.50)
Q3 = x.quantile(0.75)

print("Q1:", Q1)
print("Q2:", Q2)
print("Q3:", Q3)

# IQR
IQR = Q3 - Q1
print("IQR:", IQR)

# MAD
MAD = (x - x.mean()).abs().mean()
print("MAD:", MAD)

# Variance
variance = x.var()
print("Variance:", variance)

# Standard deviation
SD = x.std()
print("Standard Deviation:", SD)

# Complete descriptive summary
print(data.describe())
```

---

# 🧠 The entire Day 2 in one picture

```text
                 DESCRIPTIVE STATISTICS
                         │
        ┌────────────────┼────────────────┐
        │                │                │
    CENTRAL          SPREAD          POSITION
   TENDENCY
        │                │                │
   ┌────┼────┐      ┌────┼────┐      ┌────┐
   │    │    │      │    │    │      │    │
 Mean Median Mode  Range Variance SD  Q1  Q2  Q3
                                      │
                                      ▼
                                  IQR = Q3-Q1

                  MAD
                   │
          Average distance
          from the mean
```

### 🔥 Memorize these formulas

```text
Range = Max - Min

IQR = Q3 - Q1

Variance = average squared deviation from mean

SD = √Variance

MAD = average |Xi - Mean|
```

### And these Python commands

```python
x.mean()
x.median()
x.mode()
x.min()
x.max()
x.count()
x.var()
x.std()
x.quantile(0.25)
x.quantile(0.50)
x.quantile(0.75)
```

For the three custom measures:

```python
Range = x.max() - x.min()

IQR = x.quantile(0.75) - x.quantile(0.25)

MAD = (x - x.mean()).abs().mean()
```

**If you can reproduce the complete program above without looking, Day 2 is solid.** Tomorrow's graphical summary will then feel much easier because you'll already understand what the graphs are showing.
