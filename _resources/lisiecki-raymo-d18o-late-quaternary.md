---
title: "Lisiecki and Raymo (2005) Marine Oxygen Isotope curve - Late Quaternary"
image: 
categories:
  - data-vis
tags:
  - quaternary-science
  - geo-science
---

Plot of a Late Quaternary marine oxygen isotope curve. 

Download the plot, view the `R` code, and fork the repo.

## Download

<figure class="align-centre">
  <a href="{{ site.url }}{{ site.baseurl }}/assets/images/geo-science/ois-plot.png"><img src="{{ site.url }}{{ site.baseurl }}/assets/images/geo-science/ois-plot.png" alt="Late Quaternary oxygen isotope curve."></a>
  <figcaption>Marine oxygen isotope curve for the last 430 thousand years (kyr). Data from <a href="http://www.lorraine-lisiecki.com/stack.html" target="_blank">Lisiecki and Raymo (2005).</a> Author: Mark Ruddy, 2017. Download this plot <a href="{{ site.downloadurl }}06f678dc/LisieckiRaymo2005_d18O.pdf">here.</a></figcaption>
</figure> 


## `R` code
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


Focus on the Late Quaternary (around the last 400 thousand years).

```r
colnames(lr04) <- c("Age", "d18o", "d18o_sd") 
lr04.cut <- lr04 %>% filter(Age <= 435)
```

Plot the curve.

```r
# Labels and adornment
int.n <- c("Holocene", "Stage 3", "Stage 5", "Stage 7", "Stage 9", "Stage 11") # interglacial labels
gla.n <- c("Stage 2", "Stage 4", "Stage 6", "Stage 8", "Stage 10") # glacial labels

int.x <- c(5, 49, 93, 219, 322, 404) # interglacial x placement
gla.x <- c(25, 67, 160, 280, 365) # glacial x placement

rec.xmin <- c(0, 38, 75, 190, 310, 390) # interglacial rectangle limits
rec.xmax <- c(11.7, 58, 115, 245, 335, 420) # interglacial rectangle limits

t.size <- 4 # text size

# Plot
p <- ggplot(lr04.cut, aes(x = Age, y= d18o)) +
  geom_line() + 
  scale_y_reverse() + 
  scale_x_reverse(lim=c(460,0)) +
  theme_light() +
  theme(axis.text=element_text(size=12), axis.title=element_text(size=16)) +
  annotate("text", x=int.x, y=2.9, label=int.n, size=t.size, colour="#f1a340") +
  annotate("text", x=gla.x, y=5.3, label=gla.n, size=t.size, colour="#4D3E87") +
  annotate("text", x=125, y=2.9, label= "Stage 5e", size=t.size, colour="#AA3108") +
  annotate("rect", xmin=rec.xmin, ymin=3.0, xmax=rec.xmax, ymax=5.2, alpha=0.1) +
  annotate("rect", xmin=115, ymin=3.0, xmax=130, ymax=5.2, alpha=0.3, fill="#AA3108") +
  xlab("Age (kyr)") +
  ylab(expression(paste(delta^{18}, "O"))) + 
  annotate("text", x=460, y=3.3, label= "Warmer", size=5, angle=90, colour="#f1a340") + 
  annotate("text", x=460, y=4.7, label= "Colder", size=5, angle=90, colour="#4D3E87")
```

Add a footnote.

```r
# from http://statmodeling.com/best-way-to-add-a-footnote-to-a-plot-created-with-ggplot2.html

footnote <- "Mark Ruddy, 2017"
grid.newpage()
g <- arrangeGrob(p, bottom = textGrob(footnote, x = 0.82, hjust = -0.6, vjust=-2, gp = gpar(fontface = "italic", alpha=0.5, fontsize = 10)))
grid.draw(g)
```

Export.

```r
ggsave("ois-plot2.pdf",plot = g, path = "./", width = 280, height = 120, units = "mm")

# alternative format
## ggsave("ois-plot2.png",plot = g, path = "./", width = 280, height = 120, units = "mm")
```

Clean up. 

```r
rm(list=setdiff(ls(),c("g","lr04")))
```

## Fork the repo.

<iframe style="display: inline-block;" src="https://ghbtns.com/github-btn.html?user=markruddy&repo=ois5e-plot&type=fork&count=true&size=large" frameborder="0" scrolling="0" width="158px" height="30px"></iframe>




