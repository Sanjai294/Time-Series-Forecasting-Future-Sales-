# ARIMA and Seasonal ARIMA Project

## Overview
This project demonstrates the application of **ARIMA (Autoregressive Integrated Moving Average)** and **Seasonal ARIMA** models to forecast time series data. The dataset used is the "Perrin Freres monthly champagne sales" from 1964 to 1972, stored in the file `perrin-freres-monthly-champagne-.csv`. The notebook walks through the following steps:
1. Visualizing the time series data.
2. Making the time series stationary.
3. Plotting correlation and autocorrelation charts.
4. Constructing an ARIMA or Seasonal ARIMA model.
5. Using the model to make predictions.

The project is implemented in Python using libraries such as `pandas`, `numpy`, `matplotlib`, and `statsmodels`.

## Prerequisites
To run this project, you need the following:
- **Python 3.10+**: Ensure Python is installed on your system.
- **Jupyter Notebook**: For running the `.ipynb` file interactively.
- **Dataset**: The file `perrin-freres-monthly-champagne-.csv` must be available in the working directory.

### Required Python Libraries
- `numpy`: For numerical computations.
- `pandas`: For data manipulation and analysis.
- `matplotlib`: For data visualization.
- `statsmodels`: For implementing ARIMA and Seasonal ARIMA models.

## Installation
1. **Clone or Download the Repository**:
   - Clone this repository or download the notebook and dataset file to your local machine.

2. **Set Up a Virtual Environment** (Optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   Install the required libraries using `pip`:
   ```bash
   pip install numpy pandas matplotlib statsmodels
   ```

4. **Install Jupyter Notebook** (if not already installed):
   ```bash
   pip install jupyter
   ```

5. **Launch Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```
   Open the notebook file (e.g., `ARIMA_Seasonal_ARIMA.ipynb`) in your browser.

## Usage
1. **Prepare the Dataset**:
   - Ensure `perrin-freres-monthly-champagne-.csv` is in the same directory as the notebook.
   - The dataset contains two columns: `Month` (date) and `Perrin Freres monthly champagne sales millions ?64-?72` (sales data).

2. **Run the Notebook**:
   - Open the notebook in Jupyter and execute the cells sequentially.
   - The notebook performs the following:
     - Loads and cleans the data (removes invalid rows, converts `Month` to datetime, renames columns, and sets `Month` as the index).
     - Visualizes the sales data (though the plotting code is incomplete in the provided snippet).
     - Sets up the framework for ARIMA modeling and forecasting (incomplete in the snippet; requires additional code).

3. **Complete the ARIMA Model**:
   - The provided notebook snippet ends prematurely. To complete the ARIMA forecasting, add the following code after data preparation:
     ```python
     import statsmodels.tsa.arima.model as arima_model

     # Define and fit the ARIMA model
     model = arima_model.ARIMA(df['Sales'], order=(1, 1, 1))
     results = model.fit()

     # Create a future dataframe for predictions
     future_df = df.copy()
     future_df['forecast'] = results.predict(start=102, end=120, dynamic=True)

     # Plot the results
     future_df[['Sales', 'forecast']].plot(figsize=(12, 8))
     plt.show()
     ```
   - Adjust the `order=(p, d, q)` parameters based on autocorrelation analysis or use a Seasonal ARIMA model (`SARIMAX`) if seasonality is detected (e.g., `order=(1, 1, 1), seasonal_order=(1, 1, 1, 12)` for monthly data with yearly seasonality).

4. **Interpret Results**:
   - The plot will display historical sales alongside forecasted values from index 102 (July 1972) to 120.

## Project Structure
- `ARIMA_Seasonal_ARIMA.ipynb`: The main Jupyter Notebook containing the code and explanations.
- `perrin-freres-monthly-champagne-.csv`: The dataset file (not included here; must be sourced separately).

## Notes
- **Data Cleaning**: The notebook removes rows 104-106 due to invalid data (NaN and non-date entries). Verify this aligns with your dataset.
- **Stationarity**: The notebook does not explicitly check for stationarity (e.g., using the Augmented Dickey-Fuller test). Add this step before fitting the model:
  ```python
  from statsmodels.tsa.stattools import adfuller
  result = adfuller(df['Sales'])
  print('ADF Statistic:', result[0])
  print('p-value:', result[1])
  ```
- **Seasonality**: The champagne sales data likely exhibits seasonality (e.g., peaks around holidays). Consider using `SARIMAX` from `statsmodels.tsa.statespace.sarimax` for better results.
- **Error Handling**: The original `ARIMA` implementation from `statsmodels.tsa.arima_model` is deprecated. Use `statsmodels.tsa.arima.model.ARIMA` as shown above.

## Contributing
Feel free to fork this project, submit issues, or contribute enhancements via pull requests.

## License
This project is unlicensed and provided as-is for educational purposes.

---

This README provides a clear guide for setting up and running your project while addressing the incomplete parts of the notebook (e.g., the missing `results` variable). Let me know if you'd like further refinements!****
