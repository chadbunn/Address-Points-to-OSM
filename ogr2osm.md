#ogr2osm

1.Copy over ogr2osm folder from: 

	X:_data\Population\AddressPoints_to_OSM\ogr2osm

##Be sure your ADDR_PTS_PROCESSED.shp is in this folder.##

2.Hold shift + right-click on the ogr2osm folder and select Open command window here

3.Type: 

	python ogr2osmivan.py

and hit enter.

**If you receive an ImportError, open the OSGeo4W shell and enter (without the brackets):** 

	cd [Your_ogr2osm_folder_file_path_here]

**and hit enter. Now try step 3 again.**
	
##You should see this menu:

![ogr2osmivan menu](http://i1367.photobucket.com/albums/r788/chadbunn/ogr2osmivan_zps2ea58c5f.png?raw = true)

4.Now you are ready to convert your ADDR_PTS_PROCESSED.shp to a .OSM file.
	
Insert the following command and hit enter (be sure to remove the brackets and type in the file name for your processed address points .shp file):

	python ogr2osmivan.py [Your_ADDR_PTS_PROCESSED.shp] -t addrPts.py -e 2229 -o SLO_ADDR_PTS.osm -v
	
The program will run for a few minutes and then your .osm file for address points will be ready for conflation. Great work!

Your .osm address points layer will located in the ogr2osm folder on your machine. It will be called SLO_ADDR_PTS.osm

![You're awesome](http://cdn.arkarthick.com/wp-content/uploads/2011/11/entrepreneur-leadership-skills-good-job-whos-awesome.jpg?raw = true)
	
	
