# Real-Time-Macroeconomic-Signals-for-Dynamic-Asset-Allocation

This project develops a systematic asset allocation strategy that uses high-frequency macroeconomic data to estimate the current state of the economy in real time. Instead of relying on delayed GDP releases, the model combines multiple macroeconomic indicators into a single latent factor using Principal Component Analysis (PCA). That factor is then used to dynamically adjust portfolio allocations between U.S. equities and long-term Treasury bonds.

The project explores whether real-time macro signals can improve portfolio performance by responding to changes in economic momentum before they are reflected in traditional economic statistics.

# Research Question

Can high-frequency macroeconomic indicators be combined into a real-time economic signal that improves dynamic asset allocation compared to a traditional static portfolio?

# Methodology

### Data Collection
Monthly macroeconomic data (1995–2025) is sourced from the Federal Reserve Economic Data (FRED) database, including indicators representing:
- Industrial production
- Employment
- Unemployment
- Retail sales
- Housing activity
- Interest rates and financial conditions

To make the variables comparable:
- Real activity measures are converted to year-over-year growth rates.
- Unemployment is transformed into a 12-month change.
- All variables are standardized using Z-scores prior to analysis.

### Feature Engineering

Because macroeconomic indicators are released on different schedules, the model approximates the information available to investors in real time by:
- Updating the macro factor monthly.
- Using the latest available observation for each indicator.
- Carrying forward the previous observation when newer data has not yet been released.
This creates a realistic real-time information set rather than relying on revised historical data.

### Macro Factor Construction
Principal Component Analysis (PCA) is used to extract the common variation across standardized macroeconomic indicators.
The first principal component serves as the macroeconomic factor because it captures the largest share of shared economic variation (approximately 60%). Higher values represent economic expansion, while lower values indicate economic slowdown.

### Validation
To evaluate whether the extracted factor captures meaningful economic information:
- Monthly factor values are aggregated to quarterly frequency.
- The resulting series is compared with year-over-year GDP growth.
The analysis finds a strong relationship between the macro factor and GDP growth, suggesting the factor effectively tracks changes in business cycle momentum.

# Investment Strategy
The macro factor is used to dynamically allocate capital between:
- SPY (U.S. Equities)
- TLT (Long-Term U.S. Treasury Bonds)
  
Allocation weights are determined using a smooth nonlinear function of the macro factor:
- Strong macro conditions increase equity exposure.
- Weak macro conditions shift the portfolio toward Treasury bonds.
- Monthly portfolio rebalancing is performed throughout the 2002–2025 backtest period.

# Results
The dynamic allocation strategy generated higher cumulative returns than a traditional 60/40 portfolio. However, these higher returns were accompanied by:
- Greater annual volatility
- Larger maximum drawdowns
- Lower risk-adjusted performance (Sharpe Ratio)
  
# Key Takeaways
- High-frequency macroeconomic indicators can be combined into a meaningful real-time measure of economic activity.
- PCA provides an effective dimensionality reduction technique for constructing a macroeconomic factor.
- Dynamic asset allocation based on macro signals can outperform a static allocation in terms of raw returns.
- Macro signals alone may not fully compensate investors for the additional portfolio risk they introduce.

# Future Improvements

Potential extensions include:
- Incorporating credit spreads and financial conditions indices.
- Combining macro signals with momentum, valuation, or trend-following factors.
- Extending the framework to additional asset classes such as commodities, currencies, and credit.
- Applying machine learning techniques for nonlinear factor extraction and regime detection.
