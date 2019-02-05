# Tour de France routes
This project is on the routes of the Tour De France for all years from 1903 to 2019. The data [(tour_data.csv)](https://github.com/CharlieStone/tour_de_france_routes/blob/master/data/tour_data.csv) has GPS coordinates for each start and end locations for each stage of the tour along with further details for each stage. 

Maps of the routes are in the file [tour_routes.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_routes.pdf). 

A chart of the elevation (y axis) of the start and end locations of each stage (x axis) of each Tour (chart) is here [tour_elevation.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_elevation.pdf).

A chart of the distance cycled (y axis) in each stage (x axis) of each Tour (chart), and total Tour distance (colour) is here.
[tour_distance.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_distance.pdf).

The type of stage for each Tour is plotted here [tour_stage_type.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_stage_type.pdf).

The data on the routes was scraped from Wikipedia. The start and end locations GPS coordinates were obtained from the place names using geonames. The code to do the scraping and cleaning is here [scrape_wiki_tours.Rmd](tour_de_france_routes/scrape_wiki_tours.Rmd).

We initially scraped data from the Tour de France [website](https://www.letour.fr/en/history). However, there were errors in the data (eg frequent mispellings of stage names and dates missing for stages on earlier years), and we found much fewer errors in the Wikipedia data. In addition, the Tour de France data does not give the country for each place name which makes geocoding more difficult (due to places with the same name in different countries), and the Wikipedia data has information on the terrain types for each year which is not available on the Tour de France website.

## Data
#### Description
Each row of the [data](https://github.com/CharlieStone/tour_de_france_routes/blob/master/data/tour_data.csv) is a stage of a Tour. Each row contains:
+ The date the stage started.
+ The stage number and stage type (prologue, main or sub stage a to c).
+ The start and end locations of the stage (as place name, country and GPS coordinates, and elevation in metres).
+ The type of terrain for the stage (in raw form as terrain and grouped in terrain_group).
+ The winner of the stage (name and country).
+ The distance cycled in kilometres and the 'as the crow flies' distance between the start and end locations of the stage.

A limitation of the data is that it does not give the exact route the Tour followed between the start and end locations of each stage. The plots of the routes plot a straight line between the start and end locations of each stage.  This means that the route plots for the 1920s (for example) have lines going across the sea along the west coast of France. The difference between the actual distance cycled (distance_km in the [data](https://github.com/CharlieStone/tour_de_france_routes/blob/master/data/tour_data.csv)) and the 'as the crow files' distance between the start and end locations of the stage (distance_crow_km) gives an indication of the extent to which the route cycled differs from the straight line shown on the plot.

Similarly, the elevation plots, particularly for the early years (1903 to 1909), do not show the full altitude to which the Tour went in these years.

#### Checks on GPS coordinates
We have checked that the 'as the crow flies' distance (dist_start_end) between the GPS coordinates for the start and end locations of each stage is not more than 40km greater than the distance cycled (distance_km) quoted in the Wikipedia table. We used 40km as differences less than this are unlikely to be clearly noticeable in the context of the entire route of the Tour, and with a difference less than this there are more cases due to many possible GPS coordinates for large cities. 

There are two stages where the difference is more than 40km (out of 2437 stages across all years):

1965 Stage 20 (Lyon to Auxerre): The difference is 50km. This is probably due to the GPS coordinates for Lyon and Auxerre being different to the precise parts of Lyon and Auxerre that the cyclists cycled between.

1970 Stage 8 (Ciney to Felsberg): The distance cycled is quoted as 232km, but the distance between the start and end locations is 318km. We have checked for other possible locations as a possible spelling mistake (eg Feldberg or Felberg), but these are further away from Ciney. 

## Plots
The file [tour_routes.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_routes.pdf) contains a plot of every start and end location of the Tour. The colour of the route is green at the start and black at the end. Dotted lines connect the end of one stage and the start of the next. This is particularly relevant for more recent years where the Tour has not been a continuous route.

A chart of the elevation (y axis) of the start and end locations of each stage (x axis) of each tour (chart) is here [tour_elevation.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_elevation.pdf).

A chart of the distance cycled (y axis) in each stage (x axis) of each Tour (chart), and total Tour distance (colour) is here.
[tour_distance.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_distance.pdf).

The file [tour_stage_type.pdf](https://github.com/CharlieStone/tour_de_france_routes/blob/master/tour_stage_type.pdf) contains a plot of the type of stage (tile fill) for each stage (y axis) of each Tour (x axis).

The code to produce the pdf is [here](tour_de_france_routes/Plot.Rmd). This also contains:
+ A scatter plot of every stage start and end location on a map of Europe.
+ A hexagonal bin density plot of the locations by latitude and longitude.

## Data sources
Data was scraped from the stage table from the Wikipedia article for each year of the Tour. For example, here is a link to the wikipage for [1975](https://en.wikipedia.org/wiki/1975_Tour_de_France). The place names were geocoded using the geonames [api](http://www.geonames.org/export/ws-overview.html).


## Packages used
|  Task|  Packages|
|--:|--:|
|  Web scraping|  rvest, xml2|
|  Data wrangling|  dplyr, tidyr, purrr, lubridate|
|  Accessing geonames api| geonames|
|  Reading and writing files| readr|
|  Calculating distances from GPS| geosphere|
|  Plotting| ggplot2, plotly|
|  Plotting maps| maps, mapproj|
|  Picking chart colours| colourpicker (addin)|
|  Setting ggplot themes| ggthemeassist (addin)|