This python code (tested in 2.7.14) reads in a CSV text file that has polygon vertex coordinates in the following format:

|PolygonIdentifier|FirstPointX|FirstPointY|SecondPointX|SecondPointY|...|nthPointX|nthPointY|
|-----------------|-----------|-----------|------------|------------|---|---------|---------|
|polygonIdentifier1|firstPointX|firstPointY|secondPointX|secondPointY|...|nthPointX|nthPointY|
|polygonIdentifier2|firstPointX|firstPointY|secondPointX|secondPointY|...|nthPointX|nthPointY|
|polygonIdentifier3|firstPointX|firstPointY|secondPointX|secondPointY|...|nthPointX|nthPointY|
|polygonIdentifier4|firstPointX|firstPointY|secondPointX|secondPointY|...|nthPointX|nthPointY|
|polygonIdentifierN|firstPointX|firstPointY|secondPointX|secondPointY|...|nthPointX|nthPointY|

ArcGIS Desktop and ArcGIS Pro are unable to read a file of this format. The ideal format for the software is:

|PolygonIdentifier|PointX|PointY|
|-----------------|------|------|
|polygonIdentifier1|firstPointX|firstPointY|
|polygonIdentifier1|secondPointX|secondPointY|
|polygonIdentifier1|...|...|
|polygonIdentifier1|nthPointX|nthPointY|
|polygonIdentifier2|firstPointX|firstPointY|
|polygonIdentifier2|secondPointX|secondPointY|
|polygonIdentifier2|...|...|
|polygonIdentifier2|nthPointX|nthPointY|
|polygonIdentifierN|firstPointX|firstPointY|
|polygonIdentifierN|secondPointX|secondPointY|
|polygonIdentifierN|...|...|
|polygonIdentifierN|nthPointX|nthPointY|

This script reads the input CSV and makes sure that there are an even number of coordinate columns for each row to ensure you aren't missing any coordinates that may mess things up. Once all rows pass the checks in this code, you can then use my secondary code to convert the above format into a readable format for ArcMap.

A few things to note: When editing CSVs in Excel, extra commas are added sometimes, so if one polygon has 4 vertices and another has 8, the 4-vertex polygon will have a bunch of commas indicating empty columns out to the 8th coordinate. Be sure you clear these out using Notepad before running this script. Also ensure no commas exist at the end of all the rows. You can clear out the commas at the end of the rows using Microsoft Word. Copy paste the text from Notepad into Word, then use Find/Replace. Your Find will be ",^p" to search for commas at the end of lines. You replace this with just "^p". Both of these should be entered without quotes. Then copy-paste the resulting text back into Notepad as your cleaned-up CSV.

Steps in ArcMap to consume the CSV output:

1. Double-check that the data is in the right format before bringing it into ArcMap.
2. Drag the CSV file into ArcMap.
3. Right-click on the CSV in the Table of Contents and choose Display XY Data.
4. Choose the relevant X and Y fields (in the sample data in this folder, the second field is the X and the third field is the Y).
5. Choose the right coordinate system (in the sample data in this folder, the coordinate system is Web Mercator Auxiliary Sphere).
6. Click OK to create an event layer of the points.
7. Export the layer into a folder as a shapefile, or into a geodatabase as a feature class.
8. Use that new file as an input to the Points to Line (Data Management) tool. Ensure that the Line Field is set to the polygon identifier field (in the sample data in this folder, the first field (not the ObjectID field) is the polygon identifier field).
9. Use the output from step 8 in Feature to Polygon. This should complete your polygons.
