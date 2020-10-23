# song_and_movies_analysis


## goal : visualisze my spotify data in a dashboard.
Data comes from the personal report available in the platform.  
ETL with python.  
Storage via Google Cloud Storage and Big Query.  
Dashboard  has been done with Google Data Studio. [Link here](https://datastudio.google.com/s/vwVPoXiG1iY).

## Setup steps
  - [Download personal data from from spotify](https://support.spotify.com/us/article/data-rights-and-privacy-settings/)
  - Create an app within developers.spotify.com to get a service account (key & client secret)

## Data description
All files are in json format
List of files :  
-Follow.json  
-Inferences.json  
-Payments.json  
-Playlist1.json  
-Read_Me_First.pdf  
-SearchQueries.json  
-StreamingHistory0.json  
-StreamingHistory1.json  
-StreamingHistory2.json  
-Userdata.json  
-YourLibrary.json  

### yourlibrary.json --> songs stored into your library
```
{  
 "tracks": [  
    {  
      "artist": "Green Day",  
      "album": "Nimrod",  
      "track": "All the Time"  
    },   
    {  
      "artist": "Paul McCartney",  
      "album": "Egypt Station",  
      "track": "Confidante"  
    }],  

"albums": [
    {
      "artist": "The Black Keys",
      "album": "Brothers"
    },
    {
      "artist": "Aimee Mann",
      "album": "Mental Illness"
      }],

"shows": [
    {
      "name": "Aujourd'hui l'histoire",
      "publisher": "Radio-Canada"
    },
    {
      "name": "Ctrl+A par Adviso",
      "publisher": "Adviso"
    }],
"episodes": [  ],
"bannedTracks": [  ],
"other": [  ]
}
```
### Streaming history files --> songs listened
```
[
 {
    "endTime" : "2019-07-30 12:09",
    "artistName" : "Foo Fighters",
    "trackName" : "Times Like These",
    "msPlayed" : 1509
  },
  {
    "endTime" : "2019-07-30 12:15",
    "artistName" : "Foo Fighters",
    "trackName" : "Monkey Wrench",
    "msPlayed" : 1346
  },
  {
    "endTime" : "2019-07-30 12:15",
    "artistName" : "Foo Fighters",
    "trackName" : "These Days",
    "msPlayed" : 373887
  },
]
```

## Etl steps --> extract, enrich and store the data

### Merge listening files together.
In order to work with one file.

### Cleaning data
In order to maximize performance, instead of looping over every song, create a list of distinct songs. 17000 to 5000 songs ! 

### Connect to api to get token
All doc is available via [this link](https://developer.spotify.com/documentation/general/guides/authorization-guide/).

### Enrich data : 
Looping over every song in the distinct list of song.  
Add to each song the song features available through [the song feature api](https://developer.spotify.com/documentation/web-api/reference/tracks/get-audio-features/).  
This api need the song id for each song, wich is not enclosed in the data. I have to search it.  

### Find the Id with the song name and artist.
Perform a search with song and name. An array of json results is returned, with the id inside.  

### Handling exceptions.
Sometimes, the id returned does not work. A second search is then needed to return a second id. And so on.  

### Getting the feature data for each song
Calling the api with the id.  
Storing the feature result into a csv next to song name, artist and id.  

### Saving the csv
Once the loop fully done, export data into  a csv.  
Then send the csv into cloud storage.  

In the name of Google Cloud Storage, python and big query,  
AMEN.

# Big Query structure
|type  | table / view name                          | data type           |
|----- |--------------------------------------------|---------------------|
|table | netflix_consumptionbyshow                  | crunched data       |
|table | netflix_consumptionByShowAndDate           | crunched data       |
|table | netflix_consumptionbytime                  | crunched data       |
|table | netflix_viewingActivity                    | raw data            |
|table | spotify_albums                             | raw data            |
|view  | spotify_complete_dataset                   | raw data            |
|view  | spotify_consumption_per_hour_of_day        | crunched data       |
|view  | spotify_consumption_per_hour_of_day_nokids | crunched data       |
|table | spotify_full_data                          | raw data            |
|table | spotify_meta                               | raw data            |
|table | spotify_playlist                           | raw data            |
|view  | spotify_qty_and_ratings_per_day            | crunched data       |
|view  | spotify_qty_and_ratings_per_week           | crunched data       |
|view  | Spotify_quy_and_ratings_per_dayofweek      | crunched data       |
