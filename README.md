1. Project Structure
The project is organized into the following files:

data/: https://data.giss.nasa.gov/gistemp/
       csv file Global-mean monthly, seasonal, and annual means, 1880-present, updated through most recent month

notebooks/: Global Temperature Evolution - ARIMA and SARIMA

README.md: This file, which summarizes the project.

requirements.txt: Lists all necessary Python libraries.

2. Exploratory Data Analysis (EDA)
In this phase, exploratory data analysis was conducted to understand the characteristics of the temperature anomaly time series. Key steps included:

Data Loading and Cleaning: The dataset was loaded, and the date column was processed to become the DataFrame's index. The column used for this work was the column J-D with the average anomalies of all the year (Jan to Dec)

Visualization: A line plot was generated to visualize the evolution of temperature anomalies over time, showing a clear warming trend.

Stationarity Testing: The series was tested for stationarity, a prerequisite for ARIMA models. It was found that the series was not stationary, requiring differencing.

ACF and PACF Analysis: Autocorrelation (ACF) and Partial Autocorrelation (PACF) plots were used to identify the model orders.

3. Time Series Modeling
Two models were built and evaluated for forecasting temperature anomalies.

3.1 ARIMA Model
An ARIMA(p, d, q) model was fitted to the data. The orders (p, d, q) were chosen based on the analysis of the ACF and PACF plots of the differenced series.

Order (3, 1, 1):

Justification: By analyzing the Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots of your time series data, we can identify the underlying structure of the data.

The q parameter is the number of significant lags in the ACF plot that "cut off" abruptly, identified as the number os values before droping to the blue area, q=2.

The p parameter is the number of significant lags in the PACF plot that "cut off" abruptly, identified as the number os values before droping to the blue area, p=3.

After using those values, a summary table helped to adjust these parameters to obtain P>|z| values <0.05

3.2 SARIMA Model
Considering the possibility of seasonality in the data, a SARIMA(p, d, q)(P, D, Q, S) model was tested.

Order (3, 1, 1)(1, 0, 2, 10):

Justification: The values were adjusted using the summary table to obtain P>|z| values <0.05

4. Backtesting and Model Validation
To validate the accuracy of each model, a backtesting process was performed. The time series was split into a training set (1880-2015) and a testing set (2016-2025).

Each model was fitted on the training data and then used to forecast values for the test period. Accuracy was measured using the following metrics:

Model	RMSE	MAPE
ARIMA	(0.4060)	0.50%)
SARIMA	(0.4170)	(0.49%)

Evaluation Conclusion: By comparing the results we can see that ARIMA model is better to predict future temperature anomalies.
It is also evident that, as predicted in the model graph, the anomalies will continue to rise over the next years.
