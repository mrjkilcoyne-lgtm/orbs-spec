# Time-Series Forecasting

## Scope
Predicting future values in temporal sequences: ARIMA, exponential smoothing, neural network methods, and seasonality decomposition. Stationarity, trend, and evaluation for sequential data.

## Core principles
- Autocorrelation (correlation with shifted versions of itself) is key: future values depend on past values (AR), past errors (MA), or both (ARMA). Identifying autocorrelation structure guides model choice.
- Stationarity (mean, variance, autocorrelation don't change over time) simplifies modeling. Non-stationary series (trend, seasonal patterns) require differencing (subtract previous value) to make stationary before fitting ARIMA.
- Seasonality (repeating patterns at regular intervals: daily, weekly, yearly) requires seasonal ARIMA (SARIMA) or explicit seasonal decomposition (trend + seasonal + residual).
- Exogenous variables (external features: weather, promotions, holidays) improve forecasts. Include them in ARIMAX or use neural networks naturally (they condition on features).
- Train-test split for time-series is non-standard: can't shuffle or use random hold-out (violates temporal order). Use walk-forward validation (train on past, test on future, incrementally).

## Apex practices
- Start with simple baselines (exponential smoothing, naive seasonal) before neural networks. Simple methods are fast, interpretable, and often competitive.
- Decompose the series: trend (smoother over time), seasonal (repeating patterns), residuals (noise). Forecast each component separately or together.
- Check stationarity (ADF test, KPSS test) and difference if non-stationary. Non-stationary series cause spurious regression (misleading correlations).
- Use walk-forward evaluation: train on [t0...t1], test on [t1+1...t2], move window forward. Report multiple test windows to assess consistency.

## Pitfalls
- Assuming linear trends continue forever; real-world data has breaks (policy changes, anomalies). Models must detect regime shifts.
- Ignoring exogenous variables; an external shock (pandemic, policy) changes the series fundamentally. Hard to extrapolate without explanatory variables.
- Evaluating on random train-test split; time-series require temporal ordering. Random splits leak future information into training.

## Tools & references
Statsmodels (ARIMA, exponential smoothing), Prophet (Facebook, automatic seasonality), PyTorch time-series libraries, "Forecasting: Principles and Practice" (Hyndman & Athanasopoulos, free online), walk-forward evaluation, MAPE (mean absolute percentage error).
