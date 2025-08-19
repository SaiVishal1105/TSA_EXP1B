# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 17-08-25

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv("/content/car_price_prediction.csv")

# Use production year as time index
data['Prod. year'] = pd.to_datetime(data['Prod. year'], format='%Y')
data = data.groupby('Prod. year')['Price'].mean().reset_index()  # average price per year
data.set_index('Prod. year', inplace=True)

# Regular Differencing
data['price_diff'] = data['Price'] - data['Price'].shift(1)

# Seasonal Adjustment (assuming yearly seasonality)
result = seasonal_decompose(data['Price'], model='additive', period=1)
data['price_seasonal_diff'] = result.resid

# Log Transformation
data['price_log'] = np.log(data['Price'])
data['price_log_diff'] = data['price_log'] - data['price_log'].shift(1)

# Seasonal Adjustment on log-differenced data
result_log = seasonal_decompose(data['price_log_diff'].dropna(), model='additive', period=1)
data['price_log_seasonal_diff'] = result_log.resid

# Plotting
plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Price'], label='Original')
plt.legend(loc='best')
plt.title('Original Data (Avg Price per Year)')

plt.subplot(6, 1, 2)
plt.plot(data['price_diff'], label='Regular Differencing')
plt.legend(loc='best')
plt.title('Regular Differencing')

plt.subplot(6, 1, 3)
plt.plot(data['price_seasonal_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')

plt.subplot(6, 1, 4)
plt.plot(data['price_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')

plt.subplot(6, 1, 5)
plt.plot(data['price_log_diff'], label='Log Transformation + Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing')

plt.subplot(6, 1, 6)
plt.plot(data['price_log_seasonal_diff'], label='Log Transformation + Differencing + Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing + Seasonal Adjustment')

plt.tight_layout()
plt.show()


```

### OUTPUT:

ORIGINAL:
<img width="1429" height="245" alt="image" src="https://github.com/user-attachments/assets/15a6fe8b-c68a-4a6a-8f45-a4c0d900abfa" />


REGULAR DIFFERENCING:
<img width="1432" height="229" alt="image" src="https://github.com/user-attachments/assets/2b5c78ed-4c42-4a93-8e15-106e8075119b" />


SEASONAL ADJUSTMENT:
<img width="1435" height="226" alt="image" src="https://github.com/user-attachments/assets/d17d7eb0-332b-4601-ad7f-b08a89a07c60" />


LOG TRANSFORMATION:
<img width="1430" height="231" alt="image" src="https://github.com/user-attachments/assets/c8a1d001-de2d-43ee-baba-349d5b8eabc8" />

LOG TRANSFORMATION + REGULAR DIFFERENCING:
<img width="1431" height="231" alt="image" src="https://github.com/user-attachments/assets/5552fb4f-6dff-492f-99c3-126967b056a7" />

LOG TRANSFORMATION + REGULAR DIFFERENCING + SEASONAL ADJUSTMENT:
<img width="1434" height="236" alt="image" src="https://github.com/user-attachments/assets/1f361618-eb13-4381-a2e7-5ad532247673" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
