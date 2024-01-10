# case_law_trends

Applies a linear autoregression model to predict trends concerning the development of case-law by the Court of Justice of the European Union (CJEU). 

The focus here are preliminary reference judgments (Article 267 TFEU) between 2010 and 2023. The model tracks the volume of judgments across nine different areas, as using the classification scheme in the CJEU's case-law directory (1). The data comprise 112 data points.

The data are split into training (2010-2020) and test (2021-2023) sets, in order to validate model predictions against the case-law development in recent years. The model estimates up to five lags in order to predict the volume of preliminary rulings in the following year:

```math

y_{it} = \beta_0 + \beta_1 y_{it-1} + \beta_2 y_{it-2} + \beta_3 y_{it-3} + \beta_4 y_{it-4} + \beta_5 y_{it-5} + \beta_6 x_{i} + \epsilon_{it}

```

where $y_{it}$ denotes the number of judgments in area $i$ and year $t$, $x_{i}$ refers to a vector of area fixed effects, the $\beta$s represent the model parameters to be estimated, and $epsilon_{it}$ denotes the error term.

Source:
(1) https://eur-lex.europa.eu/browse/directories/new-case-law.html