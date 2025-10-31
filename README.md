**Project: Analyzing Public Interest in Nuclear Energy (2004-2025)**

**Goal**

This project investigates the drivers of public interest in nuclear energy in the United States, testing the relative impact of economic incentives (electricity prices) and information shocks / salience bias from the Fukushima Daiichi nuclear disaster.

**Data Sources**

Public Interest: Google Trends search data for "nuclear energy" (Monthly, 2004-Present, United States).

Economic Incentive: Average Retail Price of Electricity per Kilowatt-Hour (Monthly, US City Average, FRED series APU000072610).

**Methodology**

An Interrupted Time-Series (ITS) analysis was conducted using Ordinary Least Squares (OLS) regression.

Data Preparation: Both time series were cleaned, merged, and indexed by month using python (pandas)

Seasonality: The nuclear interest time series displayed strong seasonality in my intermediate visualizations, which was removed using multiplicative decomposition. The price data showed insignificant seasonality.

Stationarity: The Augmented Dickey-Fuller (ADF) test confirmed that the seasonally adjusted Nuclear Energy Interest data was stationary ($P<0.05$). The Electricity Price data was non-stationary ($P>0.05$), which was accounted for using differencing.

Intervention Variable: A dummy variable (Fukushima_Dummy) was created, taking the value 0 before March 2011 and 1 from March 2011 onwards. This was done to assess the potential long-term effects on public interest in nuclear energy caused by the event.

Model: Interest_Stationary = β0 + β1(Price_Stationary) + β2(Fukushima_Dummy)

**Key Findings**

The OLS regression yielded statistically significant results for both independent variables:

Economic Incentive Matters: Monthly changes in electricity price have a positive and significant effect on public interest ($\beta \approx 1089$, $P = 0.004$).

Information Shock Matters More: The Fukushima event created a negative and significant structural break in public interest ($\beta \approx -3.81$, $P = 0.000$). The event is associated with a lasting average drop of ~3.8 units in the baseline level of public interest, after controlling for price changes.

**Limitations**

Low Explanatory Power: The model's $\text{R-squared}$ is low ($0.082$), indicating that price changes and the Fukushima event explain only a small fraction ($8.2\%$) of the month-to-month variation in (de-seasoned) public interest. Other unmodeled factors play a larger role.

Significant Autocorrelation: The Durbin-Watson statistic is very low ($0.522$), indicating strong positive autocorrelation in the residuals. This violates a key OLS assumption and suggests the reported standard errors and p-values may be unreliable (likely appearing more significant than they truly are). The model does not fully capture the time-dependent structure remaining in the data.

Proxy Variable: Google Trends data measures search interest, which is a proxy for, but not a direct measure of, public opinion or sentiment.

Omitted Variables: The model does not account for other potential influences like political shifts, media coverage patterns (outside Fukushima), or advancements in renewable energy.

**Next Steps**

To address the autocorrelation, the analysis should be extended using models specifically designed for time-series data with serial correlation, such as ARIMAX (by adding AutoRegressive terms) or Regression with Newey-West standard errors.
