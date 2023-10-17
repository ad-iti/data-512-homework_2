## processed_data
This folder contains data that was produced after scraping article [ORES scores](https://www.mediawiki.org/wiki/ORES) from the Wikimedia [API](https://www.mediawiki.org/wiki/API:Info). Other data in this folder is a cleaned aggregation of the data from the folder input_data. 

###### state_populations.csv
- This .csv file is a cleaned aggregation of file *NST-EST2022-POP.xlsx* from folder input_data.

- Attributes
state: The US state
population: The state population

###### revision_ids.csv
- This file builds upon the data in file *us_cities_by_state_SEPT.2023.csv* from folder input_data by using the Wikimedia API to make a page info request and get the current article page Revision ID (revision_id). These revision IDs are needed to later gather the articles' ORES scores. All data scraping procedure is thoroughly outlined in file  *data_acquisition_analysis.ipynb*.

- Attributes
article_title: The title of the city article as it appears on Wikipedia
state: The US state
revision_id: The unique Wikipedia Revision ID #

###### article_scores.csv
- This data file is produced by using the revision_ids scraped in file *revision_ids.csv* and the Wikimedia API to gather the associated article ORES scores. All data scraping procedure is thoroughly outlined in file  *data_acquisition_analysis.ipynb*.

- Attributes
revision_id: The article Revision ID
article_quality: The ORES score as defined by [Wikipedia content assessment](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- FA- Featured article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- GA - Good article (sometimes called A-class)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- B - B-class article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- C - C-class article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Start - Start-class article
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Stub - Stub-class article

###### regional_divisions.csv
- This data is the cleaned aggregation of data contained in file *US States by Region - US Census Bureau.xlsx* from folder input_data.

- Attributes:
regional_division: The US regional division
state: The US state


###### wp_scored_city_articles_by_state.csv
- This is the final aggregation of the four previous data files. This file serves as the basis for the analysis. The process of merging these data is thoroughly outlined in file *data_acquisition_analysis.ipynb*.

- Attributes:
regional_division: The US regional division
state: The US state
article_title: The title of the city article as it appears on Wikipedia
population: The 2022 state population estimate 
revision_id: The unique Wikipedia article revision ID
article_quality: The quality of the article as scored by ORES