# Flood Prediction (Deep Learning)

## Table of Contents

- [About](#about)
- [Getting Started](#getting_started)
- [Usage](#usage)
- [Contributing](../CONTRIBUTING.md)

## About <a name = "about"></a>

This project was carried out to predict the potential for impending flooding for the Blackadder River by combining historical weather, river depth and volume flow data.

The prediction model is a BiLSTM model built with Tensorflow. The model is able to predict river flow rate within the timeframe of the data, as well as make river flow rate predictions beyond the date of the dataset. 

The model demonstrated sufficient ability to predict spikes in volume flow rate, which serve as indicators of flooding in the river.

## Getting Started <a name = "getting_started"></a>

To get started:
- Create a new virtual environment
- Clone this repository:
```
git clone https://github.com/theabrahamaudu/flood_prediction.git
```
- Install dependencies
```
pip install -r requirements.txt
```

## Prerequisites

Python 3.x

## Workflow
[] EDA & Preprocessing
- The datasets were loaded and inspected to gain insights on necessary EDA steps
- Datasets were cleaned by dropping unrequired columns and solving for missing values
- Categorical columns were encoded 
- The datasets were merged into one dataset on the date column
- The dataset was scaled to increase computational efficiency
- The dataset was restructured into a features and target array structure which allows for a sliding window approach

[] Model Building
- The model architecture was defined as shown below:
```
model = tf.keras.Sequential()

model.add(LSTM(256, input_shape=(trainX.shape[1], trainX.shape[2]), return_sequences=True))
model.add(LeakyReLU(alpha=0.5))
model.add(Bidirectional(LSTM(128, return_sequences=True)))
model.add(LeakyReLU(alpha=0.5))
model.add(Dropout(0.3))
model.add(Bidirectional(LSTM(64, return_sequences=False)))
model.add(Dropout(0.3))
model.add(Dense(trainY.shape[1]))

model.compile(optimizer='adam', loss='mse')
model.summary()
```
- The model was trained for 50 epochs using a tach size of 32 with early stopping criteria based on validation loss.
- Training lasted 7 epochs before stopping.
- The model gave an RMSE score of 1.6348 which is satisfactory, considering that the mean flow rate is 1.7314 m3/s, with a range between 0.17 and 27.9 m3/s
- Snapshots of the predictions for past and forecast data can be viewd [here](https://github.com/theabrahamaudu/flood_prediction/tree/main/reports)
  
  
## Usage <a name = "usage"></a>

- Navigate to the `flood_pred_LSTM_ts.ipynb` file in Notebooks directory
- Run all cells to ensure all modules are installed and helper functions are available  

[] To retrain model
- Skip to the `Train Model` section, uncomment the two training blocks and run all below.

[] To make forecast (works without retraining model)
- Skip to the `Forecasting` section and run all below.
- To switch between making past or future predictions, simply swap the commenting on the `forecast_period_dates` and the `forecast` variable in the first two blocks of the `Forecasting` section
- Note that the `Evaluation` section will break when making future forecasts beyond the dataset



### Author
[Abraham Audu](https://github.com/theabrahamaudu/) 

Socials  
[] [Twitter](https://twitter.com/the_abrahamaudu)  
[] [LinkedIn](https://www.linkedin.com/in/theabrahamaudu/)  


## Contributions and Observations
If you have any questions or contributions, please feel free to reach out to me.
Also, feel free to fork this repository and explore avenues to improve the code or approach. 
