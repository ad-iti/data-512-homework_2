## input_data
This folder contains all publicly sourced input data. This data is all pre-manipulation, straight from the source. This data is combined in *data_acquisition_analysis.ipynb* to create the cleaned data in the folder processed_data.
###### NST-EST2022-POP.xlsx
- The [US Census Bureau](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html) provides updated population estimates for every US state. This site contains data from State Population Totals and Components of Change: 2020-2022 from their website. The [excel file](https://www2.census.gov/programs-surveys/popest/tables/2020-2022/state/totals/NST-EST2022-POP.xlsx) linked on the page contains estimated populations of all US states for 2022. 

- Attributes
Geographic area: The state or region 
April 1 2020 Estimates Base: The base estimate used in the April 2020 census
2020: The 2020 population estimate as of July 1
2021: The 2021 population estimate as of July 1
2022: The 2022 population estimate as of July 1

###### US States by Region - US Census Bureau.xlsx
- The regional and divisional agglomerations as defined by the US Census Bureau

- Attributes
REGION: The US Region
DIVISION: The US Regional Division
STATE: The US state

###### us_cities_by_state_SEPT.2023.csv
- The [Wikipedia Category:Lists of cities](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state) in the United States by state was crawled to generate a list of Wikipedia article pages about US cities from each state.

- Attributes
state: The US state
page_title: The article title for the city as it appears on Wikipedia
url: The direct URL to the Wikipedia page
