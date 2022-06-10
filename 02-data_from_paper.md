---
title: "Amount of offspring for C. elegans incubated in different substances"
author: "Thijmen van Brenk"
date: "2022-06-10"
output: bookdown::render_book()
---

# Reproducability

## Reproducing data from a published paper

Here i am showing you how i am able to reproduce results from a published paper    
the data used in this assignment comes from [@vandervoetReportingGuidelineDevelopmental2021]


```r
library(tidyverse)
library(here)
library(readxl)
library(rbbt)
library(RColorBrewer)
```



```r
offspring <- read_excel(here("data/CE.LIQ.FLOW.062_Tidydata.xlsx"), sheet = 1)

# we want to see if the data for the experimental conditions have been imported correctly
offspring %>% select(c("expType", "RawData", "compName", "compConcentration"))
```

```
## # A tibble: 360 x 4
##    expType    RawData compName                   compConcentration
##    <chr>        <dbl> <chr>                      <chr>            
##  1 experiment      44 2,6-diisopropylnaphthalene 4.99             
##  2 experiment      37 2,6-diisopropylnaphthalene 4.99             
##  3 experiment      45 2,6-diisopropylnaphthalene 4.99             
##  4 experiment      47 2,6-diisopropylnaphthalene 4.99             
##  5 experiment      41 2,6-diisopropylnaphthalene 4.99             
##  6 experiment      35 2,6-diisopropylnaphthalene 4.99             
##  7 experiment      41 2,6-diisopropylnaphthalene 4.99             
##  8 experiment      36 2,6-diisopropylnaphthalene 4.99             
##  9 experiment      40 2,6-diisopropylnaphthalene 4.99             
## 10 experiment      38 2,6-diisopropylnaphthalene 4.99             
## # ... with 350 more rows
```

```r
# as we can see, the rawdata should have been an integer, the compname and expType should have been a factor and the compconcentration should have been a double. lets change that

offspring$RawData <- as.integer(offspring$RawData)
offspring$compName <- as.factor(offspring$compName)
offspring$expType <- as.factor(offspring$expType)

offspring_tidy <- offspring
offspring_tidy$compConcentration <- as.numeric(offspring_tidy$compConcentration)

# one of the values in compconcentration is accidentally classified as a character in excel and has now turned into a NA value, we will change this value manually.

character_placement <- which(is.na(offspring_tidy$compConcentration))
character_value <- offspring$compConcentration[character_placement] %>% str_replace(",", ".") %>% parse_number()
offspring_tidy$compConcentration[character_placement] <- character_value

# lets check one last time if the data types are correct.
offspring %>% select(c("RawData", "compName", "compConcentration"))
```

```
## # A tibble: 360 x 3
##    RawData compName                   compConcentration
##      <int> <fct>                      <chr>            
##  1      44 2,6-diisopropylnaphthalene 4.99             
##  2      37 2,6-diisopropylnaphthalene 4.99             
##  3      45 2,6-diisopropylnaphthalene 4.99             
##  4      47 2,6-diisopropylnaphthalene 4.99             
##  5      41 2,6-diisopropylnaphthalene 4.99             
##  6      35 2,6-diisopropylnaphthalene 4.99             
##  7      41 2,6-diisopropylnaphthalene 4.99             
##  8      36 2,6-diisopropylnaphthalene 4.99             
##  9      40 2,6-diisopropylnaphthalene 4.99             
## 10      38 2,6-diisopropylnaphthalene 4.99             
## # ... with 350 more rows
```

```r
# they are so we can now use the data for further analysis
```



```r
offspring_tidy %>%
  ggplot(aes(x = log10(compConcentration + 0.0001), y = RawData)) +
  geom_jitter(aes(shape = expType, colour = compName), width = .1) +
  labs(title = "Amount of offspring from C. elegans incubated in different substances",
       subtitle = "Experiment data from (van der Voet et al. 2021)",
       x = "Log 10 of compound concentration",
       y = "Amount of offspring per C. elegans",
       colour = "Compound name",
       shape = "Experiment type") +
  scale_shape_discrete(labels = c("Negative control", "Positive control", "Vehicle A control", "Experiment")) +
  scale_colour_brewer(palette = "Dark2") +
  theme_classic()
```

<img src="02-data_from_paper_files/figure-html/graphical visualization of the data-1.png" width="672" />

the positive control of this experiment is Ethanol and the negative control is no added substance.
<br>
<br>
<br>
to analyze this experiment I would follow these steps.       
1. making a new column which shows which condition every worm is located in. (for example, group1 would consist of 2,6-diisopropylnaphthalene with a concentration of 4.99 nM, etc.)       
2. checking normality for every condition.        
<br>
_NORMALLY DISTRIBUTED DATA:_        
3. perform ANOVA. with post-hoc tests and check if they differ from the control.       
_NOT NORMALLY DISTRIBUTED DATA:_        
3. perform kruskal - wallis test.       
<br>
4. to visualize this difference, make a smoothed line graph for every the mean of every concentration per substance.        
5. compare these graphs with each other.



```r
normalized_value <- offspring_tidy %>% 
  group_by(compName) %>% filter(compName == "S-medium") %>%
  summarise(mean = mean(RawData, na.rm = T))

offspring_tidy <- offspring_tidy %>% mutate(normalized_offspring = 
                                              RawData/normalized_value$mean)


offspring_tidy %>%
  ggplot(aes(x = log10(compConcentration + 0.0001), y = normalized_offspring)) +
  geom_jitter(aes(shape = expType, colour = compName), width = .1) +
  labs(title = "Amount of offspring from C. elegans incubated in different substances",
       subtitle = "Experiment data from (van der Voet et al. 2021)",
       x = "Log 10 of compound concentration",
       y = "Normalized offspring amount by mean of negative control",
       colour = "Compound name",
       shape = "Experiment type") +
  scale_shape_discrete(labels = c("Negative control", "Positive control", "Vehicle A control", "Experiment")) +
  scale_colour_brewer(palette = "Dark2") +
  theme_classic()
```

<img src="02-data_from_paper_files/figure-html/making normalized values-1.png" width="672" />
      
  We normalize the data so we can see the difference between the different substances more easily.
