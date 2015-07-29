# otl-metromerger
Metropolitan merger simulation with Leaflet choropleth map framework for On The Line project (http://OnTheLine.trincoll.edu)

## Demo-in-progress
http://jackdougherty.github.io/otl-metromerger

## To Do
- later add additional data variables (taxable property, school districts, etc.) and improve display

## Notes on building this
1) Begin with Leaflet choropleth tutorial at http://leafletjs.com/examples/choropleth.html

2) Create simplified geoJson layer of Connecticut town boundaries
- Download town boundaries shapefile from UConn MAGIC http://magic.libraries.uconn.edu
- Simplify the polygon shapes to reduce size in geoJson format with this general approach http://chimera.labs.oreilly.com/books/1230000000345/ch12.html#_simplify_the_shapes
- Use MapShaper web tool (http://www.mapshaper.org/) to reduce size without changing too much detail. In this case, I reduced Connecticut boundaries down to 1.5%, around 100k.
- Export "shapefile - polygons", then copy and rename new .shp and .shx files into new folder with original .dbf (to retain data) and original .prj (projection) files

3) Join spreadsheet town data to the new simplified polygon shapefile
- in GIS application (such as ArcGIS or QGIS), load the new simplified polygon shapefile and spreadsheet data
- join data to shapefile, then export > save as new shapefile in new layer, and open attributes to delete unneeded columns
- create a new folder with four files (.shp, .shx, .dbf, .prj) and zip folder for next step

4) Convert new joined shapefile (simplified boundaries + data) into js format to use in Leaflet map
- Use ogre to ogre web client (http://ogre.adc4gis.com/) to convert zipped shapefile to geojson
- Copy and paste the geojson output into a new file, and modify into json this way:
- At top of new file, declare contents as a variable by adding this text:
  - var data =
- At the bottom of the new file, add this:
  - ;
- Rename file suffix as .js, place inside local directory, and upload in the Leaflet HTML index template

5) In Leaflet index template, credit to Alvin Chang for inspiration and functions to display info window data, borrowed from CT Mirror Leaflet visualizations such as http://projects.ctmirror.org/content/2014/05/raceSchools/

## Credits
Thanks to @erose for helping me with the JavaScript logic
