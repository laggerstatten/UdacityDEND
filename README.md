# BACKGROUND

## Fictional
Sparkify is an online music streaming service, in which users can select songs to listen to and play them. The company records these listening events and has demographic information about their users. Additionally they have information about the music in their collection. The Sparkify team wants to combine information from their listening events log with their song information in order to gain insight into user behavior. This database exists in order to synthesize data from two separate data sets, a log of customer listening events and information describing songs in the library.

## Real
Sparkify is a model of an online music streaming service, similar to Spotify or Pandora. The dataset for the songs comes from the [Million Song Dataset] (http://millionsongdataset.com/) and the dataset for the user behavior was generated using the [Eventsim event simulator] (http://millionsongdataset.com/). The database is implemented using Python and Postgres.


# STRUCTURE & ETL PIPELINE

The database consists of 5 tables, a fact table (songplays) and four dimension tables (users, songs, artists, and time). These are assembled in a star schema, with each of the four dimension tables providing attribute information for the songplays fact table. Each table reflects a real-world entity within the scope of the Sparkify project. A "songplay" is an event in which a user plays a song on the app. This event necessarily involves a user and a song, and occurs at a time. Additionally, every song must have an artist.

Data about songs is found in JSON files within a song_data directory. These JSON files contain more data than is used for the Sparkify project, so during the ETL process, relevant columns are used to construct a new "songs" table, while other columns are used to construct the "artists" table. This decomposition into two separate tables is part of the normalization process, in order to separately describe the songs and artists entities.

Data about song play events is also found in JSON files in a log_data directory. During the ETL process, data about the users is extracted to a separate "users" table. Timestamp data is also used to construct a separate "time" table with derived attributes as part of the date heirarchy.

A *song_id* and an *artist_id* field serve as keys to relate the songplays table to the songs and artists tables respectively. During the ETL process, song and artist data are brought into the songplays table when a relationship exists.

![Star Schema ERD](/sparkify_erd.png)


# INSTRUCTIONS

This process is run through the terminal. The user first runs **create_table.py**, followed by **etl.py**.


# CONTENTS

**create_table.py** - this file creates the database and its constituent tables, using SQL queries found in the **sql_queries.py** file
**etl.py** - this file reads the JSON files and performs the steps in the ETL pipeline to populate the tables in the database
**sql_queries.py** - this file contains the SQL queries used by **create_table.py** and **etl.py**
**test.ipynb** - this notebook file can be used to query tables before and after running the python code in order to determine success or failure of the process
**etl.ipynb** - this notebook file was used in development of the ETL pipeline
**data** - this directory contains all of the JSON files
