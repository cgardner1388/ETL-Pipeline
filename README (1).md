# Project 2 - *Covid and Hourly Wage*
*An exercise in ETL (Extract, Load, Transform)*

![COVID Money](https://www.newhope.com/sites/newhope360.com/files/styles/article_featured_retina/public/covid19%20money.png?itok=ycJGsmTo)

## Group 5:
Bradley Barker, Cody Gardner, Yawavi Koudjonou (Vi)

## Situation: 
The CDC site offers many datasets on COVID-19, but we want to combine and clean a few CDC datasets as well as US Hourly Wage Data in order to show a greater picture.

## Questions:
1. What is the correlation between vaccination count and COVID deaths per state?
4. What states have the highest vaccination count?
5. What states have the lowest vaccination count?
6. What is the correlation between hourly wage and COVID vaccinations per state? 
7. What is the correlation between hourly wage and COVID deaths per state?

## Sources
CDC COVID-19 Datasets: 
* COVID-19 Deaths per 100k: https://covid.cdc.gov/covid-data-tracker/#cases_deathsper100k
* Total Vaccination Doses Administered per 100k: https://covid.cdc.gov/covid-data-tracker/#vaccinations_vacc-total-admin-rate-total

US Bureau of Labor Statistics:
* Modeled Wage Estimates: https://www.bls.gov/mwe/

## Tools Used
* Jupyter Notebook (python)
    * pandas library
    * csv library
* pgAdmin4 (PostgreSQL)

### ETL (Extract Transform Load) Process Outline

### Extract
1. We pulled in data from three different sources and they were all exported into CSV files
2. The next step will show how each table was cleaned before being uploaded into SQL

### Transform

### CDC - COVID-19 Deaths per 100k(9KB)
1. Downloaded raw data from CDC in csv format
        -File was saved as a CSV file
2. Imported CSV in jupyter notebook using pandas library
3. Corrected misnomers (i.e. "New York*" was corrected to "New York")
4. Created US States List
5. Removed US Territories (anything that was not in US States List)
6. Created new database with only the columns needed for answering our questions

### CDC - Total Vaccination Doses Administered per 100k (28KB)
1. Downloaded raw data from CDC in csv format
        -File was saved as a CSV file
2. Imported CSV in jupyter notebook using pandas library
3. Renamed the state "New York State" to "New York"
4. Created a list for all states in the US
5. Kept all of the data in the data frame that was in the state list, this means that any state from the data frame that matches up to the state list then we will keep that row of data
6. Remove columns where the population is 12 years or older
7. Created a new data frame by selecting by only selecting relevant information that will help us answer the questions from the proposal

### US Bureau of Labor Statistics (131MB)
1. Downloaded raw data from bureau of labor statistics 
        - File was saved as a CSV file
2. Imported CSV in jupyter notebook using pandas library
3. Displayed the type of data in each column once the new data frame has been created
4. Renamed the columns "Average Hourly Wage", "State", and "State Name"
5. I renamed the columns so that I could join the tables in SQL
6. Created a new table by only selecting the "State" and "Hourly Wage" columns

### Merging the Data in Python
1. Displayed the data types before I merged the tables
2. Removed the "-" in column "Hourly Wage" and replaced it with a "0"
3. Changed the data type in the "Hourly Wage" column from object to float
4. Merged the COVID deaths by state data frame with the Hourly Wage dataframe
        - The data was merged together on the "State" columns
5. Displayed the data types before connecting the data frames to Postgres SQL

### Load

### Creating the Databases in Postgres SQL
1. Created the database COVID by creating the engine and the connection to the SQL database
2. Created the tables "COVID by State" and connected it to SQL
3. Created the tables "COVID Vaccinations" and connected it to SQL
4. Once the tables were created in SQL, we created a couple of different queries within SQL
5. These tables will be helpful as well will be able to figure out if there is a correlation between a State's hourly wage and COVID vaccinations or deaths

