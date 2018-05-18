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

This script reads the input CSV and converts it to a readable CSV for use in ArcMap.

Note: It is expected that your script has been cleaned up prior to running this script. For more information, see:

https://github.com/RachelG-GIS/shared-resources/tree/add-files/python/just-python/python-2.7/CheckForBadCoordinatesInInputCSV
