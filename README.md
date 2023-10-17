# Considering Bias in Data
##### An Exploration of State and Regional Populations, and Wikipedia Article Quality
Aditi Shrivastava
## Description
In this assignment, I explore the concept of bias in data using Wikipedia articles. This exploration considers articles about cities in all US states. The primary data for this exploration is a combination of Wikipedia articles, as well as state populations, and data from a machine learning service called ORES that estimates the quality of the Wikipedia articles.

Via several steps of data acquisition, cleaning, formatting, and manipulation, I perform an analysis of the article coverage of US cities on Wikipedia and how the quality of articles about cities varies among states. The final output of this exploration is a series of tables that show, briefly:
- The states with the greatest and least coverage of cities on Wikipedia compared to their population.
- The states with the highest and lowest proportion of high quality articles about cities.
- A ranking of US geographic regions by articles-per-person and proportion of high quality articles.

These questions are specifically outlined in detail in the .IPYNB file containing all analyses and results.

What follows in this document is an overview of all files contained in this repo, as well as descriptions of data files, sources, and attributes. I conclude this README with a short reflection on the project about my findings from this analysis, as well as the processes required to reach those findings, ultimately helping to understand the causes and consequences of biased data in large, complex data science projects.

## Files 

#### data_acquisition_analysis.ipynb 
This notebook contains step-by-step, completely reproducible code that was used to gather, clean, format, store, and analyze datasets from several different sources. All packages are publicly available and linked, and data sources are documented at each step (as well as below). At the end of the notebook, I explore the following questions and display the inline output tables:

- Top 10 US states by coverage: The 10 US states with the highest total articles per capita (in descending order) .
- Bottom 10 US states by coverage: The 10 US states with the lowest total articles per capita (in ascending order) .
- Top 10 US states by high quality: The 10 US states with the highest high quality articles per capita (in descending order) .
- Bottom 10 US states by high quality: The 10 US states with the lowest high quality articles per capita (in ascending order).
- Census divisions by total coverage: A rank ordered list of US census divisions (in descending order) by total articles per capita.
- Census divisions by high quality coverage: Rank ordered list of US census divisions (in descending order) by high quality articles per capita.

#### input_data
This folder contains all publicly sourced input data. This data is all pre-manipulation, straight from the source. This data is combined in *data_acquisition_analysis.ipynb* to create the cleaned data in the folder processed_data.
###### NST-EST2022-POP.xlsx
- The [US Census Bureau](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html) provides updated population estimates for every US state. This site contains data from State Population Totals and Components of Change: 2020-2022 from their website. The [excel file](https://www2.census.gov/programs-surveys/popest/tables/2020-2022/state/totals/NST-EST2022-POP.xlsx) linked on the page contains estimated populations of all US states for 2022. 

- Geographic area: The state or region 
- April 1 2020 Estimates Base: The base estimate used in the April 2020 census
- 2020: The 2020 population estimate as of July 1
- 2021: The 2021 population estimate as of July 1
- 2022: The 2022 population estimate as of July 1

###### US States by Region - US Census Bureau.xlsx
- The regional and divisional agglomerations as defined by the US Census Bureau

- REGION: The US Region
- DIVISION: The US Regional Division
- STATE: The US state

###### us_cities_by_state_SEPT.2023.csv
- The [Wikipedia Category:Lists of cities](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state) in the United States by state was crawled to generate a list of Wikipedia article pages about US cities from each state.

- state: The US state
- page_title: The article title for the city as it appears on Wikipedia
- url: The direct URL to the Wikipedia page

#### processed_data
This folder contains data that was produced after scraping article [ORES scores](https://www.mediawiki.org/wiki/ORES) from the Wikimedia [API](https://www.mediawiki.org/wiki/API:Info). Other data in this folder is a cleaned aggregation of the data from the folder input_data. 

###### state_populations.csv
- This .csv file is a cleaned aggregation of file *NST-EST2022-POP.xlsx* from folder input_data.

- state: The US state
- population: The state population

###### revision_ids.csv
- This file builds upon the data in file *us_cities_by_state_SEPT.2023.csv* from folder input_data by using the Wikimedia API to make a page info request and get the current article page Revision ID (revision_id). These revision IDs are needed to later gather the articles' ORES scores. All data scraping procedure is thoroughly outlined in file  *data_acquisition_analysis.ipynb*.

- article_title: The title of the city article as it appears on Wikipedia
- state: The US state
- revision_id: The unique Wikipedia Revision ID #

###### article_scores.csv
- This data file is produced by using the revision_ids scraped in file *revision_ids.csv* and the Wikimedia API to gather the associated article ORES scores. All data scraping procedure is thoroughly outlined in file  *data_acquisition_analysis.ipynb*.

- revision_id: The article Revision ID
- article_quality: The ORES score as defined by [Wikipedia content assessment](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- FA- Featured article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- GA - Good article (sometimes called A-class)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- B - B-class article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- C - C-class article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Start - Start-class article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Stub - Stub-class article

###### regional_divisions.csv
- This data is the cleaned aggregation of data contained in file *US States by Region - US Census Bureau.xlsx* from folder input_data.

- regional_division: The US regional division
- state: The US state


###### wp_scored_city_articles_by_state.csv
- This is the final aggregation of the four previous data files. This file serves as the basis for the analysis. The process of merging these data is thoroughly outlined in file *data_acquisition_analysis.ipynb*.

- regional_division: The US regional division
- state: The US state
- article_title: The title of the city article as it appears on Wikipedia
- population: The 2022 state population estimate 
- revision_id: The unique Wikipedia article revision ID
- article_quality: The quality of the article as scored by ORES

#### resources
This folder contains resources provided to me in the DATA 512 class at the University of Washington.
###### wp_ores_liftwing_example.ipynb
- This notebook illustrates how to generate article quality estimates for article revisions using the LiftWing version of [ORES](https://www.mediawiki.org/wiki/ORES). The [ORES API documentation](https://ores.wikimedia.org) can be accessed from the main ORES page. 

###### wp_page_info_example.ipynb
- This example illustrates how to access page info data using the [MediaWiki REST API for the EN Wikipedia](https://www.mediawiki.org/wiki/API:Main_page). This example shows how to request summary 'page info' for a single article page. The API documentation, [API:Info](https://www.mediawiki.org/wiki/API:Info), covers additional details that may be helpful when trying to use or understand this example.

## Research Implications
Via this data exploration, I learned more about not only the process of reviewing and ranking Wikipedia article quality, but also about the ORES service itself, as well as of course the article coverage of several states in the U.S. region. 

In terms of the ORES modle, I was a bit underwhelmed by its efficacy. While I certainly find it difficult as a human reader to predict the score of an article, I was still surprised to see that the model almost consistently overpredicts the score of an article. And upon a quick exploration of other (non-state related) articles, I found that the predicted article subject (or "department") tended to be quite inaccurate. I believe that this finding speaks not only to the quality of the model, but also, and more importantly, the fact that the inherent process used to score and classify Wikipedia article in the first place may be in need of a more rigid standard (especially considering that article scores are so frequently revised). 

As per the findings of my article coverage exploration, I found that the states with the highest article coverage tended to be the smaller states (Vermont, ND, etc). I was also surprised to find that article coverage in general seems to be correlated with high quality article coverage-- that is, the states that have the most Wikipedia articles per capita are also the very states that produce the most high quality article per capita. Furthermore, I found there to be a stark disparity in the the number of articles for a state versus that state's population. For example, Vermont has a population of 647,064 with 328 article, while North Carolina has a population of 10,698,973 with only 50 articles. 

###### What biases did you expect to find in the data (before you started working with it), and why?
I expected smaller, less populous states to have much lower quality Wikipedia articles, since they likely have less visibility on the internet in general. Also, I was curious about the overall quality of all articles on Wikipedia-- if the majority of Wikipedia articles are all quite high quality (or at least above average), for example, then this leads to a highly imbalanced dataset that the ORES model would be trained on. I wonder what was done (if needed), to alleviate this.

###### What (potential) sources of bias did you discover in the course of your data processing and analysis?
The most standout source of bias was the fact that the data is incomplete-- two states, Connecticut and Nebraska, are missing from Wikipedia set of state cities. This introduces a large bias into our investigation of US states/city articles, given that our very representation of the US is missing two states. I wonder whether any of the top10/bottom10 tables produced in the data exploration would be altered had Connecticut or Nebraska been rightly included. Furthermore, it's hard to know which states the ORES model underperformed or overperformed on, especially coupled with the fact that the overall predicted score had a probability extremely similar to the second highest predicted score, in many cases. 

###### How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
One question I have is regarding the geographical size of these states-- I'd assume that the physical size (and number of cities) in a state would play a *much* larger role in the article coverage than simply population does. In fact, I have doubts that population would play much of a role at all in the number of Wikipedia city articles in a state (unless we assume that the state inhabitants themselves are the only ones writing their cities' articles, which is unlikely. So essentially, if we are making assumptions about which states have the highest and lowest article coverage, I think it would be wise for future researchers to look into other factors, such as square mileage. 
