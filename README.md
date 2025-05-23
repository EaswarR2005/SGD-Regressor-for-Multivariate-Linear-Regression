# SGD-Regressor-for-Multivariate-Linear-Regression

## AIM:
To write a program to predict the price of the house and number of occupants in the house with SGD regressor.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm

1.  Import Libraries
   - Import `numpy`, `pandas`, and scikit-learn modules.

2.  Load Dataset
   - Fetch the California housing dataset.
   - Create a DataFrame `df` and add the `HousingPrice` target column.

3.  Prepare Features and Target
   - Features `X`: Drop `AveOccup` and `HousingPrice` columns.
   - Targets `Y`: Keep `AveOccup` and `HousingPrice` columns.

4.  Split Data 
   - Split `X` and `Y` into training and testing sets.

5.  Standardize Data 
   - Scale `X_train`, `X_test`, `Y_train`, and `Y_test` using `StandardScaler`.

6.  Train Model 
   - Initialize `SGDRegressor` wrapped with `MultiOutputRegressor`.
   - Fit the model on `X_train` and `Y_train`.

7.  Predict and Evaluate
   - Predict on `X_test`.
   - Inverse transform predictions and true labels.
   - Calculate and print Mean Squared Error.
   - Print sample predictions.
## Program :
```
/*
Program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor.
Developed by: EASWAR R
RegisterNumber:  212223230053
*/
```
```
import numpy as np
import pandas as pd
from sklearn.datasets import fetch_california_housing
from sklearn.linear_model import SGDRegressor
from sklearn.multioutput import MultiOutputRegressor
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler
dataset=fetch_california_housing()
df=pd.DataFrame(dataset.data,columns=dataset.feature_names)
df['HousingPrice']=dataset.target
print(df.head())


X=df.drop(columns=['AveOccup','HousingPrice'])
Y=df[['AveOccup','HousingPrice']]
X_train,X_test,Y_train,Y_test=train_test_split(X,Y,test_size=0.2,random_state=42)
scaler_X=StandardScaler()
scaler_Y=StandardScaler()
X_train=scaler_X.fit_transform(X_train)
X_test=scaler_X.transform(X_test)
Y_train=scaler_Y.fit_transform(Y_train)
Y_test=scaler_Y.transform(Y_test)


sgd=SGDRegressor(max_iter=1000,tol=1e-3)
multi_output_sgd=MultiOutputRegressor(sgd)
multi_output_sgd.fit(X_train,Y_train)
Y_pred=multi_output_sgd.predict(X_test)
Y_pred=scaler_Y.inverse_transform(Y_pred)
Y_test=scaler_Y.inverse_transform(Y_test)
mse=mean_squared_error(Y_test,Y_pred)
print("Mean Squared Error:",mse)
print("\nPredictions:\n",Y_pred[:5])
```


## Output:

### Preview Datasets :
![ex4_op1](https://github.com/user-attachments/assets/e5d0af8f-8027-43c7-b86b-77035554d3e1)

### Print MSE & Predicted Value :
![image](https://github.com/user-attachments/assets/53b8c86f-f59c-4bba-812a-215ab83ee3ef)


## Result:
Thus the program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor is written and verified using python programming.
