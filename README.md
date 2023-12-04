
<!-- README.md is generated from README.Rmd. Please edit that file -->

# bis620.2023

<!-- badges: start -->

[![R-CMD-check](https://github.com/zihanwang00/bis620.2023/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/zihanwang00/bis620.2023/actions/workflows/R-CMD-check.yaml)
[![test-coverage](https://github.com/zihanwang00/bis620.2023/actions/workflows/test-coverage.yaml/badge.svg)](https://github.com/zihanwang00/bis620.2023/actions/workflows/test-coverage.yaml)
<!-- badges: end -->


The goal of bis620.2023 is to create a package that allows for the 
visualization and a platform that facilitates viewers experience with 
interacting with large and copious amounts of data. It serves to create
an interface where viewers can view the distinct features and 
attributes of the data, specifically comparing to treatment and 
condition. We apply some of the following operations: creating a world 
map of trials, creating a condition keyword search, creating an 
intervention and condition bar chart, creating a pie chart for outcomes,
having an ID count for individual countries, and finally creating a 
picture of a word cloud. Creating a world map of trials allows us to 
see the distribution of trials across the countries. The intervention 
and condition keyword search allows viewers to filter and see the brief 
titles or types of trials that they are interested in. The bar chart of 
the top 10 conditions allows us to select an intervention type and see 
a list of conditions that are  associated with studies involving that 
type of intervention. The pie chart allows us to see the proportion on
the types of outcomes. The ID count allows us to see the frequency and
distribution of subjects across each of the countries. The word cloud 
provides a visual diagram of the frequency of words that appear in the
study. All of these serve to facilitate the ability of processing and
visualizing the data more easily as well as making it more interpretable
for the viewer to see as well. 

## Installation

You can install the development version of bis620.2023 from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("zihanwang00/bis620.2023")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(bis620.2023)
accel |> 
  head(1000) |> 
  plot_accel()
```
<img src="man/figures/README-example-1.png" width="100%" />

```{r}
library(dplyr)
unzip("countries.zip")
countries <- read.csv("filtered_countries.csv")
head(countries)


countries_df <- data.frame(countries)
filtered_countries <- countries_df %>%
  filter(!removed) %>%
  group_by(name) %>%
  summarise(n =n()) %>% 
  rename(ID_count = n)
names_countries <- filtered_countries$name
list(names_countries)
```
<img src="man/figures/fig3.png" width="100%" />
<img src="man/figures/fig4.png" width="100%" />


```{r}
count_country_id <- function(country, countries) {
  countries_df <- data.frame(countries)
  filtered_countries <- countries_df %>%
    filter(!removed) %>%
    group_by(name) %>%
    summarise(n = n()) %>% 
    rename(ID_count = n)
  
  # Find the row matching the specified country
  country_row <- filtered_countries %>%
    filter(name == country)
  
  # Print the row (if found)
  if (nrow(country_row) > 0) {
    print(country_row)
  } else {
    cat("Country not found.")
  }
}

count_country_id("United States", countries)

```
<img src="man/figures/fig2.png" width="100%" />


## Test Coverage Report

You can run the following code to see test report of the package.

``` r
library(covr)
report()
```
<img src="man/figures/coverage.png" width="100%" />
