# GIS DATA

GIS data was derived from Census "Tiger files" data. The data was 
originally downloaded by By Curtis C. Bohlen, December 4, 2019.

Data was accessed through the U.S. Census web page, at
https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-line-file.html
And specifically, from the site linked to from the "web interface" button at the 
bottom of the page. The button brings you to a query page at:
https://www.census.gov/cgi-bin/geo/shapefiles/index.php.  Following the obvious
steps leads to 
https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2019&layergroup=County+Subdivisions

The downloaded zip file in the "Original_Data"" folder is
"tl_2019_23_cosub.zip." when unzipped, it provides a shapefile of "County
Subunits" used by the Census in 2019.  These correspond (roughly) to town
boundaries. Thus the source data for our census analysis is from 
"tl_2019_23_cosub.shp".

Note that these boundaries differ from the boundaries derived from the Maine
Geolibrary Town and Townships data.  In particular, the U.S Census data does not
divide Albany and Mason Townships, but combines them with Batchelder's Grant
Township as "south oxford".  Presumably, this is because data for those 
townships is aggregated for census purposes.   Other differences, especially in
detail, may also exist.

# 2000 and 2010 Census Data
"DEC_00_SF1_DP1_with_ann.csv"

"DEC_10_SF1_SF1DP1_with_ann.csv"

Data was downloaded from the U.S. Census website manually by Curtis C. Bohlen 
on December 9, 2019 and December 12, 2019.  Data was accessed through the
American Fact Finder interface.

https://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml

We download all County Subdivisions, Table DP-1 for 2000 and 2010 census.
The resulting downloaded ZIP file arrived as "aff.download(1).zip", but we
renamed the file to to "Towns.zip". The Source files are available after
unzipping the compressed file.

These data are presented here for convenience, but they were not used in the 
State of Casco Bay report.

# American Community Survey Population Estimates 
## Population Estimates 2010-2018

"sub-est2018_33.csv"

Data was downloaded from the U.S. Census website manually by Curtis C. Bohlen 
on December 9, 2019.  Data was accessed via the following link:

https://www.census.gov/data/datasets/time-series/demo/popest/2010s-total-cities-and-towns.html

It took a while to figure out which available data files correspond to the
Tiger Line files we downloaded. We needed "Subcounty Resident Population
Estimates".  The file for Maine was downloaded as "sub-est2018_33.csv"  (The
number 33  appears to refer to the state of Maine.)

## Population Estimates 2000-2009

"sub-est00int.csv"

Data was downloaded from the U.S. Census website manually by Curtis C. Bohlen
on December 13, 2019 from:

https://www.census.gov/programs-surveys/popest.html
(access to recent data -- no longer leads to 2000-2010 vintage data)

The data is currently available at:
https://www.census.gov/data/datasets/time-series/demo/popest/intercensal-2000-2010-cities-and-towns.html

this link is to something called "Intercensal Estimates of the Resident 
Population for Incorporated Places and Minor Civil Divisions: April 1, 2000 to 
July 1, 2010".  

CAUTION:  This file contains population estimates for overlapping geographies.
Check the metadata describing the file contents before analysis.
