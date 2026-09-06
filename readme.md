# Stock Market Predictor

A Streamlit web app that predicts stock closing prices using an LSTM neural network trained on historical price data pulled from Yahoo Finance.

## Features

- Fetches historical stock data for any ticker symbol via `yfinance`
- Visualizes the stock's closing price against 50-day, 100-day, and 200-day moving averages
- Uses a pre-trained LSTM model to predict prices on a held-out test set
- Plots predicted prices against actual prices for visual comparison

## Project Structure

```
.
├── app.py                          # Streamlit app (main entry point)
├── model.ipynb                     # Notebook used to build and train the LSTM model
├── Stock_Predictions_Model.keras   # Pre-trained Keras model
├── requirements.txt                # Python dependencies
└── README.md
```

## How It Works

1. Downloads daily stock data (2012–2022 by default) for a user-specified ticker
2. Splits the data into training (80%) and test (20%) sets
3. Scales the closing prices to a 0–1 range using `MinMaxScaler`
4. Feeds 100-day rolling windows into the LSTM model to predict the next day's price
5. Rescales predictions back to actual price values and plots them against real prices

## Usage

- Enter any valid stock ticker symbol (e.g., `GOOG`, `AAPL`, `TSLA`) in the input box.
- The app will fetch the corresponding historical data and display:
  - Raw stock data table
  - Moving average charts (MA50, MA100, MA200)
  - A chart comparing the model's predicted prices against actual prices

## Model

The LSTM model (`Stock_Predictions_Model.keras`) was trained in `model.ipynb` using:
- 4 stacked LSTM layers (50 → 60 → 80 → 120 units) with Dropout for regularization
- Adam optimizer, mean squared error loss
- 100-day lookback window as input, next-day closing price as the prediction target

To retrain the model on new data or a different ticker, open `model.ipynb`, update the ticker/date range, and re-run all cells. This will overwrite `Stock_Predictions_Model.keras`.

## Disclaimer

This project is for educational purposes only. Stock price predictions from this model should **not** be used as financial advice or for real trading decisions. Past performance and model backtests are not indicative of future results.

## License

Add a license of your choice here (e.g., MIT).