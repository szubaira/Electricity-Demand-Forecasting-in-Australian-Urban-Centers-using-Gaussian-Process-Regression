## **Electricity Demand Forecasting in Australian Urban Centers using Gaussian Process Regression**

### **Project Overview**

This project focused on developing a high-resolution forecasting model to predict half-hourly electricity demand over a seven-day period for a city in Australia. By utilizing **Gaussian Process Regression (GPR)** from the Scikit-learn library, the analysis successfully captured the complex, non-linear, and periodic nature of energy consumption patterns. The resulting models provided not only point estimates for demand but also quantified uncertainty through 95% confidence intervals, enabling more robust operational planning for energy providers.

### **Business Understanding**

The primary stakeholders for this project are **utility grid operators and energy providers** responsible for maintaining grid stability and optimizing power generation. The core business problem is the extreme volatility of electricity demand, which fluctuates based on daily cycles and consumer behavior.

Research indicates that accurate short-term load forecasting (STLF) can significantly reduce operational costs by preventing over-generation and mitigating the risk of grid failures during peak hours. By employing Bayesian methods like Gaussian Processes, operators can account for both periodic trends and stochastic noise, allowing for more informed decisions regarding reserve margins and spot-market purchasing.

### **Data Understanding**

The analysis was performed on a dataset recording seven days of electricity demand in an Australian city.

* **Timeframe:** The data captures a full week of demand, with measurements taken every 30 minutes, totaling 48 entries per day (336 observations).
* **Features:** The primary variables included the time index (input) and the recorded electricity demand (target).
* **Data Limitations:** The small timeframe (one week) represents a "snapshot" of demand and does not account for long-term seasonal shifts (e.g., summer vs. winter) or exogenous variables like temperature, humidity, and public holidays, which are significant drivers of electricity usage.
* **Exploratory Data Analysis (EDA):** Visualizations were generated to map observations for each day, revealing a clear daily periodicity characterized by morning and evening surges.

### **Modeling and Evaluation**

I implemented and optimized a **Gaussian Process Regressor** using a comparative kernel approach to determine the best fit for the periodic demand signal:

* **Kernels Evaluated:** * **ExpSineSquared:** Used to model the inherent daily periodicity of the demand.
* **Rational Quadratic (RQ):** Applied to capture variations across different length scales.
* **Composite Kernels:** Optimized combinations such as (Constant * ExpSineSquared) and a complex mixture (Constant * ExpSineSquared * Rational Quadratic) to account for both cyclic behavior and structural trends.


* **Evaluation Metrics:** * **95% Confidence Interval:** Used to evaluate the model's reliability and quantify predictive uncertainty.
* **Visual Fit:** Compared predictions against red-dot observations to assess how well the kernels captured the daily demand "peaks" and "valleys".


* **Optimization:** Utilized `n_restarts_optimizer` to avoid local minima and ensure the convergence of kernel hyperparameters.

### **Conclusion**

The analysis demonstrates that a Gaussian Process Regressor equipped with an **ExpSineSquared kernel** is highly effective at capturing the recurring daily cycles of urban electricity demand. Based on the results, I recommend that stakeholders utilize composite kernels that blend periodic and rational quadratic components to ensure the model remains flexible to both daily cycles and unexpected demand shifts.

**Future Steps:**

* **Feature Expansion:** Incorporate local weather data (temperature and cooling-degree days) as exogenous regressors to improve forecasting accuracy during extreme weather events.
* **Longitudinal Analysis:** Expand the training window to include several months of data to account for weekly and seasonal periodicities beyond the 24-hour cycle.
* **Cross-Validation:** Implement rolling-window cross-validation to test the model’s predictive capabilities on future days outside of the initial seven-day window.
