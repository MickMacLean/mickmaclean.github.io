## BTS Database Project

### Project at a glance
**Construct a database with data on every BTS song such that the data will be in an easily comparable format.** 

방탄소년단, Bangtan Sonyeondan, also known as BTS, is a South Korean boyband under Big Hit Entertainment whose extensive and diverse discography has garnered them a plethora of awards and millions of passionate fans dedicated to their socially-conscious music. 

With over 350 songs, their discography presents a prime opportunity to collect and explore data and its trends further.

As an avid fan myself, I am interested in understanding their music lyrically and emotionally, and as someone passionate about data, I'm interested in the analytics of their music. My main goal is to construct a database where I can store data in an easily comparable format to serve as an encyclopedia of information, as well as provide a simple way to compare the stats of each song, category, and query based on tags.
Construct a user-friendly website to display these data for fans to access and use for their own purposes.
Want data in an easily comparable format, serve as an encyclopedia of information.

**Tools:** SQL, Excel

**Primary skills:** data collection, data management, databases, 
  
 ### Structure
 The overall focus of this data is with respect to the songs themselves, and as a result I have focused the structure of this database around the songs. This results in a lot of intermediary tables due to every category of data being a many to many relationship of each category to the songs. I am currently testing this structure with a small portion of the data
 <img src="images/btsdata_schema.png" width=300>

  
Much of this data must be collected manually as there is no central site which contains all of the data to be included. Data currently taken from Korea Music Copyright Assosiation (KOMCA), Genius, Hypable, and the official Spotify and YouTube of the band.
Example dataset with information; one album of information is displayed below.

This project is in its early stages of development.

### The Data
The data to be included for each song is as follows:
  - Song title, English and Korean/Japanese
  - Release date
  - Album(s) on which it is included
  - Writers
  - Producers
  - Choreographers
  - Singers
  - Genre
  - Themes
  - Remixes
  - Awards, nominated and received 
  - Performances, where and when
  - Streams, first week and current
  - Music video

#### Songs
many songs have multiple titles depending on the language and translation chosen eg Baepsae can be called crow tit, try hard, silver spoon etc.
Songs frequently appear on multiple albums.

#### Writers, Producers, & Performers
While the band has 7 members, not all are featured on every song; units such as rap-line and vocal-line, as well as other random groupings, solos, and separate artist features are common on most albums. 
This table begins with the 7 members, then common features (usually from within the company), then external features. 

The writers and producers overlap substantially (with the performers as well) so there is potential for turning these 3 into one table. However, the intermediary table would likely end up being very large with the possibility of 20 attributes per song, so for now they are separate tables.

####Genres
while the whole of bts' discography is classified as kpop and sometimes hip-hop, dance pop, etc., their music has a variety of influences that are important for me to distinguish. Thus categorization is a bit subjective and given my lack of music genre knowledge, I will be asking others for their input via social media.

