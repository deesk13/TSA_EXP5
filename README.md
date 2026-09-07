# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 02-09-2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load the dataset
file_path = '/content/Walmart_Sales.csv'
data = pd.read_csv(file_path)

# Display column names
print("Column names in the dataset:")
print(data.columns)

# Convert Date column to datetime
# Date format = DD-MM-YYYY
data['Date'] = pd.to_datetime(
    data['Date'],
    format='%d-%m-%Y'
)

# Sort data by Date
data = data.sort_values('Date')

# Combine sales from all stores for each date
sales = data.groupby('Date')['Weekly_Sales'].sum()

# Sort the time series
sales = sales.sort_index()

# Perform seasonal decomposition
# Weekly data -> 52 weeks approximately equals 1 year
decomposition = seasonal_decompose(
    sales,
    model='additive',
    period=52
)

# Create a figure with required size
fig = plt.figure(figsize=(12, 8))

# Plot decomposition
decomposition.plot()

# Add title
plt.suptitle(
    'Seasonal Decomposition of Walmart Weekly Sales',
    fontsize=16
)

plt.tight_layout()
plt.show()

# Extract components
trend = decomposition.trend
seasonal = decomposition.seasonal
residual = decomposition.resid

# Display results
print("\nTrend Component:")
print(trend.dropna().head())

print("\nSeasonal Component:")
print(seasonal.dropna().head())

print("\nResidual Component:")
print(residual.dropna().head())
```

### OUTPUT:
FIRST FIVE ROWS:

<img width="790" height="80" alt="image" src="https://github.com/user-attachments/assets/58cc384f-9507-4517-9fa2-9a6d70a59784" />


PLOTTING THE DATA:
<img width="765" height="402" alt="image" src="https://github.com/user-attachments/assets/b917edf1-7a90-4f21-9a25-86f4bf8c0363" />

SEASONAL PLOT REPRESENTATION :
<img width="395" height="132" alt="image" src="https://github.com/user-attachments/assets/7751107e-0602-4e92-a811-4e3ed1c7ba23" />



TREND PLOT REPRESENTATION :
<img width="362" height="137" alt="image" src="https://github.com/user-attachments/assets/a2417a28-25ad-4361-a62b-a5775737d86a" />


OVERAL REPRESENTATION:
<img width="778" height="627" alt="image" src="https://github.com/user-attachments/assets/baf9d5b4-f02f-4209-ab90-5f959f987276" />




### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
