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
