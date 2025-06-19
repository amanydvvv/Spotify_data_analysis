# Spotify SQL Project

This project is about using SQL to explore and analyze Spotify data. It includes easy to advanced queries and a simple example of query optimization.

---

## About the Dataset

The dataset includes:

- Artist, track, and album info  
- Music features (danceability, energy, tempo, etc.)  
- Views, likes, comments, streams  
- Licensing and video info

### Table Schema

```sql
CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);


Easy Queries
Tracks with more than 1 billion streams
```sql
SELECT track, artist, stream
FROM spotify
WHERE stream > 1000000000;

List all albums and their artists


Total comments on licensed tracks

Find all tracks where album_type = 'single'

Medium Queries
Average danceability per album

Top 5 tracks by energy

Views and likes of tracks where official_video = TRUE

Total views for each album

Advanced Queries
Top 3 most-viewed tracks per artist using window functions

Tracks where liveness > average liveness

Difference between max and min energy in albums (with CTE)

Tracks where energy/liveness > 1.2

