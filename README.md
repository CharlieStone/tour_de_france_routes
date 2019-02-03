# Tour de France routes
This project is on the routes of the Tour De France for all years from 1903 to 2019. The data [(tour_data.csv)](https://github.com/CharlieStone/tour_de_france_routes/blob/master/data/tour_data.csv) has geocoded start and end locations for each stage of the tour along with further details for each stage. The routes have been plotted using ggplot and the routes for all years are in the file [tour_routes.pdf](tour_de_france_routes/tour_routes.pdf). The data was scraped from Wikipedia, cleaned and stage start and end locations geocoded using geonames, the code is in [scrape_wiki_tours.Rmd](tour_de_france_routes/scrape_wiki_tours.Rmd).

## Data
Each row of the [data](https://github.com/CharlieStone/tour_de_france_routes/blob/master/data/tour_data.csv) is a stage of a Tour. Each row contains:
+ The date the stage started.
+ The stage number and stage type (prologue, main or sub stage a to c).
+ The start and end locations of the stage (as place name, country and GPS coordinates).
+ The type of terrain for the stage (in raw form as terrain and grouped in terrain_group).
+ The winner of the stage (name and country).
+ The distance cycled in kilometres and the 'as the crow flies' distance between the start and end locations of the stage.

## Plots
The file [tour_routes.pdf](tour_de_france_routes/tour_routes.pdf) contains:
+ A plot of every start and end location of the Tour.
+ The code to generate 'tour_routes.pdf'.

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