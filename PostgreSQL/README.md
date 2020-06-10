# Introduction

## Project Description

Sparkify, is a music streaming startup company. It has collected information from users of their music streaming app and looking to understand their user’s streaming behavior. Sparkify’s analytics team is interested in examining the user activity logs and song data collected, but currently, the company does not have a database designed for easy queries of the data. 

As a Data Engineer, I can help Sparkify store and access their data more efficiently by creating a database better suited for their needs.

## Objectives

- To create a Postgres database with tables designed to optimize queries on song play analysis.
- Create a database schema and ETL pipeline.

# Database Design

## Data description

**Fact Table**

1. **songplays** - records in log data associated with song plays i.e. records with page *NextSong*
- *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

**Dimension Tables**

1. **users** - users in the app
- *user_id, first_name, last_name, gender, level*
2. **songs** - songs in music database
- *song_id, title, artist_id, year, duration*
3. **artists** - artists in music database
- *artist_id, name, location, latitude, longitude*
4. **time** - timestamps of records in songplays broken down into specific units
- *start_time, hour, day, week, month, year, weekday*

## Project Files
 
1. **create_tables.py** creates and drops the tables and database. When executed it reset the tables to prepare it for the ETL scripts.
2. **etl.ipynb** extracts and transforms a single file from song_data and log_data and loads the data into database tables. 
3. **test.ipynb** displays the first few rows of each table to check the database.
4. **etl.py** extracts and transforms files from song_data and log_data and loads them into database tables. 
5. **sql_queries.py** contains all your sql queries, and it is imported by **create_tables.py**, **etl.ipynb**, **etl.py**.
6. **README.md** provides the instruction to properly use the project.

## How to run the program

To properly execute the database:

1. Run **create_tables.py** to create database and tables, and drop any unnecessary tables.
2. Run **etl.ipynb** to test the connection and the ETL process.
3. Run **test.ipynb** to validate the data inserted in the the tables.
4. Run **etl.py** to extract, clean, and insert all the records to the database.

## Schema Design

A star schema design was used as it provides more simplified queries, easy aggregation of the data, and denormalization of the records.

## Diagram

![alt text](images/EDR.jpg "Star Schema")

# Query Examples

To test the database, the following sample query can be executed:

> %sql SELECT level,count(level) FROM users group by level;

![alt text](images/level_count.jpg "Total Users subscription")

> %sql SELECT level, count(distinct user_id) FROM songplays  group by level;

![alt text](images/user_count.jpg "Number of App user subscription")

> %sql SELECT weekday, COUNT(weekday) FROM songplays JOIN time ON 
                                    songplays.start_time=time.start_time 
                                    GROUP BY weekday ORDER BY COUNT(weekday) DESC;
                                    
![alt text](images/weekday_app_use.jpg "Most frequent days of use")