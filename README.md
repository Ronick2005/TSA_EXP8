# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python for daily website visitors dataset.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

warnings.filterwarnings('ignore')

file_path = '/content/daily_website_visitors.csv'
data = pd.read_csv(file_path)

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data['Page.Loads'] = pd.to_numeric(data['Page.Loads'].str.replace(',', ''), errors='coerce')
data.dropna(subset=['Page.Loads'], inplace=True)

page_loads = data['Page.Loads']

plt.figure(figsize=(12, 6))
plt.plot(page_loads, label='Original Page Loads', color='blue')
plt.title('Transform Dataset (Original Page Loads)')
plt.xlabel('Date')
plt.ylabel('Page Loads')
plt.legend()
plt.grid()
plt.show()

rolling_mean_5 = page_loads.rolling(window=5).mean()

plt.figure(figsize=(12, 6))
plt.plot(page_loads, label='Original Page Loads', color='blue')
plt.plot(rolling_mean_5, label='Moving Average (window=5)', color='orange')
plt.title('Moving Average of Page Loads')
plt.xlabel('Date')
plt.ylabel('Page Loads')
plt.legend()
plt.grid()
plt.show()

model = ExponentialSmoothing(page_loads, trend='add', seasonal=None)
model_fit = model.fit()

future_steps = 5
predictions = model_fit.predict(start=len(page_loads), end=len(page_loads) + future_steps - 1)

future_dates = pd.date_range(start=page_loads.index[-1] + pd.Timedelta(days=1), periods=future_steps, freq='D')

plt.figure(figsize=(12, 6))
plt.plot(page_loads, label='Original Page Loads', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Page Loads')
plt.xlabel('Date')
plt.ylabel('Page Loads')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()

```
### OUTPUT:

#### Moving Average
![image](https://github.com/user-attachments/assets/ec06ba6c-c5ca-4e65-8e3a-b75aa44e8985)

#### Plot Transform Dataset
![image](https://github.com/user-attachments/assets/4e1ab13f-fd16-4320-8f82-4e80d4e07b58)

#### Exponential Smoothing
![image](https://github.com/user-attachments/assets/e99f522a-837d-4920-8f2d-228dfc752ef1)



### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python for daily website visitors dataset.
