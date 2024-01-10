# case_law_trends

Applies a linear autoregression model to predict trends concerning the development of case-law by the Court of Justice of the European Union (CJEU). 

The focus here are preliminary reference judgments (Article 267 TFEU) between 2010 and 2023. The model tracks the volume of judgments across nine different areas, as using the classification scheme in the CJEU's case-law directory (1). The data comprise 112 data points.

The data are split into training (2010-2020) and test (2021-2023) sets, in order to validate model predictions against the case-law development in recent years. The model estimates up to five lags in order to predict the volume of preliminary rulings in the following year:

```math

y_i = \beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \ldots + \beta_k x_{ik} + \alpha_1 t_i + \alpha_2 t_i^2 + \ldots + \alpha_p t_i^p + \epsilon_i

```

Source:
(1) https://eur-lex.europa.eu/browse/directories/new-case-law.html