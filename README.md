<img src="weston-mackinnon-3pCRW_JRKM8-unsplash.jpg" width="1250" height="250">
Photo by <a href="https://unsplash.com/@betteratf8?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Weston MacKinnon</a> on <a href="https://unsplash.com/s/photos/sheet-music?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>

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
null | level | varchar
FK | song_id | varchar
FK | artist_id | varchar
null | session_id | varchar
null| location | varchar
null | user_agent | varchar

Table: _user_ 

Contains data on the Sparkify platform user.

Type | Column | Type
-----|--------|------
PK | user_id | int
null | first_name | varchar
null | last_name | varchar
null | gender | varchar
null | level | varchar

Table: _song_

Contains song data.

Type | Column | Type
-----|--------|------
PK | song_id | varchar
null | title | varchar
FK | artist_id | varchar
null | year | int
null | duration | decimal
 
 
Table: _artist_

Contains artist data.

Type | Column | Type
-----|--------|------
PK | artist_id | varchar
null | name | varchar
null | location | varchar
null | latitude | varchar
null | longitude | varchar

Table: _time_

Contains timestamp data from song listens as well as other time related.

Type | Column | Type
-----|--------|------
PK | start_time | timestamp
null | hour | int
null | day | int
null | week | int
null | month | int
null | year | int
null | weekday | int


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
