# create-sector-shape-KML-file
Create sector shape KML layer from given pandas dataframe

## introduction
Creating polygons with complex geometries is not a simple while working with KML format. Therefore, in order to create the shape of the sector, we must use the mathematical parameters that will allow us to calculate the shape.

Therefore, the input dataframe must include the following parameters:
- **X** & **Y** coordinates, in **wgs84 geo dd** format
- **Main angle** of the sector in relation to the north, in **degrees** (angle parameter)
- **Length** of the desired sector, in **meters** (distance parameter)
- **Angle size** of the sector, in **degrees** (std parameter)

Using this data you can calculate the sector shape, according to the following figure:
![sector](https://github.com/EtzionData/create-sector-shape-KML-file/blob/master/Pictures/sector_figure.png)

Also, another parameter defined by default in the code is the **arc-resolution** of the sector (points parameter).The default value of this variable is **points=36**.

In order to perform the calculation, we must first perform the conversion of the coordinates to the **UTM** format. This format will allow to calculated the sector by precise meters terms (calculation that base on degrees, will result getting an inaccurate shape). Also, after calculating the points that composed the sector,
the code convert them back to **wgs84 geo dd** format, so that it allow to save them later as a **KML file**.

As part of this conversion, the code also perform a calculation of the **utm zone**, And we will check whether the coordinates are located in the northern (**"U"**) or southern (**"D"**) part of the Earth. This information will be used by the code in converting the data back to wgs84 geo dd format.

As part of the calculation, the code calculated mathematically the position of the points composed the **arc** of the sector. The direction of the sector converted from degrees to **radians**, and using with the length to calculated the points that composed the arc. Every point calculated relatively the origin coordinates. It is important to note that the angles on which the calculation is made, assume that an angle of 0 degrees is oriented to the north, as can be seen in the figure:

![compass](https://github.com/EtzionData/create-sector-shape-KML-file/blob/master/Pictures/compass.png =250x250)

All the points that composed the sector shape are saved as a list of X and Y coordinates. This data is entered into the original dataframe as **"POLYGON"** field. Using this field, the code will create the new **KML layer** using the **simplekml** library.

An example of one of the KML layers created using the code can be seen in the **New York Harbor** area:

![NYH](https://github.com/EtzionData/create-sector-shape-KML-file/blob/master/Pictures/example.PNG)

All the layers created in the examples of this project uploaded to this **MyMaps** link: [sector_maps](https://www.google.com/maps/d/edit?mid=1YCqE5DIWiGnS8djtyFZ2UNDHQ55gPOve&usp=sharing)
