## *Covid and Hourly Wage - ETL (Extract, Load, Transform)*

![COVID Money](https://www.newhope.com/sites/newhope360.com/files/styles/article_featured_retina/public/covid19%20money.png?itok=ycJGsmTo)

## Situation: 
The CDC site offers many datasets on COVID-19, but we wanted to combine and clean a few CDC datasets and merge with US Hourly Wage Data in order to show a greater picture.

## Questions:
1. What is the correlation between vaccination count and COVID deaths per state?
4. What states have the highest vaccination count?
5. What states have the lowest vaccination count?
6. What is the correlation between hourly wage and COVID vaccinations per state? 
7. What is the correlation between hourly wage and COVID deaths per state?

## Sources
**CDC COVID-19 Datasets:** 
* COVID-19 Deaths per 100k: https://covid.cdc.gov/covid-data-tracker/#cases_deathsper100k
* Total Vaccination Doses Administered per 100k: https://covid.cdc.gov/covid-data-tracker/#vaccinations_vacc-total-admin-rate-total

**US Bureau of Labor Statistics:**
* Modeled Wage Estimates: https://www.bls.gov/mwe/

## Tools Used
* Jupyter Notebook (python)
    * pandas library
    * csv library
* pgAdmin4 (PostgreSQL)

## ETL (Extract Transform Load) Process Outline

### _[EXTRACT]_
1. We pulled in data from three different sources and they were all exported into CSV files
2. The next step will show how each table was cleaned before being uploaded into SQL

### _[TRANSFORM]_

### CDC - COVID-19 Deaths per 100k (9KB)
1. Downloaded raw data from CDC
   1. File was saved as a CSV file
2. Imported CSV in jupyter notebook using pandas library
3. Corrected misnomers (i.e. "New York*" was corrected to "New York")
4. Created US States List
5. Removed US Territories (anything that was not in US States List)
6. Created new data frame with only the columns needed for answering our proposed questions

### CDC - Total Vaccination Doses Administered per 100k (28KB)
1. Downloaded raw data from CDC
   1. File was saved as a CSV file
2. Imported CSV in jupyter notebook using pandas library
3. Renamed the state "New York State" to "New York"
4. Created US States List
5. Removed US Territories (anything that was not in US States List)
6. Remove columns where the population is 12 years or older
6. Created new data frame with only the columns needed for answering our proposed questions

### US Bureau of Labor Statistics (131MB)
1. Downloaded raw data from U.S. Bureau of Labor Statistics
   1. File was saved as a CSV file
2. Imported CSV in jupyter notebook using pandas library
3. Displayed the type of data in each column once the new data frame has been created
4. Renamed the columns "Average Hourly Wage", "State", and "State Name"
5. We renamed the columns so that we could join the tables in SQL
6. Created a new table by only selecting the "State" and "Hourly Wage" columns

### Merging the Data in Python
1. Displayed the data types before we merged the tables
2. Removed the "-" in column "Hourly Wage" and replaced it with a "0"
3. Changed the data type in the "Hourly Wage" column from object to float
4. Merged the COVID deaths by state data frame with the Hourly Wage data frame
   1. The data was merged together on the "State" columns
5. Displayed the data types before connecting the data frames to Postgres SQL

### _[LOAD]_

### Creating the Databases in Postgres SQL
1. Created the database "COVID" by creating the engine and the connection to the SQL database
2. Created the table "COVID by State" and connected it to SQL
3. Created the table "COVID Vaccinations" and connected it to SQL
4. Once the tables were created in SQL, we performed a few queries within SQL

## Final Notes
Through this ETL process, we now have tables that will be a great starting point to answering the questions proposed above, along with further research regarding a State's hourly wage and COVID vaccinations or deaths.
