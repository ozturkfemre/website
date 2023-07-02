---
date: "2023-03-22T22:53:58+05:30"
draft: false
hideLastModified: true
summary: theme() function in the ggplot2 package is used to customize the appearance of the drawn plots. It is a comprehensive function with dozens of arguments, although I don't know exactly how many. Below you can find some widely used arguments and what they do
tags:
- R
- Tidyverse
- ggplot
title: Create your own ggplot theme!
---

------------------------------------------------------------------------

If you are doing any work related to statistics, you will eventually need to have a plot drawn. One of the important things to consider when plotting a plot is how the plot looks. The design of the plot is at least as important as the information it provides, because it may not be possible to read information from a poorly designed plot.

Designing a plot can be long and challenging. Fortunately, some plot themes are available both in ggplot2 package and in additional packages like ggthemes. However, let's say you want to make your own theme; is this possible? Of course it is!

One of the functions in ggplot2 package, you can make your own theme and use it in every project. In this post, I will explain how you can create your own theme in R.

------------------------------------------------------------------------

theme() function in the ggplot2 package is used to customize the appearance of the drawn plots. It is a comprehensive function with dozens of arguments, although I don't know exactly how many. Below you can find some widely used arguments and what they do.

-   title: it is used to set the appearance of the chart title. For example, title = element_text(size = 14, face = "bold") sets the font size of the title to 14 and the boldness to bold.\
-   axis.title: it is used to set the appearance of axis titles. For example, axis.title.x = element_text(size = 12) sets the font size of the x axis title to 12.
-   axis.text: it is used to set the appearance of axis texts. For example, axis.text.y = element_text(angle = 90, hjust = 0.5) rotates the y axis texts 90 degrees and centers the horizontal alignment.
-   legend.title: it is used to set the appearance of the legend title.
-   legend.text: it is used to set the appearance of the legend texts.\
-   panel.background: it is used to set the background of the drawing panel.\
-   panel.grid: it is used to set the appearance of the grids in the drawing panel.

Following code chunk shows how default line plot looks like:

```         
library(ggplot2) # loading library

# creating a data frame
xValue <- 1:10 
yValue <- cumsum(rnorm(10))
data <- data.frame(xValue,yValue)

# Plot
ggplot(data, aes(x=xValue, y=yValue)) +
  geom_line()
```

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*5SmPZr7lUQhG52jEZSVpXw.jpeg)

However, if we change some of the arguments using theme() function, it will look like the following:

```         
ggplot(data, aes(x = xValue, y = yValue)) +
  geom_line()+
  labs(title = "plot.title")+
  xlab("axis.title") +
  ylab("axis.text") +
  theme(
    plot.title = element_text(size = 16, face = "bold"),
    axis.title = element_text(size = 12),
    axis.text = element_text(size = 10),
    panel.background = element_rect(fill = "white"),
    panel.grid.major = element_line(color = "lightgray", linetype = "dashed"),
    plot.background = element_rect(fill = "white"),
    plot.margin = margin(0.25, 0.5, 0.5, 0.5, "cm")
  )
```

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*HR4S2Do1gmOI0mDKWTXQ4w.jpeg)

------------------------------------------------------------------------

As I mentioned before, it is also possible to use available themes both within the ggplot2 package and through some special packages. In this post, lets focus on ggthemes package. Content of the ggthemes package consists of a set of predefined theme functions containing various themes and graphic styles. Some popular themes are:

-   theme_economist(): it emulates the graphic style of The Economist magazine.\
-   theme_fivethirtyeight(): it emulates the graphical style of FiveThirtyEight newspaper.\
-   theme_gdocs(): it emulates the graphic style of Google Docs.\
-   theme_wsj(): it emulates the graphic style of The Wall Street Journal.\
-   theme_tufte(): it follows the graphic principles of Edward Tufte.

Besides these themes, ggthemes package also provides themes with different color palettes and graphic styles.

Below, you can see how theme_economist is used on the same data set, and how it is looks.

```         
library(ggthemes)
ggplot(data, aes(x=xValue, y=yValue)) +
  geom_line()+
  theme_economist()
```

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*6-7mA7cO21tqP8rI14hK4A.jpeg)

------------------------------------------------------------------------

## Creating your own theme

Using theme() function, we can create a theme for ourselves through changes to various arguments and use it in all our analyses from now on. In this section we will focus on how to do this!

At first, lets create our theme!

```         
my_theme <- theme(
  plot.title = element_text(size = 16, face = "bold"), # Font size set to 16 and bold.
  axis.title = element_text(size = 14), # Font size set to 12.
  axis.text = element_text(size = 10), # Font size set to 10.
  legend.title = element_text(size = 12, face = "bold"), # Font size of the title of the legend set to 12 and bold.
  legend.text = element_text(size = 10), # font size of the text in the legend
  panel.background = element_rect(fill = "cornsilk"), # color of the panel background
  panel.grid.major = element_line(color = "#b29a9a", linetype = "dashed"), # color and type of the panel lines
  panel.grid.minor = element_blank(), # invisible auxiliary grids
  plot.background = element_rect(fill = "cornsilk"), # plot's background
  plot.margin = margin(1, 1, 1, 1, "cm"), # chart margins
  strip.background = element_rect(fill = "cornsilk", color = "#ff975d"), # strip background
  strip.text = element_text(size = 12, face = "bold"), # strip texts
  plot.title.position = "plot", #position of the plot title
  legend.position = "right", # position of the legend
  legend.box.background = element_rect(color = "cornsilk"), # background of the plot
  legend.key.size = unit(1, "cm") # size of the legends key
)
```

At the end, let's draw a plot with our new theme:

```         
ggplot(data, aes(x=xValue, y=yValue)) +
  geom_line()+
  labs(title = "My theme") +
  my_theme
```

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*RPQUsbbzddrrX7LtID1tCw.jpeg)
