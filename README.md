# Spotify data analysis SQL Project
![splogo](https://github.com/user-attachments/assets/5d48bcd8-1993-4c79-a6f8-54eca6905ed5)


This project is about using SQL to explore and analyze Spotify data. It includes easy to advanced queries.

---

## About the Dataset

The dataset includes:

- Artist, track, and album info  
- Music features (danceability, energy, tempo, etc.)  
- Views, likes, comments, streams  
- Licensing and video info

## Tools Used

1.PostgreSQL

2.MS Excel

## How to Use

1.Install PostgreSQL and  run pgAdmin

2.Create the table and insert data

3.Run the queries


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
```

# Queries solved
1.Tracks with more than 1 billion streams
```sql
SELECT track, artist, stream
FROM spotify
WHERE stream > 1000000000;
```
2.List all albums and their artists
```sql
SELECT DISTINCT album, artist
FROM spotify
ORDER BY artist;
```
3.Total comments on licensed tracks
```sql
SELECT SUM(comments) AS total_comments
FROM spotify
WHERE licensed = TRUE;
```
4.Tracks where album_type is 'single'
```sql
SELECT track, album
FROM spotify
WHERE album_type = 'single';
```
5.Average danceability per album
```sql
SELECT album, AVG(danceability) AS avg_danceability
FROM spotify
GROUP BY album
ORDER BY avg_danceability DESC;
```
6.Top 5 tracks by energy
```sql
SELECT track, artist, energy
FROM spotify
ORDER BY energy DESC
LIMIT 5;
```
7.Views and likes of official videos
```sql
SELECT track, views, likes
FROM spotify
WHERE official_video = TRUE
ORDER BY views DESC;
```
8.Tracks with liveness above average
```sql
Copy
Edit
SELECT track, liveness
FROM spotify
WHERE liveness > (SELECT AVG(liveness) FROM spotify);
```
9.Energy range per album (using CTE)
```sql
Copy
Edit
WITH energy_diff AS (
    SELECT album,
           MAX(energy) AS max_energy,
           MIN(energy) AS min_energy
    FROM spotify
    GROUP BY album
)
SELECT album, (max_energy - min_energy) AS energy_range
FROM energy_diff
ORDER BY energy_range DESC;
```
10.Tracks where energy/liveness > 1.2
```sql
SELECT track, energy, liveness,
       (energy / NULLIF(liveness, 0)) AS energy_liveness_ratio
FROM spotify
WHERE (energy / NULLIF(liveness, 0)) > 1.2;
```


