# sparkify-postgresql

DISCLAIMER: This project was completed as part of the "Data Engineering - Udacity Nanodegree". 

## Local execution

Assuming PostgreSQL is installed on your UNIX machine, use the following commands to start/stop the DB server.

```
# start the postgresql server
sudo service postgresql start

# stop the postgresql server
sudo service postgresql stop
```

Having started the server, execute the following statements (required only once):

```
# create the user `student`
sudo -u postgres psql -c "CREATE USER student WITH PASSWORD 'student' CREATEDB;"

# create the database `studentdb`
sudo -u postgres psql -c "CREATE DATABASE studentdb WITH ENCODING 'utf8' TEMPLATE template0;"
```

Following the database creation, run the following scripts:

```
# run the `create_tables.py` script
python3 create_tables.py

# run the `etl.py` script
python3 etl.py
```

## Database design

We follow a denormalized table design to ensure quick retrieval and avoid expensive join operations as much as possible. The schema in questions, here, is the star schema, which is composed of fact and dimension tables.

### Fact Table

- `songplays` - records in log data associated with song plays i.e. records with page NextSong 
    - `(songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent)`

### Dimension Tables

- `users` - users in the app 
    - `(user_id, first_name, last_name, gender, level)`
- `songs` - songs in music database 
    - `(song_id, title, artist_id, year, duration)`
- `artists` - artists in music database 
    - `(artist_id, name, location, latitude, longitude)`
- `time` - timestamps of records in songplays broken down into specific units 
    - `(  start_time, hour, day, week, month, year, weekday)`

## Scripts involved
### `sql_queries.py`
The file contains all the CREATE, INSERT, SELECT queries for the tables required.

### `create_tables.py`
This script contains the code to drop existing tables and create new tables from scratch.

### `etl.py`
This executes the ETL pipeline for this particular dataset.