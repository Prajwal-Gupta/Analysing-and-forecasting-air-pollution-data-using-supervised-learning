# Analysing-and-forecasting-air-pollution-data-using-supervised-learning

Our project works on extracting the values like AQI and other pollutants like PM2.5 PM10, NO2, SO2 NH3, CO and Ozone from a public website.

We compare pollution level data from 2 different stations belonging in Chennai and Delhi and then perform a comparative study on them.

And finally we use LSTM and ARIMA to forecast the data and then compare the forecasted values with the actual values.

## About the dataset ##

The data was scrapped from National Air Quality Index which is an official government website.

- Data is taken from two stations, namely-
    - Royapuram, Chennai
    - Chandni Chowk, Delhi
- Hourly data is taken for the month of August 2022.
- The data contains values for Day, Date, Time, PM2.5, PM10, NO2, NH3, SO2, CO, Ozone and AQI.
- A total of 744 rows x 11 columns of data is extracted for each city.
- Then data is checked for null values. 
- The null values found in the middle are interpolated using pandas library and the null values found in the beginning of the data are filled with the mean of the column and the columns having most of their values as null are dropped.


## Model 1- LSTM ##

- This mainly involves normalising the data and splitting the dataset into training and testing values.
- Empirical results show that the normalized quantized LSTMs achieve significantly better results than their unnormalized counterparts.
- Therefore data is normalized to have values between 0 and 1.
- The data is then split into train and test data, training comprising of nearly 90% data i.e. 28 days (672 rows) and testing comprising of the remaining 10% data i.e. 3 days (72 rows).
- A variable look_back is specified which is the number of previous time steps to use as input variables to predict the next time period.
- According to this look_back variable, we made 2 different datasets and ran the LSTM model on both of them.
- look_back = 1
    - When look_back is 1 a dataset is created where X is the AQI at a given time t, and Y is the AQI at the next time t + 1.
    - For eg-
    - ![image](https://github.com/Prajwal-Gupta/Analysing-and-forecasting-air-pollution-data-using-supervised-learning/assets/61011807/3c807f3c-878e-4f38-ac46-3d20c814aa8f)



- look_back = 3
    - When look_back is 3, a dataset is created where X is the AQI at a given time t-2, t-1, t, and Y is the AQI at the next time t + 1.
    - For eg-
    - ![image](https://github.com/Prajwal-Gupta/Analysing-and-forecasting-air-pollution-data-using-supervised-learning/assets/61011807/3d0c7939-006e-4eff-888e-94d7af0dbcdc)
 

## Model 2- ARIMA ##

- ARIMA stands for Auto Regressive Integrated Moving Average.
- Any ‘non-seasonal’ time series that exhibits patterns and is not a random white noise can be modeled with ARIMA models.
- If a time series, has seasonal patterns, then you need to add seasonal terms and it becomes SARIMA, short for ‘Seasonal ARIMA’.
- We have used  70% data for training and 30% for testing i.e. 520 rows for training and 224 rows for testing.
- First ARIMA was used and it was observed graphically that it doesn’t give very good results, hence the concept of Seasonal ARIMA is used.
- Forecasting is done on AQI values.


## Results ##

- As observed, all the pollutants except CO are more in amount in Chandni Chowk as compared to Royapuram. The only pollutant which is more in amount in Royapuram is CO.
- We also observed that the pollutants PM 2.5 and PM 10 do not vary significantly between Chandni Chowk and Royapuram.
- The Changes observed in the pollutants in Chandni Chowk are more drastic compared to Royapuram which showed a more consistent AQI readings.
- The pollutants Ozone and SO2 are also significantly high in Chandni Chowk compared to Royapuram.

- LSTM-
    - Royapuram Dataset-
    - look_back = 1
        - RMSE value obtained is- 2.96
    - look_back = 3
        - RMSE value obtained is- 2.14
    - Hence with the given such as the hyperparameters specified and the dataset used, model (b) performs better.

    - Chandni Chowk Dataset-
    - look_back = 1
        - RMSE value obtained is- 15.17 
    - look_back = 3
        - RMSE value obtained is- 13.66
    - Hence with the given such as the hyperparameters specified and the dataset used, model (b) performs better.
 
- ARIMA-
    - Royapuram Dataset-
        - RMSE value obtained is- 12.62
    - Chandni Chowk Dataset-
        - RMSE value obtained is- 36.95







