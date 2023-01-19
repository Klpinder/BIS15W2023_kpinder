<<<<<<< HEAD
---
title: "Lab 3 Homework"
author: "Kat Pinder"
date: "2023-01-19"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```


## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

allison cicchetti 1976

```r
?msleep
```

```
## starting httpd help server ... done
```

2. Store these data into a new data frame `sleep`.

```r
#setwd("~/Desktop/BIS15W2023_kpinder-main/lab3/data")
sleep <- readr::read_csv("data/mammals_sleep_allison_cicchetti_1976.csv")
```

```
## Rows: 62 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): species
## dbl (10): body weight in kg, brain weight in g, slow wave ("nondreaming") sl...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
#I initially did created sleep data frame using the data in the lab 3 file so I added code using msleep
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  


```r
dim(sleep)
```

```
## [1] 62 11
```

```r
#62 rows and 11 columns so 11 variables and 62 observations for each variable
```


```r
dim(msleep)
```

```
## [1] 83 11
```

```r
#83 rows and 11 columns so 11 variables and 83 observations for each variable
```


4. Are there any NAs in the data? How did you determine this? Please show your code.  



```r
anyNA(sleep, recursive=FALSE)
```

```
## [1] FALSE
```

```r
#no, but there are values -999.0 which are impossible so I think those indicate an NA
```


```r
anyNA(msleep, recursive = FALSE)
```

```
## [1] TRUE
```

```r
#yes, there are NAs
```


5. Show a list of the column names is this data frame.

```r
names(sleep)
```

```
##  [1] "species"                                                        
##  [2] "body weight in kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```


```r
names(msleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```


6. How many herbivores are represented in the data?  

```r
view(sleep)
#data doesn't appear to distinguish between herbivore, omnivore, carnivore
```


```r
view(msleep)
```


```r
herbivores <- filter(msleep, vore=="herbi")
herbivores
```

```
## # A tibble: 32 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake brainwt  bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>   <dbl>   <dbl>
##  1 Moun… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA      1.35e+0
##  2 Cow   Bos   herbi Arti… domest…     4       0.7   0.667  20    0.423  6   e+2
##  3 Thre… Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA      3.85e+0
##  4 Roe … Capr… herbi Arti… lc          3      NA    NA      21    0.0982 1.48e+1
##  5 Goat  Capri herbi Arti… lc          5.3     0.6  NA      18.7  0.115  3.35e+1
##  6 Guin… Cavis herbi Rode… domest…     9.4     0.8   0.217  14.6  0.0055 7.28e-1
##  7 Chin… Chin… herbi Rode… domest…    12.5     1.5   0.117  11.5  0.0064 4.2 e-1
##  8 Tree… Dend… herbi Hyra… lc          5.3     0.5  NA      18.7  0.0123 2.95e+0
##  9 Asia… Elep… herbi Prob… en          3.9    NA    NA      20.1  4.60   2.55e+3
## 10 Horse Equus herbi Peri… domest…     2.9     0.6   1      21.1  0.655  5.21e+2
## # … with 22 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

```r
dim(herbivores)
```

```
## [1] 32 11
```

```r
#32 rows: there are 32 herbivores
```



7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
names(sleep)[names(sleep)=="body weight in kg"] <- "body_weight_in_kg"
names(sleep)
```

```
##  [1] "species"                                                        
##  [2] "body_weight_in_kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```


```r
large_sleep <- filter(sleep,body_weight_in_kg>=200)
large_sleep
```

```
## # A tibble: 7 × 11
##   species        body_…¹ brain…² slow …³ parad…⁴ total…⁵ maxim…⁶ gesta…⁷ preda…⁸
##   <chr>            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
## 1 African eleph…    6654    5712  -999    -999       3.3    38.6     645       3
## 2 Asian elephant    2547    4603     2.1     1.8     3.9    69       624       3
## 3 Cow                465     423     3.2     0.7     3.9    30       281       5
## 4 Giraffe            529     680  -999       0.3  -999      28       400       5
## 5 Gorilla            207     406  -999    -999      12      39.3     252       1
## 6 Horse              521     655     2.1     0.8     2.9    46       336       5
## 7 Okapi              250     490  -999       1    -999      23.6     440       5
## # … with 2 more variables: `sleep exposure index (1-5)` <dbl>,
## #   `overall danger index (1-5)` <dbl>, and abbreviated variable names
## #   ¹​body_weight_in_kg, ²​`brain weight in g`,
## #   ³​`slow wave ("nondreaming") sleep (hrs/day)`,
## #   ⁴​`paradoxical ("dreaming") sleep (hrs/day)`,
## #   ⁵​`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`,
## #   ⁶​`maximum life span (years)`, ⁷​`gestation time (days)`, …
```



```r
small_sleep <- filter(sleep,body_weight_in_kg<=1)
small_sleep
```

```
## # A tibble: 21 × 11
##    species       body_…¹ brain…² slow …³ parad…⁴ total…⁵ maxim…⁶ gesta…⁷ preda…⁸
##    <chr>           <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1 African gian…   1         6.6     6.3     2       8.3     4.5      42       3
##  2 Arctic groun…   0.92      5.7  -999    -999      16.5  -999        25       5
##  3 Big brown bat   0.023     0.3    15.8     3.9    19.7    19        35       1
##  4 Chinchilla      0.425     6.4    11       1.5    12.5     7       112       5
##  5 Desert hedge…   0.55      2.4     7.6     2.7    10.3  -999      -999       2
##  6 Eastern Amer…   0.075     1.2     6.3     2.1     8.4     3.5      42       1
##  7 European hed…   0.785     3.5     6.6     4.1    10.7     6        42       2
##  8 Galago          0.2       5       9.5     1.2    10.7    10.4     120       2
##  9 Golden hamst…   0.12      1      11       3.4    14.4     3.9      16       3
## 10 Ground squir…   0.101     4      10.4     3.4    13.8     9        28       5
## # … with 11 more rows, 2 more variables: `sleep exposure index (1-5)` <dbl>,
## #   `overall danger index (1-5)` <dbl>, and abbreviated variable names
## #   ¹​body_weight_in_kg, ²​`brain weight in g`,
## #   ³​`slow wave ("nondreaming") sleep (hrs/day)`,
## #   ⁴​`paradoxical ("dreaming") sleep (hrs/day)`,
## #   ⁵​`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`,
## #   ⁶​`maximum life span (years)`, ⁷​`gestation time (days)`, …
```

Msleep

```r
large_msleep <- filter(msleep,bodywt>=200)
large_msleep
```

```
## # A tibble: 7 × 11
##   name    genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake brainwt bodywt
##   <chr>   <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>   <dbl>  <dbl>
## 1 Cow     Bos   herbi Arti… domest…     4       0.7   0.667  20     0.423   600 
## 2 Asian … Elep… herbi Prob… en          3.9    NA    NA      20.1   4.60   2547 
## 3 Horse   Equus herbi Peri… domest…     2.9     0.6   1      21.1   0.655   521 
## 4 Giraffe Gira… herbi Arti… cd          1.9     0.4  NA      22.1  NA       900.
## 5 Pilot … Glob… carni Ceta… cd          2.7     0.1  NA      21.4  NA       800 
## 6 Africa… Loxo… herbi Prob… vu          3.3    NA    NA      20.7   5.71   6654 
## 7 Brazil… Tapi… herbi Peri… vu          4.4     1     0.9    19.6   0.169   208.
## # … with abbreviated variable names ¹​conservation, ²​sleep_total, ³​sleep_rem,
## #   ⁴​sleep_cycle
```


```r
small_msleep <- filter(msleep,bodywt<=1)
small_msleep
```

```
## # A tibble: 36 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  2 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  3 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  4 Guin… Cavis herbi Rode… domest…     9.4     0.8   0.217  14.6  0.0055   0.728
##  5 Chin… Chin… herbi Rode… domest…    12.5     1.5   0.117  11.5  0.0064   0.42 
##  6 Star… Cond… omni  Sori… lc         10.3     2.2  NA      13.7  0.001    0.06 
##  7 Afri… Cric… omni  Rode… <NA>        8.3     2    NA      15.7  0.0066   1    
##  8 Less… Cryp… omni  Sori… lc          9.1     1.4   0.15   14.9  0.00014  0.005
##  9 Big … Epte… inse… Chir… lc         19.7     3.9   0.117   4.3  0.0003   0.023
## 10 Euro… Erin… omni  Erin… lc         10.1     3.5   0.283  13.9  0.0035   0.77 
## # … with 26 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```


8. What is the mean weight for both the small and large mammals?

```r
small_kg <- small_sleep$body_weight_in_kg
mean(small_kg)
```

```
## [1] 0.3324286
```


```r
large_kg <- large_sleep$body_weight_in_kg
mean(large_kg)
```

```
## [1] 1596.143
```

Msleep

```r
smallm_kg <- small_msleep$bodywt
mean(smallm_kg)
```

```
## [1] 0.2596667
```


```r
largem_kg <- large_msleep$bodywt
mean(largem_kg)
```

```
## [1] 1747.071
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  


```r
names(small_sleep)[names(small_sleep)=="total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"] <- "total_sleep"
```


```r
names(large_sleep)[names(large_sleep)=="total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"] <- "total_sleep"
```



```r
large_time <- large_sleep$total_sleep
mean(large_time)
```

```
## [1] -281.7143
```


```r
small_time <- small_sleep$total_sleep
mean(small_time)
```

```
## [1] 12.71905
```

Msleep

```r
largem_time <- large_msleep$sleep_total
mean(largem_time)
```

```
## [1] 3.3
```


```r
smallm_time <- small_msleep$sleep_total
mean(smallm_time)
```

```
## [1] 12.65833
```


10. Which animal is the sleepiest among the entire dataframe?

```r
#sleepiest=most time sleeping
view(sleep)
#filter by total sleep from greatest to least, should see little brown bat at the top of the list with 19.9 hrs of sleep per day total
```


```r
view(msleep)
#filter sleep_total when viewing msleep by greatest to least, little brown bat should be at the top of the list with 19.9 hrs of total sleep
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
=======
---
title: "Lab 3 Homework"
author: "Kat Pinder"
date: "2023-01-17"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```


## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

allison cicchetti 1976

```r
#is there code that will identify the publication? I just looked at the name of the file
```

2. Store these data into a new data frame `sleep`.

```r
#setwd("~/Desktop/BIS15W2023_kpinder-main/lab3/data")
sleep <- readr::read_csv("data/mammals_sleep_allison_cicchetti_1976.csv")
```

```
## Rows: 62 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): species
## dbl (10): body weight in kg, brain weight in g, slow wave ("nondreaming") sl...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

62 rows and 11 columns so 11 variables and 62 observations for each variable


```r
dim(sleep)
```

```
## [1] 62 11
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

no, but there are values -999.0 which are impossible so I think those indicate an NA

```r
anyNA(sleep, recursive=FALSE)
```

```
## [1] FALSE
```

5. Show a list of the column names is this data frame.

```r
names(sleep)
```

```
##  [1] "species"                                                        
##  [2] "body weight in kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```

6. How many herbivores are represented in the data?  

```r
view(sleep)
#data doesn't appear to distinguish between herbivore, omnivore, carnivore, not sure how to 
```

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
names(sleep)[names(sleep)=="body weight in kg"] <- "body_weight_in_kg"
names(sleep)
```

```
##  [1] "species"                                                        
##  [2] "body_weight_in_kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```


```r
large_sleep <- filter(sleep,body_weight_in_kg>=200)
large_sleep
```

```
## # A tibble: 7 × 11
##   species        body_…¹ brain…² slow …³ parad…⁴ total…⁵ maxim…⁶ gesta…⁷ preda…⁸
##   <chr>            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
## 1 African eleph…    6654    5712  -999    -999       3.3    38.6     645       3
## 2 Asian elephant    2547    4603     2.1     1.8     3.9    69       624       3
## 3 Cow                465     423     3.2     0.7     3.9    30       281       5
## 4 Giraffe            529     680  -999       0.3  -999      28       400       5
## 5 Gorilla            207     406  -999    -999      12      39.3     252       1
## 6 Horse              521     655     2.1     0.8     2.9    46       336       5
## 7 Okapi              250     490  -999       1    -999      23.6     440       5
## # … with 2 more variables: `sleep exposure index (1-5)` <dbl>,
## #   `overall danger index (1-5)` <dbl>, and abbreviated variable names
## #   ¹​body_weight_in_kg, ²​`brain weight in g`,
## #   ³​`slow wave ("nondreaming") sleep (hrs/day)`,
## #   ⁴​`paradoxical ("dreaming") sleep (hrs/day)`,
## #   ⁵​`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`,
## #   ⁶​`maximum life span (years)`, ⁷​`gestation time (days)`, …
```



```r
small_sleep <- filter(sleep,body_weight_in_kg<=1)
small_sleep
```

```
## # A tibble: 21 × 11
##    species       body_…¹ brain…² slow …³ parad…⁴ total…⁵ maxim…⁶ gesta…⁷ preda…⁸
##    <chr>           <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1 African gian…   1         6.6     6.3     2       8.3     4.5      42       3
##  2 Arctic groun…   0.92      5.7  -999    -999      16.5  -999        25       5
##  3 Big brown bat   0.023     0.3    15.8     3.9    19.7    19        35       1
##  4 Chinchilla      0.425     6.4    11       1.5    12.5     7       112       5
##  5 Desert hedge…   0.55      2.4     7.6     2.7    10.3  -999      -999       2
##  6 Eastern Amer…   0.075     1.2     6.3     2.1     8.4     3.5      42       1
##  7 European hed…   0.785     3.5     6.6     4.1    10.7     6        42       2
##  8 Galago          0.2       5       9.5     1.2    10.7    10.4     120       2
##  9 Golden hamst…   0.12      1      11       3.4    14.4     3.9      16       3
## 10 Ground squir…   0.101     4      10.4     3.4    13.8     9        28       5
## # … with 11 more rows, 2 more variables: `sleep exposure index (1-5)` <dbl>,
## #   `overall danger index (1-5)` <dbl>, and abbreviated variable names
## #   ¹​body_weight_in_kg, ²​`brain weight in g`,
## #   ³​`slow wave ("nondreaming") sleep (hrs/day)`,
## #   ⁴​`paradoxical ("dreaming") sleep (hrs/day)`,
## #   ⁵​`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`,
## #   ⁶​`maximum life span (years)`, ⁷​`gestation time (days)`, …
```


8. What is the mean weight for both the small and large mammals?

```r
small_kg <- small_sleep$body_weight_in_kg
mean(small_kg)
```

```
## [1] 0.3324286
```


```r
large_kg <- large_sleep$body_weight_in_kg
mean(large_kg)
```

```
## [1] 1596.143
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  


```r
names(small_sleep)[names(small_sleep)=="total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"] <- "total_sleep"
```


```r
names(large_sleep)[names(large_sleep)=="total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"] <- "total_sleep"
```



```r
large_time <- large_sleep$total_sleep
mean(large_time)
```

```
## [1] -281.7143
```


```r
small_time <- small_sleep$total_sleep
mean(small_time)
```

```
## [1] 12.71905
```

10. Which animal is the sleepiest among the entire dataframe?

```r
#sleepiest=most time sleeping
view(sleep)
#filter by total sleep from greatest to least, should see little brown bat at the top of the list with 19.9 hrs of sleep per day total
```



## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
>>>>>>> 0bd8726425350c315a0db0ebcafebf9049d158a7
