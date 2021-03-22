<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 0.864 seconds.


Using this HTML file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β29
* Mon Mar 22 2021 09:12:24 GMT-0700 (PDT)
* Source doc: Udacity Project two Data Model Cassandra Readme
----->


<p>
<strong>Project Two: Data Modelling with Apache Cassandra</strong>
</p>
<p>
 
</p>
<p>
<strong>Overview</strong>
</p>
<p>
This project builds an ETL pipeline for a music streaming service called Sparkify by fetching data from CSV files, processing the data, and inserting the data into a Apache Cassandra Database. This project provides Sparkify with tools to analyze the song and user data to answer questions like “What songs are our customers listening to?”
</p>
<p>
<strong>Technologies used</strong>
</p>
<ul>

<li>Python - Used for ETL of CSV Files.
</li>
</ul>
<ul>

<li>CQL  
<ul>
 
<li>Used to drop and create Sparkify Database and tables 
 
<li>Run where queries to test tables returned correct data  
<ul>

<li>Apache Cassandra 
<ul>
 
<li>NoSQL Database used
</li> 
</ul>
</li> 
</ul>
</li> 
</ul>
</li> 
</ul>
<p>
<strong>Information About Dataset</strong>
</p>
<ul>

<li><strong>Data Directory: /event_data</strong> 
<ul>
 
<li>30 CSV Files
 
<li>8056 rows concatenated 
</li> 
</ul>

<li><strong>/event_datafile_new.csv</strong> 
<ul>
 
<li>Smaller event data csv that will be used to insert data into Apache Cassandra tables
 
<li>6821 rows
</li> 
</ul>

<li><strong>Song_Sessions Table</strong> 
<ul>
 
<li>6820 rows
</li> 
</ul>

<li><strong>User_Artist_Session Table</strong> 
<ul>
 
<li>6820 rows
</li> 
</ul>

<li><strong>User_Listen_History</strong> 
<ul>
 
<li>6820 rows
</li> 
</ul>
</li> 
</ul>
<p>
<strong>Queries to ask the following three questions of the data</strong>
</p>
<p>

    1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4
</p>
<ul>

<li><strong>Query:</strong> SELECT artist, song_title, song_length FROM song_sessions WHERE session_id = 338 and item_in_session = 4;
<ul>

<li><strong>Query Result:</strong> Faithless, Music Matters (Mark Knight Dub), 495.3073 

<li><strong>Composite Primary Key </strong>(session_id, item_in_session)
<p>

    2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
</p>
<ul>

<li><strong>Query:</strong> SELECT artist, song_title, first_name, last_name FROM user_artist_session WHERE user_id = 10 and session_id = 182 ;
<ul>

<li><strong>Query Result:</strong> 4 artists
<ul>

<li><strong>Primary Key</strong> ((user_id, session_id), item_in_session) 
<ul>
 
<li>Composite Partition Key (user_id, session_id)
 
<li>Clustering Column (item_in_session)
 
<li>WITH CLUSTERING ORDER BY (item_in_session ASC)
<p>

    3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'
</p>
<ul>

<li><strong>Query:</strong> SELECT first_name, last_name FROM user_listen_history WHERE song_title = ‘All Hands Against His Own’ ;
<ul>

<li><strong>Query Result:</strong> Faithless, Music Matters (Mark Knight Dub), 495.3073 

<li><strong>Composite Primary Key</strong> (song_title, user_id)
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>
	
</p>
<p>
<strong>Database Info and Tables</strong>
</p>
<p>
The Sparkify analytics database (Sparkify) schema is aimed to answer:
</p>
<ol>

<li>What was the artist, song, and song length during a session?

<li>What artist, song, and user name during a user session ?

<li>What users are listening to a certain song?
</li>
</ol>
<ul>

<li><strong>Song_Sessions Table</strong> 
<ul>
 
<li>6820 rows
 
<li>Artist Text
 
<li>Song_Title Text
 
<li>Song_Length decimal
 
<li>Session_id int
 
<li>Item_In_Session int
 
<li>Primary Key (session_id, item_in_session)
<ul>

<li><strong>User_Artist_Session Table</strong> 
<ul>
 
<li>Artist Text
 
<li>Song_Title Text
 
<li>First_Name Text
 
<li>Last_Name Text
 
<li>Item_In_Session int
 
<li>User_id int
 
<li>Session_Id int
 
<li>Primary Key ((user_id, session_id), item_in_session)   
<ul>

<li><strong>User_Listen_History</strong> 
<ul>
 
<li>First_Name Text
 
<li>Last_Name Text
 
<li>Song_Title Text
 
<li>User_Id int
 
<li>Primary Key (song_title, user_id)	
</li> 
</ul>
</li> 
</ul>
</li> 
</ul>
</li> 
</ul>
</li> 
</ul>
</li> 
</ul>
