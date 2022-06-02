# Data Preparation
Much of this data preparation workflow was conducted by hand. Automated data
preparation in R would be easier to check and QA/QC, but at the time we
imported these data, we had not shifted fully to using automated data QA/QC and
transformation.

# GIS data
"Casco_Bay_Towns.shp" and 
"Casco_Bay_Towns_Land.shp"

These two layers were derived from U.S. Census "Tiger Line Files"", contained in
a source shapefile, "tl_2019_23_cosub.shp", as follows.

We used the "Dissolve" tool to convert separate polygons labeled as part of each
town into single multipolygon feature. Multipolygons that touch the Casco Bay 
watershed were selected using "Select by Location" and the selected shapes saved 
as "Casco_Bay_Towns.shp".

Note that these boundaries differ from the boundaries derived from the Maine
Geolibrary Town and Townships data.  In particular, the U.S Census data does not
divide Albany and Mason Townships, but combines them with Batchelder's Grant
Township (and others?) as "south oxford".  Other differences, especially in
smaller details may also exist.

Data was then clipped to land by clipping it to the aggregate
Maine_Land_Area.shp layer (itself derived as the union of all county polygons
from Maine Geolibrary's county boundaries, omitting areas that were not mapped
as land). That produces "Casco_Bay_Towns_Land.shp".

# American Community Survey Population Estimates
## Population Estimates 2010-2018
Town by Town Population 2010-2018 estimates were derived from ACS estimates 
as follows:  

1.  Original data is from "sub-est2018_33.csv". The file contains estimates for
    a variety of different type of census subunits, but ONLY data for Maine.
    
2.  We want to line up with our geographic data, which is based on county 
    subunits -- that is, towns and townships in Maine parlance. Metadata 
    suggests those values are identified in the table by `SUMLEV == 61`.

3.  Open CSV file in Excel  
    *  Sort by SUMLEV.  
    *  Delete other categories  
    *  Save as "ME_Town_Pop_Est 2010.2019.csv"  (Not retained here.)

4.  These data can be matched up with Casco Bay Town data by matching county 
    subunit codes.  Unfortunately, the codes in the GIS layer are character 
    strings, while the codes from the CSV file are interpreted as numbers, so we
    need to create a numeric match code in the GIS shapefile,
    "Casco_Bay_Town_Land"."

    *  Open Attribute Table
    *  Add Field.  Name = "MatchCode"; short integer, precision = 6;
    *  Right click on the "MatchCode" column; Field Calculator; 
       MatchCode = [COUSUBFP].  (this correctly converts from string to number)

5.  Join the Population Data Tables to the GIS Layer.  That MatchCode works to 
    import population estimates (via a "Join") into GIS. Note that some areas 
    may not match. 
    *  Join....  MatchCode.... COSUB

6. Export attribute table as "CB_Town_Pop_Est 2010.2018.csv"

7. 4. 
Simplify data to remove unneeded columns, reorder columns to include:

|  Variable Name       |
|----------------------|
|  NAME                |
|  NAMELSAD            |
|  ALAND               |
|  AWATER              |
|  COUSUB              |
|  CENSUS2010POP       |
|  ESTIMATESBASE2010   |
|  POPESTIMATE2010     |
|  POPESTIMATE2011     |
|  POPESTIMATE2012     |
|  POPESTIMATE2013	   |
|  POPESTIMATE2014     |
|  POPESTIMATE2015     |
|  POPESTIMATE2016     |
|  POPESTIMATE2017     |
|  POPESTIMATE2018     |


## Population Estimates 2000-2010
Town by Town Population 2000-2010 estimates were derived from source ACS 
data as follows:  

1.  Open file "sub-est00int.csv"
    *  Select only Maine locations.  Data is already sorted by state.  Delete 
    all rows that do not correspond to Maine.  Save as  
    "ME_Town_Pop_Est_2000.2010.csv"

2.  We want to select only data that will line up with our geographic layer,
    derived from the Tiger Line files.  The Tiger files which is based on county 
    subunits -- that is, towns and townships in Maine parlance.  The metadata 
    suggests those estimates are identified by SUMLEV = 61.

3.  Open CSV file in Excel
    *  Sort by SUMLEV.
    *  Delete other categories (all rows with SUMLEV != 61)
    *  Simplify data table by dropping data columns.  Keep the following:

|  Variable Name       |
|----------------------|
|  COUSUB              |
|  NAME                |
|  STNAME              |
|  ESTIMATESBASE2000   |
|  POPESTIMATE2000     |
|  POPESTIMATE2001     |
|  POPESTIMATE2002     |
|  POPESTIMATE2003     |
|  POPESTIMATE2004     |
|  POPESTIMATE2005     |
|  POPESTIMATE2006     |
|  POPESTIMATE2007     |
|  POPESTIMATE2008     |
|  POPESTIMATE2009     |
|  CENSUS2010POP       |
|  POPESTIMATE2010     |

    *  Save as "ME_Town_Pop_Est 2000.2010.csv"  (Not retained here.)
 

4.  Import 2000-2010 estimates into ArcGIS.
    *  Join with the Casco_Bay_Towns_Land.shp geographic data by
    matching `MatchCode` from the GIS data with `COSUB` from these data.
    
5.  Export attribute table as "CB_Town_Pop_Est_2000.2010.csv"  This adds
    Geographic Codes and details from GIS to the exported data.


# Combined Population Estimates
Open Two CB population data files just created
     *  "CB_Town_Pop_Est_2000.2010.csv"  
     *  "CB_Town_Pop_Est 2010.2018.csv"  

and combine them column wise, as follows:


1.  Copy and paste all data into a new CSV file:
"CB_Population_1970-2018_Combined.csv"
   *  Since all were exported after joins to the same attribute table in GIS,
      rows should all line up, but to be sure, we used simple formulas in Excel
      to check that MatchCode and NAME aligned.  They all did.

2.  Rename Columns for the census data to make clear that is what they are.
   *  AV0AA1970 -> Census 1970
   *  AV0AA1980 -> Census 1980
   *  AV0AA1990 -> Census 1990
   *  AV0AA2000 -> Census 2000
   *  AV0AA2010 -> Census 2010

3.  Simplify data by deleting duplicated identifier information

4.  Further Simplify by deleting duplicated Census Data.  In particular, Census 
    2010 data is listed in several places.

5.  Rename Estimate data columns, but be aware that there is a jump in estimates
    across the U.S  Census years, so you need to keep both before and after 
    census population estimates for consistency.  Note that Estimates Base, 
    Estimates, and Census numbers for the same year are not the same.  
    Differences are generally small, but not zero.

   *  ESTIMATESBASE2000 -> Base 2000
   *  POPESTIMATE2000   -> Estimate 2000
   *  POPESTIMATE2001   -> Estimate 2000
   *  POPESTIMATE2002   -> Estimate 2000
   *  POPESTIMATE2003   -> Estimate 2000
   *  POPESTIMATE2004   -> Estimate 2000
   *  POPESTIMATE2005   -> Estimate 2000
   *  POPESTIMATE2006   -> Estimate 2000
   *  POPESTIMATE2007   -> Estimate 2000
   *  POPESTIMATE2008   -> Estimate 2000
   *  POPESTIMATE2009	  -> Estimate 2000
   *  POPESTIMATE2010   -> Estimate 2000
   *  ESTIMATESBASE2010 -> Base 2010
   *  POPESTIMATE2010   -> Estimate 2000 v2010
   *  POPESTIMATE2011   -> Estimate 2000
   *  POPESTIMATE2012	  -> Estimate 2000
   *  POPESTIMATE2013   -> Estimate 2000
   *  POPESTIMATE2014   -> Estimate 2000
   *  POPESTIMATE2015   -> Estimate 2000
   *  POPESTIMATE2016   -> Estimate 2000
   *  POPESTIMATE2017   -> Estimate 2000
   *  POPESTIMATE2018   -> Estimate 2000


This leaves us with the following data columns:

|  Variable Name        |     Contents                                         |
|-----------------------|------------------------------------------------------|
|  NAME                 |  Town Name -- Short Form
|  NAMELSAD             |  Town Name -- Long Form
|  ALAND                |  Area of Land within the Census Area (usually a town)
|  AWATER               |  Area of Water within the Census Area (usually a town)
|  COUSUB               |  Match Code for this specific Geography in Census Records
|  Base 2000            |  Base used to caculate ACS population estimates 2000-2010
|  Estimate 2000        |  ACS Population Estimates
|  Estimate 2001        |
|  Estimate 2002        |
|  Estimate 2003        |
|  Estimate 2004        |
|  Estimate 2005        |
|  Estimate 2006        |
|  Estimate 2007        |
|  Estimate 2008        |
|  Estimate 2009        |
|  Estimate 2010        | Estimated 2010 population, based on 2000 Base
|  Base 2010            | Base used ACS population estimates 2010-2018
|  Estimate 2010 v2010  | This is the estimate of population in 2010, derived from Base 2010
|  Estimate 2011        | ACS Population Estimates
|  Estimate 2012        |
|  Estimate 2013        |
|  Estimate 2014        |
|  Estimate 2015        |
|  Estimate 2016        |
|  Estimate 2017        |
|  Estimate 2018        |


# Data Manipulation in R

"CB_Total_Pop.csv"
"CB_Towns_Growth_Rates.csv"

We processed "CB_Population_2000-2018_Combined.csv" in R to produce certain 
summaries and rates.  Steps are documented in the R Notebook 
"Census Reorganization and Summaries.Rmd".

We provide totals and growth rates only for the period 2000 through 2018, based
on the American Community Survey 2000-2018, because older (pre-2000) historical
census data was available through a web portal (The IPUMS National Historical
Geographic Information System) that does not permit data redistribution.  We
could not find historical data at the level of resolution we needed from the
U.S. Census web portals. Furthermore, the analysis of older census data is
complicated because of changes in census areas over time, especially at smaller
spatial scales (census tracts and blocks).

##  Generate Total Regional Population Numbers

"CB_Total_Pop.csv"

Total Population data for the 48 (+) town area is provided in:
"CB_Total_Pop.csv"  This provides data on total population of the 48 "Towns" 
(really, County Subdivisions) that touch the Casco Bay Watershed. 


Here are the meaning of each data columns:

|  Variable Name   |  Content
|------------------|----------------------------------------------------------|
|  [Blank]         |  Arbitrary Row Numbers                                   |
|  Group           |  Source of estimate  -- "Base", "Estimate" or "Estimate2"|
|  Year            |  Year of population estimate                             |
|  Total           |  Total population of 48 Casco Bay watershed Towns        |

The `Group` variable refers to different sources of estimates that were included
in the source ACS data,  "Base" refers to the "base Population" used to
calculate estimates for each 10 year period.  "Estimate" provides the regular
estimate from the ACS for each year.  For the decade year of 2010, two decades
overlap, so the ACS provides three population figures: an estimate based on the 
ACS data from the previous decade (2000 through 2010), a new "base" population 
figure, and a new estimate derived from that new base and other ACS data.  This 
third population estimate is placed in Group = "Estimate2". 

Differences among the three population values are small, so not generally
material to our analysis.  We used "Estimate" throughout,
with the recognition that the change-over from 2000-2010 ACS estimates to 2010-2018
estimates involves a small adjustment (~ 300 people out of ~ 370,000, so 
less than 0.1%) in year 2010.


#E Generate Growth Rate Estimates

'CB_Towns_Growth_Rates.csv'

Town by Town growth rate data (along with related on the first year each town 
appears in the record and selected population estimates) were exported as
'CB_Towns_Growth_Rates.csv'

It does this by direct calculation based on the first and last population 
estimate ONLY in each time interval and calculating the annual (exponential) 
rate of growth that would lead to the estimated population change. (Note that 
this is not quite the same as calculating an annual rate of growth based on a 
linear model on transformed data).


Here are the meaning of each data columns:

|  Variable Name   |  Content
|------------------|----------------------------------------------------------|
|  [Blank]         |  Arbitrary Row Numbers                                   |
|  NAME            |  Name of the Town (Shorter Form)                         |
|  NAMELSAD        |  Name of Town (Longer Form)                              |
|  COUSUB          |  Census Code for geography, here the "County Subunit"  or Town |
|  FirstYr         |  First year with a recorded population estimate (NOT first year of town) |
|  ACSFirstYr      |  First Year the town appears in the ACS estimates        |
|  ACSPop2000      |  ACS Population Estimate 2000                            |
|  ACSPop2010Left  |  ACS Population Estimate 2010, based on the prior decades model and methods |
|  ACSPop2010Right |  ACS Population Estimate 2010, based on subsequent decade's model and methods. |
|  ACSPop2018      |  ACS population estimate for 2018                        |
|  ACSAnnRate      |  Annual growth rate (percent) 2000-2018 based on ACS estimates     |
|  ACS2000AnnRate  |  Annual growth rate 2000 to 2005                         |
|  ACS2005AnnRate  |  Annual growth rate 2005 to 2010                         |
|  ACS2010AnnRate  |  Annual growth rate 2010 to 2015                         |
|  ACS2015AnnRate  |  Annual growth rate 2015 to 2018                         |
|  ACSGrowth       |  Total growth from 2000 through 2018 (percent).          |

