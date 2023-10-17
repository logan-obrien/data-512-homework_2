# data-512-homework_2
## Project Info:
### Project Goal:
The goal of this project was to analyze the number and quality of Wikipedia
articles written on cities throughout the U.S., analyze the state and regional
division per capita ranking of those articles, and consider whether or not there
is any suspected biases in the data.

### Source Data:
- **us_cities_by_state_SEPT.2023.csv**: This file was provided by the professor
and I was told it was scrapped from https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state to generate the list of
Wikipedia articles contained in the csv. I am not completely sure what license
the data falls under, but on the webpage linked it says that the text is
"available under the Creative Commons Attribution-ShareAlike License 4.0;
additional terms may apply." License: https://en.wikipedia.org/wiki/Wikipedia:Text_of_the_Creative_Commons_Attribution-ShareAlike_4.0_International_License.
So this is the license I believe it falls under. 
- **NST-EST2022-POP.xlsx**: This file contains the US Census Bureau's population
estimates for the United States states. It was acquired here: https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html. I searched all over, but was unable to find
any information on the website about what license agreement is applicable for
using this data. Normally, I would try to not use data before confirming its
license supports the use I intend, however, since this was a homework project,
I assume it is okay to use.

Citation: "Annual Estimates of the Resident Population for the United States,
Regions, States, District of Columbia, and Puerto Rico: April 1, 2020 to July 1,
2022 (NST-EST2022-POP). Source: U.S. Census Bureau, Population Division.
Release Date: December 2022. "
- **'US States by Region - US Census Bureau.xlsx'**: This file was provided
with the assignment materials for me to use. It contains regional geographic
divisions of the U.S. Once again, no license info was provided to me for this
data, but I am assuming I can use it since it was provided to me.

- **Wikipedia Article Revision IDs Data**: I utilized the MediaWiki API:Info
request to retrieve the article IDs. Link to documentation: https://www.mediawiki.org/wiki/API:Info.
I was unable to track down the terms of use and license agreement for the data
retrieved by this API. I am assuming it is permissable to use and will seek
clarification from the professor on how to locate the missing information.

- **ORES Article Prediction Scores**: I used the LiftWing (https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing) version of the ORES API to request Wikipedia article
predictions. I looked through several webpages of documentation but was unable
to find the license info. As before, I am assuming it is permissible to use
since I was told to use this tool for this class.

### API Documentation:
-API:Info: 
    - https://www.mediawiki.org/wiki/API:Main_page
    - https://www.mediawiki.org/wiki/API:Info
- ORES:
    - https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing
    - https://www.mediawiki.org/wiki/ORES
    - https://ores.wikimedia.org/
    - https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage

### Data Files:
**Intermediary Data Files:**
- **Article_data_with_Revision_Ids.csv**: This file contains four fields
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'url': the weblink for the article
- **Error_Log1.csv:** This file contains the error log data for the first
batch of articles whose scores were retrieved from ORES. It contains two fields:
    - 'Article_ID': the ID of the article that ORES failed to get a score for
    - 'Error': if provided, the error message associated with the request
    failure. There were 4 occurrences of an unexpected issue with this column,
    described under 'Source Code Notes' below.
- **Error_Log2.csv:** This file contains the error log data for the second
batch of articles whose scores were retrived from ORES. It contains two fields:
    - 'Article_ID': the ID of the article that ORES failed to get a score for
    - 'Error': if provided, the error message associated with the request
    failure. There were 4 occurrences of an unexpected issue with this column,
    described under 'Source Code Notes' below.
- **df_data1.csv:** This file contains the data from
the 'Article_data_with_Revision_Ids.csv' with the addition of a new column
containing the predicted article quality score for the first batch of articles.
It contains five fields:
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'article_quality': the ORES predict quality score for the article. Note,
    the value of this field is 'NaN' when the API request fails to retrieve
    a score.
    - 'url': the weblink for the article
- **df_data2.csv:** This file contains the data from
the 'Article_data_with_Revision_Ids.csv' with the addition of a new column
containing the predicted article quality score for the second batch of articles.
It contains five fields:
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'article_quality': the ORES predict quality score for the article. Note,
    the value of this field is 'NaN' when the API request fails to retrieve
    a score.
    - 'url': the weblink for the article
- **df_data_total.csv:** This file contains the result of merging the
'df_data1.csv' and 'df_data2.csv' files and contains the same five fields:
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'article_quality': the ORES predict quality score for the article. Note,
    the value of this field is 'NaN' when the API request fails to retrieve
    a score.
    - 'url': the weblink for the article
- **Article_data_with_RevIDs_Scores1.csv:** This file is the exact same as
'df_data1.csv' except it has had the 'NaN' values in the 'article_quality'
column filtered out. It contains the data from the
'Article_data_with_Revision_Ids.csv' with the addition of a new column
containing the predicted article quality score for the first batch of articles.
It contains five fields:
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'article_quality': the ORES predict quality score for the article
    - 'url': the weblink for the article
- **Article_data_with_RevIDs_Scores2.csv:** This file is the exact same as
'df_data2.csv' except it has had the 'NaN' values in the 'article_quality'
column filtered out. It contains the data from
the 'Article_data_with_Revision_Ids.csv' with the addition of a new column
containing the predicted article quality score for the second batch of articles.
It contains five fields:
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'article_quality': the ORES predict quality score for the article
    - 'url': the weblink for the article
- **Article_data_with_RevIDs_Scores_Full_Valid.csv:** This file is the exact
same as 'df_data_total.csv' except it has had the 'NaN' values in the
'article_quality' column filtered out. This file contains the result of merging
the 'Article_data_with_RevIDs_Scores1.csv' and
'Article_data_with_RevIDs_Scores2.csv' files and contains the same five fields:
    - 'revision_id': the revision id for the article
    - 'page_title': the title of the Wikipedia article
    - 'state': the state that the town the article is about is located in
    - 'article_quality': the ORES predict quality score for the article
    - 'url': the weblink for the article

**Final Output Data Files:**
- **wp_scored_city_articles_by_state.csv:** This file contains the results of
merging the three original data source files together and includes six fields:
    - 'state': the state of the town the article is written about
    - 'regional_division': the geographic region associated with that state
    - 'population': the 2022 estimated population for the state
    - 'article_title': the title of the article
    - 'revision_id': the revision ID linked to that article
    - 'article_quality': the ORES prediction quality score for the article
- **Error_Log_Total.csv:** This file contains the result of merging the
'Error_Log1.csv' and 'Error_Log2.csv' files and contains the same two fields:
    - 'Article_ID': the ID of the article that ORES failed to get a score for
    - 'Error': if provided, the error message associated with the request
    failure. There were 4 occurrences of an unexpected issue with this column,
    described under 'Source Code Notes' below.

### Source Code Notes:
- My source code for this project is contained in two Jupyter Notebooks. The
first is called 'DATA 512 HW2 - Acquire Rev Ids and Article Quality Scores.ipynb'
and the second: 'DATA 512 HW2 Merge and Analyze Data.ipynb'. You should be able
to reproduct the results of my analysis by running these files in this order, 
provided you have all the source data files in the same directory.
- One note: I did observe a small issue with my error log. I wrote code to
append any article IDs and the corresponding error message when I was unable to
retrive the associated article prediction. Additionally, in special cases where
an error message was not provided in the usual manner, I attempted to instead
store the dictionary of the data from the API request directly in that cell
of the log file. There were four cases where the Error column was blank and I am
not sure why. However, I do not believe this issue is signifanct, though,
because the log file will still contain the article ID, so these troublesome
articles will still be tracked.

## Research Implications
### What did I learn? 
At first, when I was reviewing the ranking tables I built in Step 5, I believed
that it would make sense to see the more populated states at the top of the
per-capita rankings. I thought this because I thought it likely that the more
people a state has, the more articles it should have - and by association,
the more high quality articles it should have. However, this line of thining
was a bit elementary, as the whole point of comparing "per-capita" values is
that you are controlling for population. So, while I was surprised to see that
the top for most populated states (California, Texas, Florida, and New York)
didn't appear on the top 10 states with most article coverage or high quality
coverage, I shouldn't have been as surprised by this. This simply means, I belive
that generally the state's population increase out-paced the increase in articles.


Initially, while a bit simplistic, I

- surprised some less populated states made top coverage list (table1). 5 were
less than 1 million in population. While 7 of the bottom states by coverage
were greater than a million. Hunch is that population varies a lot more than
number of articles. 
- I would have expected the most populated states to win at coverage. Didn't
happen according to the above. However, it does appear when you inspect the top
states by high-quality articles that there is a rough positive correlation
between the number of high quality articles and the state's population. For
instance, 4 of the 5 states with > 1 high quality article had over 8 million
in population.
- I would expect a strong correlation between the top US states by coverage and
top US states by high quality articles. 
    - articles that were in coverage but not in top quality:
        - North Dakota
        - South Dakota
        - Iowa
        - Alaska
        - Wyoming
        - Arkansas
    - articles that were not in top coverage but were in top quality:
        - West Virginia
        - Idaho
        - Virginia
        - Alabama
        - Maryland
        - Illinois
- I would have expected the most populated states to win at quality and coverage
but, according to the NST 2022 estimated state population, the four states
with the greatest population (California, Texas, Florida, and New York) do not
appear in the top 10 in either category. Furthermore, many of the top 10 states
by coverage per capita are the states with the lowest populations, such as
Wyoming, Vermont, Alaska, North and South Dakota. 

We can also see that the two regions with the lowest total coverage of articles
per capita are the two most populated regions: South Atlantic and the Pacific
(see Table 5).

Less of a discernable pattern for the region ranking by high quality coverage
per capita. However, we can tell by inspection that the least populated region,
New England, is ranked #1. Based on this grouping, it is clear that almost all
of the high quality articles appear in the Eastern half of the US. Why? I don't
know. I am not as surprised that the East coast tops the list of high quality
articles because I'm guessing it's related to all the history or our Nation.
However, I am surprised that the East North Central (part of the MidWest) is the
#3 region. I just checked the rank of regions by population and East North
Central is #3, so this is balanced after all!

Why? 
### Reflection Questions from Assignment:
#### 1.	"What biases did you expect to find in the data (before you started working with it), and why?"
I honestly did not expect to see much bias in the results - perhaps a bit
towards states with more large tech cities as their city populations may have
more residents inclined to write Wikipedia articles/edits. But, I did not see
that in my cursory analysis.

#### 2.	"What (potential) sources of bias did you discover in the course of your data processing and analysis?"
The analysis I performed for the assignment was a bit cursory, as I based my
assessment predominately off of the 6 tables I created in Step 4 of my
assignment. However, it does appear that there is some potential bias in the
findings. As I mentioned earlier, if there was no bias and all people were
equally represented in terms of the number of articles and number of high quality
articles per capita for each state or region, we would expect the most populated
states to appear in the top rankings. However, the top four largest states
(California, Texas, Florida, and New York) did not appear in either top 10 list.

I have identified through my analysis that the most populated states
(California, Texas, Florida, and New York) seem to be heavily underrepresented
in terms of the number of articles written, i.e. coverage per capita. It seems
that there is not an obvious positive correlation between the population of
a state and the article coverage. Additionally, from a regional division perspective, we see that while New
England has the smallest population of all regions, it is the top result for
high quality coverage and 2nd highest result for total article coverage (Table
5 and 6). 

Without studying the data more deeply, beyond the scope of this assignment, I
cannot provide a good answer as to what is causing these perceived biases.
As discussed earlier, we can observe
from the tables produced in this analysis that the states with lower populations
seem to be overrepresented while most of the larger states have a lower per capita
score. One hypothesis I have for this behavior is that perhaps this is not due
to a bias in the data or the processes that generated the data, but rather
because the populations of states vary much more than the number of articles
written about the cities in each state. Perhaps most states have a relatively
simillar number of cities within them, resulting in a similar number of city
articles. 

Likewise, I am not sure why the New England regional division and the rest of
the Eastern half of the United States has the vast majority of the high quality
articles. One untested hypothesis that I do have is that because the first
colonies in America were established on the East coast, there is a lot more
historical events that occurred in some of these cities that are foundational
to American history and hence merit more well-written articles. These are just
untested ideas, though, and I am very curious as to what is causing these
apparent biases. 

#### 3.	"What might your results suggest about (English) Wikipedia as a data source?"
In short, I believe that there are advantages and disadvantages to using the
English Wikipedia as a data source. It is helpful, on the one hand, because
of the data's accessibility and volume. However, as this exercise demonstrated,
there are some interesting quirks of the data that may indicate the presence of
bias and merit a deeper investigation before using the data.