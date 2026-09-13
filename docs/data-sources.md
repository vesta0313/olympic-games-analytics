# Data Sources and Methodology

This project combines three data inputs. The original datasets are not
redistributed in this repository.

## 1. Olympic Athletes and Global Inequality

**Project file:**  
`Olympic_Athletes_&_Global_Inequality_(1896-2024).xlsx`

This integrated workbook contains historical Olympic athlete-event records
together with country-level economic and demographic indicators.

Fields used in the analysis include:

- Athlete and team identifiers
- Olympic year and season
- Sport and event
- Medal and finishing position
- Gender and age
- Country and nationality information
- GDP per capita at purchasing-power parity
- Total GDP
- Population
- Gini coefficient

The Olympic records draw on historical information associated with
[Olympedia](https://www.olympedia.org/). The socioeconomic indicators are
associated with sources including [Gapminder](https://www.gapminder.org/data/)
and the [World Bank](https://data.worldbank.org/).

The repository does not include this workbook. The readable Qlik script shows
how its fields were cleaned, validated and transformed.

## 2. Olympic Host Data

**Project file:**  
`olympic_hosts.csv`

The host dataset was published by Petro Ivaniuk on Kaggle and contains Olympic
year, season, host country, host city and source URL information. Its original
information was collected from the official Olympics website.

The data required additional handling for historical cases, including the 1956
Summer Games, whose equestrian events were held separately in Stockholm.

The repository does not redistribute the CSV file.

## 3. World Bank Historical Income Classifications

**Project file:**  
`OGHIST_2026_07_15.xlsx`

Historical income classifications were obtained from the World Bank’s country
and lending-group resources:

[World Bank Country and Lending Groups](https://datahelpdesk.worldbank.org/knowledgebase/articles/906519-world-bank-country-and-lending-groups)

The source classifies economies as:

- Low income
- Lower-middle income
- Upper-middle income
- High income

The source years were transformed into Olympic years before being joined to the
country-year dimension. Country-name mappings were used where the World Bank
and Olympic datasets applied different historical or modern names.

## Data Modelling Approach

The data was transformed into a star schema consisting of:

- `FactParticipation`
- `DimAthlete`
- `DimGames`
- `DimEvent`
- `DimCountryYear`

Economic information was stored once per country and Olympic year instead of
being repeated across every athlete-event record.

Additional fields were created for:

- Data availability
- Conflicting socioeconomic values
- Historical country-name reconciliation
- World Bank income-group ordering
- GDP-per-capita quartiles within each Olympic year
- Host-country identification
- Medal-record indicators
- Age-quality validation

## Important Interpretation Notes

A row in the fact table represents an athlete participating in an event.
Consequently, team medals may appear once for each athlete recorded as part of
the team. Dashboard labels use “medal-winning records” where this distinction
is important.

Historical countries and teams are retained according to the source data.
Current geographic boundaries used in maps may therefore differ from the
historical entities represented in the records.