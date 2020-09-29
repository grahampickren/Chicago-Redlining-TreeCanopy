
This series of maps looks at the relationship between redlining and tree canopy in Chicago, borrowing ideas and methods from several other studies done on this topic in other cities. 
- see https://osf.io/preprints/socarxiv/97zcs 

What I found was that there does seem to be a correlation between how an area was zoned by the Home Owners Lending Corporation and the percentage of tree canopy in those zones. In areas zoned as 'hazardous' by the HOLC, the average tree canopy was only 19%, as opposed to 50% in areas rated as 'best'. 

I also looked at street rights-of-way to gauge specifically whether public ROWs also lacked trees in areas deemed unfavorable by the HOLC. The purpose of looking at ROW is that you are evaluating the tree canopy on public streets and not just private property.

# RESULTS

“A = BEST” AREAS HAD 50% CANOPY

“B = STILL DESIRABLE’ AREAS HAD 35% CANOPY

“C = DEFINITELY DECLINING” AREAS HAD 24% CANOPY

“D = HAZARDOUS” AREAS HAD 19% CANOPY

# METHODS
Part 1 - Relationship between tree canopy

Two objectives:

Find the Percent Canopy Cover in Redlined Grades (A-D)

Find the Percent Canopy Cover in Redlined Districts (Within A-D, districts are individually graded with specific details about the area described in the attribute table of the shapefiles).


# Data:

1. High-Resolution Land Cover, Cook County 2010 the Chicago Region Trees Initiative https://datahub.cmap.illinois.gov/dataset/high-resolution-land-cover-cook-county-2010

2. Home Owners Lending Corporation Redlining shapefile for Chicago from here: https://dsl.richmond.edu/panorama/redlining/#loc=9/41.944/-87.771&maps=0&text=downloads
This layer has four redlining ‘grades’ that indicate how viable a neighborhood was for lending. These grades were symbolized as polygons of different colors.
Illinois or CMAP region streets

3. Street centerlines of Cook County https://hub-cookcountyil.opendata.arcgis.com/datasets/4569d77e6d004c0ea5fada54640189cf_5 

Here is my work flow for calculating tree canopy within redlined zones:

Step 1: Reclassify the raster into 0=not canopy 1= canopy

Step 2 (optional): Use the Clip tool (Data Management) to clip the raster to the zones

Step 3: Run the Zonal Statistics as Table tool using 

	a) Redlining layer as the feature zone data (the polygon zones are the four grades)

	b) ‘holc_grade’ as my Zone Field 

	c) My new Tree Canopy raster as the Input Value Raster

	d) selecting all statistics


Step 4 (optional): Dissolve the HOLC_Grade boundaries


RESULTS

“A = BEST” AREAS HAD 50% CANOPY

“B = STILL DESIRABLE’ AREAS HAD 35% CANOPY

“C = DEFINITELY DECLINING” AREAS HAD 24% CANOPY

“D = HAZARDOUS” AREAS HAD 19% CANOPY

# Part 2 Calculating tree canopy within public ROW 

Step 1: Add streets shape files

Step 2: Clip streets to redlined areas 

Step 3: Buffer street centerlines 50ft to capture ROW
- Set options to Dissolve by List, using full street name 

Step 4: Intersect Buffered streets with HOLC polygons so buffered streets has the same attribute table

Step 5: Run the Zonal Stats as Table tool using
a) Buffered streets as the zone

b1) full street name as field
b2) run a second time with holc_id as field

c) Reclassed tree canopy as raster

d) all statistics

Step 5: Run an ANOVA test to determine if there are significant differences in percent canopy cover within the ROW between categorical redline level classes within the city. 


