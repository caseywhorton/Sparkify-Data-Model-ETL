# Sparkify Songplay Data Extract Transform Load (ETL)

## Introduction

This project is intended to create a postgres database for **Sparkify** platform song and artist data and combine that information with **Sparkify** songplay data to create a descriptive set of records of **Sparkify** platform song plays.

## Table of Contents
+ Installation
+ Usage
+ Database Design
+ ETL Process
+ Files
    + data (folder)
        + log_data
        + song_data
    + create_tables.py
    + etl.py
    + sql_queries.py
    + etl.ipynb
    + test.ipynb

## Installation

**Python 3**

`pip install pyscopg2`

## Usage

From the command line, run these commands:

`$ python create_tables.py`

`$ python etl.py`

## Database Design

The **Sparkify** database consists of only 5 separate tables linked by primary and foreign keys. Below are descriptions of the tables and schema. 

Table: _songplay_

Contains data to show the songs listened to by **Sparkify** platform users. Also shows the time and location of when and where the user listened to the song.

Type | Column | Type
-----|--------|------
PK | songplay_id | int
FK | start_time | timestamp
FK | user_id | int
 | level | varchar
 FK | song_id | varchar
 FK | artist_id | varchar
  | session_id | varchar
   | location | varchar
    | user_agent | varchar

Table: _user_ 

Contains data on the Sparkify platform user.

Type | Column | Type
-----|--------|------
PK | user_id | int
  | first_name | varchar
  | last_name | varchar
  | gender | varchar
  | level | varchar

Table: _song_

Contains song data.

Type | Column | Type
-----|--------|------
PK | song_id | varchar
  | title | varchar
 FK | artist_id | varchar
  | year | int
  | duration | decimal
 
 
Table: _artist_

Contains artist data.

Type | Column | Type
-----|--------|------
PK | artist_id | varchar
  | name | varchar
  | location | varchar
  | latitude | varchar
  | longitude | varchar

Table: _time_

Contains timestamp data from song listens as well as other time related.

Type | Column | Type
-----|--------|------
PK | start_time | timestamp
 | hour | int
 | day | int
 | week | int
 | month | int
 | year | int
 | weekday | int


## ETL Process

song_data **=>** insert song data into song table
song_data **=>** insert artist data into artist data

log_data **=>** extract timestamp and time information from songplay, insert into time table **=>** find artist_id and song_id from artist and song tables **=>** 
insert artist, song, and songplay data into songplay table

## Files

**data (folder)**

+ log_data
    + json records of Sparkify song plays
+ song_data
    + json records of Sparkify song and artist information

**create_tables.py**

Python module that drops tables if they exist and creates them in the database using queries from _sql_queries_.

**etl.py**

Python module that moves songplay, song and artist data from the song_data and log_data folders and inserts data into the songplay table.

**etl.ipynb**

Notebook for developing _etl.py_ module.

**sql_queries.py**

Python module that contains all SQL queries for table creation and inserts.

**test.ipynb**

Notebook for testing _etl.py_ module.
