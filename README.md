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

<img width="742" height="570" alt="Screenshot 2025-08-19 093409" src="https://github.com/user-attachments/assets/d8a6255f-5de4-4beb-926d-0a9c93724be3" />


SEASONAL ADJUSTMENT:

<img width="720" height="569" alt="Screenshot 2025-08-19 093419" src="https://github.com/user-attachments/assets/60805ceb-74af-4a23-9de2-6ffdf490d40a" />


LOG TRANSFORMATION:

<img width="749" height="570" alt="Screenshot 2025-08-19 093428" src="https://github.com/user-attachments/assets/c2c25aba-4319-416d-8cdf-cbc177e6b768" />


LOG TRANSFORMATION AND REGULAR DIFFERENCING:

<img width="723" height="570" alt="Screenshot 2025-08-19 093437" src="https://github.com/user-attachments/assets/224c0ef0-6f57-4606-b0ba-2590a4643784" />


LOG TRANSFORMATION AND REGULAR DIFFERENCING AND SEASONAL ADJUSTMENT:

<img width="818" height="593" alt="Screenshot 2025-08-19 090932" src="https://github.com/user-attachments/assets/92504223-fafa-46f7-a4fe-63c7026fa24a" />

<img width="724" height="541" alt="Screenshot 2025-08-19 090943" src="https://github.com/user-attachments/assets/84eb3c4b-6f51-4eb3-9a49-08d38bd3d89a" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
