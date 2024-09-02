### Developed by: Shriram S
### Register Number: 212222240098
### Date :

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:
To perform regular differncing,seasonal adjustment and log transformation on Vegetable Price specificalyy Methi Price Data.

### ALGORITHM:

1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.

### PROGRAM:

```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
```py
file_path = '/content/prices.csv'
data = pd.read_csv(file_path)
```

```py
data['Price Dates'] = pd.to_datetime(data['Price Dates'], format='%d-%m-%Y') 
data.set_index('Price Dates', inplace=True)  
data.fillna(method='ffill', inplace=True)  
```

```py
apc_data = data['Methi']
```
```py
# Plot Original Data for APC
plt.figure(figsize=(14, 8))
plt.plot(apc_data, label='Methi')
plt.title('Original Methi Price')
plt.legend()
plt.show()
```
```py
# Regular Differencing for APC
apc_diff = apc_data.diff().dropna()
```
```py
# Plot Differenced Data for APC
plt.figure(figsize=(14, 8))
plt.plot(apc_diff, label='Methi (Diff)')
plt.title('Differenced Methi Price')
plt.legend()
plt.show()
```
```py
# Log Transformation for APC
apc_log = np.log(apc_data + 1)  # Adding 1 to avoid log(0)
```
```py
# Plot Log-Transformed Data for APC
plt.figure(figsize=(14, 8))
plt.plot(apc_log, label='Methi (Log)')
plt.title('Log-Transformed Methi Price')
plt.legend()
plt.show()
```
```py
# Seasonal Adjustment (using moving average) for APC
apc_seasonal_adjustment = apc_log - apc_log.rolling(window=7).mean()
apc_seasonal_adjustment.dropna(inplace=True)
```
```py
plt.figure(figsize=(14, 8))
plt.plot(apc_seasonal_adjustment, label='Methi (Seasonally Adjusted)')
plt.title('Seasonally Adjusted Log-Transformed Methi Price')
plt.legend()
plt.show()
```

### OUTPUT:

![image](https://github.com/user-attachments/assets/47e21f7b-d932-47d5-ba01-d937027bc6a5)


REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/b3323ee3-91b1-44c1-b5fa-2b2f45aada0b)

SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/f6faf90b-2e21-4577-ab5b-561e9856cfa7)


LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/952d0fb0-0389-4c31-86db-e08226bd98f5)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on vegetable price
data.
