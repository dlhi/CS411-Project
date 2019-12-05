# CS411-Project
CAS CS411 Final Project

database.py - driver code to access database

requirements: pymongo python module

Functions:

 - init_db(): initializes database

 - init_user(username): creates a new user entry with given username and an empty playlist entry

 - input_playlist(username, playlist_name, playlist): adds playlist to user's list of playlists
    - playlist: array of [song name, link, artist name]
 
 - youtube_query_songs(username, playlist_name): returns a list of strings formatted for youtube api queries - song name concatenated to artist name
