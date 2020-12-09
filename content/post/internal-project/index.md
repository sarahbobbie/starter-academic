---
title: "Creating Beautiful, Informative Visualizations with R"
external_link: ''
date: '2016-04-27T00:00:00Z'
links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/georgecushen
slides: example
summary: Use ggplot to visualize your data.
image:
  caption: null
  focal_point: Smart
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''
---

R is a programming language that can be used to accomplish a wide variety of tasks. When managing a research project, R can serve as an excellent tool for nearly every step, from wrangling data to performing statistical analyses to producing effective visualizations. In this post, I will walk you through the basic steps of creating such visualizations using ggplot, a plotting package that provides a simple and intuitive way to create plots from your data.

If you'd like to follow along with my plots, you can download {{< staticref "media/ggplot_tutorial_dataset.csv" "newtab" >}}this made-up dataset{{< /staticref >}}.

First, you'll need to have R import the data. I like to use the function read_csv, which imports your data as a tibble; if you import the data this way, you'll need to install tidyverse and call readr from the library. Here's how I imported my data: 
```{r}
tutorial_csv <- read_csv("./ggplot_tutorial_dataset.csv")
```
Now let's take a look at what kind of data we have. 
I recommend taking a look at {{< staticref "media/ggplot2-cheatsheet.pdf" "newtab" >}}this ggplot cheatsheet{{< /staticref >}}. It's an excellent reference for all aspects of ggplot, and can even be used to help you figure out which type of plot is most suitable for your data.

You can also play around with the aesthetics of the plot. Select colours based on their names in R using {{< staticref "media/Rcolor.pdf" "newtab" >}}this handy chart,{{< /staticref >}} or enter the HEX values for any colour you like. You can even find some downloadable user-made colour palettes that will give your plots a nice cohesive look - [this Wes Anderson-inspired package](https://github.com/karthik/wesanderson) is a personal favourite. 




