# Bayesian Stochastic Volatility Modeling for SPY ETF

## Description

This repository contains a practical application of Bayesian filtering and time-series modeling to real-world financial data. It implements a **Stochastic Volatility with Leverage (SVL)** model to analyze the daily returns of the SPY ETF, which tracks the S&P 500 index.

The primary goal of this project is to move beyond the assumption of constant volatility (a key flaw in many simpler financial models) and instead model volatility as a hidden, time-varying process. This allows us to capture two fundamental "stylized facts" of financial markets:
1.  **Volatility Clustering:** Periods of high volatility tend to be followed by more high volatility, and vice versa.
2.  **Leverage Effect:** Asset returns are often negatively correlated with changes in their volatility (i.e., large drops in price are associated with bigger spikes in volatility than large rallies).

The project uses the modern probabilistic programming library **PyMC** to define the SVL model, calibrate its parameters using MCMC (Markov Chain Monte Carlo) sampling, and generate forecasts for future volatility.

The code is provided as a self-contained Google Colab notebook (`ML_in_Finance-SPY_ETF_SVL_Application.ipynb`), which handles everything from data acquisition to final visualization.

---

## Key Features

- **Data Acquisition:** Downloads up-to-date daily price data for the SPY ETF using the `yfinance` library.
- **Bayesian Modeling:** Implements a Stochastic Volatility with Leverage (SVL) model using `pymc`.
- **Custom Time-Series Distribution:** Defines a custom AR(1) distribution to model the latent volatility process.
- **MCMC Calibration:** Uses the No-U-Turn Sampler (NUTS) to fit the model and find the full posterior distributions of its parameters (`μ`, `φ`, `σv`, `ρ`).
- **Volatility Forecasting:** Includes a robust forecasting module to predict future volatility and quantify the associated uncertainty with credible intervals.
- **Rich Visualization:** Generates clear, publication-quality plots using `matplotlib` and `arviz` to display:
    -   Diagnostic trace plots.
    -   Posterior parameter distributions.
    -   The inferred historical latent volatility.
    -   A forward-looking volatility forecast with uncertainty bands.

---

## Sample Results

The model successfully uncovers the hidden volatility from the SPY return data and confirms key financial theories.

#### Inferred Historical Volatility
The model accurately identifies periods of high market stress, aligning perfectly with major historical events like the 2011 debt crisis, the 2018 sell-off, and the 2020 COVID-19 crash.



#### Volatility Forecast
The model can generate a forward-looking forecast, complete with uncertainty bands that naturally widen over time, providing a realistic view of future risk.


*(**Note:** You would replace this URL with a link to your own saved forecast plot image).*

#### Key Parameter Findings
- **High Persistence (`phi` ≈ 0.94):** Confirms that volatility is "sticky" and comes in clusters.
- **Strong Leverage Effect (`rho` ≈ -0.75):** Provides strong evidence that market drops are associated with larger spikes in volatility than market rallies.

---

## How to Use

The easiest way to run this project is to use Google Colab.

1.  **Open in Colab:** Click the "Open in Colab" badge at the top of this README.
2.  **Run the Notebook:** Once the notebook is open, click on `Runtime` -> `Run all`.
3.  **Process:** The notebook will automatically:
    -   Install all necessary dependencies (`!pip install ...`).
    -   Download the latest SPY data.
    -   Define and compile the PyMC model.
    -   Run the MCMC sampler to fit the model (this step may take several minutes).
    -   Generate and display all the summary tables and plots.

---

## Dependencies

The model is built using modern Python libraries. The notebook handles the installation for you.
- `pymc`
- `pytensor`
- `yfinance`
- `arviz`
- `numpy`
- `pandas`
- `matplotlib`

---

## Applications and Conclusion

This model is more than just an academic exercise. The daily volatility estimates and forecasts it produces have several practical applications in trading and risk management:

-   **Dynamic Position Sizing:** Adjusting trade sizes based on current volatility to maintain constant risk exposure.
-   **Options Trading:** Identifying potentially cheap or expensive options by comparing the model's statistical volatility forecast to the market's implied volatility (e.g., VIX).
-   **Regime-Based Strategies:** Switching between mean-reversion and trend-following strategies based on the current volatility regime (calm vs. stormy).
-   **Smarter Stop-Losses:** Setting stop-loss levels that are proportional to the daily volatility, making them more adaptive to market conditions.

This project serves as a clear, end-to-end example of how modern Bayesian methods can be applied to solve complex, real-world problems in quantitative finance.

---

*This project is based on the concepts and code presented in the notebook "ML_in_Finance-Kalman_Filters.ipynb" by M.F. Dixon, I. Halperin, and P. Bilokon.*
