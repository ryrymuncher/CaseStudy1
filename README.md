---
output: html_document
editor_options: 
  chunk_output_type: console
---
# CaseStudy1
Just try to start!

```{r}
Beers = read.csv(file.choose(),header = TRUE)
Breweries = read.csv(file.choose(),header = TRUE)
```

#1.   How many breweries are present in each state?
```{r}
table(Breweries$State)

install.packages("dplyr")
library(dplyr)
install.packages("ggplot2")
library(ggplot2)
install.packages("stringr")
library(stringr)

Breweries = as.data.frame(Breweries)
Breweries.in.each.state = Breweries %>% count(State)

Breweries.in.each.state$State <- str_replace_all(string=Breweries.in.each.state$State, pattern=" ", repl="")
names(Breweries.in.each.state)[1] <- "state"

install.packages("usmap")
library(usmap)

centroid_labels <- utils::read.csv(system.file("extdata", paste0("us_", "states", "_centroids.csv"), package = "usmap"), stringsAsFactors = FALSE)

labels <- merge(x = centroid_labels, y = Breweries.in.each.state, by.x = "abbr", by.y = "state", all.x=TRUE)
names(labels)[6] <- "breweries_count"

plot_usmap(data = Breweries.in.each.state, values = "n", labels=FALSE) + scale_fill_continuous( low = "white", high = "orange", name = "# of Breweries", label = scales::comma) + theme(legend.position = "right") + theme(panel.background = element_rect(colour = "black")) + labs(title = "Number of Breweries by State") + geom_text(data = labels, ggplot2::aes(x = x, y = y, label = scales::number(breweries_count,accuracy = 1)), color = "black")

plot_usmap(include = .northeast_region)
```