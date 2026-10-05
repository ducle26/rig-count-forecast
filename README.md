# How far ahead can the rig count be forecast?

A case study for BZAN 6351 (University of Houston, Fall 2026), by Duc (Bill) Le.

Work in downhole tools can arrive with little notice, while the longest parts take months to come in. This project tests how far ahead the US rig count can be forecast well enough for a buyer to act on.

The full write-up, with a tool that replays every forecast, is on my portfolio:
https://ducle26.github.io/bill-portfolio/projects/rig-count.html

## What I found

- The rig count has no season, but it has strong momentum: a rising count tends to keep rising.
- ARIMA and ETS models beat "assume no change" for about a quarter. Out to three months, their typical miss is about a third smaller.
- By six months most of that edge is gone, and past eight months the models do no better than assuming no change.
- Both models missed the big turns in late 2014 and early 2020.
- So the forecast works as a monthly check on which way activity is heading. It is not a way to decide how much to buy.

## How it was tested

Each method was replayed over sixteen years. For every month from December 2009 on, the model saw only the data known that month, forecast the next twelve months, and was scored against what happened. That is 200 forecasts per method.

## Files

| File | What it is |
|---|---|
| `rig_count_forecast.Rmd` | The R Markdown file: data, checks, models, the sixteen-year replay, and the forecast |
| `data/NG_ENR_DRILL_S1_M.xls` | Monthly US rotary rig count, January 1973 to August 2026, as downloaded from EIA |

## Run it

1. Download this folder and open `rig_count_forecast.Rmd` in RStudio. Keep the `data` folder beside it.
2. Install the packages once:

   ```r
   install.packages(c("dplyr", "tidyr", "ggplot2", "scales", "readxl", "forecast", "knitr"))
   ```

3. Press Knit. The replay refits the models 200 times, so it takes a minute or two.

To update the data, download the latest file from EIA and replace the one in `data`:
https://www.eia.gov/dnav/ng/xls/NG_ENR_DRILL_S1_M.xls

## Data and method

Data: U.S. Energy Information Administration, *Crude Oil and Natural Gas Drilling Activity*, rotary rigs in operation, sourced from Baker Hughes. https://www.eia.gov/dnav/ng/ng_enr_drill_s1_m.htm

Method: Hyndman, R. J., & Athanasopoulos, G. (2018). *Forecasting: Principles and Practice* (2nd ed.). https://otexts.com/fpp2/
