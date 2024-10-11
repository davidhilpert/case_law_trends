# Trends in CJEU case load

Applies a linear autoregression model to predict trends concerning the development of case-law by the Court of Justice of the European Union (CJEU). 

The focus is on preliminary reference judgments (Article 267 TFEU) between 2010 and 2023. The model tracks the volume of judgments across nine different areas, as using the classification scheme in the CJEU's case-law directory (1). The data comprise 112 data points. The data are split into training (2010-2020) and test (2021-2023) sets, in order to validate model predictions against the case-law development in recent years. 

In line with the time-series cross-sectional structure of the data, with repeated observations of the same areas, I opted for a simple linear regression framework rather than an ARIMA-based model (2). The model estimates up to five lags in order to predict the volume of preliminary rulings in the following year. In this way, it is possible to remain agnostic concerning the effect of the (relatively) distant past on future developments, letting the data speak for itself. Furthermore, a linear regression framework allows for the inclusion of exogenous variables, such as the number of legal acts adopted in the previous years which might be an important predictor of legal disputes. To obtain this data, I use Michal Ovadek's R-Package `eurlex` (3). I let the model estimate five lags in order to stay agnostic about the effect of the past on the volume of judgments.

The model can be represented mathematically as follows:  

```math

\mathbf{y}_t = \beta_0 + \mathbf{Y}_{t-1:t-5} \mathbf{\beta_{1:5}} + \mathbf{Z}_{t-1:t-5} \mathbf{\beta_{6:10}} + \mathbf{X} \mathbf{\beta_{12}} + \boldsymbol{\epsilon}_t

```

Where:
$\mathbf{y}_t$

- $\mathbf{y}_t$ is a vector of response variables for all entities at time \(t\).
- $\mathbf{Y}$ is a matrix of lagged values $y_{it-1}, y_{it-2}, \dots, y_{it-5}$.
- $\mathbf{Z}$ is a matrix of lagged external variables $z_{t-1}, z_{t-2}, \dots, z_{t-5}$.
- $\mathbf{X}$ is a matrix of entity-specific features \(x_i\).
- $\mathbf{\beta_{1:5}}, \mathbf{\beta_{6:10}}, \mathbf{\beta_{12}}$ are vectors of corresponding coefficients.
- $\boldsymbol{\epsilon}_t$ is the error term vector.

Sources:

(1) https://eur-lex.europa.eu/browse/directories/new-case-law.html

(2) Box GEP, Jenkins GM (1970). Time series analysis, forecasting, and control. Holden-Day, Oakland

(3) Ovádek, Michal (2021). "Facilitating access to data on European Union laws." Political Research Exchange 3.1: 1870150.
