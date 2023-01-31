---
title: "Midterm 1"
author: "Kat Pinder"
date: "2023-01-31"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above.  

After the first 50 minutes, please upload your code (5 points). During the second 50 minutes, you may get help from each other- but no copy/paste. Upload the last version at the end of this time, but be sure to indicate it as final. If you finish early, you are free to leave.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean! Use the tidyverse and pipes unless otherwise indicated. This exam is worth a total of 35 points. 

Please load the following libraries.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ecs21351-sup-0003-SupplementS1.csv`. These data are from Soykan, C. U., J. Sauer, J. G. Schuetz, G. S. LeBaron, K. Dale, and G. M. Langham. 2016. Population trends for North American winter birds based on hierarchical models. Ecosphere 7(5):e01351. 10.1002/ecs2.1351.  

Please load these data as a new object called `ecosphere`. In this step, I am providing the code to load the data, clean the variable names, and remove a footer that the authors used as part of the original publication.

```r
ecosphere <- read_csv("data/ecs21351-sup-0003-SupplementS1.csv", skip=2) %>% 
  clean_names() %>%
  slice(1:(n() - 18)) # this removes the footer
```

Problem 1. (1 point) Let's start with some data exploration. What are the variable names?

```r
names(ecosphere)
```

```
##  [1] "order"                       "family"                     
##  [3] "common_name"                 "scientific_name"            
##  [5] "diet"                        "life_expectancy"            
##  [7] "habitat"                     "urban_affiliate"            
##  [9] "migratory_strategy"          "log10_mass"                 
## [11] "mean_eggs_per_clutch"        "mean_age_at_sexual_maturity"
## [13] "population_size"             "winter_range_area"          
## [15] "range_in_cbc"                "strata"                     
## [17] "circles"                     "feeder_bird"                
## [19] "median_trend"                "lower_95_percent_ci"        
## [21] "upper_95_percent_ci"
```

Problem 2. (1 point) Use the function of your choice to summarize the data.

```r
summary(ecosphere)
```

```
##     order              family          common_name        scientific_name   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##      diet           life_expectancy      habitat          urban_affiliate   
##  Length:551         Length:551         Length:551         Length:551        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  migratory_strategy   log10_mass    mean_eggs_per_clutch
##  Length:551         Min.   :0.480   Min.   : 1.000      
##  Class :character   1st Qu.:1.365   1st Qu.: 3.000      
##  Mode  :character   Median :1.890   Median : 4.000      
##                     Mean   :2.012   Mean   : 4.527      
##                     3rd Qu.:2.685   3rd Qu.: 5.000      
##                     Max.   :4.040   Max.   :17.000      
##                                                         
##  mean_age_at_sexual_maturity population_size     winter_range_area  
##  Min.   : 0.200              Min.   :    15000   Min.   :       11  
##  1st Qu.: 1.000              1st Qu.:  1100000   1st Qu.:   819357  
##  Median : 1.000              Median :  4900000   Median :  2189639  
##  Mean   : 1.592              Mean   : 18446745   Mean   :  5051047  
##  3rd Qu.: 2.000              3rd Qu.: 18000000   3rd Qu.:  6778598  
##  Max.   :12.500              Max.   :300000000   Max.   :185968946  
##                              NA's   :273                            
##   range_in_cbc        strata          circles       feeder_bird       
##  Min.   :  0.00   Min.   :  1.00   Min.   :   2.0   Length:551        
##  1st Qu.:  2.35   1st Qu.:  3.00   1st Qu.:  46.5   Class :character  
##  Median : 30.30   Median : 11.00   Median : 184.0   Mode  :character  
##  Mean   : 38.48   Mean   : 32.43   Mean   : 558.9                     
##  3rd Qu.: 72.95   3rd Qu.: 42.00   3rd Qu.: 661.0                     
##  Max.   :100.00   Max.   :159.00   Max.   :3202.0                     
##                                                                       
##   median_trend   lower_95_percent_ci upper_95_percent_ci
##  Min.   :0.739   Min.   :0.5780      Min.   :    0.798  
##  1st Qu.:0.993   1st Qu.:0.9675      1st Qu.:    1.011  
##  Median :1.009   Median :0.9930      Median :    1.027  
##  Mean   :1.016   Mean   :0.9857      Mean   :   33.709  
##  3rd Qu.:1.030   3rd Qu.:1.0140      3rd Qu.:    1.055  
##  Max.   :1.396   Max.   :1.3080      Max.   :18000.000  
## 
```

```r
dim(ecosphere)
```

```
## [1] 551  21
```

```r
glimpse(ecosphere)
```

```
## Rows: 551
## Columns: 21
## $ order                       <chr> "Anseriformes", "Anseriformes", "Anserifor…
## $ family                      <chr> "Anatidae", "Anatidae", "Anatidae", "Anati…
## $ common_name                 <chr> "American Black Duck", "American Wigeon", …
## $ scientific_name             <chr> "Anas rubripes", "Anas americana", "Buceph…
## $ diet                        <chr> "Vegetation", "Vegetation", "Invertebrates…
## $ life_expectancy             <chr> "Long", "Middle", "Middle", "Long", "Middl…
## $ habitat                     <chr> "Wetland", "Wetland", "Wetland", "Wetland"…
## $ urban_affiliate             <chr> "No", "No", "No", "No", "No", "No", "No", …
## $ migratory_strategy          <chr> "Short", "Short", "Moderate", "Moderate", …
## $ log10_mass                  <dbl> 3.09, 2.88, 2.96, 3.11, 3.02, 2.88, 2.56, …
## $ mean_eggs_per_clutch        <dbl> 9.0, 7.5, 10.5, 3.5, 9.5, 13.5, 10.0, 8.5,…
## $ mean_age_at_sexual_maturity <dbl> 1.0, 1.0, 3.0, 2.5, 2.0, 1.0, 0.6, 2.0, 1.…
## $ population_size             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ winter_range_area           <dbl> 3212473, 7145842, 1812841, 360134, 854350,…
## $ range_in_cbc                <dbl> 99.1, 61.7, 69.8, 53.7, 5.3, 0.5, 17.9, 72…
## $ strata                      <dbl> 82, 124, 37, 19, 36, 5, 26, 134, 145, 103,…
## $ circles                     <dbl> 1453, 1951, 502, 247, 470, 97, 479, 2189, …
## $ feeder_bird                 <chr> "No", "No", "No", "No", "No", "No", "No", …
## $ median_trend                <dbl> 1.014, 0.996, 1.039, 0.998, 1.004, 1.196, …
## $ lower_95_percent_ci         <dbl> 0.971, 0.964, 1.016, 0.956, 0.975, 1.152, …
## $ upper_95_percent_ci         <dbl> 1.055, 1.009, 1.104, 1.041, 1.036, 1.243, …
```

Problem 3. (2 points) How many distinct orders of birds are represented in the data?

```r
tabyl(ecosphere$order)
```

```
##    ecosphere$order   n     percent
##       Anseriformes  44 0.079854809
##        Apodiformes  15 0.027223230
##   Caprimulgiformes   5 0.009074410
##    Charadriiformes  81 0.147005445
##      Ciconiiformes  29 0.052631579
##      Columbiformes  11 0.019963702
##      Coraciiformes   3 0.005444646
##       Cuculiformes   3 0.005444646
##      Falconiformes  31 0.056261343
##        Galliformes  21 0.038112523
##        Gaviiformes   4 0.007259528
##         Gruiformes  12 0.021778584
##      Passeriformes 237 0.430127042
##         Piciformes  22 0.039927405
##   Podicipediformes   6 0.010889292
##  Procellariiformes   4 0.007259528
##     Psittaciformes   6 0.010889292
##       Strigiformes  16 0.029038113
##      Trogoniformes   1 0.001814882
```

```r
#there are 19 different orders of birds
```

Problem 4. (2 points) Which habitat has the highest diversity (number of species) in the data?

```r
tabyl(ecosphere$habitat)
```

```
##  ecosphere$habitat   n    percent valid_percent
##          Grassland  36 0.06533575    0.06703911
##              Ocean  44 0.07985481    0.08193669
##          Shrubland  82 0.14882033    0.15270019
##            Various  45 0.08166969    0.08379888
##            Wetland 153 0.27767695    0.28491620
##           Woodland 177 0.32123412    0.32960894
##               <NA>  14 0.02540835            NA
```

```r
ecosphere%>%
  filter(habitat == "Wetland")
```

```
## # A tibble: 153 × 21
##    order    family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##    <chr>    <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
##  1 Anserif… Anati… "Ameri… Anas r… Vege… Long    Wetland No      Short      3.09
##  2 Anserif… Anati… "Ameri… Anas a… Vege… Middle  Wetland No      Short      2.88
##  3 Anserif… Anati… "Barro… Buceph… Inve… Middle  Wetland No      Modera…    2.96
##  4 Anserif… Anati… "Black… Branta… Vege… Long    Wetland No      Modera…    3.11
##  5 Anserif… Anati… "Black… Melani… Inve… Middle  Wetland No      Modera…    3.02
##  6 Anserif… Anati… "Black… Dendro… Vege… Short   Wetland No      Withdr…    2.88
##  7 Anserif… Anati… "Blue-… Anas d… Vege… Middle  Wetland No      Modera…    2.56
##  8 Anserif… Anati… "Buffl… Buceph… Inve… Middle  Wetland No      Short      2.6 
##  9 Anserif… Anati… "Cackl… Branta… Vege… Middle  Wetland Yes     Short      3.45
## 10 Anserif… Anati… "Canva… Aythya… Vege… Middle  Wetland No      Short      3.08
## # … with 143 more rows, 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

```r
#153 rows = 153 species
```

```r
ecosphere%>%
  filter(habitat == "Grassland")
```

```
## # A tibble: 36 × 21
##    order    family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##    <chr>    <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
##  1 Charadr… Chara… Mounta… Charad… Inve… Short   Grassl… No      Modera…    1.98
##  2 Charadr… Chara… Pacifi… Pluvia… Inve… Short   Grassl… No      Long       2.18
##  3 Charadr… Scolo… Long-b… Numeni… Inve… Middle  Grassl… No      Modera…    2.77
##  4 Falconi… Accip… Ferrug… Buteo … Vert… Middle  Grassl… No      Short      3.17
##  5 Falconi… Accip… Rough-… Buteo … Vert… Middle  Grassl… No      Modera…    2.98
##  6 Falconi… Accip… White-… Buteo … Vert… Middle  Grassl… No      Reside…    3.01
##  7 Falconi… Falco… Aploma… Falco … Vert… Middle  Grassl… No      Reside…    2.53
##  8 Falconi… Falco… Gyrfal… Falco … Vert… Middle  Grassl… No      Irrupt…    3.16
##  9 Falconi… Falco… Prairi… Falco … Vert… Short   Grassl… No      Short      2.85
## 10 Gallifo… Phasi… Gray P… Perdix… Seed  Short   Grassl… No      Reside…    2.61
## # … with 26 more rows, 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

```r
#36 rows= 36 species
```

```r
ecosphere%>%
  filter(habitat == "Ocean")
```

```
## # A tibble: 44 × 21
##    order    family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##    <chr>    <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
##  1 Anserif… Anati… Common… Somate… Inve… Middle  Ocean   No      Short      3.31
##  2 Charadr… Alcid… Ancien… Synthl… Inve… Short   Ocean   No      Short      2.34
##  3 Charadr… Alcid… Atlant… Frater… Vert… Long    Ocean   No      Short      2.77
##  4 Charadr… Alcid… Black … Cepphu… Vert… Long    Ocean   No      Withdr…    2.58
##  5 Charadr… Alcid… Cassin… Ptycho… Inve… Middle  Ocean   No      Short      2.27
##  6 Charadr… Alcid… Common… Uria a… Vert… Long    Ocean   No      Short      3   
##  7 Charadr… Alcid… Dovekie Alle a… Inve… Middle  Ocean   No      Withdr…    2.26
##  8 Charadr… Alcid… Marble… Brachy… Inve… Short   Ocean   No      Withdr…    2.34
##  9 Charadr… Alcid… Pigeon… Cepphu… Vert… Middle  Ocean   No      Withdr…    2.72
## 10 Charadr… Alcid… Razorb… Alca t… Vert… Long    Ocean   No      Short      2.86
## # … with 34 more rows, 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

```r
#44 rows =44 species
```

```r
ecosphere%>%
  filter(habitat == "Woodland")
```

```
## # A tibble: 177 × 21
##    order    family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##    <chr>    <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
##  1 Apodifo… Apodi… Vaux's… Chaetu… Inve… Short   Woodla… No      Modera…    1.28
##  2 Apodifo… Troch… Anna's… Calypt… Nect… Short   Woodla… Yes     Short      0.63
##  3 Apodifo… Troch… Black-… Archil… Nect… Middle  Woodla… Yes     Short      0.48
##  4 Apodifo… Troch… Blue-t… Lampor… Nect… Short   Woodla… No      Short      0.88
##  5 Apodifo… Troch… Broad-… Cynant… Nect… Short   Woodla… Yes     Withdr…    0.48
##  6 Apodifo… Troch… Broad-… Selasp… Nect… Middle  Woodla… Yes     Modera…    0.55
##  7 Apodifo… Troch… Buff-b… Amazil… Nect… Middle  Woodla… Yes     Reside…    0.6 
##  8 Apodifo… Troch… Callio… Stellu… Nect… Short   Woodla… No      Modera…    0.48
##  9 Apodifo… Troch… Magnif… Eugene… Nect… Short   Woodla… No      Short      0.9 
## 10 Apodifo… Troch… Ruby-t… Archil… Nect… Short   Woodla… Yes     Modera…    0.49
## # … with 167 more rows, 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

```r
#177 rows= 177 species
#Not accounting for Various or NA, Woodland has the highest number of species, with 177 different species
```

Run the code below to learn about the `slice` function. Look specifically at the examples (at the bottom) for `slice_max()` and `slice_min()`. If you are still unsure, try looking up examples online (https://rpubs.com/techanswers88/dplyr-slice). Use this new function to answer question 5 below.

```r
?slice_max
```

Problem 5. (4 points) Using the `slice_max()` or `slice_min()` function described above which species has the largest and smallest winter range?

```r
slice_max(ecosphere,winter_range_area, with_ties=TRUE)
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Procella… Proce… Sooty … Puffin… Vert… Long    Ocean   No      Long        2.9
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```


```r
slice_min(ecosphere,winter_range_area, with_ties=TRUE)
```

```
## # A tibble: 1 × 21
##   order     family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##   <chr>     <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
## 1 Passerif… Alaud… Skylark Alauda… Seed  Short   Grassl… No      Reside…    1.57
## # … with 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

```r
#largest winter range is the sooty shearwater with an area of 185968946, the smallest winter range is the skylark with an area of 11
```

Problem 6. (2 points) The family Anatidae includes ducks, geese, and swans. Make a new object `ducks` that only includes species in the family Anatidae. Restrict this new dataframe to include all variables except order and family.

```r
ducks <- filter(ecosphere, family=="Anatidae")
ducks <- select(ducks, -order, -family)
ducks
```

```
## # A tibble: 44 × 19
##    commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶ mean_…⁷ mean_…⁸
##    <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>   <dbl>   <dbl>
##  1 "Ameri… Anas r… Vege… Long    Wetland No      Short      3.09     9       1  
##  2 "Ameri… Anas a… Vege… Middle  Wetland No      Short      2.88     7.5     1  
##  3 "Barro… Buceph… Inve… Middle  Wetland No      Modera…    2.96    10.5     3  
##  4 "Black… Branta… Vege… Long    Wetland No      Modera…    3.11     3.5     2.5
##  5 "Black… Melani… Inve… Middle  Wetland No      Modera…    3.02     9.5     2  
##  6 "Black… Dendro… Vege… Short   Wetland No      Withdr…    2.88    13.5     1  
##  7 "Blue-… Anas d… Vege… Middle  Wetland No      Modera…    2.56    10       0.6
##  8 "Buffl… Buceph… Inve… Middle  Wetland No      Short      2.6      8.5     2  
##  9 "Cackl… Branta… Vege… Middle  Wetland Yes     Short      3.45     5       1  
## 10 "Canva… Aythya… Vege… Middle  Wetland No      Short      3.08     8       1  
## # … with 34 more rows, 9 more variables: population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass, ⁷​mean_eggs_per_clutch, ⁸​mean_age_at_sexual_maturity
```

Problem 7. (2 points) We might assume that all ducks live in wetland habitat. Is this true for the ducks in these data? If there are exceptions, list the species below.

```r
filter(ducks, habitat != "Wetland")
```

```
## # A tibble: 1 × 19
##   common…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶ mean_…⁷ mean_…⁸
##   <chr>    <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>   <dbl>   <dbl>
## 1 Common … Somate… Inve… Middle  Ocean   No      Short      3.31       5     2.5
## # … with 9 more variables: population_size <dbl>, winter_range_area <dbl>,
## #   range_in_cbc <dbl>, strata <dbl>, circles <dbl>, feeder_bird <chr>,
## #   median_trend <dbl>, lower_95_percent_ci <dbl>, upper_95_percent_ci <dbl>,
## #   and abbreviated variable names ¹​common_name, ²​scientific_name,
## #   ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy, ⁶​log10_mass,
## #   ⁷​mean_eggs_per_clutch, ⁸​mean_age_at_sexual_maturity
```

```r
#The common eider's habitat is the ocean, not the wetlands
```

Problem 8. (4 points) In ducks, how is mean body mass associated with migratory strategy? Do the ducks that migrate long distances have high or low average body mass?

```r
ducks%>%
  filter(migratory_strategy =="Long")%>%
  summary()
```

```
##  common_name        scientific_name        diet           life_expectancy   
##  Length:2           Length:2           Length:2           Length:2          
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##    habitat          urban_affiliate    migratory_strategy   log10_mass  
##  Length:2           Length:2           Length:2           Min.   :2.85  
##  Class :character   Class :character   Class :character   1st Qu.:2.86  
##  Mode  :character   Mode  :character   Mode  :character   Median :2.87  
##                                                           Mean   :2.87  
##                                                           3rd Qu.:2.88  
##                                                           Max.   :2.89  
##                                                                         
##  mean_eggs_per_clutch mean_age_at_sexual_maturity population_size
##  Min.   : 8.500       Min.   :1                   Min.   : NA    
##  1st Qu.: 8.875       1st Qu.:1                   1st Qu.: NA    
##  Median : 9.250       Median :1                   Median : NA    
##  Mean   : 9.250       Mean   :1                   Mean   :NaN    
##  3rd Qu.: 9.625       3rd Qu.:1                   3rd Qu.: NA    
##  Max.   :10.000       Max.   :1                   Max.   : NA    
##                                                   NA's   :2      
##  winter_range_area   range_in_cbc       strata         circles     
##  Min.   :12883658   Min.   :0.000   Min.   : 6.00   Min.   : 46.0  
##  1st Qu.:13257664   1st Qu.:1.525   1st Qu.: 7.75   1st Qu.: 99.5  
##  Median :13631671   Median :3.050   Median : 9.50   Median :153.0  
##  Mean   :13631671   Mean   :3.050   Mean   : 9.50   Mean   :153.0  
##  3rd Qu.:14005678   3rd Qu.:4.575   3rd Qu.:11.25   3rd Qu.:206.5  
##  Max.   :14379684   Max.   :6.100   Max.   :13.00   Max.   :260.0  
##                                                                    
##  feeder_bird         median_trend   lower_95_percent_ci upper_95_percent_ci
##  Length:2           Min.   :1.004   Min.   :0.9440      Min.   :1.046      
##  Class :character   1st Qu.:1.014   1st Qu.:0.9647      1st Qu.:1.047      
##  Mode  :character   Median :1.024   Median :0.9855      Median :1.048      
##                     Mean   :1.024   Mean   :0.9855      Mean   :1.048      
##                     3rd Qu.:1.033   3rd Qu.:1.0063      3rd Qu.:1.050      
##                     Max.   :1.043   Max.   :1.0270      Max.   :1.051      
## 
```

```r
#mean log10_mass was 2.87
```

```r
ducks%>%
  filter(migratory_strategy !="Long")%>%
  summary()
```

```
##  common_name        scientific_name        diet           life_expectancy   
##  Length:42          Length:42          Length:42          Length:42         
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##    habitat          urban_affiliate    migratory_strategy   log10_mass   
##  Length:42          Length:42          Length:42          Min.   :2.530  
##  Class :character   Class :character   Class :character   1st Qu.:2.880  
##  Mode  :character   Mode  :character   Mode  :character   Median :2.985  
##                                                           Mean   :3.051  
##                                                           3rd Qu.:3.160  
##                                                           Max.   :4.040  
##                                                                          
##  mean_eggs_per_clutch mean_age_at_sexual_maturity population_size
##  Min.   : 3.500       Min.   :0.400               Min.   : NA    
##  1st Qu.: 5.750       1st Qu.:1.000               1st Qu.: NA    
##  Median : 8.250       Median :1.750               Median : NA    
##  Mean   : 8.226       Mean   :1.764               Mean   :NaN    
##  3rd Qu.:10.000       3rd Qu.:2.500               3rd Qu.: NA    
##  Max.   :14.500       Max.   :5.500               Max.   : NA    
##                                                   NA's   :42     
##  winter_range_area  range_in_cbc        strata          circles      
##  Min.   : 212068   Min.   : 0.000   Min.   :  2.00   Min.   :  11.0  
##  1st Qu.: 806452   1st Qu.: 8.625   1st Qu.: 20.75   1st Qu.: 313.5  
##  Median :3716338   Median :61.900   Median : 58.50   Median : 884.0  
##  Mean   :3839087   Mean   :51.231   Mean   : 67.95   Mean   :1107.5  
##  3rd Qu.:6580292   3rd Qu.:79.525   3rd Qu.:121.25   3rd Qu.:1951.0  
##  Max.   :9346116   Max.   :99.100   Max.   :156.00   Max.   :3006.0  
##                                                                      
##  feeder_bird         median_trend    lower_95_percent_ci upper_95_percent_ci
##  Length:42          Min.   :0.9120   Min.   :0.8210      Min.   :0.969      
##  Class :character   1st Qu.:0.9965   1st Qu.:0.9643      1st Qu.:1.020      
##  Mode  :character   Median :1.0190   Median :0.9955      Median :1.040      
##                     Mean   :1.0213   Mean   :0.9902      Mean   :1.051      
##                     3rd Qu.:1.0342   3rd Qu.:1.0197      3rd Qu.:1.062      
##                     Max.   :1.1960   Max.   :1.1520      Max.   :1.243      
## 
```

```r
#mean log10_mass for birds that are not long distance migrators is 3.051
```


Problem 9. (2 points) Accipitridae is the family that includes eagles, hawks, kites, and osprey. First, make a new object `eagles` that only includes species in the family Accipitridae. Next, restrict these data to only include the variables common_name, scientific_name, and population_size.

```r
eagles <- filter(ecosphere, family=="Accipitridae")
eagles <- select(eagles, common_name,scientific_name,population_size)
eagles
```

```
## # A tibble: 20 × 3
##    common_name         scientific_name          population_size
##    <chr>               <chr>                              <dbl>
##  1 Bald Eagle          Haliaeetus leucocephalus              NA
##  2 Broad-winged Hawk   Buteo platypterus                1700000
##  3 Cooper's Hawk       Accipiter cooperii                700000
##  4 Ferruginous Hawk    Buteo regalis                      80000
##  5 Golden Eagle        Aquila chrysaetos                 130000
##  6 Gray Hawk           Buteo nitidus                         NA
##  7 Harris's Hawk       Parabuteo unicinctus               50000
##  8 Hook-billed Kite    Chondrohierax uncinatus               NA
##  9 Northern Goshawk    Accipiter gentilis                200000
## 10 Northern Harrier    Circus cyaneus                    700000
## 11 Red-shouldered Hawk Buteo lineatus                   1100000
## 12 Red-tailed Hawk     Buteo jamaicensis                2000000
## 13 Rough-legged Hawk   Buteo lagopus                     300000
## 14 Sharp-shinned Hawk  Accipiter striatus                500000
## 15 Short-tailed Hawk   Buteo brachyurus                      NA
## 16 Snail Kite          Rostrhamus sociabilis                 NA
## 17 Swainson's Hawk     Buteo swainsoni                   540000
## 18 White-tailed Hawk   Buteo albicaudatus                    NA
## 19 White-tailed Kite   Elanus leucurus                       NA
## 20 Zone-tailed Hawk    Buteo albonotatus                     NA
```

Problem 10. (4 points) In the eagles data, any species with a population size less than 250,000 individuals is threatened. Make a new column `conservation_status` that shows whether or not a species is threatened.

```r
eagles%>%
  filter(population_size<=250000)%>%
  mutate(conservation_status="threatened")
```

```
## # A tibble: 4 × 4
##   common_name      scientific_name      population_size conservation_status
##   <chr>            <chr>                          <dbl> <chr>              
## 1 Ferruginous Hawk Buteo regalis                  80000 threatened         
## 2 Golden Eagle     Aquila chrysaetos             130000 threatened         
## 3 Harris's Hawk    Parabuteo unicinctus           50000 threatened         
## 4 Northern Goshawk Accipiter gentilis            200000 threatened
```

```r
eagles%>%
  filter(population_size>=250000)%>%
  mutate(conservation_status="not_threatened")
```

```
## # A tibble: 8 × 4
##   common_name         scientific_name    population_size conservation_status
##   <chr>               <chr>                        <dbl> <chr>              
## 1 Broad-winged Hawk   Buteo platypterus          1700000 not_threatened     
## 2 Cooper's Hawk       Accipiter cooperii          700000 not_threatened     
## 3 Northern Harrier    Circus cyaneus              700000 not_threatened     
## 4 Red-shouldered Hawk Buteo lineatus             1100000 not_threatened     
## 5 Red-tailed Hawk     Buteo jamaicensis          2000000 not_threatened     
## 6 Rough-legged Hawk   Buteo lagopus               300000 not_threatened     
## 7 Sharp-shinned Hawk  Accipiter striatus          500000 not_threatened     
## 8 Swainson's Hawk     Buteo swainsoni             540000 not_threatened
```


Problem 11. (2 points) Consider the results from questions 9 and 10. Are there any species for which their threatened status needs further study? How do you know?

```r
ecosphere%>%
  filter(population_size <= 250000)%>%
  filter(family !="Accipitridae")
```

```
## # A tibble: 24 × 21
##    order    family commo…¹ scien…² diet  life_…³ habitat urban…⁴ migra…⁵ log10…⁶
##    <chr>    <chr>  <chr>   <chr>   <chr> <chr>   <chr>   <chr>   <chr>     <dbl>
##  1 Falconi… Falco… Gyrfal… Falco … Vert… Middle  Grassl… No      Irrupt…    3.16
##  2 Falconi… Falco… Prairi… Falco … Vert… Short   Grassl… No      Short      2.85
##  3 Falconi… Pandi… Osprey  Pandio… Vert… Middle  Wetland Yes     Short      3.22
##  4 Passeri… Cincl… Americ… Cinclu… Inve… Short   Wetland Yes     Reside…    1.75
##  5 Passeri… Corvi… Clark'… Nucifr… Seed  Middle  Woodla… No      Reside…    2.11
##  6 Passeri… Corvi… Mexica… Aphelo… Omni… Middle  Woodla… No      Reside…    2.12
##  7 Passeri… Ember… Bachma… Peucae… Omni… Short   Woodla… No      Withdr…    1.29
##  8 Passeri… Ember… Black-… Spizel… Omni… Short   Shrubl… No      Short      1.1 
##  9 Passeri… Ember… Seasid… Ammodr… Inve… Short   Wetland No      Withdr…    1.35
## 10 Passeri… Mimid… Bendir… Toxost… Inve… Short   Shrubl… No      Withdr…    1.79
## # … with 14 more rows, 11 more variables: mean_eggs_per_clutch <dbl>,
## #   mean_age_at_sexual_maturity <dbl>, population_size <dbl>,
## #   winter_range_area <dbl>, range_in_cbc <dbl>, strata <dbl>, circles <dbl>,
## #   feeder_bird <chr>, median_trend <dbl>, lower_95_percent_ci <dbl>,
## #   upper_95_percent_ci <dbl>, and abbreviated variable names ¹​common_name,
## #   ²​scientific_name, ³​life_expectancy, ⁴​urban_affiliate, ⁵​migratory_strategy,
## #   ⁶​log10_mass
```

```r
#There are 24 species that have less than 250,000 population size that are not in the Accipitridae family that would be considered endangered
```

Problem 12. (4 points) Use the `ecosphere` data to perform one exploratory analysis of your choice. The analysis must have a minimum of three lines and two functions. You must also clearly state the question you are attempting to answer.

Does diet affect winter range area and body mass? Which diet has the highest and which has the lowest winter range are? Which diet has the largest and smallest body masses?

```r
tabyl(ecosphere$diet)
```

```
##  ecosphere$diet   n    percent
##           Fruit  11 0.01996370
##   Invertebrates 216 0.39201452
##          Nectar  13 0.02359347
##        Omnivore 114 0.20689655
##            Seed  64 0.11615245
##      Vegetation  31 0.05626134
##     Vertebrates 102 0.18511797
```


```r
ecosphere%>%
  filter(diet=="Fruit")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area    log10_mass   
##  Length:11          Min.   :   83675   Min.   :1.340  
##  Class :character   1st Qu.:  477049   1st Qu.:1.680  
##  Mode  :character   Median :  979536   Median :1.900  
##                     Mean   : 3456763   Mean   :1.966  
##                     3rd Qu.: 6134730   3rd Qu.:2.330  
##                     Max.   :11021363   Max.   :2.500
```

```r
#Fruit has a mean range of 3,456,763 and mean log10 mass of 1.966
```

```r
ecosphere%>%
  filter(diet=="Invertebrates")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area    log10_mass  
##  Length:216         Min.   :   61809   Min.   :0.70  
##  Class :character   1st Qu.:  725203   1st Qu.:1.14  
##  Mode  :character   Median : 1614168   Median :1.67  
##                     Mean   : 3732427   Mean   :1.73  
##                     3rd Qu.: 4307914   3rd Qu.:2.16  
##                     Max.   :25380422   Max.   :3.77
```

```r
#invertebrates has a mean range of 3,732,427 and mean log10 mass of 1.73
```

```r
ecosphere%>%
  filter(diet=="Nectar")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area   log10_mass    
##  Length:13          Min.   :  42584   Min.   :0.4800  
##  Class :character   1st Qu.: 238000   1st Qu.:0.4800  
##  Mode  :character   Median : 391181   Median :0.5500  
##                     Mean   : 468399   Mean   :0.6038  
##                     3rd Qu.: 584491   3rd Qu.:0.6500  
##                     Max.   :1271937   Max.   :0.9000
```

```r
#Nectar has a mean range of 468,399 and a mean log10 mass of 0.6500
```

```r
ecosphere%>%
  filter(diet=="Omnivore")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area    log10_mass   
##  Length:114         Min.   :     193   Min.   :0.980  
##  Class :character   1st Qu.:  830478   1st Qu.:1.452  
##  Mode  :character   Median : 1695475   Median :1.785  
##                     Mean   : 3371031   Mean   :1.894  
##                     3rd Qu.: 4728754   3rd Qu.:2.220  
##                     Max.   :15172222   Max.   :3.760
```

```r
#Omnivore has a mean range of 3,371,031 and a mean log10 mass of 1.894
```

```r
ecosphere%>%
  filter(diet=="Seed")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area    log10_mass   
##  Length:64          Min.   :      11   Min.   :0.940  
##  Class :character   1st Qu.: 1136643   1st Qu.:1.220  
##  Mode  :character   Median : 2798066   Median :1.470  
##                     Mean   : 4822350   Mean   :1.640  
##                     3rd Qu.: 7722476   3rd Qu.:2.087  
##                     Max.   :23373085   Max.   :2.940
```

```r
#Seed has a mean range of 4,822,350 and a mean log10 mass of 1.640
```

```r
ecosphere%>%
  filter(diet=="Vegetation")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area    log10_mass   
##  Length:31          Min.   :  212068   Min.   :2.530  
##  Class :character   1st Qu.: 1699660   1st Qu.:2.800  
##  Mode  :character   Median : 5781869   Median :2.950  
##                     Mean   : 5154818   Mean   :3.039  
##                     3rd Qu.: 7289893   3rd Qu.:3.135  
##                     Max.   :14379684   Max.   :4.040
```

```r
#Vegetation has a mean range of 5,154,818 and a mean log10 mass of 3.039
```

```r
ecosphere%>%
  filter(diet=="Vertebrates")%>%
  select(diet, winter_range_area, log10_mass)%>%
  summary()
```

```
##      diet           winter_range_area     log10_mass   
##  Length:102         Min.   :   103930   Min.   :1.570  
##  Class :character   1st Qu.:  2163859   1st Qu.:2.572  
##  Mode  :character   Median :  6267334   Median :2.870  
##                     Mean   : 10589038   Mean   :2.845  
##                     3rd Qu.: 11645547   3rd Qu.:3.167  
##                     Max.   :185968946   Max.   :3.930
```

```r
#Vertebrates has a mean range of 10,589,038 and a mean log10 mass of 2.845
```
The diet with the largest average winter range was Vertebrates with an average of 10,589,038. The diet with the smallest average winter range was Nectar with  an average of 468,399. Nectar was also the diet with the smallest average log10 body mass at 0.6500. Vegetation had the largest average log10 mass at 3.039.


Please provide the names of the students you have worked with with during the exam:

```r
#No one
```

Please be 100% sure your exam is saved, knitted, and pushed to your github repository. No need to submit a link on canvas, we will find your exam in your repository.
