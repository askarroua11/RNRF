Dhaka City Profile
Group: RNRF
This map is developed by four students from Hochschule Karlsruhe Technik und Wirstchaft- The department of Geomatics. 
Akter, Naznin - Askar, Roua - Naghiyev ,Fuad - Tukacs, Renátó
Dhaka’s city map was established for an educational purpose, and the goal was to have different  thematic maps with the routing functionality to be used by different users.
Software requirements 
GeoServer version 2.6.1.
pgAdmin III version 1.18.1
Postgis (OSGeo-Live).
External Libraries:
Open Layers 3 (http://openlayers.org/en/v3.0.0/css/ol.css)
Open Layers 2 (GitHUB)
 JQuery function (GitHUB)



Installation Steps:
1.	Create a new database on PostGIS using OSGEO Live 8.
2.	Restore the pgrouting.backup from the routing_layer  folder  to the new database you have created.
3.	In GeoServer create a new workspace and two data stores. One data store should contains the Shape files and the second one is for PostGIS data. Publish a wms layers using  PostGIS formatted  data from GeoServer data store. Click “Edit SQL view” and put the following sql sytax : “SELECT ST_MakeLine(route.geom) FROM (SELECT geom FROM pgr_fromAtoB('ways', %x1%, %y1%, %x2%, %y2%) ORDER BY seq) AS route”. Put the default values to 0 and the validation regular expression should be like this “^-?[\d.]+$” for the four coordinates. In the attribute list click refresh change the type field as “LineString” and also SRID to 4326. The declared SRS is EPSG:3857 for the layer and use the option “Reproject native to declared” in SRS handling. Then compute the bounding boxes. Use the default SLD line style for the layer. Save your layer giving a name and title for example  “pgrouting”.
4.	Publish also 8 vector layer using the shape file from GeoServer data store. The Declared SRSs are EPSG:4326 for every layer. Use the default  SLD style to each layer according to the geometry type(point, line, polygon).
5.	In the index.html, update lines 55,62,69,79,86, 93,100, 107 with the url of your GeoServer. In the routing.html, updates line 81 with the url of your Geoserver.
6.	Update lines 56, 63, 70, 80, 87, 94, 101, 108 with the names of your layers in GeoServer. In the routing.html, updates line 39 with your layer in Geoserver.



