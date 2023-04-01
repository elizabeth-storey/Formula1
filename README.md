<p align = "center">
  <img src="https://user-images.githubusercontent.com/128324837/229282750-acca6c03-96d2-4c50-add9-df97ae2e7f77.png" width=60% height=60%>
</p>

# Formula 1 Data Exploration

## 1. Background and Motivation
<p align = "justify"> Formula One (F1) is one of the most exciting and high-profile sports in the world, with a global fan base of millions. The sport's popularity is fueled by its high-speed, adrenaline-fueled action, as well as its history and prestige. F1 racing involves cutting-edge technology, precision engineering, and world-class drivers, all of which come together to create a thrilling and unpredictable spectacle. 
    </p>
  
<p align = "justify"> In recent years, the F1 world has seen a surge in the amount of data generated by the sport. From telemetry data to race results, there is a wealth of information available that can be used to gain insights into the sport and help teams and drivers optimize their performance.
    </p>

<p align = "justify"> This project aims to conduct a comprehensive analysis of F1 data using SQL to answer several research questions. To achieve this, a large and diverse dataset that contains historical data on F1 races, teams, drivers, and track conditions will be leveraged and SQL queries will be used to extract relevant data from the database, transform it into meaningful insights, and visualize the results to facilitate interpretation and communication. his project will also involve cleaning and organizing the data to ensure it is in a format that can be easily analyzed
     </p>

<p align = "justify"> The insights generated from this project could be useful for a wide range of stakeholders in the F1 ecosystem, including teams, drivers, sponsors, and fans. By understanding the factors that contribute to success in F1, teams and drivers can make data-driven decisions to improve their performance and gain a competitive edge. Sponsors could use the insights to identify potential opportunities for branding and marketing, while fans could gain a deeper appreciation and understanding of the sport they love.
    </p>

<p align = "justify"> Overall, this project aims to provide valuable insights into the performance of F1 teams and drivers and advance our understanding of the factors that contribute to success in the sport. By leveraging the power of big data and SQL, we can unlock hidden patterns and trends in the data that can inform decision-making and enhance our appreciation of this thrilling sport.
  </p>

## 2. Research Questions
I have chosen the following reseach questions to focus on in this project:

1. Which constructor teams are the most successful in terms of total races entered and total points earned?
2. Which drivers are the most successful in terms of total points and wins?
3. Which country produces the most world champions?
4. Does higher altitude cause more engine failures in Formula 1 races?

## 3. Dataset: Data Retrieval and Standard Descriptive Analysis

The dataset used in the project is available at: [https://www.kaggle.com/cjgdev/formula-1-race-data-19502017](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)

It contains race entries from 1950 to present. 

The dataset includes:

1. **circuits.csv:** This file contains data on all the circuits that have hosted a Formula 1 race.
2. **constructor_results.csv:** This file contains data on the race results for each constructor.
3. **constructor_standings.csv:** This file contains data on the final constructor standings for each season.
4. **constructors.csv:** This file contains data on each constructor that has participated in Formula 1.
5. **driver_standings.csv:** This file contains data on the final driver standings for each season.
6. **drivers.csv:** This file contains data on each driver that has participated in Formula 1.
7. **lap_times.csv:** This file contains data on the lap times for each driver in each race.
8. **pit_stops.csv:** This file contains data on the pit stops made by each driver in each race.
9. **qualifying.csv:** This file contains data on the qualifying sessions for each race.
10. **races.csv:** This file contains data on each race, including the race's ID.
11. **results.csv:** This file contains data on the results of each race.
12. **seasons.csv:** This file contains data on each season of Formula 1.
13. **status.csv:** This file contains information about the status codes that can be assigned to a driver's car during a race.

## 5. Import the Data to SQL
The next step into import the data into mySQL

```sql 
-- Create tables and import data

# 1: Circuits
CREATE TABLE circuits (
    circuitId integer,
    circuitRef varchar(255),
    name varchar(255),
    location varchar(255),
    country varchar(255),
    lat integer,
    lng integer,
    alt integer,
	url varchar(255)
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/circuits.csv'
INTO TABLE circuits
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM circuits;
# 2: Lap Times
CREATE TABLE lap_times (
    raceId integer,
	driverId integer,
    lap integer,
    position integer,
    time time,
    milliseconds integer
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/lap_times.csv'
INTO TABLE lap_times
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM lap_times;

# 3: Pit Stops
CREATE TABLE pit_stops (
    raceId integer,
	driverId integer,
    stop integer,
    lap integer,
    time time,
    milliseconds integer,
    duration time
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/pit_stops.csv'
INTO TABLE pit_stops
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM pit_stops;

# 4: Seasons
CREATE TABLE seasons (
    year varchar(255),
    url varchar(255)
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/seasons.csv'
INTO TABLE seasons
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM seasons;

# 5: Status
CREATE TABLE status (
    statusId integer,
    status varchar(255)
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/status.csv'
INTO TABLE status
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM status;

# 6: Constructor Standings
CREATE TABLE constructor_standings (
	constructorStandingId integer,
    raceId integer,
    constructorId integer,
    points integer,
    position integer,
    positionText varchar(255),
    wins integer
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/constructor_standings.csv'
INTO TABLE constructor_standings
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM constructor_standings;

# 7: Constructors
CREATE TABLE constructors (
	constructorId integer,
    constructorRef varchar(255),
    name varchar(255),
    nationality varchar(255),
    url varchar(255)
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/constructors.csv'
INTO TABLE constructors
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM constructors;

# 8: Driver Standings
CREATE TABLE driver_standings (
	driverStandingId integer,
    raceId integer,
    driverId integer,
    points integer,
    position integer,
    positionText varchar(255),
    wins integer
    );

LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/driver_standings.csv'
INTO TABLE driver_standings
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM driver_standings;

# 9: Drivers
CREATE TABLE drivers (
	driverId integer,
    driverRef varchar(255),
    forename varchar(255),
    surname varchar(255),
    dob date,
    nationality varchar(255),
    url varchar(255)
    );

LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/drivers.csv'
INTO TABLE drivers
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM drivers;

# 10: Races
CREATE TABLE races(
	raceId integer,
    year varchar(255),
    round integer,
    circuitId integer,
    name varchar(255),
    date date,
    time time,
    url varchar(255)
    );

LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/races.csv'
INTO TABLE races
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM races;

# 11: Constructor Results
CREATE TABLE constructor_results (
	constructorResultsId integer,
    raceId integer,
    constructorId integer,
    points integer
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/constructor_results.csv'
INTO TABLE constructor_results
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM constructor_results;

# 12: Results
drop table results;
CREATE TABLE results (
	resultsId integer,
    raceId integer,
    driverId integer,
    constructorId integer,
    number integer,
    grid integer,
    position integer,
    positionText varchar(255),
    positionOrder integer,
    points integer,
    laps integer,
    time time,
    milliseconds integer,
    fastestLap integer,
    ranks integer,
    fastestLapTime decimal(10,3),
    fastestSpeed integer,
    statusId integer
    );
    
LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula1/Data/Cleaned/results.csv'
INTO TABLE results
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM results;

# 13: Qualifying
CREATE TABLE qualifying (
	qualifyId integer,
    raceId integer,
    driverId integer,
    constructorId integer,
    number integer,
    position integer,
	q1 time,
    q2 time,
    q3 time
    );

LOAD DATA LOCAL INFILE '/Users/elizabeth/Documents/GitHub/Formula 1/Data/Cleaned/qualifying.csv'
INTO TABLE qualifying
FIELDS TERMINATED BY ','
IGNORE 1 ROWS;

SELECT *
FROM qualifying;
```
## . Analyzing Data to Find the Most Successful Constructors
``` sql
-- Join results table and constructors table
SELECT *
FROM results r
JOIN constructors c
ON r.constructorId = c.constructorId;
```

### Methods Implemented 
This project contains implementations of scientific methods such as: 
- Data Wrangling
- Data Integration & Data Enrichment
- Linear Regression
