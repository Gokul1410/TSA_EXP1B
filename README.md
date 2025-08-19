# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

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
data=pd.read_csv('/content/Crypto Data Since 2015.csv')
data['Date']=pd.to_datetime(data['Date'])
data.set_index('Date',inplace=True)

data['Bitcoin (USD)_diff']=data['Bitcoin (USD)']-data['Bitcoin (USD)'].shift(1)

result = seasonal_decompose(data['Bitcoin (USD)'], model='additive', period=12)
data['Bitcoin (USD)_sea_diff']=result.resid

data['Bitcoin (USD)_log'] = np.log(data['Bitcoin (USD)'])
data['Bitcoin (USD)_log_diff']=data['Bitcoin (USD)_log']-data['Bitcoin (USD)_log'].shift(1)
result = seasonal_decompose(data['Bitcoin (USD)_log_diff'].dropna(), model='additive', period=30)
plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 1)
plt.plot(data['Bitcoin (USD)'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('No of Bitcoin (USD)')
plt.subplot(6, 1, 2)
plt.plot(data['Bitcoin (USD)_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced No of Bitcoin (USD)')
plt.subplot(6, 1, 3)
plt.plot(data['Bitcoin (USD)_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally djusted No of Bitcoin (USD)')
plt.subplot(6, 1, 4)
plt.plot(data['Bitcoin (USD)_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(No of Bitcoin (USD))')
plt.subplot(6, 1, 5)
plt.plot(data['Bitcoin (USD)_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(No of Bitcoin (USD)))')
plt.subplot(6, 1, 6)
from statsmodels.tsa.seasonal import seasonal_decompose

result = seasonal_decompose(
    data['Bitcoin (USD)_log_diff'].dropna(), 
    model='additive', 
    period=30 
)

data['Bitcoin (USD)_log_seasonal_diff'] = result.resid

plt.plot(data['Bitcoin (USD)_log_seasonal_diff'], label='Log Transformation and regular Diff')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(No of Bitcoin (USD))))')
plt.tight_layout()
plt.show()

data.plot(kind='line')
```

### OUTPUT:
ORIGINAL DATA:

<img width="1392" height="470" alt="Screenshot 2025-08-19 090828" src="https://github.com/user-attachments/assets/50142fd6-91a1-49e8-9ef2-b9d4844cdb82" />


REGULAR DIFFERENCING:

<img width="726" height="573" alt="Screenshot 2025-08-19 090842" src="https://github.com/user-attachments/assets/0bfe2b72-1aa2-415e-a884-9e85713494a2" />


SEASONAL ADJUSTMENT:

<img width="730" height="570" alt="Screenshot 2025-08-19 090852" src="https://github.com/user-attachments/assets/47983838-a36d-4b6f-a78d-768cbc95c675" />


LOG TRANSFORMATION:

<img width="725" height="570" alt="Screenshot 2025-08-19 090906" src="https://github.com/user-attachments/assets/0a80b358-1492-404e-b893-f30e758d9524" />


LOG TRANSFORMATION AND REGULAR DIFFERENCING:

<img width="727" height="566" alt="Screenshot 2025-08-19 090918" src="https://github.com/user-attachments/assets/7a4df255-b3b1-466d-bdd5-5aabbb06b487" />


LOG TRANSFORMATION AND REGULAR DIFFERENCING AND SEASONAL ADJUSTMENT:

<img width="818" height="593" alt="Screenshot 2025-08-19 090932" src="https://github.com/user-attachments/assets/92504223-fafa-46f7-a4fe-63c7026fa24a" />

<img width="724" height="541" alt="Screenshot 2025-08-19 090943" src="https://github.com/user-attachments/assets/84eb3c4b-6f51-4eb3-9a49-08d38bd3d89a" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
