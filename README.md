# SGD-Regressor-for-Multivariate-Linear-Regression

## AIM:
To write a program to predict the price of the house and number of occupants in the house with SGD regressor.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
1. Load California housing data, preprocess by scaling features and target variables.
2. Split data into training and testing sets (80% train, 20% test).
3. Train a MultiOutputRegressor with SGDRegressor on the scaled data.
4. Predict on the test set, inverse transform predictions, and calculate the mean squared error.

## Program:
Program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor.
Developed by: Venkatachalam S
RegisterNumber:  212224220121

```
import numpy as np
import pandas as pd
from sklearn.datasets import fetch_california_housing
from sklearn.linear_model import SGDRegressor
from sklearn.multioutput import MultiOutputRegressor
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler

dataset = fetch_california_housing()
df = pd.DataFrame(dataset.data, columns=dataset.feature_names)
df['HousingPrice'] = dataset.target
print(df.head())

X = df.drop(columns = ['AveOccup','HousingPrice'])
Y = df[['AveOccup','HousingPrice']]
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=42)
scaler_X = StandardScaler()
scaler_Y = StandardScaler()
X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)
Y_train = scaler_Y.fit_transform(Y_train)
Y_test = scaler_Y.transform(Y_test)

sgd = SGDRegressor(max_iter=100, tol=1e-3)
multi_output_sgd = MultiOutputRegressor(sgd)
multi_output_sgd.fit(X_train, Y_train)
Y_pred = multi_output_sgd.predict(X_test)
Y_pred = scaler_Y.inverse_transform(Y_pred)
Y_test = scaler_Y.inverse_transform(Y_test)
mse = mean_squared_error(Y_test, Y_pred)
print("Mean Squared Error: ", mse)
print("Predictions: ",Y_pred[:5])


```

## Output:
![image](https://github.com/user-attachments/assets/b7621a3a-130d-4fde-a392-da611db9bb55)
![image](https://github.com/user-attachments/assets/1c78baa1-c08c-440c-9713-5d84ce5a7236)

## Result:
Thus the program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor is written and verified using python programming.
