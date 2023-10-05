# Data Visualization in R



This lesson will go a little deeper into data visualization and how to customize figures and tables and make them 'publication ready'.

First start by reading in the packages for this lesson, which in this case is only the {tidyverse}:


```r
library(tidyverse)
```

### Data Preparation

For today's lesson we are going to be working with some census data for Larimer County, CO. This data can be found on Canvas in .csv format titled `larimer_census.csv`. Download that file and put it in a `data/` folder in the your R Project.

After that, read the .csv into your R session using `read_csv()`:


```r
census_data <- read_csv("data/larimer_census.csv")
```

Inspect `census_data` and the structure of the data frame. This data contains information on median income, median age, and race and ethnicity for each census tract in Larimer County.

::: {.alert .alert-info}
Note: This census data for Larimer county was retrieved entirely in R using the `tidycensus` package. If you are interested in how I did this, I've uploaded the script to do so on Canvas titled 'getCensusData.R'. Note that you will need to retrieve your own census API key and paste it at the top of the script to run it (API keys are free and easy to get [here](https://api.census.gov/data/key_signup.html)). To learn more about `tidycensus`, check out [Analyzing U.S. Census Data](https://walker-data.com/census-r/index.html) by Kyle Walker.
:::

<hr>

## Publication Ready Figures with `ggplot2`

For this exercise you will learn how to spruce up your `ggplot2` figures with theme customization, annotation, color palettes, and more.

To demonstrate some of these advanced visualization techniques, we will be analyzing the relationships among some census data for Larimer county.

Let's start with this basic plot:


```r
census_data %>% 
  ggplot(aes(x = median_age, y = percent_bipoc))+
  geom_point(color = "black")
```

<img src="04-viz_files/figure-html/unnamed-chunk-4-1.png" width="672" />

And by the end of this lesson turn it into this:

![](images/census_plot.png)

### General Appearance

#### Customize points within `geom_point()`

-   color or size points by a variable or apply a specific color/number

-   change the transparency with `alpha` (ranges from 0-1)


```r
#specific color and size value
census_data %>% 
  ggplot(aes(x = median_age, y = percent_bipoc))+
  geom_point(color = "red", size = 4, alpha = 0.5)
```

<img src="04-viz_files/figure-html/unnamed-chunk-5-1.png" width="672" />

When sizing or coloring points by a variable in the dataset, it goes within `aes():`


```r
# size by a variable
census_data %>% 
  ggplot(aes(x = median_age, y = percent_bipoc))+
  geom_point(aes(size = median_income), color = "red")
```

<img src="04-viz_files/figure-html/unnamed-chunk-6-1.png" width="672" />


```r
# color by a variable
census_data %>% 
  ggplot(aes(x = median_age, y = percent_bipoc))+
  geom_point(aes(color = median_income), size = 4)
```

<img src="04-viz_files/figure-html/unnamed-chunk-7-1.png" width="672" />

#### Titles and limits

-   add title with `ggtitle`

-   edit axis labels with `xlab()` and `ylab()`

-   change axis limits with `xlim()` and `ylim()`


```r
census_data %>% 
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black")+
  ggtitle("Census Tract socioeconomic data for Larimer County")+
  xlab("Median Age")+
  ylab("People of Color (%)")+
  xlim(c(20, 70))+
  ylim(c(0, 35))
```

<img src="04-viz_files/figure-html/unnamed-chunk-8-1.png" width="672" />

Be cautious of setting the axis limits however, as you notice it omits the full dataset which could lead to dangerous misinterpretations of the data.

You can also put multiple label arguments within `labs()` like this:


```r
census_data %>% 
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black")+
  labs(
    title = "Census Tract socioeconomic data for Larimer County",
    x = "Median Age",
    y = "People of Color (%)"
  ) +
  xlim(c(20, 70))+
  ylim(c(0, 35))
```

<img src="04-viz_files/figure-html/unnamed-chunk-9-1.png" width="672" />

#### Chart components with `theme()`

All `ggplot2` components can be customized within the `theme()` function. The full list of editable components (there's a lot!) can be found [here](https://ggplot2.tidyverse.org/reference/theme.html). Note that the functions used within `theme()` depend on the type of components, such as `element_text()` for text, `element_line()` for lines, etc.


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)") +
  theme(
    #edit plot title
    plot.title = element_text(size = 16, color = "blue"),
    # edit x axis title
    axis.title.x = element_text(face = "italic", color = "orange"),
    # edit y axis ticks
    axis.text.y = element_text(face = "bold"),
    # edit grid lines
    panel.grid.major = element_line(color = "black"),

  )
```

<img src="04-viz_files/figure-html/unnamed-chunk-10-1.png" width="672" />

Another change you may want to make is the value breaks in the axis labels (i.e., what values are shown on the axis). To customize that for a continuous variable you can use `scale_x_continuous()` / `scale_y_continuous` (for discrete variables use `scale_x_discrete` ). In this example we will also add `anlge =` to our axis text to angle the labels so they are not too jumbled:


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)") +
  scale_x_continuous(breaks = seq(15, 90, 5))+
  theme(
    # angle axis labels
    axis.text.x = element_text(angle = 45)
  )
```

<img src="04-viz_files/figure-html/unnamed-chunk-11-1.png" width="672" />

While these edits aren't necessarily *pretty*, we are just demonstrating how you would edit specific components of your charts. To edit overall aesthetics of your plots you can change the theme.

#### Themes

`ggplot2` comes with many built in theme options (see the complete list [here](https://r-graph-gallery.com/192-ggplot-themes)).

For example, see what `theme_minimal()` and `theme_classic()` look like:


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  theme_minimal()
```

<img src="04-viz_files/figure-html/unnamed-chunk-12-1.png" width="672" />


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  theme_classic()
```

<img src="04-viz_files/figure-html/unnamed-chunk-13-1.png" width="672" />

You can also import many different themes by installing certain packages. A popular one is `ggthemes`. A complete list of themes with this package can be seen [here](https://yutannihilation.github.io/allYourFigureAreBelongToUs/ggthemes/)

To run this example, first install the `ggthemes` package and then load it in to your session:


```r
install.packages("ggthemes")
```


```r
library(ggthemes)
```

Now explore a few themes, such as `theme_wsj`, which uses the Wall Street Journal theme, and `theme_economist` and `theme_economist_white` to use themes used by the Economist.


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  ggthemes::theme_wsj()+
  # make the text smaller
  theme(text = element_text(size = 8))
```

<img src="04-viz_files/figure-html/unnamed-chunk-16-1.png" width="672" />

::: {.alert .alert-info}
Note you may need to click 'Zoom' in the Plot window to view the figure better.
:::


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  ggthemes::theme_economist()
```

<img src="04-viz_files/figure-html/unnamed-chunk-17-1.png" width="672" />

Some themes may look messy out of the box, but you can apply any elements from `theme()` afterwards to clean it up. For example, change the legend position:


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income), color = "black") +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  ggthemes::theme_economist()+
  theme(
    legend.position = "bottom"
  )
```

<img src="04-viz_files/figure-html/unnamed-chunk-18-1.png" width="672" />

### Color, Size and Legends

#### Color

To specify a single color, the most common way is to specify the name (e.g., `"red"`) or the Hex code (e.g., `"#69b3a2"`).

You can also specify an entire color palette. Some of the most common packages to work with color palettes in R are `RColorBrewer` and [`viridis`](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html). Viridis is designed to be color-blind friendly, and RColorBrewer has a [web application](https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3) where you can explore your data requirements and preview various palettes.

First, if you want to run these examples install and load the `RColorBrewer` and `viridis` packages:


```r
install.packages("RColorBrewer")
install.packages("viridis")
```


```r
library(RColorBrewer)
library(viridis)
```

Now, lets color our points using the palettes in `viridis`. To customize continuous color scales with `viridis` we use `scale_color_viridis()`.


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income)) +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  viridis::scale_colour_viridis()
```

<img src="04-viz_files/figure-html/unnamed-chunk-21-1.png" width="672" />

Second, let's see how to do that with an `RColorBrewer` palette, using the 'Greens' palette and `scale_color_distiller()` function. We add `direction = 1` to make it so that darker green is associated with higher values for income.


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income)) +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  scale_color_distiller(palette = "Greens", direction = 1)
```

<img src="04-viz_files/figure-html/unnamed-chunk-22-1.png" width="672" />

#### Size

You can edit the range of the point radius with `scale_radius` :


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income)) +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  scale_color_distiller(palette = "Greens", direction = 1)+
  scale_radius(range = c(0.5, 6))
```

<img src="04-viz_files/figure-html/unnamed-chunk-23-1.png" width="672" />

#### Legends

In the previous plots we notice that two separate legends are created for size and color. To create one legend where the circles are colored, we use `guides()` like this, specifying the same title for color and size:


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income)) +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  scale_color_distiller(palette = "BuGn", direction = 1)+
  scale_radius(range = c(2, 6))+
  theme_minimal()+
  #customize legend
  guides(color= guide_legend(title = "Median Income"), size=guide_legend(title = "Median Income"))
```

<img src="04-viz_files/figure-html/unnamed-chunk-24-1.png" width="672" />

### Annotation

Annotation is the process of adding text, or 'notes' to your charts. Say we wanted to highlight some details to specific points in our data, for example some of the outliers.

When investigating the outlying point with the highest median age and high percentage of people of color, it turns out that census tract includes Rocky Mountain National Park and the surrounding area, and also the total population of that tract is only 53. Lets add these details to our chart with `annotate()`. This function requires several arguments:

-   `geom`: type of annotation, most often `text`

-   `x`: position on the x axis to put the annotation

-   `y`: position on the y axis to put the annotation

-   `label`: what you want the annotation to say

-   Optional: `color`, `size`, `angle`, and more.


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income)) +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)")+
  scale_color_distiller(palette = "BuGn", direction = 1)+
  scale_radius(range = c(2, 6))+
  theme_minimal()+
  guides(color= guide_legend(title = "Median Income"), size=guide_legend(title = "Median Income"))+
  # add annotation
  annotate(geom = "text", x=76, y = 62,
           label = "Rocky Mountain National Park region \n Total Populaion: 53")
```

<img src="04-viz_files/figure-html/unnamed-chunk-25-1.png" width="672" />

We can also add an arrow to point at the data point the annotation is referring to with `geom_curve` and a few other arguments like so:


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income)) +
  ggtitle("Census Tract socioeconomic data for Larimer County") +
  xlab("Median Age") +
  ylab("People of Color (%)") +
  scale_color_distiller(palette = "BuGn", direction = 1) +
  scale_radius(range = c(2, 6)) +
  theme_minimal() +
  guides(color = guide_legend(title = "Median Income"),
         size = guide_legend(title = "Median Income")) +
  annotate(geom = "text",
           x = 74,
           y = 62,
           label = "Rocky Mountain National Park region \n Total Populaion: 53") +
  # add arrow
  geom_curve(
    aes(
      x = 82,
      xend = 88,
      y = 60,
      yend = 57.5
    ),
    arrow = arrow(length = unit(0.2, "cm")),
    size = 0.5,
    curvature = -0.3
  )
```

```
## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
## ℹ Please use `linewidth` instead.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```

<img src="04-viz_files/figure-html/unnamed-chunk-26-1.png" width="672" />

::: {.alert .alert-info}
Note that with annotations you may need to mess around with the x and y positions to get it just right. Also, the preview you see in the 'plot' window may look jumbled and viewing it by clicking 'Zoom' can help.
:::

### Finalize and save

We are almost done with this figure. I am going to add/change a few more elements below. Feel free to add your own!


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income), alpha = 0.9) +
  labs(
    title = "Socioeconomic data for Larimer County",
    subtitle = "Median age, median income, and percentage of people of color for each census tract",
    x = "Median Age",
    y = "People of Color (%)",
    caption = "Data obtained from the U.S. Census 5-year American Community Survey Samples for 2017-2021"
  )+
  scale_radius(range = c(2, 6)) +
  theme_classic() +
  scale_color_viridis() + #use the Viridis palette
  guides(color = guide_legend(title = "Median Income"),
         size = guide_legend(title = "Median Income")) +
  theme(
    axis.title = element_text(face = "bold", size = 10),
    plot.title = element_text(face = "bold",size = 15, margin = unit(c(1,1,1,1), "cm")),
    plot.subtitle = element_text(size = 10, margin = unit(c(-0.5,0.5,0.5,0.5), "cm")),
    plot.caption = element_text(face = "italic", hjust = -0.2),
    plot.title.position = "plot", #sets the title to the left
    legend.position = "bottom",
    legend.text = element_text(size = 8)
  ) +
  annotate(geom = "text",
           x = 74,
           y = 62,
           label = "Rocky Mountain National Park region \n Total Populaion: 53",
           size = 3,
           color = "black") +
  geom_curve(
    aes(
      x = 82,
      xend = 88,
      y = 60,
      yend = 57.5
    ),
    arrow = arrow(length = unit(0.2, "cm")),
    size = 0.5,
    color = "black",
    curvature = -0.3
  )
```

<img src="04-viz_files/figure-html/unnamed-chunk-27-1.png" width="672" />

**Want to make it dark theme?**

`ggdark` is a fun package to easily convert your figures to various dark themes. If you want to test it out, install the package and try `dark_theme_classic()` instead of `theme_classic()` in the previous figure:


```r
install.packages("ggdark")
```


```r
library(ggdark)
```


```r
census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income), alpha = 0.9) +
  labs(
    title = "Socioeconomic data for Larimer County",
    subtitle = "Median age, median income, and percentage of people of color for each census tract",
    x = "Median Age",
    y = "People of Color (%)",
    caption = "Data obtained from the U.S. Census 5-year American Community Survey Samples for 2017-2021"
  )+
  scale_radius(range = c(2, 6)) +
  dark_theme_classic() +
  scale_color_viridis() + #use the Viridis palette
  guides(color = guide_legend(title = "Median Income"),
         size = guide_legend(title = "Median Income")) +
  theme(
    axis.title = element_text(face = "bold", size = 10),
    plot.title = element_text(face = "bold",size = 15, margin = unit(c(1,1,1,1), "cm")),
    plot.subtitle = element_text(size = 10, margin = unit(c(-0.5,0.5,0.5,0.5), "cm")),
    plot.caption = element_text(face = "italic", hjust = -0.2),
    plot.title.position = "plot", #sets the title to the left
    legend.position = "bottom",
    legend.text = element_text(size = 8)
  ) +
  annotate(geom = "text",
           x = 74,
           y = 62,
           label = "Rocky Mountain National Park region \n Total Populaion: 53",
           size = 3) +
  geom_curve(
    aes(
      x = 82,
      xend = 88,
      y = 60,
      yend = 57.5
    ),
    arrow = arrow(length = unit(0.2, "cm")),
    size = 0.5,
    curvature = -0.3
  )
```

<img src="04-viz_files/figure-html/unnamed-chunk-30-1.png" width="672" />

**Saving with `ggsave`**

You can save your plot in the "Plots" pane by clicking "Export", or you can also do it programmatically with `ggsave()`, which also lets you customize the output file a little more. Note that you can give the argument a variable name of a ggplot object, or **by default it will save the last plot in the "Plots" pane**.


```r
#specify the file path and name, and height/width (if necessary)
ggsave(filename = "data/census_plot.png", width = 6, height = 5, units = "in")
```

#### Want to make it interactive?

The `plotly` package and the `ggplotly()` function lets you make your charts interactive.


```r
install.packages("plotly")
```


```r
library(plotly)
```

We can put our entire ggplot code above inside `ggplotly()` below to make it interactive:


```r
ggplotly(census_data %>%
  ggplot(aes(x = median_age, y = percent_bipoc)) +
  geom_point(aes(size = median_income, color = median_income), alpha = 0.9) +
  labs(
    title = "Socioeconomic data for Larimer County",
    subtitle = "Median age, median income, and percentage of people of color for each census tract",
    x = "Median Age",
    y = "People of Color (%)",
    caption = "Data obtained from the U.S. Census 5-year American Community Survey Samples for 2017-2021"
  )+
  scale_radius(range = c(2, 6)) +
  dark_theme_classic() +
  scale_color_viridis() + #use the Viridis palette
  guides(color = guide_legend(title = "Median Income"),
         size = guide_legend(title = "Median Income")) +
  theme(
    axis.title = element_text(face = "bold", size = 10),
    plot.title = element_text(face = "bold",size = 15, margin = unit(c(1,1,1,1), "cm")),
    plot.subtitle = element_text(size = 10, margin = unit(c(-0.5,0.5,0.5,0.5), "cm")),
    plot.caption = element_text(face = "italic", hjust = -0.2),
    plot.title.position = "plot", #sets the title to the left
    legend.position = "bottom",
    legend.text = element_text(size = 8)
  ))
```

```{=html}
<div id="htmlwidget-d85ef1622100efe3f811" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-d85ef1622100efe3f811">{"x":{"data":[{"x":[29.8,24.2,32.6,40.1,30,29.4,22.6,23.2,24.5,27,19.4,28.4,40.1,34.3,30.1,36.3,27.8,41.5,37.9,34,44.6,57.1,30.2,32.5,27.3,30.6,26.4,28,36.4,43.6,54.3,49.6,35.5,24.6,29.5,38.9,39.2,41.8,33.6,36.2,30.7,32.1,38.9,36.1,42.9,37.8,35.8,36.9,30.7,39.3,36.6,46.9,30.3,37.6,44.3,55,42,55.9,47.3,42.3,48.1,50,57.6,53,31.3,37.6,38.3,56.5,45.4,43,62.3,55.2,49.2,51.6,40.4,38.4,45.9,35.8,35,49.6,44,44.7,61.8,89,53,51.3],"y":[13.7081955163543,16.2698412698413,16.6341272940258,6.54911838790932,14.2926829268293,8.94181960171808,29.759837962963,16.1633493479753,22.6958525345622,8.85662431941924,28.1241341091715,7.23871492476616,10.9748224661072,17.0418006430868,10.9698996655518,14.5723601705543,18.6789388197076,9.2436974789916,19.4548872180451,12.4867724867725,12.7721335268505,4.74368783473604,14.0389105058366,21.7688575209528,18.745247148289,19.5910169800986,13.8800672520082,15.81589958159,21.3188798554652,9.34128336172629,7.01438848920863,13.920046016681,66.1141804788214,25.3155919481406,26.2735412164248,22.5527426160338,10.960960960961,42.8230805913209,18.737565563393,25,24.1459029026458,19.4771241830065,15.0260352095214,17.5846833578792,14.165149760053,16.4490861618799,22.973281571135,12.2115546572343,20.3195854027208,13.699031974186,18.1371454098727,10.5620841002407,19.944232462577,10.6115542663766,19.4259012016021,7.21816707218167,12.8602663486384,7.87545787545788,9.46184738955823,10.4175824175824,12.8051948051948,20.1746529332736,3.43110127282789,14.0962671905697,19.76246105919,13.0434782608696,15.4713940370669,9.40451745379877,4.45109407144193,6.19286346210557,5.16556291390728,1.64271047227926,11.7647058823529,15.1875571820677,21.8319886093972,3.3252427184466,9.72674855853597,6.68355416991426,12.9088378566458,2.30134607034303,10.3042198233562,12.6859928168291,9.54344624447717,55.5555555555556,5.18301610541728,14.5526960784314],"text":["median_age: 29.8<br />percent_bipoc: 13.708196<br />median_income:  42798<br />median_income:  42798","median_age: 24.2<br />percent_bipoc: 16.269841<br />median_income:  36000<br />median_income:  36000","median_age: 32.6<br />percent_bipoc: 16.634127<br />median_income:  72292<br />median_income:  72292","median_age: 40.1<br />percent_bipoc:  6.549118<br />median_income: 104006<br />median_income: 104006","median_age: 30.0<br />percent_bipoc: 14.292683<br />median_income:  64415<br />median_income:  64415","median_age: 29.4<br />percent_bipoc:  8.941820<br />median_income:  60250<br />median_income:  60250","median_age: 22.6<br />percent_bipoc: 29.759838<br />median_income:  40156<br />median_income:  40156","median_age: 23.2<br />percent_bipoc: 16.163349<br />median_income:  31958<br />median_income:  31958","median_age: 24.5<br />percent_bipoc: 22.695853<br />median_income:  40940<br />median_income:  40940","median_age: 27.0<br />percent_bipoc:  8.856624<br />median_income:  62750<br />median_income:  62750","median_age: 19.4<br />percent_bipoc: 28.124134<br />median_income:  22163<br />median_income:  22163","median_age: 28.4<br />percent_bipoc:  7.238715<br />median_income:  73361<br />median_income:  73361","median_age: 40.1<br />percent_bipoc: 10.974822<br />median_income:  86319<br />median_income:  86319","median_age: 34.3<br />percent_bipoc: 17.041801<br />median_income:  53646<br />median_income:  53646","median_age: 30.1<br />percent_bipoc: 10.969900<br />median_income:  60124<br />median_income:  60124","median_age: 36.3<br />percent_bipoc: 14.572360<br />median_income:  80074<br />median_income:  80074","median_age: 27.8<br />percent_bipoc: 18.678939<br />median_income:  55443<br />median_income:  55443","median_age: 41.5<br />percent_bipoc:  9.243697<br />median_income: 115786<br />median_income: 115786","median_age: 37.9<br />percent_bipoc: 19.454887<br />median_income:  64601<br />median_income:  64601","median_age: 34.0<br />percent_bipoc: 12.486772<br />median_income:  72083<br />median_income:  72083","median_age: 44.6<br />percent_bipoc: 12.772134<br />median_income:  95938<br />median_income:  95938","median_age: 57.1<br />percent_bipoc:  4.743688<br />median_income: 109583<br />median_income: 109583","median_age: 30.2<br />percent_bipoc: 14.038911<br />median_income:  60815<br />median_income:  60815","median_age: 32.5<br />percent_bipoc: 21.768858<br />median_income:  65786<br />median_income:  65786","median_age: 27.3<br />percent_bipoc: 18.745247<br />median_income:  67670<br />median_income:  67670","median_age: 30.6<br />percent_bipoc: 19.591017<br />median_income:  79398<br />median_income:  79398","median_age: 26.4<br />percent_bipoc: 13.880067<br />median_income:  54466<br />median_income:  54466","median_age: 28.0<br />percent_bipoc: 15.815900<br />median_income:  42606<br />median_income:  42606","median_age: 36.4<br />percent_bipoc: 21.318880<br />median_income:  92765<br />median_income:  92765","median_age: 43.6<br />percent_bipoc:  9.341283<br />median_income: 116797<br />median_income: 116797","median_age: 54.3<br />percent_bipoc:  7.014388<br />median_income: 162778<br />median_income: 162778","median_age: 49.6<br />percent_bipoc: 13.920046<br />median_income:  71406<br />median_income:  71406","median_age: 35.5<br />percent_bipoc: 66.114180<br />median_income:  36345<br />median_income:  36345","median_age: 24.6<br />percent_bipoc: 25.315592<br />median_income:  57273<br />median_income:  57273","median_age: 29.5<br />percent_bipoc: 26.273541<br />median_income:  61016<br />median_income:  61016","median_age: 38.9<br />percent_bipoc: 22.552743<br />median_income:  94844<br />median_income:  94844","median_age: 39.2<br />percent_bipoc: 10.960961<br />median_income: 105708<br />median_income: 105708","median_age: 41.8<br />percent_bipoc: 42.823081<br />median_income:  93600<br />median_income:  93600","median_age: 33.6<br />percent_bipoc: 18.737566<br />median_income:  95962<br />median_income:  95962","median_age: 36.2<br />percent_bipoc: 25.000000<br />median_income:  79304<br />median_income:  79304","median_age: 30.7<br />percent_bipoc: 24.145903<br />median_income:  84475<br />median_income:  84475","median_age: 32.1<br />percent_bipoc: 19.477124<br />median_income:  94110<br />median_income:  94110","median_age: 38.9<br />percent_bipoc: 15.026035<br />median_income: 101419<br />median_income: 101419","median_age: 36.1<br />percent_bipoc: 17.584683<br />median_income: 151655<br />median_income: 151655","median_age: 42.9<br />percent_bipoc: 14.165150<br />median_income:  68359<br />median_income:  68359","median_age: 37.8<br />percent_bipoc: 16.449086<br />median_income:  57222<br />median_income:  57222","median_age: 35.8<br />percent_bipoc: 22.973282<br />median_income: 100789<br />median_income: 100789","median_age: 36.9<br />percent_bipoc: 12.211555<br />median_income:  70230<br />median_income:  70230","median_age: 30.7<br />percent_bipoc: 20.319585<br />median_income:  77500<br />median_income:  77500","median_age: 39.3<br />percent_bipoc: 13.699032<br />median_income: 145178<br />median_income: 145178","median_age: 36.6<br />percent_bipoc: 18.137145<br />median_income: 153641<br />median_income: 153641","median_age: 46.9<br />percent_bipoc: 10.562084<br />median_income: 131728<br />median_income: 131728","median_age: 30.3<br />percent_bipoc: 19.944232<br />median_income:  94087<br />median_income:  94087","median_age: 37.6<br />percent_bipoc: 10.611554<br />median_income:  77426<br />median_income:  77426","median_age: 44.3<br />percent_bipoc: 19.425901<br />median_income:  80107<br />median_income:  80107","median_age: 55.0<br />percent_bipoc:  7.218167<br />median_income:  86802<br />median_income:  86802","median_age: 42.0<br />percent_bipoc: 12.860266<br />median_income:  86413<br />median_income:  86413","median_age: 55.9<br />percent_bipoc:  7.875458<br />median_income:  79697<br />median_income:  79697","median_age: 47.3<br />percent_bipoc:  9.461847<br />median_income:  99213<br />median_income:  99213","median_age: 42.3<br />percent_bipoc: 10.417582<br />median_income:  83555<br />median_income:  83555","median_age: 48.1<br />percent_bipoc: 12.805195<br />median_income:  62114<br />median_income:  62114","median_age: 50.0<br />percent_bipoc: 20.174653<br />median_income:  62286<br />median_income:  62286","median_age: 57.6<br />percent_bipoc:  3.431101<br />median_income:  91404<br />median_income:  91404","median_age: 53.0<br />percent_bipoc: 14.096267<br />median_income: 127875<br />median_income: 127875","median_age: 31.3<br />percent_bipoc: 19.762461<br />median_income:  56961<br />median_income:  56961","median_age: 37.6<br />percent_bipoc: 13.043478<br />median_income:  65726<br />median_income:  65726","median_age: 38.3<br />percent_bipoc: 15.471394<br />median_income:  66047<br />median_income:  66047","median_age: 56.5<br />percent_bipoc:  9.404517<br />median_income: 110227<br />median_income: 110227","median_age: 45.4<br />percent_bipoc:  4.451094<br />median_income:  89684<br />median_income:  89684","median_age: 43.0<br />percent_bipoc:  6.192863<br />median_income:  89000<br />median_income:  89000","median_age: 62.3<br />percent_bipoc:  5.165563<br />median_income:  73419<br />median_income:  73419","median_age: 55.2<br />percent_bipoc:  1.642710<br />median_income:  83438<br />median_income:  83438","median_age: 49.2<br />percent_bipoc: 11.764706<br />median_income: 119167<br />median_income: 119167","median_age: 51.6<br />percent_bipoc: 15.187557<br />median_income:  84808<br />median_income:  84808","median_age: 40.4<br />percent_bipoc: 21.831989<br />median_income:  91071<br />median_income:  91071","median_age: 38.4<br />percent_bipoc:  3.325243<br />median_income: 156511<br />median_income: 156511","median_age: 45.9<br />percent_bipoc:  9.726749<br />median_income: 109258<br />median_income: 109258","median_age: 35.8<br />percent_bipoc:  6.683554<br />median_income:  99531<br />median_income:  99531","median_age: 35.0<br />percent_bipoc: 12.908838<br />median_income:  95115<br />median_income:  95115","median_age: 49.6<br />percent_bipoc:  2.301346<br />median_income: 118083<br />median_income: 118083","median_age: 44.0<br />percent_bipoc: 10.304220<br />median_income: 111071<br />median_income: 111071","median_age: 44.7<br />percent_bipoc: 12.685993<br />median_income:  91677<br />median_income:  91677","median_age: 61.8<br />percent_bipoc:  9.543446<br />median_income:  75481<br />median_income:  75481","median_age: 89.0<br />percent_bipoc: 55.555556<br />median_income:  74034<br />median_income:  74034","median_age: 53.0<br />percent_bipoc:  5.183016<br />median_income:  85929<br />median_income:  85929","median_age: 51.3<br />percent_bipoc: 14.552696<br />median_income:  63438<br />median_income:  63438"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":["rgba(70,51,127,1)","rgba(72,36,117,1)","rgba(46,110,142,1)","rgba(32,163,134,1)","rgba(52,96,141,1)","rgba(56,88,140,1)","rgba(71,46,124,1)","rgba(72,27,109,1)","rgba(71,47,125,1)","rgba(54,93,141,1)","rgba(68,1,84,1)","rgba(45,112,142,1)","rgba(37,133,142,1)","rgba(62,74,137,1)","rgba(56,88,140,1)","rgba(41,123,142,1)","rgba(61,78,138,1)","rgba(53,183,121,1)","rgba(52,96,141,1)","rgba(46,110,142,1)","rgba(31,150,139,1)","rgba(39,173,129,1)","rgba(56,89,140,1)","rgba(51,98,141,1)","rgba(49,102,142,1)","rgba(41,122,142,1)","rgba(61,77,138,1)","rgba(70,51,127,1)","rgba(33,145,140,1)","rgba(56,185,119,1)","rgba(253,231,37,1)","rgba(47,108,142,1)","rgba(72,37,118,1)","rgba(59,82,139,1)","rgba(56,89,140,1)","rgba(31,148,140,1)","rgba(34,167,133,1)","rgba(32,146,140,1)","rgba(31,150,139,1)","rgba(41,122,142,1)","rgba(38,130,142,1)","rgba(32,146,140,1)","rgba(31,160,136,1)","rgba(202,225,31,1)","rgba(49,103,142,1)","rgba(59,82,139,1)","rgba(31,159,136,1)","rgba(48,106,142,1)","rgba(42,118,142,1)","rgba(170,220,50,1)","rgba(211,226,27,1)","rgba(109,206,89,1)","rgba(32,146,140,1)","rgba(42,118,142,1)","rgba(41,123,142,1)","rgba(36,134,142,1)","rgba(36,134,142,1)","rgba(41,122,142,1)","rgba(30,156,137,1)","rgba(38,129,142,1)","rgba(55,91,141,1)","rgba(54,92,141,1)","rgba(33,143,141,1)","rgba(93,201,98,1)","rgba(59,81,139,1)","rgba(51,98,141,1)","rgba(51,99,141,1)","rgba(40,174,128,1)","rgba(34,139,141,1)","rgba(35,138,141,1)","rgba(45,112,142,1)","rgba(38,129,142,1)","rgba(63,188,115,1)","rgba(37,131,142,1)","rgba(33,142,141,1)","rgba(225,228,24,1)","rgba(38,173,129,1)","rgba(30,156,137,1)","rgba(31,148,140,1)","rgba(59,187,117,1)","rgba(41,175,127,1)","rgba(33,143,141,1)","rgba(44,115,142,1)","rgba(45,113,142,1)","rgba(37,133,142,1)","rgba(53,94,141,1)"],"opacity":0.9,"size":[9.77761078233105,9.04672920223059,12.9486348075566,16.3583403726207,12.101745397958,11.6539487252427,9.49355824708165,8.61215677699285,9.57784938547511,11.922734243079,7.55905511811024,13.0635674949834,14.4567365910325,10.9439249013263,11.6404019351437,13.7853103674774,11.1371279315471,17.6248577326654,12.121743040485,12.9261643382655,15.4909157494594,16.9579471058099,11.7146942522737,12.2491473759394,12.4517041421808,13.7126307634545,11.0320865511766,9.75696805456122,15.1497731702216,17.7335545960784,22.6771653543307,12.8533772200354,9.08382160369199,11.3338789306032,11.7363046079077,15.3732952068543,16.5413295531637,15.2395475331789,15.4934960904306,13.7025244279838,14.2584803930764,15.2943797788175,16.0802011187637,21.4812848283735,12.5257814308965,11.3283957060394,16.012467168269,12.7269405124452,13.5085687983131,20.7849153087632,21.6948080437426,19.3388492228039,15.2919069520534,13.5006127469852,13.7888583363128,14.5086659530784,14.4668429265031,13.7447775113877,15.843024777825,14.1595673225127,11.8543552073414,11.8728476509686,15.0034463343115,18.9245969827146,11.3003344979772,12.2426965235113,12.2772085840015,17.0271862552046,14.8185218980401,14.7449821803601,13.0698033189972,14.1469881602779,17.9883632669872,14.2942826240522,14.9676441033357,22.0033738182187,16.9230049884912,15.8772142956938,15.4024315569877,17.8718178664534,17.1179282460261,15.0327977128592,13.2914976141086,13.1359245563849,14.41480605025,11.9967040175875],"symbol":"circle","line":{"width":1.88976377952756,"color":["rgba(70,51,127,1)","rgba(72,36,117,1)","rgba(46,110,142,1)","rgba(32,163,134,1)","rgba(52,96,141,1)","rgba(56,88,140,1)","rgba(71,46,124,1)","rgba(72,27,109,1)","rgba(71,47,125,1)","rgba(54,93,141,1)","rgba(68,1,84,1)","rgba(45,112,142,1)","rgba(37,133,142,1)","rgba(62,74,137,1)","rgba(56,88,140,1)","rgba(41,123,142,1)","rgba(61,78,138,1)","rgba(53,183,121,1)","rgba(52,96,141,1)","rgba(46,110,142,1)","rgba(31,150,139,1)","rgba(39,173,129,1)","rgba(56,89,140,1)","rgba(51,98,141,1)","rgba(49,102,142,1)","rgba(41,122,142,1)","rgba(61,77,138,1)","rgba(70,51,127,1)","rgba(33,145,140,1)","rgba(56,185,119,1)","rgba(253,231,37,1)","rgba(47,108,142,1)","rgba(72,37,118,1)","rgba(59,82,139,1)","rgba(56,89,140,1)","rgba(31,148,140,1)","rgba(34,167,133,1)","rgba(32,146,140,1)","rgba(31,150,139,1)","rgba(41,122,142,1)","rgba(38,130,142,1)","rgba(32,146,140,1)","rgba(31,160,136,1)","rgba(202,225,31,1)","rgba(49,103,142,1)","rgba(59,82,139,1)","rgba(31,159,136,1)","rgba(48,106,142,1)","rgba(42,118,142,1)","rgba(170,220,50,1)","rgba(211,226,27,1)","rgba(109,206,89,1)","rgba(32,146,140,1)","rgba(42,118,142,1)","rgba(41,123,142,1)","rgba(36,134,142,1)","rgba(36,134,142,1)","rgba(41,122,142,1)","rgba(30,156,137,1)","rgba(38,129,142,1)","rgba(55,91,141,1)","rgba(54,92,141,1)","rgba(33,143,141,1)","rgba(93,201,98,1)","rgba(59,81,139,1)","rgba(51,98,141,1)","rgba(51,99,141,1)","rgba(40,174,128,1)","rgba(34,139,141,1)","rgba(35,138,141,1)","rgba(45,112,142,1)","rgba(38,129,142,1)","rgba(63,188,115,1)","rgba(37,131,142,1)","rgba(33,142,141,1)","rgba(225,228,24,1)","rgba(38,173,129,1)","rgba(30,156,137,1)","rgba(31,148,140,1)","rgba(59,187,117,1)","rgba(41,175,127,1)","rgba(33,143,141,1)","rgba(44,115,142,1)","rgba(45,113,142,1)","rgba(37,133,142,1)","rgba(53,94,141,1)"]}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":46.1535907015359,"r":7.30593607305936,"b":38.854296388543,"l":35.9319219593192},"plot_bgcolor":"rgba(0,0,0,1)","paper_bgcolor":"rgba(0,0,0,1)","font":{"color":"rgba(255,255,255,1)","family":"","size":14.6118721461187},"title":{"text":"<b> Socioeconomic data for Larimer County <\/b>","font":{"color":"rgba(255,255,255,1)","family":"","size":19.9252801992528},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[15.92,92.48],"tickmode":"array","ticktext":["20","40","60","80"],"tickvals":[20,40,60,80],"categoryorder":"array","categoryarray":["20","40","60","80"],"nticks":null,"ticks":"outside","tickcolor":"rgba(204,204,204,1)","ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(178,178,178,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":true,"linecolor":"rgba(255,255,255,1)","linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"<b> Median Age <\/b>","font":{"color":"rgba(255,255,255,1)","family":"","size":13.2835201328352}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.58086302804784,69.3377539791485],"tickmode":"array","ticktext":["0","20","40","60"],"tickvals":[-2.22044604925031e-16,20,40,60],"categoryorder":"array","categoryarray":["0","20","40","60"],"nticks":null,"ticks":"outside","tickcolor":"rgba(204,204,204,1)","ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(178,178,178,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":true,"linecolor":"rgba(255,255,255,1)","linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"x","title":{"text":"<b> People of Color (%) <\/b>","font":{"color":"rgba(255,255,255,1)","family":"","size":13.2835201328352}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(0,0,0,1)","bordercolor":"transparent","borderwidth":0,"font":{"color":"rgba(255,255,255,1)","family":"","size":10.6268161062682},"title":{"text":"Median Income","font":{"color":"rgba(255,255,255,1)","family":"","size":14.6118721461187}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"19a82b78aef":{"x":{},"y":{},"size":{},"colour":{},"type":"scatter"}},"cur_data":"19a82b78aef","visdat":{"19a82b78aef":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

Note that we removed the annotations as `plotly` doesn't yet support them.

------------------------------------------------------------------------

## The Assignment

This week's assignment is to use anything you've learned today, in previous lessons and additional resources (if you want) to make two plots. One 'good plot' and one 'bad plot'. Essentially you will first make a good plot, and then break all the rules of data viz and ruin it. For the bad map you **must specify two things** that are wrong with it (e.g., it is not color-blind friendly, jumbled labels, wrong plot for the job, poor legend or axis descriptions, etc.) Be as 'poorly' creative as you want! Check out [this thread](https://twitter.com/NSilbiger/status/1642006283103662080?s=20) by Dr. Nyssa Silbiger and [this thread](https://twitter.com/drdrewsteen/status/1172547837046820864?s=20) by Dr. Drew Steen for some bad plot examples, which were both the inspiration for this assignment.

You can create these plots with any data (e.g., the census data from today, the penguins data past lessons, or new ones!), the good (and bad) visualization just has to be something we have not made in class before.

To submit the assignment, create an R Markdown document that includes reading in of the data and libraries, and the code to make the good figure and the bad figure. You will render your assignment to Word or HTML (**and make sure both code and plots are shown in the output**), and don't forget to add the two reasons (minimum) your bad figure is 'bad'. You will then submit this rendered document on Canvas. (25 pts. total)

*Note: the class will vote on the worst bad plot and the winner will receive 5 points of extra credit!*

<hr>

### Acknowledgements and Resources

The `ggplot2` content in this lesson was created with the help of [Advanced data visualization with R and ggplot2](https://www.yan-holtz.com/PDF/Ggplot2_advancedTP_correction.html#2-_annotation) by Yan Holtz. For more information on working with census data in R check out [Analyzing US Census Data](https://walker-data.com/census-r/index.html) by Kyle Walker (which includes a [visualization chapter](https://walker-data.com/census-r/exploring-us-census-data-with-visualization.html)).
