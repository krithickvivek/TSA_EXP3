# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
### Date: 
## AIM:
To compute the AutoCorrelation Function (ACF) of the given Revenue (millions) data to determine the model type suitable for the data.
## DATASET
Apple 2009-2005
## SOFTWARE REQUIRED
Google Colab
## ALGORITHM:
1. Import the necessary packages
2. Load the dataset and clean the Revenue column by removing symbols
3. Apply first-order differencing to make the data stationary
4. Find the mean and variance of the differenced data
5. Compute autocorrelation values for all possible lags
6. Store the results in an array
7. Plot the autocorrelation values using a graph

## PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load dataset
data = pd.read_csv('Apple 2009-2024.csv')

# Clean Revenue column
data['Revenue (millions)'] = data['Revenue (millions)'] \
    .str.replace('$','', regex=False) \
    .str.replace(',','', regex=False) \
    .astype(float)

# Apply differencing
data['diff'] = data['Revenue (millions)'] - data['Revenue (millions)'].shift(1)
data = data.dropna()

values = data['diff'].values

# Number of lags (maximum possible)
lags = range(len(values))

# Pre-allocate autocorrelation list
autocorr_values = []

# Mean
mean_data = np.mean(values)

# Variance
variance_data = np.var(values)

# Compute autocorrelation
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum((values[:-lag] - mean_data) * (values[lag:] - mean_data)) / len(values)
        autocorr_values.append(auto_cov / variance_data)

# Plot graph
plt.figure(figsize=(10, 6))
plt.stem(list(lags), autocorr_values)
plt.title('Autocorrelation of Differenced Revenue')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)
plt.show()
```

## OUTPUT:
<img width="867" height="550" alt="image" src="https://github.com/user-attachments/assets/debeebfb-af4f-44a3-aa09-ca2c55ab1e96" />

## RESULT:
Thus we have successfully implemented the auto correlation function in python.
