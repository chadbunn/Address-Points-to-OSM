#STEPS:

##**In QGIS**

###**Add most current address points shp file to be editied**

**1. Fix NAME = HWY issues:**

-Create a selection query with below expression:

"NAME"  =   'HWY' or  "NAME" = 'HWY 1' or  "NAME" = 'HWY 101' or  "NAME" = 'HWY 101N' or "NAME" = 'HWY 101S' 
or "NAME" = 'HWY 229' or "NAME" = 'HWY 33' or "NAME" = 'HWY 41' or "NAME" = 'HWY 46' or "NAME" = 'HWY 46 E' 
or "NAME" = 'HWY 46 WEST' or "NAME" = 'Hwy 41' or "NAME" = 'Hwy 46' 

-Start edit session and open Field Calculator

-Only update selected features.

-Check Update existing field and select NAME.

-Paste script below into Expression box:

case when "NAME" = 'HWY' then 'HIGHWAY 41' when "NAME" = 'HWY 1' then 'HIGHWAY 1' 
when "NAME" = 'HWY 101' then 'HIGHWAY 101' when "NAME" = 'HWY 101N' then 'HIGHWAY 101 NORTH' 
when "NAME" = 'HWY 101S' then 'HIGHWAY 101 SOUTH' when "NAME" = 'HWY 229' then 'HIGHWAY 229' 
when "NAME" = 'HWY 33' then 'HIGHWAY 33' when "NAME" = 'HWY 41' then 'HIGHWAY 41' 
when "NAME" = 'HWY 46' then 'HIGHWAY 46' when "NAME" = 'HWY 46 E' then 'HIGHWAY 46 EAST' 
when "NAME" = 'HWY 46 WEST' then 'HIGHWAY 46 WEST' when "NAME" = 'Hwy 41' then 'HIGHWAY 41' 
when "NAME" = 'Hwy 46' then 'HIGHWAY 46'end

-Click OK

-Clear the selection

**2. Create new Text(string) fields for "PREFIX2","TYPE2","NAME2" and "Fullname2"**

-"NAME2" is a string field with a width of 15, populate it with the following command:

title("NAME")

-Populate "PREFIX2" and "TYPE2" with following commands:

--PREFIX2, Output field width:10--

case when "PREFIX" = 'N' then 'North' when "PREFIX" = 'S' then 'South' when "PREFIX" = 'E' then 'East' 
when "PREFIX" = 'W' then 'West' when "PREFIX" = 'NO' then 'North' when "PREFIX" = 'SO' then 'South' 
when "PREFIX" = 'EA' then 'East' when "PREFIX" = 'WE' then 'West'end

--TYPE2, Output field width:10--

case when "TYPE" = 'AV' then 'Avenue' when "TYPE" = 'AVE' then 'Avenue' when "TYPE" = 'BLVD' then 'Boulevard' 
when "TYPE" = 'CIR' then 'Circle' when "TYPE" = 'CR' then 'Circle' when "TYPE" = 'CT' then 'Court' 
when "TYPE" = 'Ct' then 'Court' when "TYPE" = 'DR' then 'Drive' when "TYPE" = 'HWY' then 'Highway' 
when "TYPE" = 'LN' then 'Lane' when "TYPE" = 'LOOP' then 'Loop' when "TYPE" = 'PKWY' then 'Parkway' 
when "TYPE" = 'PL' then 'Place' when "TYPE" = 'PY'then 'Parkway' when "TYPE" = 'RD' then 'Road' 
when "TYPE" = 'ROAD' then 'Road' when "TYPE" = 'ST' then 'Street' when "TYPE" = 'TRL' then 'Trail' 
when "TYPE" = 'WAY' then 'Way' when "TYPE" = 'WY' then 'Way' end

**3. Populate "Fullname2" with following command:**

--Fullname2, Output field width:30--

concat ( tostring("ADDRESS"),' ',"PREFIX2",' ',title("NAME"),' ',"TYPE2")

**4. For Name = HIGHWAY 46 and TYPE = HWY select:**

"NAME" = 'HIGHWAY 41' and "TYPE" = 'HWY'

Then use script below in field calculator on the selected features to update the "Fullname2" field:

concat ( tostring("ADDRESS"),' ',"PREFIX2",' ',title("NAME"))

-Clear selection.

---------------------------------------------------------

**5. Populate NULL "Fullname2" values by creating the below selection queries and then using the following expressions 
in the Field Calculator to update your existing field "Fullname2".**  
###Ex.
Selection query

Field Calculator expression

###1
"PREFIX2" is NULL and "NAME" is not NULL and "TYPE2" is not NULL

concat ( tostring("ADDRESS"),' ',title("NAME"),' ',"TYPE2")

###2
"PREFIX2" is NULL and "NAME" is not NULL and "TYPE2" is NULL

concat ( tostring("ADDRESS"),' ',title("NAME"))

###3
"PREFIX2" is NULL and "NAME" is NULL and "TYPE2" is not NULL

concat ( tostring("ADDRESS"),' ',"TYPE2")

###4
"PREFIX2" is NULL and "NAME" is NULL and "TYPE2" is NULL and "ADDRESS" is not NULL

concat ( tostring("ADDRESS"))

###5
"PREFIX2" is not NULL and "NAME" is not NULL and "TYPE2" is NULL

concat ( tostring("ADDRESS"),' ',"PREFIX2",' ',title("NAME"))

###6
"PREFIX2" is not NULL and "NAME" is NULL and "TYPE2" is NULL

concat ( tostring("ADDRESS"),' ',"PREFIX2")

###7
"ADDRESS" is NULL and "PREFIX2" is NULL and "NAME" is not NULL and "TYPE2" is not NULL

concat ( title("NAME"),' ',"TYPE2")

###8
"ADDRESS" is NULL and "PREFIX2" is NULL and "NAME" is not NULL and "TYPE2" is NULL

concat ( title("NAME"))

###9
"ADDRESS" is not NULL AND "NAME" IS NULL 

concat ( tostring("ADDRESS"))

###10
"ADDRESS" is not NULL AND "NAME" is NULL AND "PREFIX2" is not NULL

concat ( tostring("ADDRESS"),' ',"PREFIX2",' ','Unknown Name ')

###11
"ADDRESS" is NULL and "PREFIX2" is not NULL and "NAME" is not NULL and "TYPE2" is not NULL

concat ( "PREFIX2",' ',title("NAME"),' ',"TYPE2")

###12
"ADDRESS" is NULL and "PREFIX2" is not NULL and "NAME" is not NULL and "TYPE2" is NULL

concat ( "PREFIX2",' ',title("NAME"))

###13
"ADDRESS" is NULL and "PREFIX2" is NULL and "NAME" is NULL and "TYPE2" is not NULL

concat('Address & Street Unknown',' ',"TYPE2")

---------------------------------------------------------

**6.SAVE EDITS**

##In ArcMap 10.1

**7. Trim Leading Zeros from "Fullname2"**

The next step is to remove the leading zeros from the addresses.  For a description of this workflow you can visit this page:

http://www.geospatialanalyst.com/2011/03/remove-leading-zeros-from-string.html

The VB script has already been saved to the X:\ at this location:

  X:\_data\Population\AddressPoints_to_OSM\TrimLeadingZeros_VB.cal

***Follow these steps to make it happen.***

a) Open the address points shp file you edited in QGIS.

b) Right-click the Fullname2 field and select the Field Calculator.

c) Set the Parser to VB Script if not already selected.

d) Load the TrimLeadingZeros_VB.cal file.

e) Replace [YOUR_FIELD] with [Fullname2] and click OK.

**Save as ADDR_PTS_PROCESSED.shp**
---------------------------------------------------------
###Now you can proceed to the ogr2osm section.

https://github.com/chadbunn/Address-Points-to-OSM/blob/master/ogr2osm.md

