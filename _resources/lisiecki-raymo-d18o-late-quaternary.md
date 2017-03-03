---
title: "Lisiecki and Raymo (2005) Marine Oxygen Isotope curve - Late Quaternary"
image: 
categories:
  - data-vis
tags:
  - quaternary-science
  - geo-science
---

Here's the `R` code and plot download for a Late Quaternary marine oxygen isotope curve.

## `R` plot
Packages 

```r
library(tidyverse)
library(httr)
library(grid) # plotting
library(gridExtra) # plotting
```


Get marine oxygen isotope data from <http://www.lorraine-lisiecki.com/>

```r
url <- "http://www.lorraine-lisiecki.com/LR04stack.txt"
lr04 <- read.table(url, header=TRUE, sep="\t", quote="", skip=4)
glimpse(lr04)
```

```
## Observations: 2,115
## Variables: 3
## $ Time..ka.                <dbl> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11,...
## $ Benthic.d18O..per.mil.   <dbl> 3.23, 3.23, 3.18, 3.29, 3.30, 3.26, 3...
## $ Standard.error..per.mil. <dbl> 0.03, 0.04, 0.03, 0.03, 0.03, 0.03, 0...
```


Focus on Late Quaternary (around the last 400 thousand years).

```r
colnames(lr04) <- c("Age", "d18o", "d18o_sd") 
lr04.cut <- lr04 %>% filter(Age <= 435)
```

Plot the curve.

```r
# from http://statmodeling.com/best-way-to-add-a-footnote-to-a-plot-created-with-ggplot2.html

footnote <- "Mark Ruddy, 2017"
grid.newpage()
g <- arrangeGrob(p, bottom = textGrob(footnote, x = 0.82, hjust = -0.6, vjust=-2, gp = gpar(fontface = "italic", alpha=0.5, fontsize = 10)))
grid.draw(g)
```


```r
ggsave("ois-plot2.pdf",plot = g, path = "./", width = 280, height = 120, units = "mm")

# alternative format
## ggsave("ois-plot2.png",plot = g, path = "./", width = 280, height = 120, units = "mm")
```

Clean up. 

```r
rm(list=setdiff(ls(),c("g","lr04")))
```

## Download

<figure class="align-centre">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/geo-science/ois-plot.png"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/geo-science/ois-plot.png" alt="Late Quaternary oxygen isotope curve."></a>
  <figcaption>Marine oxygen isotope curve for the last 430 thousand years (kyr). Data from <a href="http://www.lorraine-lisiecki.com/stack.html" target="_blank">Lisiecki and Raymo (2005).</a> Author: Mark Ruddy, 2017. Download this plot <a href="{{ site.downloadurl }}06f678dc/LisieckiRaymo2005_d18O.pdf">here.</a></figcaption>
</figure> 


