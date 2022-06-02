# CB_Census
Population and population growth in Casco Bay watershed towns

<img
    src="https://www.cascobayestuary.org/wp-content/uploads/2014/04/logo_sm.jpg"
    style="position:absolute;top:10px;right:50px;" />


# Introduction
This archive includes R scripts, GIS Files and Excel files analyzing 
US Census Decennial Census, American Community Survey, and Annual Population 
Estimates for our region, with a focus on the 48 towns that touch the Casco Bay 
watershed.

# Statement of Purpose
CBEP is committed to the ideal of open science.  Our State of the Bay data
archives ensure the science underlying the 2020 State of the Bay report is
documented and reproducible by others. The purpose of these archives is to
release raw data and data analysis code whenever possible to allow others to
review, critique, learn from, and build upon CBEP science.

# Archive Structure
CBEP 2020 State of the Bay data analysis repositories are divided into from two
to four sub-folders.  All archives contain at least an "Original_Data" and a
"Graphics" folder.  The other two folders are only included if necessary.

- Original Data.  Original data, with a "DATA_SOURCES.md" or "READ ME.txt" file 
that documents data sources.
**DATA IN THIS FOLDER IS AS ORIGINALLY PROVIDED OR ACCESSED.** 

- Derived Data.  Data derived from the original raw data.  Includes
documentation of data reorganization steps, either in the form of files (R
notebooks, Excel files, etc.) that embody data transformations, or via README.md
or DATA_NOTES.md files.

- Analysis.  Contains one or more R Notebooks or other files proceeding through 
the data analysis steps. This often includes both preliminary data analysis --
principally graphical, and detailed analysis where necessary.

- Graphics.  Contains files stepping through development of graphics, and
also copies of resulting graphics, usually in \*.png and \*.pdf formats.  These
graphics may differ from graphics as they appear in final State of the Bay
graphical layouts.

# Summary of Data Sources
All data presented here are ultimately derived from U.S. Census data, but data
was accessed both directly from the U.S. Census website, and also indirectly 
(for historical data) from The National Historical Geographic Information 
System (NHGIS) https://www.nhgis.org/.  

Users are not permitted to redistribute NHGIS data, so original data is not 
available for data accessed through their service. Only data accessed directly
from teh US Census website are included in this archive, although some data 
derived from NHGIS data are presented in the "Derived Data" folder.
