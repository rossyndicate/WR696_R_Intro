# R Skills Review



In this lesson you will take all of the skills you have learned up to this point and use them on a completely new set of data.

#### Necessary packages:




```r
library(tidyverse)
library(rstatix)

# new packages! Only if you want to work through the data retrieval process
library(httr)
library(jsonlite)
library(dataRetrieval)
```

## Tidying datasets

We are interested in looking at how the Cache la Poudre River's flow changes over time and space as it travels out of the mountainous Poudre Canyon and through Fort Collins.

There are four stream flow monitoring sites on the Poudre that we are interested in: two managed by the US Geological Survey (USGS), and two managed by the Colorado Division of Water Resources (CDWR):


```{=html}
<div id="htmlwidget-f620ecd2c811a3e800d0" style="width:864px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-f620ecd2c811a3e800d0">{"x":{"options":{"minZoom":1,"maxZoom":52,"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}},"preferCanvas":false,"bounceAtZoomLimits":false,"maxBounds":[[[-90,-370]],[[90,370]]]},"calls":[{"method":"addProviderTiles","args":["CartoDB.Positron","CartoDB.Positron","CartoDB.Positron",{"errorTileUrl":"","noWrap":false,"detectRetina":false,"pane":"tilePane"}]},{"method":"addProviderTiles","args":["CartoDB.DarkMatter","CartoDB.DarkMatter","CartoDB.DarkMatter",{"errorTileUrl":"","noWrap":false,"detectRetina":false,"pane":"tilePane"}]},{"method":"addProviderTiles","args":["OpenStreetMap","OpenStreetMap","OpenStreetMap",{"errorTileUrl":"","noWrap":false,"detectRetina":false,"pane":"tilePane"}]},{"method":"addProviderTiles","args":["Esri.WorldImagery","Esri.WorldImagery","Esri.WorldImagery",{"errorTileUrl":"","noWrap":false,"detectRetina":false,"pane":"tilePane"}]},{"method":"addProviderTiles","args":["OpenTopoMap","OpenTopoMap","OpenTopoMap",{"errorTileUrl":"","noWrap":false,"detectRetina":false,"pane":"tilePane"}]},{"method":"createMapPane","args":["point",440]},{"method":"addCircleMarkers","args":[[40.6645,40.5880833,40.5519269,40.5013],[-105.2242,-105.0692222,-105.011365,-104.967],6,null,"Poudre River Monitoring",{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}},"pane":"point","stroke":true,"color":"#333333","weight":1,"opacity":[0.9,0.9,0.9,0.9],"fill":true,"fillColor":["#007094","#00BE7D","#4B0055","#FDE333"],"fillOpacity":[0.6,0.6,0.6,0.6]},null,null,["<div class='scrollableContainer'><table class=mapview-popup id='popup'><tr class='coord'><td><\/td><th><b>Feature ID&emsp;<\/b><\/th><td>1&emsp;<\/td><\/tr><tr><td>1<\/td><th>site&emsp;<\/th><td>Canyon Mouth&emsp;<\/td><\/tr><tr><td>2<\/td><th>site_no&emsp;<\/th><td>CLAFTCCO&emsp;<\/td><\/tr><tr><td>3<\/td><th>source&emsp;<\/th><td>CDWR&emsp;<\/td><\/tr><tr><td>4<\/td><th>geometry&emsp;<\/th><td>sfc_POINT&emsp;<\/td><\/tr><\/table><\/div>","<div class='scrollableContainer'><table class=mapview-popup id='popup'><tr class='coord'><td><\/td><th><b>Feature ID&emsp;<\/b><\/th><td>2&emsp;<\/td><\/tr><tr><td>1<\/td><th>site&emsp;<\/th><td>Lincoln Bridge&emsp;<\/td><\/tr><tr><td>2<\/td><th>site_no&emsp;<\/th><td>06752260&emsp;<\/td><\/tr><tr><td>3<\/td><th>source&emsp;<\/th><td>USGS&emsp;<\/td><\/tr><tr><td>4<\/td><th>geometry&emsp;<\/th><td>sfc_POINT&emsp;<\/td><\/tr><\/table><\/div>","<div class='scrollableContainer'><table class=mapview-popup id='popup'><tr class='coord'><td><\/td><th><b>Feature ID&emsp;<\/b><\/th><td>3&emsp;<\/td><\/tr><tr><td>1<\/td><th>site&emsp;<\/th><td>Boxelder&emsp;<\/td><\/tr><tr><td>2<\/td><th>site_no&emsp;<\/th><td>06752280&emsp;<\/td><\/tr><tr><td>3<\/td><th>source&emsp;<\/th><td>USGS&emsp;<\/td><\/tr><tr><td>4<\/td><th>geometry&emsp;<\/th><td>sfc_POINT&emsp;<\/td><\/tr><\/table><\/div>","<div class='scrollableContainer'><table class=mapview-popup id='popup'><tr class='coord'><td><\/td><th><b>Feature ID&emsp;<\/b><\/th><td>4&emsp;<\/td><\/tr><tr><td>1<\/td><th>site&emsp;<\/th><td>Timnath&emsp;<\/td><\/tr><tr><td>2<\/td><th>site_no&emsp;<\/th><td>CLARIVCO&emsp;<\/td><\/tr><tr><td>3<\/td><th>source&emsp;<\/th><td>CDWR&emsp;<\/td><\/tr><tr><td>4<\/td><th>geometry&emsp;<\/th><td>sfc_POINT&emsp;<\/td><\/tr><\/table><\/div>"],{"maxWidth":800,"minWidth":50,"autoPan":true,"keepInView":false,"closeButton":true,"closeOnClick":true,"className":""},["Canyon Mouth","Lincoln Bridge","Boxelder","Timnath"],{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]},{"method":"addScaleBar","args":[{"maxWidth":100,"metric":true,"imperial":true,"updateWhenIdle":true,"position":"bottomleft"}]},{"method":"addHomeButton","args":[-105.2242,40.5013,-104.967,40.6645,true,"Poudre River Monitoring","Zoom to Poudre River Monitoring","<strong> Poudre River Monitoring <\/strong>","bottomright"]},{"method":"addLayersControl","args":[["CartoDB.Positron","CartoDB.DarkMatter","OpenStreetMap","Esri.WorldImagery","OpenTopoMap"],"Poudre River Monitoring",{"collapsed":true,"autoZIndex":true,"position":"topleft"}]},{"method":"addLegend","args":[{"colors":["#4B0055","#007094","#00BE7D","#FDE333"],"labels":["Boxelder","Canyon Mouth","Lincoln Bridge","Timnath"],"na_color":null,"na_label":"NA","opacity":1,"position":"topright","type":"factor","title":"Poudre River Monitoring","extra":null,"layerId":null,"className":"info legend","group":"Poudre River Monitoring"}]}],"limits":{"lat":[40.5013,40.6645],"lng":[-105.2242,-104.967]},"fitBounds":[40.5013,-105.2242,40.6645,-104.967,[]]},"evals":[],"jsHooks":{"render":[{"code":"function(el, x, data) {\n  return (\n      function(el, x, data) {\n      // get the leaflet map\n      var map = this; //HTMLWidgets.find('#' + el.id);\n      // we need a new div element because we have to handle\n      // the mouseover output separately\n      // debugger;\n      function addElement () {\n      // generate new div Element\n      var newDiv = $(document.createElement('div'));\n      // append at end of leaflet htmlwidget container\n      $(el).append(newDiv);\n      //provide ID and style\n      newDiv.addClass('lnlt');\n      newDiv.css({\n      'position': 'relative',\n      'bottomleft':  '0px',\n      'background-color': 'rgba(255, 255, 255, 0.7)',\n      'box-shadow': '0 0 2px #bbb',\n      'background-clip': 'padding-box',\n      'margin': '0',\n      'padding-left': '5px',\n      'color': '#333',\n      'font': '9px/1.5 \"Helvetica Neue\", Arial, Helvetica, sans-serif',\n      'z-index': '700',\n      });\n      return newDiv;\n      }\n\n\n      // check for already existing lnlt class to not duplicate\n      var lnlt = $(el).find('.lnlt');\n\n      if(!lnlt.length) {\n      lnlt = addElement();\n\n      // grab the special div we generated in the beginning\n      // and put the mousmove output there\n\n      map.on('mousemove', function (e) {\n      if (e.originalEvent.ctrlKey) {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                           ' lon: ' + (e.latlng.lng).toFixed(5) +\n                           ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                           ' | zoom: ' + map.getZoom() +\n                           ' | x: ' + L.CRS.EPSG3857.project(e.latlng).x.toFixed(0) +\n                           ' | y: ' + L.CRS.EPSG3857.project(e.latlng).y.toFixed(0) +\n                           ' | epsg: 3857 ' +\n                           ' | proj4: +proj=merc +a=6378137 +b=6378137 +lat_ts=0.0 +lon_0=0.0 +x_0=0.0 +y_0=0 +k=1.0 +units=m +nadgrids=@null +no_defs ');\n      } else {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                      ' lon: ' + (e.latlng.lng).toFixed(5) +\n                      ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                      ' | zoom: ' + map.getZoom() + ' ');\n      }\n      });\n\n      // remove the lnlt div when mouse leaves map\n      map.on('mouseout', function (e) {\n      var strip = document.querySelector('.lnlt');\n      if( strip !==null) strip.remove();\n      });\n\n      };\n\n      //$(el).keypress(67, function(e) {\n      map.on('preclick', function(e) {\n      if (e.originalEvent.ctrlKey) {\n      if (document.querySelector('.lnlt') === null) lnlt = addElement();\n      lnlt.text(\n                      ' lon: ' + (e.latlng.lng).toFixed(5) +\n                      ' | lat: ' + (e.latlng.lat).toFixed(5) +\n                      ' | zoom: ' + map.getZoom() + ' ');\n      var txt = document.querySelector('.lnlt').textContent;\n      console.log(txt);\n      //txt.innerText.focus();\n      //txt.select();\n      setClipboardText('\"' + txt + '\"');\n      }\n      });\n\n      }\n      ).call(this.getMap(), el, x, data);\n}","data":null},{"code":"function(el, x, data) {\n  return (function(el,x,data){\n           var map = this;\n\n           map.on('keypress', function(e) {\n               console.log(e.originalEvent.code);\n               var key = e.originalEvent.code;\n               if (key === 'KeyE') {\n                   var bb = this.getBounds();\n                   var txt = JSON.stringify(bb);\n                   console.log(txt);\n\n                   setClipboardText('\\'' + txt + '\\'');\n               }\n           })\n        }).call(this.getMap(), el, x, data);\n}","data":null}]}}</script>
```

We are going to work through retrieving the raw data from both the USGS and CDWR databases.

### Get USGS stream flow data

Using the {dataRetrieval} package we can pull all sorts of USGS water data. You can read more about the package, functions available, metadata etc. here: <https://doi-usgs.github.io/dataRetrieval/index.html>


```r
# pulls USGS daily ('dv') stream flow data for those two sites:
usgs <- dataRetrieval::readNWISdv(siteNumbers = c("06752260", "06752280"), # USGS site code for the Poudre River at the Lincoln Bridge and the ELC
                                  parameterCd = "00060", # USGS code for stream flow
                                  startDate = "2020-10-01", # YYYY-MM-DD formatting
                                  endDate = "2023-10-01") %>% # YYYY-MM-DD formatting
  rename(q_cfs = X_00060_00003) %>% # USGS code for stream flow units in cubic feet per second (CFS)
  mutate(Date = lubridate::ymd(Date), # convert the Date column to "Date" formatting using the `lubridate` package
         Site = case_when(site_no == "06752260" ~ "Lincoln", 
                          site_no == "06752280" ~ "Boxelder")) 

# if you want to save the data:
#write_csv(usgs, 'data/review-usgs.csv')
```

### Get CDWR stream flow data

Alas, CDWR doesn't have an R packge to easily pull data from their API like USGS does, but they do have user-friendly instructions about how to develop API calls.

**Don't stress if you have no clue what an API is**! We will learn a lot more about them in 523A, but this is good practice for our function writing and mapping skills.

Using the ["URL Generator" steps outlined]((https://dwr.state.co.us/Rest/GET/Help/SurfaceWaterTSDayGenerator)), if we wanted data from 2020-2022 for the Canyon mouth side (site abbreviation = CLAFTCCO), it generates this URL to retrieve that data:

<https://dwr.state.co.us/Rest/GET/api/v2/surfacewater/surfacewatertsday/?format=json&dateFormat=dateOnly&fields=abbrev%2CmeasDate%2Cvalue%2CmeasUnit&encoding=deflate&abbrev=CLAFTCCO&min-measDate=10%2F01%2F2020&max-measDate=09%2F30%2F2022>

However, we want to pull this data for two different sites, and may want to change the year range of data. Therefore, we can write a function to pull data for our various sites and time frames:


```r
# Functin to retrieve data
co_water_data <- function(site, start_year, end_year){
  
  raw_data <- httr::GET(url = paste0("https://dwr.state.co.us/Rest/GET/api/v2/surfacewater/surfacewatertsday/?format=json&dateFormat=dateOnly&fields=abbrev%2CmeasDate%2Cvalue%2CmeasUnit&encoding=deflate&abbrev=",site,
                                     "&min-measDate=10%2F01%2F", start_year,
                                     "&max-measDate=09%2F30%2F", end_year))
  
  # extract the text data, returns a JSON object
  extracted_data <- httr::content(raw_data, as = "text", encoding = "UTF-8") 
  
  # parse text from JSON to data frame
  final_data <- jsonlite::fromJSON(extracted_data)[["ResultList"]]
  
  return(final_data)
  
}
```

Now, lets use that function to pull data for our two CDWR sites of interest, which we can iterate over with `map()`. Since this function returns data frames with the same structure an variable names, we can use `map_dfr()` to bind the two data frames into a single one:


```r
# run function for our two sites
sites <- c("CLAFTCCO","CLARIVCO")

cdwr <- sites %>% 
  map_dfr(~ co_water_data(site = .x, start_year = 2020, end_year = 2023))
 
# If you want to save this file
#write_csv(cdwr, 'data/review-cdwr.csv') 
```

### OR, read in the .csv's we already generated and saved for you:

Read in our two data sets. You will find that they provide the same information (daily streamflow from 2020-2022) but their variable names and structures are different:


```r
usgs <- read_csv('data/review-usgs.csv')

cdwr <- read_csv('data/review-cdwr.csv') 
```

When we look at these two datasets, we see they provide the same information (daily streamflow from 2020-2023) but their variable names and structures are different:


```r
glimpse(usgs)
```

```
## Rows: 2,191
## Columns: 6
## $ agency_cd        <chr> "USGS", "USGS", "USGS", "USGS", "USGS", "USGS", "USGS…
## $ site_no          <chr> "06752260", "06752260", "06752260", "06752260", "0675…
## $ Date             <date> 2020-10-01, 2020-10-02, 2020-10-03, 2020-10-04, 2020…
## $ q_cfs            <dbl> 6.64, 7.41, 7.04, 6.84, 6.79, 7.81, 6.49, 11.30, 20.2…
## $ X_00060_00003_cd <chr> "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A"…
## $ Site             <chr> "Lincoln", "Lincoln", "Lincoln", "Lincoln", "Lincoln"…
```

```r
glimpse(cdwr)
```

```
## Rows: 2,147
## Columns: 4
## $ abbrev   <chr> "CLAFTCCO", "CLAFTCCO", "CLAFTCCO", "CLAFTCCO", "CLAFTCCO", "…
## $ measDate <date> 2020-10-01, 2020-10-02, 2020-10-03, 2020-10-04, 2020-10-05, …
## $ value    <dbl> 42, 36, 34, 32, 35, 30, 30, 34, 34, 27, 21, 29, 26, 43, 39, 4…
## $ measUnit <chr> "cfs", "cfs", "cfs", "cfs", "cfs", "cfs", "cfs", "cfs", "cfs"…
```

Therefore, in order to combine these two datasets from different sources we need to do some data cleaning.

Lets first focus on cleaning the cdwr dataset to match the structure of the usgs one:


```r
cdwr_clean <- cdwr %>%
  # rename data and streamflow vars to match name of usgs vars
  rename(q_cfs = value) %>%
  # Add site and agency vars
  mutate(Date = lubridate::ymd(measDate),
         Site = ifelse(abbrev == "CLAFTCCO", "Canyon",
                       "Timnath"),
         agency_cd = "CDWR")
```

Now, we can join our USGS and CDWR data frames together with `bind_rows()`.


```r
data <- bind_rows(usgs,cdwr_clean)
```

## Exploratory Data Analysis

Let's explore the data to see if there are any trends we can find visually. We can first visualize the data as time series:


```r
# Discharge (in CFS) through time displaying all four of our monitoring sites.
data %>%
  ggplot(aes(x = Date, y = q_cfs, color = Site)) +
  geom_line() +
  theme_bw() +
  xlab("Date") +
  ylab("Discharge (cfs)") +
  facet_wrap( ~ Site, ncol = 1)
```

<img src="09-review_files/figure-html/unnamed-chunk-12-1.png" width="864" />

Say we wanted to examine differences in annual stream flow. We can do this with a little data wrangling, using the `separate()` function to split our "Date" column into Year, Month, and Day columns.


```r
data_annual <- data %>% 
  separate(Date, into = c("Year", "Month", "Day"), sep = "-") %>% 
  # create monthly avg for plots
  group_by(Site, Year, Month) %>%
  summarise(monthly_q = mean(q_cfs))

# visualize annual differences across the course of each year
data_annual %>% 
  ggplot(aes(x = Month, y = monthly_q, group = Year)) +
  geom_line(aes(colour = Year))+
  facet_wrap(~Site) +
  theme_bw()
```

<img src="09-review_files/figure-html/unnamed-chunk-13-1.png" width="864" />

Let's look at the daily difference in discharge between the mouth of the Cache la Poudre River (Canyon Mouth site) and each of the sites downstream. This will require some more wrangling of our data.


```r
dif_data <- data %>%
  # select vars of interest
  select(Site, Date, q_cfs) %>%
  # create a column of streamflow values for each site
  pivot_wider(names_from = Site, values_from = q_cfs) %>%
  # for each downstream site, create a new column that is the difference from the Canyon mouth site
  mutate_at(c("Boxelder", "Lincoln", "Timnath"), .funs = ~ (Canyon - .)) %>% 
  # if you wanted to create new variables use this instead:
  #mutate_at(c("Boxelder", "Lincoln", "Timnath"), .funs = list(dif = ~ (Canyon - .))) %>%
  # then pivot these new columns (i.e., NOT the date and canyon columns) longer again
  pivot_longer(-c(Canyon, Date))


dif_data %>% 
  mutate(name = fct(name, levels = c("Lincoln", "Boxelder", "Timnath"))) %>% 
  ggplot() +
    geom_line(aes(x = Date, y = value, color = name)) +
    theme_bw() +
    facet_wrap("name")+
    ylab("Streamflow Difference from Poudre Mouth")
```

<img src="09-review_files/figure-html/unnamed-chunk-14-1.png" width="864" />

## Data Analysis

Through our exploratory data analysis, it *appears* that stream flow decreases as we move through town. But, how can we test if these flows are significantly different, and identify the magnitude/direction of these differences?

Because we will be comparing daily stream flow across multiple sites, we can use an ANOVA test to assess this research question. We will set our alpha at 0.05.

### Testing for normal distribution

ANOVA assumes normal distribution within each group - we can visualize each site's data with a histogram:


```r
ggplot(data = data, aes(x = q_cfs)) +
         geom_histogram() + 
  facet_wrap (~Site)
```

<img src="09-review_files/figure-html/unnamed-chunk-15-1.png" width="864" />

... and use the `shapiro_test()` function along with `group_by()` to statistically test for normality within each site's daily stream flow data:


```r
data %>%
  group_by(Site) %>%
  shapiro_test(q_cfs)
```

```
## # A tibble: 4 × 4
##   Site     variable statistic        p
##   <chr>    <chr>        <dbl>    <dbl>
## 1 Boxelder q_cfs        0.485 1.86e-48
## 2 Canyon   q_cfs        0.648 1.29e-42
## 3 Lincoln  q_cfs        0.486 2.08e-48
## 4 Timnath  q_cfs        0.427 2.07e-49
```

Since the null hypothesis of the Shapiro-Wilk test is that the data is normally distributed, these results tell us all groups do not fit a normal distribution for daily stream flow. It is also quite clear from their histograms that they are not normally distributed.

### Testing for equal variance

To test for equal variances among more than two groups, it is easiest to use a Levene's Test like we have done in the past:


```r
data %>%
  levene_test(q_cfs ~ Site)
```

```
## # A tibble: 1 × 4
##     df1   df2 statistic        p
##   <int> <int>     <dbl>    <dbl>
## 1     3  4334      41.8 1.31e-26
```

Given this small p-value, we see that the variances of our groups are not equal.

### ANOVA - Kruskal-Wallis

After checking our assumptions we need to perform a non-parametric ANOVA test, the Kruskal-Wallis test.


```r
data %>%
  kruskal_test(q_cfs ~ Site)
```

```
## # A tibble: 1 × 6
##   .y.       n statistic    df         p method        
## * <chr> <int>     <dbl> <int>     <dbl> <chr>         
## 1 q_cfs  4338      860.     3 5.36e-186 Kruskal-Wallis
```

Our results here are highly significant (at alpha = 0.05), meaning that at least one of our group's mean stream flow is significantly different from the others.

### ANOVA post-hoc analysis

Since we used the non-parametric Kruskal-Wallace test, we can use the associated Dunn's test to test across our sites for significant differences in mean stream flow:


```r
data %>% 
  dunn_test(q_cfs ~ Site)
```

```
## # A tibble: 6 × 9
##   .y.   group1   group2     n1    n2 statistic         p     p.adj p.adj.signif
## * <chr> <chr>    <chr>   <int> <int>     <dbl>     <dbl>     <dbl> <chr>       
## 1 q_cfs Boxelder Canyon   1096  1095     28.9  1.92e-183 1.15e-182 ****        
## 2 q_cfs Boxelder Lincoln  1096  1095     10.6  1.77e- 26 3.54e- 26 ****        
## 3 q_cfs Boxelder Timnath  1096  1052     15.1  2.39e- 51 9.56e- 51 ****        
## 4 q_cfs Canyon   Lincoln  1095  1095    -18.2  2.94e- 74 1.47e- 73 ****        
## 5 q_cfs Canyon   Timnath  1095  1052    -13.5  1.27e- 41 3.81e- 41 ****        
## 6 q_cfs Lincoln  Timnath  1095  1052      4.53 5.84e-  6 5.84e-  6 ****
```

The results of our Dunn test signify that all of our sites are significantly different from eachother mean streamflow across our sites are significantly different.

THOUGHT EXPERIMENT 1: Based on our results, which of our two gages have the greatest difference in mean daily stream flow?

THOUGHT EXPERIMENT 2: Is this an appropriate test to perform on stream flow data? Why or why not?
