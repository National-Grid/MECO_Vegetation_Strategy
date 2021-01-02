# MECO_Vegetation_Strategy

1.	Calculates SAIDI and SAIFI forecasts for multiple vegetation management budgeting scenarios.

## Main Contributors from ADA Data Science
* Goldberg, Andrew ([Andrew.Goldberg@nationalgrid.com](mailto:Andrew.Goldberg@nationalgrid.com))
* Bryant, Kathryn

## Project finished with resulting forecasts delivered to MECO Vegetation Management group

## Main Contact from business units
* Moe, Ryan ([Ryan.Moe@nationalgrid.com](mailto:Ryan.Moe@nationalgrid.com)) 

## Requirements
* Main packages: python 3.6, jupyter, statsmodels, cx_Oracle
* DB access: IDS (read)
* OS: code developed and tested on Windows 7 machines
* Memory: recommend 8 GB or above

## Model Specifications:
1.	Calculates SAIDI and SAIFI forecasts for multiple budgeting scenarios:
  a.	Assumes a budget of $10.1M in 2021, adding 5% each year, and calculates miles pruned considering:
    i.	Tree Trimming Labor Costs
    ii.	2021 – 2024 Tree Trimming Schedule
2.	Moving Parts:
  a.	Feeders are deferred due to budgetary limitations
  b.	Deferred feeders require higher labor costs to trim
3.	Forecasting Methodology for CI/CMI, sum of:
  a.	Forecasted tree-related ci/cmi for scheduled feeders
  b.	Forecasted tree-related ci/cmi for unscheduled feeders
  c.	Median outage predictions due to diseased or infested trees, converted to ci/cmi
  d.	Historical average of non-tree related ci/cmi

Data Specifications:
1.	MA - Cycle Prune - FY 2008-2018.xlsx
  Initial spreadsheet that Ryan Moe sent to the team, for analysis. He retrieved this dataset from the internal National Grid IDS user interface (http://infonetus/operations_asset_strat/Data/adhoc-statadhoc/)
2.	Cycle Prune datasets:
  The “cycle prune” files are data sets processed from Ryan Moe’s original excel sheets (1). They have event history from before the pruning year (Year 3 Before – Year 1 Before), during (Year 1 After) and after (Year 2 After – Year 4 After). 
  Because there are cases when there were less than 5 years between prunes (the typical National Grid cycle is 5 years), there are additional columns that say how many ‘years since’ the last pruning of that feeder, and how many ‘years until’ the next recorded pruning. The fiscal year is included in its own column, allowing calculations for the actual fiscal year of last pruning and next prune. 
  Files are split by event metric, including count of outages (‘events’), customers interrupted (‘ci’), and customer minutes interrupted (‘cmi’). 
3.	Feeder_Metrics.csv: 
Descriptive columns for each feeder, retrieved from the IDS SQL database

4.	MECO_custs_svd_sent.csv
Counts of customers served per year for each feeder, retrieved from internal SQL database

5.	Outages_ma_cdf.csv
Full history of every MECO outage with the related feeder
