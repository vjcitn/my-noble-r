# World Development Data Structure

This document describes the contents of the RDS file `worlddevrds`, which was inspected in R with `readRDS()`.

## Overview

The object is a `data.frame` with the following dimensions:

- 396,970 rows
- 70 columns
- 265 unique country names
- 1,498 unique indicator names

This is a wide tabular dataset representing country-level development indicators across many years.

## Data model

The object is structured as a long-form-style table with one row per country/indicator combination, and one column per year.

### Column layout

The first four columns identify the observation:

1. `Country Name` — country or region name
2. `Country Code` — standardized ISO-like country code
3. `Indicator Name` — the development metric being measured
4. `Indicator Code` — short code for the indicator

The remaining columns are years from 1960 through 2025:

- `1960`, `1961`, ..., `2025`

These year columns hold numeric values for the indicator for that country and year.

## Example

A small example from the data looks like this:

| Country Name | Country Code | Indicator Name | Indicator Code | 1960 | 2000 | 2023 |
|---|---|---|---|---:|---:|---:|
| Africa Eastern and Southern | AFE | Access to clean fuels and technologies for cooking (% of population) | EG.CFT.ACCS.ZS | NA | 11.49 | 22.54 |
| Africa Eastern and Southern | AFE | Access to clean fuels and technologies for cooking, rural (% of rural population) | EG.CFT.ACCS.RU.ZS | NA | 3.55 | 10.29 |
| Africa Eastern and Southern | AFE | Access to clean fuels and technologies for cooking, urban (% of urban population) | EG.CFT.ACCS.UR.ZS | NA | 32.35 | 41.29 |

This shows that each row corresponds to a single country and a specific indicator, with the annual values stored in separate year columns.

## Structural interpretation

The dataset is effectively a matrix-like panel in which:

- rows are indexed by country + indicator
- columns are indexed by year
- each cell is the numeric value for that country/indicator in that year

In other words, the file is a country-by-indicator time series table.

## Numeric and missing-value pattern

The year-value columns are numeric (`num` in R), and many cells are missing (`NA`), especially for earlier years. For example:

- 1960 through 1999 are mostly empty for many indicators
- values begin to populate more consistently around the year 2000
- the object contains both observed values and missing values, which is typical for development datasets with historical coverage gaps

## Data scale and coverage

The dataset includes:

- 265 countries or reporting entities
- 1,498 distinct indicators
- values spanning 1960 to 2025

Since `265 * 1498 = 396,970`, the row count matches the simple expectation that each country appears once for each indicator.

## Summary

The RDS object is a wide `data.frame` representing a historical development database. It captures many country-level indicators over time, with one row per country-indicator combination and annual values stored as separate columns from 1960 through 2025.

This structure is well suited for tabular analysis in R, reshaping to long format, or selection of specific countries, indicators, and years.
