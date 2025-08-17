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

data = data.sort_values(by='Prod. year') 
data.set_index('Prod. year', inplace=True)
data["Engine volume"] = data["Engine volume"].str.replace(r'[^0-9.]', '', regex=True).astype(float)
# --- 1. Log Transformation ---
data['log_engine_volume'] = np.log(data['Engine volume'])

# --- 2. Regular Differencing ---
data['diff_engine_volume'] = data['Engine volume'].diff()

# --- 3. Seasonal Adjustment ---
# Assuming yearly data with seasonality period of 12 (adjust if monthly/quarterly etc.)
decomposition = seasonal_decompose(data['Engine volume'], model='additive', period=12)

data['seasonal'] = decomposition.seasonal
data['trend'] = decomposition.trend
data['residual'] = decomposition.resid
data['seasonally_adjusted'] = data['Engine volume'] - data['seasonal']

# --- Plot results ---
plt.figure(figsize=(12,10))

plt.subplot(511)
plt.plot(data['Engine volume'], label='Original')
plt.legend()

plt.subplot(512)
plt.plot(data['diff_engine_volume'], label='Differenced')
plt.legend()

plt.subplot(513)
plt.plot(data['log_engine_volume'], label='Log Transformed')
plt.legend()

plt.subplot(514)
plt.plot(data['seasonal'], label='Seasonal Component')
plt.legend()

plt.subplot(515)
plt.plot(data['seasonally_adjusted'], label='Seasonally Adjusted')
plt.legend()
plt.show()

```

### OUTPUT:

ORIGINAL:
<img width="1254" height="205" alt="image" src="https://github.com/user-attachments/assets/6fd48d9e-042d-41a6-a767-37e5c5219cda" />

REGULAR DIFFERENCING:
<img width="1276" height="211" alt="image" src="https://github.com/user-attachments/assets/a466a946-bf91-4ad6-9bbc-28ad9731e36d" />

SEASONAL ADJUSTMENT:
<img width="1248" height="222" alt="image" src="https://github.com/user-attachments/assets/4f565c53-619a-4978-b928-93d23128962f" />

LOG TRANSFORMATION:
<img width="1243" height="198" alt="image" src="https://github.com/user-attachments/assets/874e5121-41ee-470c-9af9-8ab25b923b2d" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
