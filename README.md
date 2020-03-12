# ETL_project

Jasmin Schaefer and Shaun Ramirez

Scope: Build a database to be able to see the efficacy of spending on homelessness by state from 2015-2018. 

## Extract: ##
Raw data for our project was extracted from the following sources and was obtained in excel (.xlsx) format:

* 2007-2019 Point-in-Time Estimates by CoC - [hudexchange.info](https://www.hudexchange.info/resource/5948/2019-ahar-part-1-pit-estimates-of-homelessness-in-the-us/)

* 2010-2019 Population for Each State - [https://www.census.gov](https://www.census.gov/data/tables/time-series/demo/popest/2010s-state-total.html)

* Award data by state - [hudexchange.info](https://www.hudexchange.info/grantees/allocations-awards)

## Transform: ##
For each data set that was obtained, a python environment was established, jupyter notebook was launched and the data was imported using the pandas library for python then cleaned. 

Cleaning for the '2007-2019 Point-in-Time Estimates by CoC' data invlolved only importing the desired years 2015-1018, each year was on a seperate tab in the excel file. Once imported, for each years data:
* Null vaules were dropped
* The 'CoC Number' was split into 'State' and 'Number' columns
* Data was then grouped by 'State'
* Columns were listed to fully inspect the data
* "Overall Homeless" data columns were selected
* Each column was renamed for simplicity and to remove special characters
* Out lying American territories were removed
Once each years data was cleaned, all data was then merged on 'State' and exported as a CSV file.

For the cleaning of the '2010-2019 Population for Each State' modification of the raw data was neccessary in exel prior to importation into jupyter notebook. No data was removed in excel only unneccessary headers to simplify the importing process. once the data was imported the following took place:
* '0' column was renamed to 'State'
* Null values were dropped
* Indexes of the regional polulation data and overall United States population data was identified and dropped
* Columns were renamed to simplify column names
* State abbreviations were added to the table for each state
* Columns were selected to include desired years (2015-2018), state abbriviations, census, and estimated base
* Data was then exported into CSV


