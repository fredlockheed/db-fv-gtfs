# Unofficial DB Fernverkehr Timetable GTFS Feed

Deutsche Bahn (German Railways) now publishes its long-distance trains timetable via [REST-like API](http://data.deutschebahn.com/apis/fahrplan/) under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

This is a big step forward one can now legally access timetables of the German Railways. The API provides the following operations:

* search the stop via title or input string;
* get arrivals or departure board for the given stop and date/time;
* get a train run (you have to start from the entry in the arrivals or departure board).

Still, most real-world timetable applications are not possible with just an API. For instance, for timetable-based routing or spatial-temporal analysis you will need the whole dataset at once.

Since the API essentially returns static data, it is possible to rebuild the whole timetable in the  [GTFS](https://developers.google.com/transit/gtfs/) format, it just takes time.

To save you the effort, this repository provides the complete timetable of the DB Fernverkehr in GTFS format.  
GTFS feeds are provided per full timetable period.

# Downloads

Please refer to the [releases](https://github.com/fredlockheed/db-fv-gtfs/releases) page.

# How these GTFS Files are Produced

Provided GTFS files are produced using the [db_to_gtfs.py](https://raw.githubusercontent.com/patrickbr/db-api-to-gtfs/master/db_to_gtfs.py) Python script from the [db-api-to-gtfs](https://github.com/patrickbr/db-api-to-gtfs) project. (It is done without any knowledge of, consent of or endorsment from the author of the [db-api-to-gtfs](https://github.com/patrickbr/db-api-to-gtfs) project.)

# Instructions

Anyone with enough server resources an patience can produce the provided GTFS feed. Instructions:

* Request a DB Fahrplan API key via [DBOpenData@deutschebahn.com](mailto:DBOpenData@deutschebahn.com?subject=Fahrplan-API Key)
* Launch an AWS EC2 Instance
  * Prefer EU (Frankfurt) region
  * Prefer Debian GNU/Linux 8 (Jessie) AMI
  * Recommended `m4.xlarge` instance size due to memory and network resources
* Connect via `ssh`
* Execute:  
```
sudo apt-get update
sudo apt-get ugrade
sudo apt-get install git
sudo apt-get install python-pip
sudo pip install docopt
sudo pip install python-dateutil
sudo pip install unicodecsv
git clone https://github.com/patrickbr/db-api-to-gtfs.git
cd db-api-to-gtfs
nohup ./db_to_gtfs.py --api-key <API_KEY> --start-date 2015-12-13 --end-date 2016-12-11 > std.txt 2> err.txt &
tail -f std.txt`
```
* Wait for approximately 2 days until the script finishes
* Download the data

# License

GTFS feed in this repository is provided under the [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/) license.

# Attribution

GTFS feed in this repository is produced based on the [DB Fahrplan API](http://data.deutschebahn.com/apis/fahrplan/), published by the DB Vertrieb GmbH, which is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). No endorsement of the DB Vertrieb GmbH is implied.

Apart from the formatting as GTFS feed, the data was not intentionally changed.

# Legal Aspects

DB OpenData Portal states that the data of the DB Fahrplan API is provided under the CC BY 4.0 license:

> Die Daten dieser API werden bereitgestellt unter der Lizenz [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

There are no limitations on downloading the data using scripts or similar technical means, in any volume. The license directy permits "remix, transform, and build upon the material for any purpose".

According to our reading of the license of the DB Fahrplan API, publication of this GTFS feed und the same license is perfectly legal.
