# Code Readme - Database Skill

There are multiple files inside of this code folder, however only one holds the code that we actually implement.

## final.js
This is the code that sets up the database, parses the txt file for information, puts this information in the database, and then queries this data.

Line 13 creates or opens the underlying LevelDB store, depending on whether it exists or not.

Lines 56-66 read in the txt file, and parses it using a tab delimiter. Whenever it received the next line from parsing the file, it stores that line with a respective id. When its finished parsing it prints that it has done so to the console. 

Lines 41-53 handle a new client connection, and it is on this connection that the function readDb is called.

Lines 21 - 39 contain this readDB function, which simply reads through all the keys in the database and prints this key-value pair to the console.

## mydbfinal 
This simply contains the LevelDB

## index.html 
This contains the client code, which doesn't do anything here but has been modified for the quest. This is needed to establish this client connection to then query the data from the DB.

## smoke.txt 
This is the file that is parsed. 

Code adapted from skill17 as well as the Design Pattern – Databases + Visualization client/server side code on the class website.
