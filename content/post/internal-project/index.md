---
title: "Create Beautiful, Informative Visualizations with R"
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

R is a programming language that can be used to accomplish a wide variety of tasks (including [creating this website!)](https://wowchemy.com/docs/). When managing a research project, R can serve as an excellent tool for nearly every step, from wrangling data to performing statistical analyses to producing effective visualizations. In this post, I will walk you through the basic steps of creating such visualizations using ggplot, a plotting package that provides a simple and intuitive way to create plots from your data.

If you'd like to follow along with my plots, you can download {{< staticref "media/ggplot_tutorial_dataset.csv" "newtab" >}}this made-up dataset{{< /staticref >}}.

First, you'll need to have R import the data. I like to use the function read_csv, which imports your data as a tibble; if you import the data this way, you'll need to install tidyverse and call readr from the library. Alternatively, you can just call the entire tidyverse, which will also call ggplot2. Here's how I imported my data: 

```{r}
install.packages("tidyverse")
library(tidyverse)

tutorial_csv <- read_csv("./ggplot_tutorial_dataset.csv")
```

Now let's take a look at what kind of data we have. You'll see that we have columns for participant ID, age, and sex, followed by their relationship status ("Yes" indicates that the participant is in a long-term relationship, whereas "No" indicates that they are not) and some scores on measures of happiness and optimism. In this case, let's assume that a "5" indicates higher levels of happiness/optimism, and a "1" indicates lower levels. 

Now that we're familiar with our data, we can get to work creating some plots. First, I recommend taking a look at {{< staticref "media/ggplot2-cheatsheet.pdf" "newtab" >}}this ggplot cheatsheet{{< /staticref >}}. It's an excellent reference for all aspects of ggplot, and can even be used to help you figure out which type of plot is most suitable for your data.


Let's start with a simple scatterplot of the relationship between "Happiness" and "Optimism" scores. First, you'll want to start with:

```{r}
ggplot()
```

We'll now pass in the arguments for our plot. The first piece of information ggplot needs is the dataframe we're working with. If you recall from above, we've named this dataframe "tutorial_csv". 

```{r}
ggplot(data = tutorial_csv)
```

Now let's add in our variables. After you specify your dataframe, you can specify your x and y variables in the plot's aesthetic properties:

```{r}
ggplot(data = tutorial_csv, aes(x = Happiness, y = Optimism)) 
```

Next, we can add some information about the type of plot we're interested in. If we consult our ggplot cheatsheet, we can see that for a scatterplot, we want to use "geom_jitter". Following the syntax of ggplot, we can add this on using "+" and entering a new line of code: 

```{r}
ggplot(data = tutorial_csv, aes(x = Happiness, y = Optimism)) +
  geom_jitter()
```

Now we need to fill those brackets with some information. Here, we can specify the colour of the dots, as well as their width and height.

```{r}
ggplot(data = tutorial_csv, aes(x = Happiness, y = Optimism)) +
  geom_jitter(colour = "violetred4", width = 0.5, height = 0.5)
```

If you run that code now, you should see a scatterplot appear in the "Plots" tab of the viewer. Yay! 

To save the plot, use ggsave() and specify the name of the plot, the file type, and the size of the image: 

```{r}
ggsave("Happiness_Optimism.png", width = 6, height = 6, dpi = 300)
```

What about other types of plots? ggplot has got you covered. Let's try something a little more complex - a violin plot. 

We start off with the same syntax, but this time, in addition to x and y variables, we also need a "fill" variable. The "fill" variable in a violin plot is what actually makes up our "violins". In this case, let's say we want to examine how age is differentially distributed by relationship status and sex, with one "violin" showing us the data for males and the other "violin" showing us the data from females. We would input the data as follows:


```{r}
ggplot(data = tutorial_csv, aes(x = LT_Relationship, y = Age, fill = Sex)) +
```
Next, we need to specify the type of plot (violin):

```{r}
ggplot(relationship_csv, aes(x = LT_Relationship, y = Age, fill = Sex)) +
  geom_violin() +
```

Finally, you can specify the colours of the plot:

```{r}
ggplot(relationship_csv, aes(x = LT_Relationship, y = Age, fill = Sex)) +
  geom_violin() +
  scale_fill_manual(values = c("lightpink1","lightskyblue1")) 
```

Voila! 

Just for fun, let's build one more plot. This time, let's make a histogram comparing the distribution of Happiness scores by relationship status. You can probably guess how it starts:

```{r}
ggplot(relationship_csv, aes(x = Happiness, fill = LT_Relationship)) +
```
Then we need to specify the type of plot:

```{r}
ggplot(relationship_csv, aes(x = Happiness, fill = LT_Relationship)) +
  geom_histogram()
```

Then we can fill in the specifications for how the plot will look. We can use "colour" to give our bars an outline. "alpha" can be used to specify the transparency of our bars - a value of 1 makes the bars completely opaque, and a value of 0 will make the bars entirely transparent. With position, we can determine how our relationship status information is going to be displayed. The bars can either be stacked on top of each other (position 'stack') or we can have them overlap ('identity'). Finally, with binwidth, you dictate how the x-axis data is grouped. In this case, we want to see the number of people with scores at each happiness value, so our bin width should be 1. Let's give it a try:

```{r}
ggplot(relationship_csv, aes(x = Happiness, fill = LT_Relationship)) +
  geom_histogram(color="#e9ecef", alpha=0.6, position = 'identity', binwidth = 1) 
```

Last but not least, you can specify the colours of your bars:

```{r}
ggplot(relationship_csv, aes(x = Happiness, fill = LT_Relationship)) +
  geom_histogram(color="#e9ecef", alpha=0.6, position = 'identity', binwidth = 1) +
  scale_fill_manual(values=c("mediumseagreen", "chocolate2"))
```

And there you have it! 

Experiment with different elements of the ggplot function. I have a lot of fun playing around with the colours of my plots. Select colours based on their names in R using {{< staticref "media/Rcolor.pdf" "newtab" >}}this handy chart,{{< /staticref >}} or enter the HEX values for any colour you like. You can even find some downloadable user-made colour palettes that will give your plots a nice cohesive look - [this Wes Anderson-inspired package](https://github.com/karthik/wesanderson) is a personal favourite. 

Hopefully, with this tutorial, you have a basic understanding of the functionality of ggplot2 and how to use it in your own data visualizations. Now go forth and ggplot!
