# ETL_project

Jasmin Schaefer and Shaun Ramirez

Scope: Build a database to be able to see the efficacy of spending on homelessness by state from 2015-2018. 

## Required Installations ##
For required environments and installs:

    $ pip install -r install_env.txt

To clean data:

1. Run the jupyter notebook file "Cleaning 2007-2019-PIT-Counts-by-CoC.ipynb"
2. Run the jupyter notebook file "Cleaning 2010-2019_Population_Data.ipynb"
3. Run the jupyter notebook file "Cost data.ipynb"
4. Initialize Mongod in terminal/command line and run 'MongoDB.ipynb" to create database

## Extract: ##
Raw data for our project was extracted from the following sources and was obtained in excel (.xlsx) format and saved in 'raw_data' folder:

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

Once each years data was cleaned, all data was then merged on 'State' and exported as a CSV file. To execute the cleaning, run the jupyter notebook file "Cleaning 2007-2019-PIT-Counts-by-CoC.ipynb"

For the cleaning of the '2010-2019 Population for Each State' modification of the raw data was neccessary in exel prior to importation into jupyter notebook. No data was removed in excel only unneccessary headers to simplify the importing process. once the data was imported the following took place:
* '0' column was renamed to 'State'
* Null values were dropped
* Indexes of the regional polulation data and overall United States population data was identified and dropped
* Columns were renamed to simplify column names
* State abbreviations were added to the table for each state
* Columns were selected to include desired years (2015-2018), state abbriviations, census, and estimated base
* Data was then exported into CSV

To execute the cleaning, run the jupyter notebook file "Cleaning 2010-2019_Population_Data.ipynb"

Cleaning of the 'Award data by state' was obtined in excel format but converted to a CSV prior to importing it into the jupyter notebook. Once the CSV was imported into jupyter notebook the cleaning involved the following to be able to visualize the total awards recieved by each state:
* Data was indexed by 'state_cost_id'
* Columns were renamed to simplify column names
* Indexes of American territories was identified and removed
* Desired columns were selected : 'year', 'state', 'award_amount'
* data was grouped by 'state' and 'year'
* awards for each state were then summed together
* Index was reset then set back to 'state_cost_id' and exported to CSV
To be able to visualize the breakdown of award that was awarded to each state by the Continuum of Care (CoC) the 'Award data by state' was then transformed in the following way:
* Desired columns were selected: 'year', 'state', 'coc_name', 'award_amount'
* The data was then grouped by year and state
* the index was then reset and a new index was added entitles 'coc_id'
* The data was then exported as a CSV file

To execute the cleaning, run the jupyter notebook file "Cost data.ipynb"

## Load ##
The database chosen to load this data into was a non-relational database (Mongodb).

Creating the database:
* Establishing a connection to localhost (27017)
* Create database called 'db'

Create function 'insert_csv' to upload csv to mongo
* two parameters (csv_name,collection_name)
* set variable 'collection' to db.collection_name
* set variable data to read in the csv pathway and name
* set variable data_json to convert 'data' to json
* insert json data into the collection (i.e., variable 'collection')
* query collection and set to results
* print query with for statement

Call functions for each dataset
* Use insert_csv function with two arguments for each dataset
* ('award_amount_coc',db.coc_award)
* ('award_by_state',db.state_award)
* ('state_population',db.state_pop)
* ('2015-2018_homeless_data',db.homeless_data)

Run example queries
* Sample:
* myquery = {'State':'UT'}
* state_query = db.homeless_data.find(myquery)
* for info in state_query:
*    print(info)















