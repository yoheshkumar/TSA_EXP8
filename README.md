## DEVELOPED BY: YOHESH KUMAR R.M
## REGISTER NO: 212222240118
## DATE:

# Ex.No: 08     MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 
## AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
## ALGORITHM:
1. Import necessary libraries
2. Read the House Sales time series data from a CSV file,Display the shape and the first 20 rows of
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
## PROGRAM:
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

warnings.filterwarnings('ignore')

file_path = 'Microsoft_Stock.csv'
data = pd.read_csv(file_path)

print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data['Close'] = pd.to_numeric(data['Close'], errors='coerce')
data = data.dropna()

plt.figure(figsize=(12, 6))
plt.plot(data['Close'], label='Original Price', color='blue')
plt.title('Original Price Data')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.grid()
plt.show()

rolling_mean_3 = data['Close'].rolling(window=3).mean()

plt.figure(figsize=(12, 6))
plt.plot(data['Close'], label='Original Price', color='blue')
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title('Moving Average of Price')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.grid()
plt.show()

model = ExponentialSmoothing(data['Close'], trend='add', seasonal=None)
model_fit = model.fit()

future_steps = 5
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

future_dates = pd.date_range(start=data.index[-1] + pd.Timedelta(days=1), periods=future_steps)

plt.figure(figsize=(12, 6))
plt.plot(data['Close'], label='Original Price', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Price')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()

```

## OUTPUT:
### GIVEN DATA
![Screenshot 2024-10-17 213953](https://github.com/user-attachments/assets/e5d5e5b3-5c49-471b-a15e-3fe907467860)

### Moving Average
![image](https://github.com/user-attachments/assets/a78978ab-fecd-482d-9463-75e496540d12)

### Plot Transform Dataset
![image](https://github.com/user-attachments/assets/d061e82d-c887-4bac-b431-9d0516589926)

### Exponential Smoothing
![image](https://github.com/user-attachments/assets/90bedb8f-71b3-45ca-8b6e-1185cf40ea48)



## RESULT:
Thus, the program to implement the Moving Average Model and Exponential smoothing using python is executed successfully.
