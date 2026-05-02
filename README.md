# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:02/05/26
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
A - LINEAR TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
data = pd.read_csv('/content/salary_prediction_data.csv')

data.head()

# Sort data by Experience
data = data.sort_values(by='Experience')

# Reset index
data.reset_index(drop=True, inplace=True)

# Select required columns
resampled_data = data[['Experience', 'Salary']].copy()

resampled_data.head()

# Reset index (same structure as your code)
resampled_data.reset_index(inplace=True)

# Rename column
resampled_data.rename(columns={'Experience': 'Year'}, inplace=True)

# Convert experience to numeric index
resampled_data['Year'] = range(1, len(resampled_data)+1)

# X and Y
years = resampled_data['Year'].tolist()
prices = resampled_data['Salary'].tolist()

# -------------------------------
# Linear Trend Estimation
# -------------------------------
n = len(years)

X = [i - years[len(years)//2] for i in years]
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, prices)]

b = (n * sum(xy) - sum(prices) * sum(X)) / (n * sum(x2) - (sum(X)**2))
a = (sum(prices) - b * sum(X)) / n

linear_trend = [a + b * X[i] for i in range(n)]

# -------------------------------
# Polynomial Trend (Degree 2)
# -------------------------------
x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i, j in zip(x2, prices)]

coeff = [
    [len(X), sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [sum(prices), sum(xy), sum(x2y)]

A = np.array(coeff)
B = np.array(Y)

solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution

poly_trend = [a_poly + b_poly*X[i] + c_poly*(X[i]**2) for i in range(n)]

# -------------------------------
# Visualization
# -------------------------------
print(f"Linear Trend: y = {a:.2f} + {b:.2f}x")
print(f"Polynomial Trend: y = {a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x^2")

# Add trend columns
resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend
plt.figure(figsize=(10,5))

plt.plot(resampled_data.index, resampled_data['Salary'], label='Actual Salary', marker='o')
plt.plot(resampled_data.index, resampled_data['Linear Trend'],
         linestyle='--', label='Linear Trend')

plt.title("Salary Linear Trend")
plt.xlabel("Experience Index")
plt.ylabel("Salary")
plt.legend()
plt.grid()

plt.show()
```

B- POLYNOMIAL TREND ESTIMATION
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
data = pd.read_csv('/content/salary_prediction_data.csv')

data.head()

# Sort data by Experience
data = data.sort_values(by='Experience')

# Reset index
data.reset_index(drop=True, inplace=True)

# Select required columns
resampled_data = data[['Experience', 'Salary']].copy()

resampled_data.head()

# Reset index (same structure as your code)
resampled_data.reset_index(inplace=True)

# Rename column
resampled_data.rename(columns={'Experience': 'Year'}, inplace=True)

# Convert experience to numeric index
resampled_data['Year'] = range(1, len(resampled_data)+1)

# X and Y
years = resampled_data['Year'].tolist()
prices = resampled_data['Salary'].tolist()

# -------------------------------
# Linear Trend Estimation
# -------------------------------
n = len(years)

X = [i - years[len(years)//2] for i in years]
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, prices)]

b = (n * sum(xy) - sum(prices) * sum(X)) / (n * sum(x2) - (sum(X)**2))
a = (sum(prices) - b * sum(X)) / n

linear_trend = [a + b * X[i] for i in range(n)]

# -------------------------------
# Polynomial Trend (Degree 2)
# -------------------------------
x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i, j in zip(x2, prices)]

coeff = [
    [len(X), sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [sum(prices), sum(xy), sum(x2y)]

A = np.array(coeff)
B = np.array(Y)

solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution

poly_trend = [a_poly + b_poly*X[i] + c_poly*(X[i]**2) for i in range(n)]

# -------------------------------
# Visualization
# -------------------------------
print(f"Linear Trend: y = {a:.2f} + {b:.2f}x")
print(f"Polynomial Trend: y = {a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x^2")

# Add trend columns
resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend
plt.figure(figsize=(10,5))

plt.plot(resampled_data.index, resampled_data['Salary'],
         label='Actual Salary', marker='o')

plt.plot(resampled_data.index, resampled_data['Polynomial Trend'],
         label='Polynomial Trend')

plt.title("Salary Polynomial Trend")
plt.xlabel("Experience Index")
plt.ylabel("Salary")
plt.legend()
plt.grid()

plt.show()
```

### OUTPUT
A - LINEAR TREND ESTIMATION

<img width="877" height="473" alt="image" src="https://github.com/user-attachments/assets/0e857180-906d-4e24-bbf1-93ceed07816f" />


B- POLYNOMIAL TREND ESTIMATION

<img width="878" height="472" alt="image" src="https://github.com/user-attachments/assets/0e6fedac-1ab3-49c0-8590-e8b0f9998aeb" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
