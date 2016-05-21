A Look at the Update 2016 of the WHO Global Urban Ambient Air Pollution Database
================================================================================

The WHO has recently published an update of its database about PM2.5 and PM10 ambient average annual concentrations in many cities of the world. The database can be found [on this website](http://www.who.int/phe/health_topics/outdoorair/databases/cities/en/) along with documentation and analyses.

The database has two limitations:

-   Not all countries are represented, since some of them do not monitor these pollutants or do not make the data available.

-   Because of the delay in countries publishing their air pollution figures, or because the last available figures are from an external study (for instance an occupational health work about Swedish soldiers for one city in Afghanistan), the year from which the data originate is often not 2015 or even not 2014. This was noted for instance in [this artiche of The Hindu](http://www.thehindu.com/news/cities/Delhi/outdated-data-misleading-experts/article8598361.ece?utm_source=RSS_Feed&utm_medium=RSS&utm_campaign=RSS_Syndication&utm_source=twitterfeed&utm_medium=twitter), or [this blog post of OpenAQ](https://medium.com/@openaq/surprising-make-up-of-yearly-air-quality-data-from-most-recent-who-report-61ae780df2ce#.8f4n8g6fd).

I decided to make a map showing that

1.  The sources are less numerous in some parts of the world

2.  The age of the data is different according to country.

For this, I had to geocode all cities in the database, which I did using the [opencage R package](https://github.com/ropenscilabs/opencage) (it's on [CRAN](https://cran.r-project.org/web/packages/opencage/index.html) too) for the [OpenCage Geocoder](https://geocoder.opencagedata.com/)

In the file (data\_prep1.R)\[data\_prep1.R\] I transformed the 3-letter ISO code of the country in the two-letter ISO code using the R package [countrycode](https://cran.r-project.org/web/packages/countrycode/index.html), and then I used the `opencage_forward` function with the city as `placename` and the country code as `country`. When the results had more than one line I took the first one, since at this scale I do not care whether I get the city itself or its airport. Out of 2973 cities, only 7 could not be geolocated this way so I added their coordinates per hand in (data\_prep2.R)\[data\_prep2.R\]. For instance I could not find "Nabih Saleh" in Bahrain as such, but searching for "Saleh" I could locate it, or on [this website](http://nelson.govt.nz/environment/air-quality/air-monitoring/airsheds-in-nelson/) I could understand that "Nelson Airshed A" was in Nelson.

Maybe I could have used the ID.WHO.city for geolocation instead but I realized this afterwards and I do not know what this ID is.