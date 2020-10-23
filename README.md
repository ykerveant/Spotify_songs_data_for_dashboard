# song_and_movies_analysis


##goal : visualisze my spotify data in a dashboard.
Data comes from the personal report available in the platform. 
ETL with python. 
Storage via Google Cloud Storage and Big Query.

##Steps
- setup :
  - dl and content from spotify : https://support.spotify.com/us/article/data-rights-and-privacy-settings/
  - create an app within developers.spotify.com to get a service account (key & client secret)

##data description
All files are in json format
List of files :
  Follow.json
  Inferences.json
  Payments.json
  Playlist1.json
  Read_Me_First.pdf
  SearchQueries.json
  StreamingHistory0.json
  StreamingHistory1.json
  StreamingHistory2.json
  Userdata.json
  YourLibrary.json

streaminghistory.json example :

yourlibrary.json :
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
Streaming history files :
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

enrich the data : merge file, connect to api. In the name of Google Cloud Storage python and big query, AMEN.
