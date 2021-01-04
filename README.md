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

## 1.How many breweries are present in each state?
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

plot_usmap(data = Breweries.in.each.state, values = "n", labels=FALSE) + 
  scale_fill_continuous(low = "white", 
                        high = "orange", 
                        name = "# of Breweries", 
                        label = scales::comma) + 
  theme(legend.position = "right") + 
  theme(panel.background = element_rect(colour = "black")) + 
  labs(title = "Number of Breweries by State") + 
  geom_text(data = labels, 
            ggplot2::aes(x = x, y = y, 
            label = scales::number(breweries_count,accuracy = 1)),
            color = "black")

##plot_usmap(include = .northeast_region)
```

## 2.Merge beer data with the breweries data. Print the first 6 observations and the last six observations to check the merged file.
```{r}
merge_df <- merge(x = Beers, y = Breweries,
                  by.x = "Brewery_id", by.y = "Brew_ID", all = TRUE)

names(merge_df)[names(merge_df)=="Name.x"] <- "Beer_name"
names(merge_df)[names(merge_df)=="Name.y"] <- "Brewery_name"

head(merge_df, 6)
tail(merge_df, 6)
```

## 3.Address the missing values in each column.
```{r}
merge_df$Style <- lapply(merge_df$Style,function(x) if(identical(x,"")) NA else x)

sapply(merge_df, function(x) sum(is.na(x)))
```

## 4.Compute the median alcohol content and international bitterness unit for each state. Plot a bar chart to compare.
```{r}
#Puri: I do not remove empty rows from the datset because there are 1,005 missing value for IBU which I think it is huge amount.  Any thought?

merge_df %>%
  ggplot(aes(x=State, y=ABV)) + geom_boxplot() + cord_
```