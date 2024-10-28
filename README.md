# Ex.No: 08     MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING
## NAME : A.Ssidharan
## REGISTER NUMBER : 212221240049
### Date: 



### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
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

# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset from a CSV file
file_path = '/content/globaltemper.csv'  # Update with your actual file path
data = pd.read_csv(file_path)

# Display the shape and the first few rows of the dataset
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Ensure the 'dt' column (or your date column name) is in datetime format and set it as index
# Replacing 'Date' with 'dt' assuming 'dt' is your date column
# Changed the format to '%d-%m-%Y' to match the date format in your data
data['dt'] = pd.to_datetime(data['dt'], format='%d-%m-%Y')  
data.set_index('dt', inplace=True)  

# Plot Original Value Data
# Assuming 'AverageTemperature' is the column you want to plot
plt.figure(figsize=(12, 6))
# Replacing 'Close' with 'AverageTemperature'
plt.plot(data['AverageTemperature'], label='Original Average Temperature', color='blue')  
plt.title('Original Average Temperature Data')
plt.xlabel('Date')
plt.ylabel('Average Temperature')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 3 (adjust as needed)
# Replacing 'Close' with 'AverageTemperature'
rolling_mean_3 = data['AverageTemperature'].rolling(window=3).mean()  

# Plot Moving Average
plt.figure(figsize=(12, 6))
# Replacing 'Close' with 'AverageTemperature'
plt.plot(data['AverageTemperature'], label='Original Average Temperature', color='blue')  
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title('Moving Average of Average Temperature')
plt.xlabel('Date')
plt.ylabel('Average Temperature')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
# Replacing 'Close' with 'AverageTemperature'
model = ExponentialSmoothing(data['AverageTemperature'], trend='add', seasonal=None)  
model_fit = model.fit()

# Make predictions for the next 5 periods (adjust as needed)
future_steps = 5
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

# Create a future index for the predicted dates
future_dates = pd.date_range(start=data.index[-1] + pd.Timedelta(days=1), periods=future_steps)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
# Replacing 'Close' with 'AverageTemperature'
plt.plot(data['AverageTemperature'], label='Original Average Temperature', color='blue')  
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Average Temperature')
plt.xlabel('Date')
plt.ylabel('Average Temperature')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```
### OUTPUT:

![image](https://github.com/user-attachments/assets/1dcfce11-9685-430c-b5e2-4f288b42cf23)



Moving Average:

![image](https://github.com/user-attachments/assets/b62ce5dc-4053-4abc-9587-0c90ce81b54c)



Plot Transform Dataset:
![image](https://github.com/user-attachments/assets/c87338ab-72da-4f8e-8976-a722dd780f55)


Exponential Smoothing:

![image](https://github.com/user-attachments/assets/17b258b8-0ef9-4bd7-9d92-f57f99579473)



### RESULT:
Thus,Program was successfully implemented the Moving Average Model and Exponential smoothing using python.
