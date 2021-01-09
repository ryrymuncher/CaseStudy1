# MSDS 6306: Doing Data Science - Case Study 01

## Beers and Breweries of the United States

### Team 3 

### Data Files:
- **Beers.csv** - data set in a comma-seperated values list containing 2410 beers and key data  
  - ***Name:***  a character string describing the beer's name
  - ***Beer_ID:***  an integer key value (primary) used to identify the beer
  - ***ABV:***  Alcohol by Volume; a double used to describe the alcohol content of the beer (e.g. 0.061 is 6.1%)
  - ***IBU:***  International Bitterness Units; an integer value from 1 (least) to 100 (most) used to describe the bitternes of a beer 
  - ***Brewery_id:***  an integer key value (foreign) used to map the beer to the breweries in the Breweries.csv data set.
  - ***Style:***  a character string used to describe the style of beer. Some examples are: IPA, Pilsner, Stout. Imports into R as a factor.
  - ***Ounces:***  a double used to describe the number of fluid ounces in a standard packaged beer. Typically 12 or 16 ounces.

- **Breweries.csv** - data set in a comma-seperated values list containing 558 breweries and key data  
  - ***Brew_ID:***  an integer key value (primary) used to identify the brewery.
  - ***Name:***  a character string describing the brewery's name
  - ***City:***  a character string describing the city the brewery is located in
  - ***State:***   a character string describing the state the brewery is located in. Used 2-digit character codes. Imports into R as a factor.
