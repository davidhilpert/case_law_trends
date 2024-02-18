# Trends in CJEU case load

Applies a linear autoregression model to predict trends concerning the development of case-law by the Court of Justice of the European Union (CJEU). 

The focus is on preliminary reference judgments (Article 267 TFEU) between 2010 and 2023. The model tracks the volume of judgments across nine different areas, as using the classification scheme in the CJEU's case-law directory (1). The data comprise 112 data points. The data are split into training (2010-2020) and test (2021-2023) sets, in order to validate model predictions against the case-law development in recent years. 

In line with the time-series cross-sectional structure of the data, with repeated observations of the same areas, I opted for a simple linear regression framework rather than an ARIMA-based model (2). The model estimates up to five lags in order to predict the volume of preliminary rulings in the following year. In this way, it is possible to remain agnostic concerning the effect of the (relatively) distant past on future developments, letting the data speak for itself. Furthermore, a linear regression framework allows for the inclusion of exogenous variables, such as the number of legal acts adopted in the previous years which might be an important predictor of legal disputes. To obtain this data, I use Michal Ovadek's R-Package `eurlex` (3). I let the model estimate five lags in order to stay agnostic about the effect of the past on the volume of judgments.

The model can be represented mathematically as follows:  

```math

y_{it} = \beta_0 + \beta_1 y_{it-1} + \beta_2 y_{it-2} + \beta_3 y_{it-3} + \beta_4 y_{it-4} + \beta_5 y_{it-5} + \beta_6 z_{t} + \beta_7 z_{t-1} + \beta_8 z_{t-2} + \beta_9 z_{t-3} + \beta_{10} z_{t-4} + \beta_{11} z_{t-5} + \beta_{12i} x_{i} + \epsilon_{it}

```

where $y_{it}$ denotes the number of judgments in area $i$ and year $t$, $z_{it}$ denotes the number of legal acts adopted in year $t$, $x_{i}$ refers to a vector of area fixed effects, the $\beta$ coefficients represent the model parameters to be estimated, and $\epsilon_{it}$ denotes the error term.

Sources:

(1) https://eur-lex.europa.eu/browse/directories/new-case-law.html

(2) Box GEP, Jenkins GM (1970). Time series analysis, forecasting, and control. Holden-Day, Oakland

(3) Ovádek, Michal (2021). "Facilitating access to data on European Union laws." Political Research Exchange 3.1: 1870150.
