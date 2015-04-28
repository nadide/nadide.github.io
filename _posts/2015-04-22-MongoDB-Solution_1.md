---
layout: post
title: Data Wrangling with MongoDB - Problem 1 Solutions
---

### Solution for the problem 1 

The task was simple for the first problem. We need to parse the given csv data into lists in Python. CSV data is from NREL (National Renewable Energy Laboratory) website. Each file contains information from one meteorological station, in particular - about amount of solar and wind energy for each hour of day.

Here is the first 3 lines of the data.

```
745090,"MOUNTAIN VIEW MOFFETT FLD NAS",CA,-8.0,37.400,-122.050,12
Date (MM/DD/YYYY),Time (HH:MM),ETR (W/m^2),ETRN (W/m^2),GHI (W/m^2),GHI source,GHI uncert (%),DNI (W/m^2),DNI source,DNI uncert (%),DHI (W/m^2),DHI source,DHI uncert (%),GH illum (lx),GH illum source,Global illum uncert (%),DN illum (lx),DN illum source,DN illum uncert (%),DH illum (lx),DH illum source,DH illum uncert (%),Zenith lum (cd/m^2),Zenith lum source,Zenith lum uncert (%),TotCld (tenths),TotCld source,TotCld uncert (code),OpqCld (tenths),OpqCld source,OpqCld uncert (code),Dry-bulb (C),Dry-bulb source,Dry-bulb uncert (code),Dew-point (C),Dew-point source,Dew-point uncert (code),RHum (%),RHum source,RHum uncert (code),Pressure (mbar),Pressure source,Pressure uncert (code),Wdir (degrees),Wdir source,Wdir uncert (code),Wspd (m/s),Wspd source,Wspd uncert (code),Hvis (m),Hvis source,Hvis uncert (code),CeilHgt (m),CeilHgt source,CeilHgt uncert (code),Pwat (cm),Pwat source,Pwat uncert (code),AOD (unitless),AOD source,AOD uncert (code),Alb (unitless),Alb source,Alb uncert (code),Lprecip depth (mm),Lprecip quantity (hr),Lprecip source,Lprecip uncert (code)
01/01/2005,01:00,0,0,0,2,0,0,2,0,0,2,0,0,2,0,0,2,0,0,2,0,0,2,0,3,E,9,3,E,9,8.0,A,7,6.0,A,7,87,A,7,1013,A,7,150,A,7,2.1,A,7,16100,A,7,77777,A,7,1.1,E,8,0.099,F,8,0.160,F,8,0,1,A,7

```
As you realized, the data has a different style. In first line we have an information about the data source, then second line is a header and then the data actually starts from the third line. 

Here is the code provided in the beginning.

```Python
import csv
import os

DATADIR = ""
DATAFILE = "745090.csv"


def parse_file(datafile):
    name = ""
    data = []
    with open(datafile,'rb') as f:
        pass
    # Do not change the line below
    return (name, data)


def test():
    datafile = os.path.join(DATADIR, DATAFILE)
    name, data = parse_file(datafile)

    assert name == "MOUNTAIN VIEW MOFFETT FLD NAS"
    assert data[0][1] == "01:00"
    assert data[2][0] == "01/01/2005"
    assert data[2][5] == "2"


if __name__ == "__main__":
    test()

```

What we need to do is to change only parse_file function to achieve parsing csv into list. There are two hints for us to use. csv.reader and next() is to things to make our task easier. 

Here is my approach to problem. I need name  and data which are taken from the datafile. For name I need to get the first lines second column. For data I need to gather from third line.

```Python
def parse_file(datafile):
	
	# First initialized name and data.
    name = ""
    data = []

    # Open datafile to read
    with open(datafile,'rb') as f:
    	# Reading csv, when reading done go to next one.
    	reading1 = csv.reader(f).next()
    	# Get the second element in the first list for the name
    	name = list(reading1)[1]
    	# reading again csv
    	reading = csv.reader(f)
    	# Go to next line again.
    	next(f)
    	# get the data from reading as a list.
    	data = list(reading)
    # Get name and data as a tuple.
    return (name, data)
```

