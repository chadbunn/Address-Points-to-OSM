#ogr2osm

1.Copy over ogr2osm folder from: 

	X:_data\Population\AddressPoints_to_OSM\ogr2osm

##Be sure your ADDR_PTS_Processed.shp is in this folder.##

2.Hold shift + right-click on the ogr2osm folder and select Open command window here

3.Type "python ogr2osmivan.py" and hit enter.

**If you receive an ImportError, open the OSGeo4W shell and enter (without the brackets):** 

cd [Your_ogr2osm_folder_file_path_here]

**and hit enter. Now try step 3 again.**
	
##You should see this menu:

![ogr2osmivan menu](http://postimg.org/image/473eqtr5v/

C:\_data\Population\AddressPoints_to_OSM\ogr2osm> 

4.Now you are ready to convert your ADDR_PTS_PROCESSED.shp to an OSM file.
	
Insert the following command and hit enter:

	python ogr2osmivan.py [Your_ADDR_PTS_PROCESSED.shp] -t addrPts.py -e 2229 -o SLO_ADDR_PTS.osm -v

	
	
