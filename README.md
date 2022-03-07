---
title: 'Homework #6'
author: "Nick Preszler"
date: "3/9/2022"
output: html_document
---
Import Packages and Data
```{r}
library(tidyverse)
happy = readRDS("~/DS202/Homework-6/data/HAPPY.rds")
```

Clean Data
```{r}
h1 = replace(happy, happy %in% c('IAP', 'DK', 'NA'), NA)
h1 = replace(happy, happy == 'IAP', NA)
h1 = replace(h1, h1 == 'DK', NA)
h1 = replace(h1, h1 == 'NA', NA)

#Change age to numeric
h1 = h1 %>% mutate(AGE = replace(AGE, AGE == "89 OR OLDER", 89)) %>%
  mutate(AGE = as.numeric(AGE, na.rm = TRUE))
```

Reorder Factors & Save RDS file
```{r}
h1$DEGREE = factor(h1$DEGREE, levels=c('LT High School',
                                    'High School',
                                    'Junior College',
                                    'Bachelor',
                                    'Graduate'))
saveRDS(h1,'happiness')
```

Is there a relationship between happiness and sex of marital status?
Visualisation of relationship between happiness and sex broken down by marital status.
```{r}
h1 %>% ggplot(aes(x=SEX,fill=HAPPY)) + geom_bar() + facet_wrap(~MARITAL)
```

The above visualization seperates the happiness of individuals by their sex and marital status and plots the quanitiy of each happiness category in the sex-marital status pairs with differing colors. This visualization suggests that there is no large impact on the happiness of an individual on the basis of their sex or marital status. Married people, for example, have a very similar ratio of happiness categories as divorced people. Similarly, male and female married people have very similar distributions of happiness.
