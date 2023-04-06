# Linear Regression

$y \equiv \beta_1 x_1 + \beta_0$

y is the target
$x_1, ...,x_n$ are the explanatory variables
$\beta_1$ is the slope
$\beta_0$ is the intercept

package: sklearn.model_selection
  - train_test_split()

`X_train, X_test, y_train, y_test = train_test_split(X, y, test_size)`
*test_size*: is given as the percentage of datapoints that will be added to the test_set. 

package: sklearn.linear_model
  - LinearRegression

`lrModel = LinearRegression()`
Instantiate a linear regression model

`lrModel.fit(X_train, y_train)`
fits the model with the training set. 
(We do not know yet how that works exactly ??) 

`y_pred = lrModel.predict(X_test)`
Predicting the value of y for the test set

package:  sklearn.metrics
  - mean_squared_error
  - mean_absolute_error

`mse_test = mean_squared_error(y_test, y_pred)`
Computing the MSE for the predicted vector

## Preprocessing

package: sklearn.preprocessing
  - PolynomialFeatures

TODO



