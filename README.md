# Final-Task-FT: Task, working, data sources
1. Task
2. Charts
3. Working

## 1. Task
An FT reporter is writing a story about how the US film industry is recovering from the cinema shutdown during the pandemic, and has asked the visual and data team for help. You have been handed the task to:

1. Find a reliable data source for US domestic cinema "box office” revenue

2. Using the visualisation tool(s) of your choice, design 1-2 charts that show how the US film industry is (or is not) recovering. 

These do not need to be in FT style, but they do need to include real data and suggested wording for publication. Provide clear documentation of your workings, ie how you obtained, cleaned and transformed the data needed for your chart(s).


Scroll down for charts and working, or see the files section.


## 2. Charts
American cinemas are struggling after Covid. It’s not the virus: the problem is the movies. The US movie industry made $7.37bn in 2022, down 35% on 2019. But why? 
 
One theory is that Americans are still staying home more after Covid lockdowns. But we can test this - some states locked down much harder than others. As the first chart shows there is no correlation: cinemas in lockdown-hating Tennessee, for example, are emptier than those in New York, which imposed heavy restrictions.

<img src="https://github.com/Android022/Final-Task-FT-/blob/main/graph1.jpg?raw=true" alt="alt text" style="width: 54%;">

The real reason is simpler: there are fewer blockbusters to see. Studios shut down in Covid, and the pipeline of films dried up. As the second chart shows, when films go on “wide” release across America - like Tom Cruise’s Top Gun Maverick - they still make a lot of revenue, as Americans are still keen to see them in big numbers. The problem is there are fewer big films around. When the movies return, so will the moviegoers.

<img src="https://github.com/Android022/Final-Task-FT-/blob/main/graph2.jpg?raw=true" alt="alt text" style="width: 54%;">


## 3. Working
I started by reading several online articles about the US film industry post-Covid. They helped me to identify three main trends to explore: the impact of (a) lockdowns, (b) streaming services and (c) film quality/quantity.

The most helpful articles included:

* https://en.wikipedia.org/wiki/Impact_of_the_COVID-19_pandemic_on_cinema

* https://www.economist.com/business/2022/06/02/top-gun-flies-high-sparking-hopes-of-a-theatrical-recovery

* https://www.cnbc.com/2023/04/05/box-office-almost-back-to-pre-covid-levels.html

* https://www.cnet.com/culture/entertainment/movie-theaters-didnt-die-but-theyll-never-be-the-same-again/

* https://variety.com/2022/film/news/box-office-top-gun-elvis-pandemic-return-1235303574/

* https://www.statista.com/chart/21425/annual-box-office-earnings-in-north-america/


### Chart 1:
This chart links 2020 lockdown severity to 2023 cinema trips, showing that the severity of lockdown does not seem to have an enduring effect on cinema trips.

The lockdown data comes from the excellent Oxford Covid-19 Government Response Stringency index: https://data.humdata.org/dataset/oxford-covid-19-government-response-tracker

I removed all the superfluous data (non-US states and indices other than lockdown stringency).

Then, for each state, I averaged their stringency score for each day in 2020. This is a helpful summary statistic as it includes both the length and severity of lockdowns.

Unfortunately, state-level Box Office data is not available. Therefore, I used the proxy of Google searches for the word 'cinema'.

Searches for cinema over time looks to be an accurate proxy of Box Office revenue because:

* a. several academic studies have shown that Google Trends gives an accurate estimate of behaviour, e.g. Vosen & Schmidt 2011 (https://onlinelibrary.wiley.com/doi/full/10.1002/for.1213?casa_token=dwJLfjjz_rcAAAAA%3APXn4iZrw4DWJhi20wOx4rvm_M9RteX2O1mNhA2V7ZxjkuFrNCIfcA35bnJE54hykVSJWGgW1ebLJlw), Choi & Varian 2009 (https://static.googleusercontent.com/media/www.google.com/en//googleblogs/pdfs/google_predicting_the_present.pdf)

* b. eyeballing it, searches for cinema were fairly constant, dropped severely during Covid, and have recovered but not back to their pre-Covid levels.

Google Trends does not have an official API, so I wrote Python code to scrape Google Trends for 'cinema' searches in each state for each year of 2019-23. This guide was particularly helpful: https://hackernoon.com/how-to-use-google-trends-api-with-python

My Python code is [here](https://github.com/Android022/Final-Task-FT-/blob/main/Google_Trends_Scraping.ipynb)

With the data, I calculated the percentage change for each state from 2019 to 2023 (i.e. proxy for percentage change in Box Office revenue, 2023 vs 2019, the last full year before the pandemic).

I then merged these two datasets, to have three columns: state, average 2020 lockdown stringency, and percentage change in Google searches for 'cinema' (2023 vs 2019).

Finally, I added the party of the Governor of each state at the start of 2020 (relevant since Governors were generally the ones in charge of state-wide lockdown policy).

The dataset is [here](https://github.com/Android022/Final-Task-FT-/blob/main/Graph1Data.csv)

And the chart is [here](https://github.com/Android022/Final-Task-FT-/blob/main/graph1.jpg)

(During my research, I did a very similar analysis with Google searches for Netflix, to test the theory that people have shifted from cinemas to streaming. This looked like another dud theory: only about a third of states saw a decline in cinemas and an upswing in Netflix.)

### Chart 2:
This chart links monthly wide movie releases to box office revenue, showing that Box Office revenues are below pre-Covid levels because there have been fewer wide releases.

The number of wide movie releases comes from RunPee, a popular cinema-related app: https://runpee.com/wide-release-movie-count-by-month/ 

Monthly Box Office revenue comes from Box Office Mojo (owned by IMDb): https://www.boxofficemojo.com/month/by-year/2022/?grossesOption=calendarGrosses

I merged these two datasets, to have three columns: month (from Jan 2019 to Dec 2022), Box Office revenue, and number of wide releases.

Finally, I annotated the graph with several of the biggest post-Covid films, again from Box Office Mojo: https://www.boxofficemojo.com/month/by-year/?grossesOption=calendarGrosses

The dataset is [here](https://github.com/Android022/Final-Task-FT-/blob/main/Graph2Data.csv)

And the chart is [here](https://github.com/Android022/Final-Task-FT-/blob/main/graph2.jpg)
