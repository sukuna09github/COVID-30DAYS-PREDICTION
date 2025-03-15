Here’s a documentation template for your Fbprophet class and its usage, which describes the purpose, methods, parameters, and outputs. This will help in understanding the model’s functionality and how it is utilized.

---

## **Fbprophet Class Documentation**

### **Overview**
The `Fbprophet` class is a custom wrapper for the **Prophet** model (a forecasting tool developed by Facebook) used for time series prediction. The model is suitable for daily, weekly, or yearly seasonality patterns and is ideal for forecasting univariate data with a clear trend. This class fits the model to historical data, performs forecasting, evaluates performance using R² score, and visualizes the forecasts.

### **Dependencies**
This class relies on the following libraries:
- **prophet**: For time series forecasting.
- **sklearn.metrics**: To compute the R² score for model performance evaluation.
- **matplotlib**: For plotting the forecast and components.

To install the required libraries, run:
```bash
pip install prophet
pip install matplotlib
pip install scikit-learn
```

### **Class: Fbprophet**

#### **Constructor: `__init__`**

**Purpose**:  
The constructor initializes the model and sets up necessary variables for forecasting.

```python
def __init__(self):
    self.model = None
    self.data = None
    self.df_forecast = None
    self.future = None
```

#### **Method 1: `fit`**

**Purpose**:  
Fits the **Prophet** model to the provided historical data. The model learns the patterns from the data and becomes ready to make future predictions.

**Parameters**:
- `data` (pd.DataFrame): A DataFrame containing historical data with two columns:
  - **ds**: The datetime column (date of observations).
  - **y**: The values of the observed time series (numeric).

**Example**:
```python
model.fit(df_fb)
```

#### **Method 2: `forecast`**

**Purpose**:  
Generates future forecasts for a specified number of periods and frequency.

**Parameters**:
- `periods` (int): The number of future periods to predict.
- `freq` (str): The frequency of the future periods. For example, `"D"` for daily, `"W"` for weekly, etc.

**Example**:
```python
model.forecast(periods=30, freq="D")
```

#### **Method 3: `plot`**

**Purpose**:  
Plots the forecasted values and their uncertainty bounds. Also plots the components of the time series, such as trends and seasonality.

**Parameters**:
- `xlabel` (str, optional): Label for the x-axis (default is "Years").
- `ylabel` (str, optional): Label for the y-axis (default is "Values").

**Example**:
```python
model.plot(xlabel="Date", ylabel="Cases")
```

#### **Method 4: `R2`**

**Purpose**:  
Calculates the R² score, which measures how well the model's predicted values match the actual data.

**Returns**:
- `float`: The R² score indicating the goodness of fit.

**Example**:
```python
model.R2()
```

---

### **Usage Example**

```python
import pandas as pd
import matplotlib.pyplot as plt

# Example DataFrame setup (time series data)
df_fb = pd.DataFrame({"ds": [], "y": []})
df_fb["ds"] = pd.to_datetime(df.index)  # Replace with actual datetime index
df_fb["y"] = df.iloc[:, 0].values  # Replace with your data's values

# Initialize model
model = Fbprophet()

# Fit the model
model.fit(df_fb)

# Forecast the next 30 days
model.forecast(periods=30, freq="D")

# Print R² score
print("R² Score:", model.R2())

# Plot the forecast
model.plot(xlabel="Date", ylabel="Forecasted Cases")

# Show the plot
plt.show()
```

---

### **Output**

1. **R² Score**: A floating-point value representing the R² score, which indicates how well the model's predictions fit the actual data.
   - **Higher values** (close to 1) indicate a better fit.

2. **Forecast Plot**:  
   A plot showing:
   - The historical values (`y`).
   - The forecasted values (`yhat`).
   - Confidence intervals (`yhat_lower` and `yhat_upper`).

3. **Component Plots**:  
   The component plots reveal the underlying patterns of the time series, such as:
   - Trend.
   - Seasonal components (weekly, yearly).
   - 
### **Considerations**
- **Data Quality**: Ensure that the input data has correct datetime formatting and no missing or incorrect values.
- **Tuning**: The Prophet model allows you to tune various hyperparameters such as seasonality, holidays, and changepoints. Customizations can improve forecast accuracy.
- **R² Interpretation**: An R² score above 0.7 is considered good, but in cases with high volatility (such as COVID-19 cases), a lower R² might still be acceptable.

### **Conclusion**

The `Fbprophet` class offers a convenient wrapper around the Prophet model, making it easier to perform time series forecasting, evaluate model performance, and visualize the results. Whether you are working with daily, weekly, or yearly data, the `Fbprophet` class can be customized for various forecasting needs, including trend analysis and future predictions.

