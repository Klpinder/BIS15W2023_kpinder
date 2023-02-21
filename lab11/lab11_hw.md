---
title: "Lab 11 Homework"
author: "Kat Pinder"
date: "2023-02-21"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

**In this homework, you should make use of the aesthetics you have learned. It's OK to be flashy!**

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we will use for midterm 2 so this is good practice.

```r
#install.packages("gapminder")
library("gapminder")
```

```
## Warning: package 'gapminder' was built under R version 4.2.2
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NA's are treated in the data.**  

```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, …
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8…
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12…
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, …
```


```r
any_na(gapminder)
```

```
## [1] FALSE
```


```r
miss_var_summary(gapminder)
```

```
## # A tibble: 6 × 3
##   variable  n_miss pct_miss
##   <chr>      <int>    <dbl>
## 1 country        0        0
## 2 continent      0        0
## 3 year           0        0
## 4 lifeExp        0        0
## 5 pop            0        0
## 6 gdpPercap      0        0
```

```r
#no NAs
```


```r
gapminder%>%
  arrange(gdpPercap)
```

```
## # A tibble: 1,704 × 6
##    country          continent  year lifeExp      pop gdpPercap
##    <fct>            <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Congo, Dem. Rep. Africa     2002    45.0 55379852      241.
##  2 Congo, Dem. Rep. Africa     2007    46.5 64606759      278.
##  3 Lesotho          Africa     1952    42.1   748747      299.
##  4 Guinea-Bissau    Africa     1952    32.5   580653      300.
##  5 Congo, Dem. Rep. Africa     1997    42.6 47798986      312.
##  6 Eritrea          Africa     1952    35.9  1438760      329.
##  7 Myanmar          Asia       1952    36.3 20092996      331 
##  8 Lesotho          Africa     1957    45.0   813338      336.
##  9 Burundi          Africa     1952    39.0  2445618      339.
## 10 Eritrea          Africa     1957    38.0  1542611      344.
## # … with 1,694 more rows
```

```r
#doesn't appear to be any negative values to denote NAs
```

**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**


```r
gapminder%>%
  ggplot(aes(x=year,y=lifeExp,group=year,fill=year))+geom_boxplot()
```

![](lab11_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**


```r
gapminder%>%
  filter(year=="1952"|year=="2007")%>%
  ggplot(aes(x=year,y=lifeExp,group=year,fill=year))+geom_boxplot()
```

![](lab11_hw_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**


```r
gapminder%>%
  group_by(country)%>%
  summarise(avg_life=mean(lifeExp), .groups='keep')%>%
  arrange(-avg_life)
```

```
## # A tibble: 142 × 2
## # Groups:   country [142]
##    country     avg_life
##    <fct>          <dbl>
##  1 Iceland         76.5
##  2 Sweden          76.2
##  3 Norway          75.8
##  4 Netherlands     75.6
##  5 Switzerland     75.6
##  6 Canada          74.9
##  7 Japan           74.8
##  8 Australia       74.7
##  9 Denmark         74.4
## 10 France          74.3
## # … with 132 more rows
```

```r
gapminder%>%
  group_by(country)%>%
  slice_max(lifeExp)
```

```
## # A tibble: 142 × 6
## # Groups:   country [142]
##    country     continent  year lifeExp       pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>     <int>     <dbl>
##  1 Afghanistan Asia       2007    43.8  31889923      975.
##  2 Albania     Europe     2007    76.4   3600523     5937.
##  3 Algeria     Africa     2007    72.3  33333216     6223.
##  4 Angola      Africa     2007    42.7  12420476     4797.
##  5 Argentina   Americas   2007    75.3  40301927    12779.
##  6 Australia   Oceania    2007    81.2  20434176    34435.
##  7 Austria     Europe     2007    79.8   8199783    36126.
##  8 Bahrain     Asia       2007    75.6    708573    29796.
##  9 Bangladesh  Asia       2007    64.1 150448339     1391.
## 10 Belgium     Europe     2007    79.4  10392226    33693.
## # … with 132 more rows
```

```r
gapminder%>%
  group_by(country)%>%
  slice_min(lifeExp)
```

```
## # A tibble: 142 × 6
## # Groups:   country [142]
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Albania     Europe     1952    55.2  1282697     1601.
##  3 Algeria     Africa     1952    43.1  9279525     2449.
##  4 Angola      Africa     1952    30.0  4232095     3521.
##  5 Argentina   Americas   1952    62.5 17876956     5911.
##  6 Australia   Oceania    1952    69.1  8691212    10040.
##  7 Austria     Europe     1952    66.8  6927772     6137.
##  8 Bahrain     Asia       1952    50.9   120447     9867.
##  9 Bangladesh  Asia       1952    37.5 46886859      684.
## 10 Belgium     Europe     1952    68    8730405     8343.
## # … with 132 more rows
```
**5. How has life expectancy changed between 1952-2007 for each continent?**

```r
gapminder %>% 
  group_by(year, continent)%>% 
  summarise(avg_life=mean(lifeExp),.groups='keep')%>% 
  ggplot(aes(x=year, y=avg_life, group=continent, color=continent))+
  geom_line()
```

![](lab11_hw_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**

```r
gapminder%>%
  ggplot(aes(x=gdpPercap,y=lifeExp))+geom_point()
```

![](lab11_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

**7. Which countries have had the largest population growth since 1952?**

```r
gapminder%>%
  select(country,pop,year)%>%
  pivot_wider(names_from = year,names_prefix = "yr_",values_from = pop)%>%
  mutate(pop_growth=yr_2007-yr_1952)%>%
  select(country,pop_growth,yr_1952,yr_2007)%>%
  arrange(-pop_growth)
```

```
## # A tibble: 142 × 4
##    country       pop_growth   yr_1952    yr_2007
##    <fct>              <int>     <int>      <int>
##  1 China          762419569 556263527 1318683096
##  2 India          738396331 372000000 1110396331
##  3 United States  143586947 157553000  301139947
##  4 Indonesia      141495000  82052000  223547000
##  5 Brazil         133408087  56602560  190010647
##  6 Pakistan       127924057  41346560  169270617
##  7 Bangladesh     103561480  46886859  150448339
##  8 Nigeria        101912068  33119096  135031164
##  9 Mexico          78556574  30144317  108700891
## 10 Philippines     68638596  22438691   91077287
## # … with 132 more rows
```

**8. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
gapminder%>%
  filter(country=="China"|country=="India"|country=="United States"|country=="Indonesia"|country=="Brazil")%>%
  ggplot(aes(x=year,y=pop,group=country,color=country))+geom_line()
```

![](lab11_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

**9. How does per-capita GDP growth compare between these same five countries?**

```r
gapminder%>%
  filter(country=="China"|country=="India"|country=="United States"|country=="Indonesia"|country=="Brazil")%>%
  ggplot(aes(x=year,y=gdpPercap,group=country,color=country))+geom_line()
```

![](lab11_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

**10. Make one plot of your choice that uses faceting!**

```r
gapminder%>%
  filter(country=="Iceland"|country=="Sweden"|country=="Norway"|country=="Netherlands"|country=="Switzerland")%>%
  ggplot(aes(x=year,y=pop,group=country,color=country))+geom_line()
```

![](lab11_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
