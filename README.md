# Project: Data Lake

## Introduction

A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights in what songs their users are listening to.

You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

## Deployment

First of all, you need to fill your AWS access key (AWS_ACCESS_KEY_ID) and AWS secret key (AWS_SECRET_ACCESS_KEY) in `dl-template.cfg`.

Then, please change the name of `dl-template.cfg` to `dl.cfg`.

If you are using local as your development environement, please move project directory from local to EMR with:

`scp -i <.pem-file> <local-path> <username>@<EMR-MasterNode-Endpoint>:~<EMR-path>`

Then please run spark job with:

`spark-submit etl.py --master yarn --deploy-mode client --driver-memory 4g --num-executors 2 --executor memory 2g --executor-core 2`

## ETL Pipeline

1. Read data from S3.

* Song data : s3://udacity-dend/song_data
* Log data  : s3://udacity-dend/log_data

2. Process data using spark

    #### Fact Table
    
    ##### songplays (log data associated with song plays)
    
    * songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
    
    #### Dimension Tables
    
    ##### users (information on users)
    
    * user_id, first_name, last_name, gender, level
    
    ##### songs (information on songs)
    
    * song_id, title, artist_id, year, duration
    
    ##### artists (information on artists)
    
    * artist_id, name, location, lattitude, longitude
    
    ##### time (information on time)
    
    * start_time, hour, day, week, month, year, weekday
    
3. Load it back to S3

    Write them to partitioned parquet files in table directories on S3.
