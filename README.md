# Stock-Price-Prediction
Google Stock Price Prediction Model using recurrent neural networks

Data Source: Yahoo Finance Website 
Training Data: 5 Years Data from Feb-2018 to Jan-2023
Testing Data: 19 Financial Days from Feb-2023

DATA PREPROCESSING

Prior to the model building, the data underwent some preprocessing to be made suitable for the algorithm chosen.

Test and Train Split

We had data spanning from 2018-2023, we had to split this into training and test set
Training data spanned for 5 years (only business days) from 02-01-2018 to 01-31-2023
Test data was the data we would test our model performance on spanned from 02-01-2023 – 02-28-2023

Scaling

As per the requirement of deep neural networks data must be scaled and there should not be a lot of difference between values 
We normalised the values and brought them between 0 and 1
We created two separate scaler objects using MinMaxScaler from Scikit-Learn. One for the whole input data and one for only open prices (this would come in handy later)

Timestep

As required for time-series analysis we chose a timestep of 60 days as input for predicting the value of next days opening price
We divided and reshaped our training data accordingly into a 3-D array
Final dimensions of the array was (1198,60,5) which indicated 1198 – instances, 60 samples in each batch and 5 variables
Similarly we repeated the process for the test data and the dimensions were (19,60,5)

Data was cleaned and scaled down ready for the model training


Algorithm chosen – LSTM
LSTM specifications - Four LSTM Layers with 70 neurons in each layer were used and we used a dropout regularization of 15% 
Dropout Regularization was used to avoid the problem of overfitting

Model Training

The 4 layers were then fitted on the training data of 5 years
Optimizer used – “Adam”
Loss function – “Mean Squared Error”
4 layers of LSTM was trained in 100 epochs with  batch size of 32
Early stopping was  used to avoid the problem of overfitting

Model Testing 

We now passed the test set through our model to test the overall performance of our model 
As we needed past 60 days data as input for predicting next days opening price so we had to combine 60 previous values for each day in February. Hence, some were used from the training data
For example for predicting the value of 28-Feb-23 we used data of past 60 business days. We obtained 18 values from our test set and rest from training set 
Predictions which are in the scaled format are inverse transformed to obtain predicted stock price values 

Model Evaluation 

The performance was evaluated on the basis of some metrics and validated with unseen data prediction.
Model Evaluation Metrics
MAE - 1.211 (Mean Absolute Error)
MAPE -  1.206(Mean Absolute Percentage Error)
Validation 
Evaluating Model performance on unseen data is crucial to evaluate how it will perform in real world scenario
We used our model to predict the price on 1-March-23
Model Prediction - 89.38348
Actual Stock Price on 03/01 -  90.160004


Notes: Avoiding overfitting

Several methodologies or parameters were adopted to tune the model and get the highest performance
No. of neurons in each layer of the LSTM algorithm 
Only four LSTM hidden layers were used to avoid making the model complex
Dropout Regularisation rate 
Early Stopping 









