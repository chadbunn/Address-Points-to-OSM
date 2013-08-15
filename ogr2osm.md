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

C:\_data\Population\AddressPoints_to_OSM\ogr2osm>python ogr2osmivan.py
Usage: ogr2osmivan.py SRCFILE

Options:
  -h, --help            show this help message and exit
  -t TRANSLATION, --translation=TRANSLATION
                        Select the attribute-tags translation method. See the
                        translations/ directory for valid values.
  -o OUTPUT, --output=OUTPUT
                        Set destination .osm file name and location.
  -e EPSG_CODE, --epsg=EPSG_CODE
                        EPSG code of source file. Do not include the 'EPSG:'
                        prefix. If specified, overrides projection from source
                        metadata if it exists.
  -p PROJ4_STRING, --proj4=PROJ4_STRING
                        PROJ.4 string. If specified, overrides projection from
                        source metadata if it exists.
  -v, --verbose
  -d, --debug-tags      Output the tags for every feature parsed.
  -a, --atribute-stats  Outputs a summary of the different tags / attributes
                        encountered.
  -f, --force           Force overwrite of output file. 

C:\_data\Population\AddressPoints_to_OSM\ogr2osm> 

4.Now you are ready to convert your ADDR_PTS_PROCESSED.shp to an OSM file.
	
Insert the following command and hit enter:

	python ogr2osmivan.py [Your_ADDR_PTS_PROCESSED.shp] -t addrPts.py -e 2229 -o SLO_ADDR_PTS.osm -v

	
	
