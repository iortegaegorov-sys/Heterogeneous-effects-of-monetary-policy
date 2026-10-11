# Monetary policy in wartime Russia

Code and prepared data for *Heterogeneous effects of monetary policy in wartime Russia*.

Set the working directory to this folder. Install the packages once:

```r
install.packages(c("dplyr", "readxl", "fixest", "purrr", "broom",
                   "stringr", "ggplot2", "car", "rmarkdown", "knitr"))
```

Run everything with:

```r
source("run.R")
```

Alternatively, knit `Regressions.Rmd` in RStudio. All graphs are written to `graphs/`; heterogeneity tests and session information are written to `results/`.

The code produces 61 named PNG graphs, covering all four aggregate outcomes, both panel outcomes, the preliminary regressions and additional plot variants. Knitting also produces the figures used in the HTML report, with the prefix `knit-`.

Bands are pointwise 90% confidence intervals. Aggregate models use ordinary OLS standard errors; panel models cluster standard errors by month. Shocks are measured in percentage points. The main graphs show cumulative percentage responses to a one percentage point shock; the standardised graphs use a 25 basis point shock and divide responses by the standard deviation of monthly outcome growth.

The aggregate data contain 130 months, January 2015–October 2025. The panel contains 3,922 sector-month observations, January 2017–October 2025. Actual estimation samples vary with missing values, lags, outcome and horizon. Missing observations are retained in the input files and excluded by the estimators where required.

The spreadsheets contain only the inputs needed by this code. Lags, interactions, aggregate PPI growth and stock-market growth are calculated during the run. Macro controls are lagged before joining them to the panel; sector-specific variables and shock interactions are lagged within sectors.

These are prepared research datasets. The original source descriptions are in the article; this folder does not reconstruct the data from the providers' raw releases.

## Model descriptions

The sections below follow the order and numbering in `Regressions.Rmd`. Local projections estimate cumulative responses at horizons 0–24 months. The main shock measure is the change in the three-month ROISfix rate (`roisfix_3M_chg`). The main panel models use sectoral producer prices (PPI) and industrial production (IPI) as dependent variables, with two lags of the shock and controls. Panel models include sector and calendar-month fixed effects; specifications allowing for the war use separate sector fixed effects for each period. The war period starts in March 2022.

- **Preliminary shock checks:** examine the association between a candidate shock measure, future aggregate consumer prices and firms' inflation expectations.
- **1) Preliminary aggregate regressions:** estimate consumer-price responses using the policy rate and the alternative ROISfix measures supplied in the dataset. These provide an initial comparison of the explanatory variables.
- **2.1) One-stage aggregate regressions:** estimate responses of CPI, aggregate PPI, aggregate IPI and the rouble–dollar exchange rate to the main shock measure, controlling for macroeconomic conditions and inflation expectations.
- **2.2) Aggregate regressions before and after the war:** allow the response to the monetary shock to differ before March 2022 and from March 2022 onward, for each of the four aggregate outcomes.
- **3) Simple panel LPs (Regression 0):** interact the monetary shock with sector indicators to estimate sector-specific PPI and IPI responses. The section produces the alternative sector plots, responses standardised for visual comparison, and Wald tests of whether sector responses are equal.
- **4.1) Broad sectors (Regression 1):** replace the individual-sector shock interactions with durable goods, non-durable goods, raw materials and utilities groups. This checks whether these broad classifications explain response heterogeneity. The section also compares durable goods and raw materials with non-durable goods at the 24-month horizon.
- **4.2) War dummy (Regression 2):** allow each sector's response to differ before and after the start of the war, to examine whether the war changed sectoral monetary transmission.
- **4.3) Broad sectors and war dummy (Regression 3; demand channel):** estimate separate pre-war and wartime responses for the four broad sector groups, checking whether the pattern follows their demand characteristics.
- **4.4) Wages (Regression 4; labour market check):** add lagged sector-specific wage growth and its interaction with the war period to the sector-level specification. This examines whether wages help account for response heterogeneity and the price puzzle after the start of the war.
- **4.5) Sanctions exposure (Regression 5; sanctions check):** interact the shock with sanctions-exposure categories separately before and after the war. The implemented model uses the categorical sanctions measure and retains the original exclusions of sectors 16 and 29.
- **4.6) War-related industries (Regression 6; military demand check):** use the war-related classification from Simola (2023) as the moderating variable, with separate responses before and after the war. The original exclusion of sector 29 is retained.
- **4.7) Government ownership (Regression 7; military demand check):** compare monetary-policy responses in sectors with high and low revenue shares of state-owned firms, using a 15% threshold and separate responses before and after the war.



The corrected transformations and lags change some estimates. The existing figures embedded in the Word article have not been replaced; use the new graphs when revising the paper. The article's aggregate error notes, expectations specification and figure notes have been corrected.
