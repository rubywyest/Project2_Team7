# Project2_Team7

#### Team Members:  Ruby Mittal, Luis Santana, Jeff Eickholt

#### Project Title: Do you want to relocate to ...?

#### Description:  We created an interactive dashboard that allowed the uses to view some key informaton about a chosen city in the United States.  To make the interaction more manageable, we allow the user to first choose the state that they are interested in through a standard drop-down list.  Based on the state chosen, a second drop-down is populated with the cities available for that state.  This drop-down is searchable, so the user can type the first letter of the city to quickly find the city of interest.  We originally had planned to allow the user to view state or city data, but we eventually decided to focus on just displaying the city.  We did process state data, so you will see a table for that in our database.  Below is a quick description of how this project met the project requirements.  Our original proposal is included at the very bottom of this readme.

1.  We input data from the Census American Community Survey from csv files at the city and state level.  Here is the link for Census files https://www.census.gov/data/tables.html. We also obtained weather data though webscraping at the state level only. Here is the link to the site https://www.usclimatedata.com/.  This data was processed and then output to a PostgreSQL datebase.  The data from the database was then accessed by a Flask application, which had several routes and published the necessary data in a JSON format.

2.  We created an interactive dashboard using the data from the Flask application and javascript code.  The visualizations on the page update based on the city chosen.

3.  We used a new libary call numeral.js (http://numeraljs.com/).  This libary was used to apply formatting to numeric data that we presented on the dashboard, such as presenting numbers as a percentages or as currency.

4.  Our city level data had a total of 519 cities to choose from.  These are based on the metropolitan statistical area, which is a census bureau definition, and include metropolitan areas with a population greater than 50,000.

5.  Our dashboard had a total of 6 different views of the data.


### Repo Contents:

#### Main folder contains:
  1.  index_master.html:  html code that creates the dashboard page.
  2.  Dashboard_Preview.pptx:  This was the example that we developed as part of the original proposal;

#### statis/py folder contains:
  1. app-weather.py:  This is the Flask application that brings in the data from the PostgreSQL database and publishes as an API in JSON format.
  2. census_data_prep_jeff.ipynb:  This is the file that Jeff used to read in census data on commuting, median income, and population and clean up.  This file also reads in census data on education and diversity which Luis processed and data on home value and weather that Ruby processed, and output final cleaned data that is output to the database in file described below. 
  3.  create_db_jeff.ipynb:  This file reads in the clean data and outputs to a PostgreSQL database.  Some renaming of variables was also included.  Note that the database with name city_state_data_db has to first be created in PostgreSQL, but no tables or data need to be added.  This notebook will create the tables and populate the database.
  4.  create_db_ruby.ipynb:  This is a copy of create_db_jeff.ipynb that Ruby used to create a copy of the database.  She was not able ot use create_db_jeff, due to different password.
  4.  div_edu_las.ipynb:  This is the notebook Luis used to read in a process the census data on education and diversity.  It then outputs a csv file that is used in census_data_prep_jeff.ipynb.
  5. weather_data_ruby.ipynb:  This is the notebook that Ruby used to scrape weather data a the state level, process, and output a csv file that is used in census_data_prep_jeff.ipynb.

#### static/js folder contains:
  1.  app_master.js:  This is the final javascript file that contains all the the code to create the visualizations. This final version was compiled from indiducal js scripts developed by each team member.
  2. config.js:  File used to store key for mapbox map.
  3. shp.min.js:  This is a 3rd party library to load shape files to the Leaflet maps
            https://github.com/calvinmetcalf/leaflet.shapefile
            We found it from the list of plugins on Leaflet 
            https://leafletjs.com/plugins.html


#### static/data folder contains:  Note we originally planned to use the census API to get the data we were interested in.  However, after investigation, we found that the API didn't get us the data we expected, so we relied on downloads from the census website.  The website makes a user pick a particular report to run, so to get all of the data we were interested in, we had to run several reports at both the city and state level, which explains the large number of files. 
  1.  cb_2018_us_cbsa_20m.zip This file contains the shapes of all the US metros
          https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.html
  2.  cb_2018_us_state_20m.zip This file contains the shapes of all the US states - we got it from US Census
          https://www.census.gov/geographies/mapping-files/time-series/geo/carto-boundary-file.html
  3.  census_commuting.csv:  This file contains the raw census data on commuting at the city level. Input to census_data_prep_jeff.ipynb.
  4.  census_commuting_state.csv:  This file contains the raw census data on commuting at the state level.  Input to census_data_prep_jeff.ipynb.
  5.  census_income.csv:  This file contains the raw census data on income at the city level.  Input to census_data_prep_jeff.ipynb.
  6.  census_income_state.csv:  This file contains the raw census data on income at the state level.  Input to census_data_prep_jeff.ipynb.
  7.  Census_median_home_value_by_metro.csv: This file contains the raw census data on home value at the city level.  Input to census_data_prep_jeff.ipynb. 
  8.  census_median_home_value_by_state.csv: This file contains the raw census data on home value at the state level.  Input to census_data_prep_jeff.ipynb.
  9.  census_population.csv:  This file contains the raw census data on population at the city level.  Input to census_data_prep_jeff.ipynb.
  10. census_population_state.csv:  This file contains the raw census data on population at the state level.  Input to census_data_prep_jeff.ipynb.
  11. census_unemployment.csv:  This file contains the raw census data on unemployment at the state level.  Input to census_data_prep_jeff.ipynb.
  12. census_unemployment_state.csv:  This file contains the raw census data on unemployment at the state level.  Input to census_data_prep_jeff.ipynb.
  13. data_diver_city.csv:  This file contains the raw census data on diversity at the city level.  Input to div_edu_las.ipynb.
  14. data_diver_state.csv:  This file contains the raw census data on diversity at the state level.  Input to div_edu_las.ipynb.
  15. data_edu_city.csv:  This file contains the raw census data on education at the city level.  Input to div_edu_las.ipynb.
  16. data_edu_state.csv:  This file contains the raw census data on education at the state level.  Input to div_edu_las.ipynb.
  17. state_lat_long.csv:  Data on the center latitude and longiture use for create map.
  18. state_temprature.csv:  Data on the weather for each state.  Output from weather_data_ruby.ipynb. Input to census_data_prep_jeff.ipynb
  19. state_to_stateabbr.csv:  Data that maps state name to state abbreviation. Input to census_data_prep_jeff.ipynb.
  

#### static/data/cleaned folder contains:
  1.  master_city_data.csv:  This file contains all of the census data at the city level after it was processed and cleaned.  This file was then read into create_db_jeff.ipynb and output to city_data table in the database.
  2. master_mapping_data.csv:  This file contains the state name and two letter state abbreviation. It was needed, as some data sourced had the full name, but others just had the two letter abbreviation.  This file was then read into create_db_jeff.ipynb and output to mapping_data table in the database.
  3.  master_state_data.csv:  This file contains all of the census data at the state level after it was processed and cleaned.  This file was then read into create_db_jeff.ipynb and output to state_data table in the database.
  4.  master_weather_data.csv:  This data contains all of the weather data at the state level after it was processed and cleaned. This file was then read into create_db_jeff.ipynb and output to weather_data table in the database.

#### static/css folder contains:
  1.  css_master.css:  Contains syling that is applied to index_master.html;
  2.  shutterstock_1486328387.jpg:  Picture that is displayed at the top of our website.


### Original Proposal (This was the original proposal that we submitted.  After exploring the data and timing, we had to make a few adjustments)

### Project Title: Do you want to relocate to ...?

#### In this project, we will be creating an application that will allow users to view details of a state or city to decide if they want to move there.  This app will contain two dashoards.  The first will be for a particular State of City that the user chooses.  It will display some key statitics and chart about the city.  The second dashboard will allow the user to choose two states or cities and see a side by side comparison the the same key statistic and charts. This will allow them to compare the current state/city that they live in to anothre  state/city that they are thinking of moving to.

####  The main dataset will be the US Census Data American Community Data (link below).  We will also be attempting to gather temperature data from the National Centers for Environmental Education (second link below).  We haven't yet determined if we can figure out the weather API.  If we can't figure this out in the next couple of days, we will drop this data source and replace the chart with a different chart based on census data.

https://www.census.gov/acs/www/data/data-tables-and-tools/

https://www.ncei.noaa.gov/support/access-data-service-api-user-documentation


#### The final output will look very similar to the Dashboard_Preview Power Point included in the repo.

