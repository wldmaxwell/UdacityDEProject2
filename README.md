
**Project Two: Data Modelling with Apache Cassandra**

 

**Overview**

This project builds an ETL pipeline for a music streaming service called Sparkify by fetching data from CSV files, processing the data, and inserting the data into a Apache Cassandra Database. This project provides Sparkify with tools to analyze the song and user data to answer questions like “What songs are our customers listening to?”

**Technologies used**



*   Python - Used for ETL of CSV Files.
*   CQL 
    *   Used to drop and create Sparkify Database and tables 
    *   Run where queries to test tables returned correct data  
*   Apache Cassandra
    *   NoSQL Database used

**Information About Dataset**



*   **Data Directory: /event_data**
    *   30 CSV Files
    *   8056 rows concatenated 
*   **/event_datafile_new.csv**
    *   Smaller event data csv that will be used to insert data into Apache Cassandra tables
    *   6821 rows
*   **Song_Sessions Table**
    *   6820 rows
*   **User_Artist_Session Table**
    *   6820 rows
*   **User_Listen_History**
    *   6820 rows

**Queries to ask the following three questions of the data**


    1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4



*   **Query:** SELECT artist, song_title, song_length FROM song_sessions WHERE session_id = 338 and item_in_session = 4;
*   **Query Result:** Faithless, Music Matters (Mark Knight Dub), 495.3073 
*   **Composite Primary Key **(session_id, item_in_session)

    2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182

*   **Query:** SELECT artist, song_title, first_name, last_name FROM user_artist_session WHERE user_id = 10 and session_id = 182 ;
*   **Query Result:** 4 artists
*   **Primary Key** ((user_id, session_id), item_in_session)
    *   Composite Partition Key (user_id, session_id)
    *   Clustering Column (item_in_session)
    *   WITH CLUSTERING ORDER BY (item_in_session ASC)

    3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'

*   **Query:** SELECT first_name, last_name FROM user_listen_history WHERE song_title = ‘All Hands Against His Own’ ;
*   **Query Result:** Faithless, Music Matters (Mark Knight Dub), 495.3073 
*   **Composite Primary Key** (song_title, user_id)

	

**Database Info and Tables**

The Sparkify analytics database (Sparkify) schema is aimed to answer:



1. What was the artist, song, and song length during a session?
2. What artist, song, and user name during a user session ?
3. What users are listening to a certain song?
*   **Song_Sessions Table**
    *   6820 rows
    *   Artist Text
    *   Song_Title Text
    *   Song_Length decimal
    *   Session_id int
    *   Item_In_Session int
    *   Primary Key (session_id, item_in_session)
*   **User_Artist_Session Table**
    *   Artist Text
    *   Song_Title Text
    *   First_Name Text
    *   Last_Name Text
    *   Item_In_Session int
    *   User_id int
    *   Session_Id int
    *   Primary Key ((user_id, session_id), item_in_session)   
*   **User_Listen_History**
    *   First_Name Text
    *   Last_Name Text
    *   Song_Title Text
    *   User_Id int
    *   Primary Key (song_title, user_id)	
