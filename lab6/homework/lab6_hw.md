---
title: "Lab 6 Homework"
author: "Kat Pinder"
date: "2023-02-02"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv(file = "data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
names(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

```r
dim(fisheries)
```

```
## [1] 17692    71
```

```r
anyNA(fisheries)
```

```
## [1] TRUE
```

```r
class(fisheries)
```

```
## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"
```

```r
summary(fisheries)
```

```
##    Country          Common name        ISSCAAP group#  ISSCAAP taxonomic group
##  Length:17692       Length:17692       Min.   :11.00   Length:17692           
##  Class :character   Class :character   1st Qu.:33.00   Class :character       
##  Mode  :character   Mode  :character   Median :36.00   Mode  :character       
##                                        Mean   :37.38                          
##                                        3rd Qu.:38.00                          
##                                        Max.   :77.00                          
##  ASFIS species#     ASFIS species name FAO major fishing area
##  Length:17692       Length:17692       Min.   :18.00         
##  Class :character   Class :character   1st Qu.:31.00         
##  Mode  :character   Mode  :character   Median :37.00         
##                                        Mean   :45.34         
##                                        3rd Qu.:57.00         
##                                        Max.   :88.00         
##    Measure              1950               1951               1952          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1953               1954               1955               1956          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1957               1958               1959               1960          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1961               1962               1963               1964          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1965               1966               1967               1968          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1969               1970               1971               1972          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1973               1974               1975               1976          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1977               1978               1979               1980          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1981               1982               1983               1984          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1985               1986               1987               1988          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1989               1990               1991               1992          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1993               1994               1995               1996          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1997               1998               1999               2000          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2001               2002               2003               2004          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2005               2006               2007               2008          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2009               2010               2011               2012          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
## 
```

```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
## $ Country                   <chr> "Albania", "Albania", "Albania", "Albania", …
## $ `Common name`             <chr> "Angelsharks, sand devils nei", "Atlantic bo…
## $ `ISSCAAP group#`          <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33, …
## $ `ISSCAAP taxonomic group` <chr> "Sharks, rays, chimaeras", "Tunas, bonitos, …
## $ `ASFIS species#`          <chr> "10903XXXXX", "1750100101", "17710001XX", "2…
## $ `ASFIS species name`      <chr> "Squatinidae", "Sarda sarda", "Sphyraena spp…
## $ `FAO major fishing area`  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, …
## $ Measure                   <chr> "Quantity (tonnes)", "Quantity (tonnes)", "Q…
## $ `1950`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1951`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1952`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1953`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1954`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1955`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1956`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1957`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1958`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1959`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1960`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1961`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1962`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1963`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1964`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1965`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1966`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1967`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1968`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1969`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1970`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1971`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1972`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1973`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1974`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1975`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1976`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1977`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1978`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1979`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1980`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1981`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1982`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ `1983`                    <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, N…
## $ `1984`                    <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, N…
## $ `1985`                    <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, N…
## $ `1986`                    <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, N…
## $ `1987`                    <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, N…
## $ `1988`                    <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, N…
## $ `1989`                    <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, N…
## $ `1990`                    <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, N…
## $ `1991`                    <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, N…
## $ `1992`                    <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, N…
## $ `1993`                    <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA,…
## $ `1994`                    <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA,…
## $ `1995`                    <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30"…
## $ `1996`                    <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA,…
## $ `1997`                    <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4"…
## $ `1998`                    <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA,…
## $ `1999`                    <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA,…
## $ `2000`                    <chr> "30", "25", "2", NA, NA, NA, "220", "20", NA…
## $ `2001`                    <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA,…
## $ `2002`                    <chr> "79", "24", NA, "34", "6", NA, "150", "84", …
## $ `2003`                    <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA,…
## $ `2004`                    <chr> "4", "2", "2", "15", "1", "2", "76", "285", …
## $ `2005`                    <chr> "68", "23", "4", "12", "5", "6", "68", "150"…
## $ `2006`                    <chr> "55", "30", "7", "18", "8", "9", "86", "102"…
## $ `2007`                    <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA,…
## $ `2008`                    <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA,…
## $ `2009`                    <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA,…
## $ `2010`                    <chr> "78", "23", "7", NA, NA, NA, "80", "228", NA…
## $ `2011`                    <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, "…
## $ `2012`                    <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA, …
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <-janitor::clean_names(fisheries)
```


```r
fisheries$country <- as.factor(fisheries$country)
fisheries$isscaap_group_number <- as.factor(fisheries$isscaap_group_number)
fisheries$asfis_species_number <- as.factor(fisheries$asfis_species_number)
fisheries$fao_major_fishing_area <- as.factor(fisheries$fao_major_fishing_area)
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
tabyl(fisheries_tidy$country)
```

```
##     fisheries_tidy$country     n      percent
##        Saint Barth\xe9lemy     6 1.592479e-05
##                 R\xe9union   736 1.953441e-03
##           C\xf4te d'Ivoire  1859 4.934032e-03
##                 Cura\xe7ao    18 4.777438e-05
##                    Albania   934 2.478959e-03
##                    Algeria  1561 4.143100e-03
##             American Samoa   556 1.475697e-03
##                     Angola  2119 5.624106e-03
##                   Anguilla   129 3.423830e-04
##        Antigua and Barbuda   356 9.448710e-04
##                  Argentina  3403 9.032011e-03
##                      Aruba   172 4.565107e-04
##                  Australia  8183 2.171876e-02
##                    Bahamas   423 1.122698e-03
##                    Bahrain  1169 3.102680e-03
##                 Bangladesh   169 4.485483e-04
##                   Barbados   795 2.110035e-03
##                    Belgium  2530 6.714954e-03
##                     Belize  1075 2.853192e-03
##                      Benin  1419 3.766213e-03
##                    Bermuda   846 2.245396e-03
##   Bonaire/S.Eustatius/Saba     4 1.061653e-05
##     Bosnia and Herzegovina    21 5.573677e-05
##                     Brazil  4784 1.269737e-02
##   British Indian Ocean Ter    97 2.574508e-04
##     British Virgin Islands   332 8.811719e-04
##          Brunei Darussalam   186 4.936686e-04
##                   Bulgaria  1596 4.235995e-03
##                 Cabo Verde   462 1.226209e-03
##                   Cambodia   238 6.316834e-04
##                   Cameroon  1340 3.556537e-03
##                     Canada  5099 1.353342e-02
##             Cayman Islands    84 2.229471e-04
##            Channel Islands  1313 3.484875e-03
##                      Chile  3878 1.029272e-02
##                      China  2801 7.434224e-03
##       China, Hong Kong SAR  1782 4.729663e-03
##           China, Macao SAR   206 5.467512e-04
##                   Colombia  2710 7.192698e-03
##                    Comoros   965 2.561237e-03
##    Congo, Dem. Rep. of the   484 1.284600e-03
##         Congo, Republic of  1527 4.052860e-03
##               Cook Islands   810 2.149847e-03
##                 Costa Rica  1171 3.107989e-03
##                    Croatia   947 2.513463e-03
##                       Cuba  2981 7.911968e-03
##                     Cyprus  1703 4.519987e-03
##                    Denmark  3741 9.929108e-03
##                   Djibouti   352 9.342545e-04
##                   Dominica   213 5.653301e-04
##         Dominican Republic  1958 5.196791e-03
##                    Ecuador  1595 4.233341e-03
##                      Egypt  2467 6.547744e-03
##                El Salvador   620 1.645562e-03
##          Equatorial Guinea   551 1.462427e-03
##                    Eritrea   653 1.733148e-03
##                    Estonia  1088 2.887696e-03
##                   Ethiopia   129 3.423830e-04
##     Falkland Is.(Malvinas)   502 1.332374e-03
##              Faroe Islands  2283 6.059384e-03
##          Fiji, Republic of  1798 4.772129e-03
##                    Finland   706 1.873817e-03
##                     France 10639 2.823731e-02
##              French Guiana   231 6.131045e-04
##           French Polynesia   672 1.783577e-03
##       French Southern Terr   139 3.689244e-04
##                      Gabon  1089 2.890350e-03
##                     Gambia  1214 3.222116e-03
##                    Georgia   428 1.135969e-03
##                    Germany  4813 1.277434e-02
##                      Ghana  2462 6.534473e-03
##                  Gibraltar    61 1.619021e-04
##                     Greece  4091 1.085805e-02
##                  Greenland  1311 3.479567e-03
##                    Grenada  1635 4.339506e-03
##                 Guadeloupe   372 9.873371e-04
##                       Guam   520 1.380149e-03
##                  Guatemala   622 1.650870e-03
##                     Guinea   697 1.849930e-03
##               GuineaBissau   634 1.682720e-03
##                     Guyana   251 6.661872e-04
##                      Haiti   204 5.414429e-04
##                   Honduras   842 2.234779e-03
##                    Iceland  2346 6.226594e-03
##                      India  5588 1.483129e-02
##                  Indonesia  9274 2.461442e-02
##     Iran (Islamic Rep. of)  1210 3.211500e-03
##                       Iraq   150 3.981198e-04
##                    Ireland  3235 8.586117e-03
##                Isle of Man   952 2.526734e-03
##                     Israel  1359 3.606966e-03
##                      Italy  4567 1.212142e-02
##                    Jamaica   149 3.954657e-04
##                      Japan 15429 4.095060e-02
##                     Jordan   226 5.998339e-04
##                      Kenya   958 2.542659e-03
##                   Kiribati   875 2.322366e-03
##   Korea, Dem. People's Rep   210 5.573677e-04
##         Korea, Republic of 10824 2.872833e-02
##                     Kuwait   805 2.136576e-03
##                     Latvia  1101 2.922199e-03
##                    Lebanon   614 1.629637e-03
##                    Liberia  1514 4.018356e-03
##                      Libya   578 1.534088e-03
##                  Lithuania  1274 3.381364e-03
##                 Madagascar  1008 2.675365e-03
##                   Malaysia  6963 1.848072e-02
##                   Maldives   487 1.292562e-03
##                      Malta  2156 5.722309e-03
##           Marshall Islands   292 7.750066e-04
##                 Martinique   672 1.783577e-03
##                 Mauritania  1501 3.983852e-03
##                  Mauritius   991 2.630245e-03
##                    Mayotte   194 5.149016e-04
##                     Mexico  6202 1.646093e-02
##  Micronesia, Fed.States of   413 1.096157e-03
##                     Monaco    43 1.141277e-04
##                 Montenegro   168 4.458942e-04
##                 Montserrat    63 1.672103e-04
##                    Morocco  4758 1.262836e-02
##                 Mozambique   434 1.151893e-03
##                    Myanmar   117 3.105335e-04
##                    Namibia   905 2.401990e-03
##                      Nauru   150 3.981198e-04
##                Netherlands  2944 7.813765e-03
##       Netherlands Antilles   338 8.970966e-04
##              New Caledonia   789 2.094110e-03
##                New Zealand  4594 1.219308e-02
##                  Nicaragua   904 2.399335e-03
##                    Nigeria  1479 3.925461e-03
##                       Niue   145 3.848492e-04
##             Norfolk Island    41 1.088194e-04
##       Northern Mariana Is.   488 1.295216e-03
##                     Norway  3747 9.945033e-03
##                       Oman  1086 2.882387e-03
##                  Other nei  1556 4.129830e-03
##                   Pakistan  2166 5.748850e-03
##                      Palau   636 1.688028e-03
##    Palestine, Occupied Tr.   429 1.138623e-03
##                     Panama  1773 4.705776e-03
##           Papua New Guinea   686 1.820735e-03
##                       Peru  2767 7.343983e-03
##                Philippines  4548 1.207099e-02
##           Pitcairn Islands    63 1.672103e-04
##                     Poland  2553 6.775999e-03
##                   Portugal 11570 3.070831e-02
##                Puerto Rico   918 2.436493e-03
##                      Qatar   941 2.497538e-03
##                    Romania  1738 4.612882e-03
##         Russian Federation  4736 1.256997e-02
##               Saint Helena   609 1.616366e-03
##      Saint Kitts and Nevis   397 1.053690e-03
##                Saint Lucia   558 1.481006e-03
##   Saint Vincent/Grenadines   715 1.897704e-03
##                SaintMartin     6 1.592479e-05
##                      Samoa   386 1.024495e-03
##      Sao Tome and Principe  1035 2.747027e-03
##               Saudi Arabia  2200 5.839091e-03
##                    Senegal  2988 7.930547e-03
##      Serbia and Montenegro   516 1.369532e-03
##                 Seychelles  1142 3.031019e-03
##               Sierra Leone  1526 4.050206e-03
##                  Singapore  1937 5.141054e-03
##               Sint Maarten     4 1.061653e-05
##                   Slovenia   644 1.709261e-03
##            Solomon Islands   505 1.340337e-03
##                    Somalia   141 3.742326e-04
##               South Africa  3881 1.030069e-02
##                      Spain 17482 4.639954e-02
##                  Sri Lanka  1351 3.585732e-03
##    St. Pierre and Miquelon  1038 2.754989e-03
##                      Sudan     3 7.962396e-06
##             Sudan (former)    90 2.388719e-04
##                   Suriname   234 6.210669e-04
##     Svalbard and Jan Mayen    41 1.088194e-04
##                     Sweden  3115 8.267621e-03
##       Syrian Arab Republic   793 2.104727e-03
##   Taiwan Province of China  9927 2.634757e-02
##   Tanzania, United Rep. of  1277 3.389327e-03
##                   Thailand  4843 1.285396e-02
##                 TimorLeste    98 2.601049e-04
##                       Togo  1723 4.573070e-03
##                    Tokelau   102 2.707215e-04
##                      Tonga   403 1.069615e-03
##        Trinidad and Tobago   923 2.449764e-03
##                    Tunisia  3019 8.012825e-03
##                     Turkey  3326 8.827643e-03
##       Turks and Caicos Is.   193 5.122475e-04
##                     Tuvalu   162 4.299694e-04
##                    Ukraine  1823 4.838483e-03
##         Un. Sov. Soc. Rep.  7084 1.880187e-02
##       United Arab Emirates  1801 4.780092e-03
##             United Kingdom  6577 1.745623e-02
##   United States of America 18080 4.798671e-02
##                    Uruguay  2134 5.663918e-03
##          US Virgin Islands   348 9.236380e-04
##                    Vanuatu   789 2.094110e-03
##    Venezuela, Boliv Rep of  3409 9.047936e-03
##                   Viet Nam   405 1.074923e-03
##      Wallis and Futuna Is.   128 3.397289e-04
##             Western Sahara     0 0.000000e+00
##                      Yemen  1278 3.391981e-03
##             Yugoslavia SFR  1383 3.670665e-03
##                   Zanzibar   247 6.555706e-04
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
select(fisheries_tidy, country, isscaap_group_number, asfis_species_name, asfis_species_number,year,catch)
```

```
## # A tibble: 376,771 × 6
##    country isscaap_group_number asfis_species_name asfis_species_n…¹  year catch
##    <fct>   <fct>                <chr>              <fct>             <dbl> <dbl>
##  1 Albania 38                   Squatinidae        10903XXXXX         1995    NA
##  2 Albania 38                   Squatinidae        10903XXXXX         1996    53
##  3 Albania 38                   Squatinidae        10903XXXXX         1997    20
##  4 Albania 38                   Squatinidae        10903XXXXX         1998    31
##  5 Albania 38                   Squatinidae        10903XXXXX         1999    30
##  6 Albania 38                   Squatinidae        10903XXXXX         2000    30
##  7 Albania 38                   Squatinidae        10903XXXXX         2001    16
##  8 Albania 38                   Squatinidae        10903XXXXX         2002    79
##  9 Albania 38                   Squatinidae        10903XXXXX         2003     1
## 10 Albania 38                   Squatinidae        10903XXXXX         2004     4
## # … with 376,761 more rows, and abbreviated variable name ¹​asfis_species_number
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
tabyl(fisheries_tidy$asfis_species_number)
```

```
##  fisheries_tidy$asfis_species_number     n      percent
##                           1020100101   103 2.733756e-04
##                           1020100201     2 5.308264e-06
##                           10201XXXXX    23 6.104504e-05
##                           1030300603    10 2.654132e-05
##                           10303XXXXX    54 1.433231e-04
##                           1050200201    45 1.194359e-04
##                           1050200301     4 1.061653e-05
##                           1050200502    26 6.900743e-05
##                           1060100301   119 3.158417e-04
##                           1060200501    23 6.104504e-05
##                           1060403601     1 2.654132e-06
##                           1060600601   208 5.520595e-04
##                           1060600602     3 7.962396e-06
##                           1060600603    71 1.884434e-04
##                           10606006XX   116 3.078793e-04
##                           1060800201   801 2.125960e-03
##                           1060800203    38 1.008570e-04
##                           10608002XX    34 9.024049e-05
##                           1060800301   690 1.831351e-03
##                           1060800701    27 7.166157e-05
##                           10608XXXXX    17 4.512025e-05
##                           1070300901    50 1.327066e-04
##                           1080100104    60 1.592479e-04
##                           1080100106     5 1.327066e-05
##                           1080100301    99 2.627591e-04
##                           1080100302    60 1.592479e-04
##                           10801003XX   103 2.733756e-04
##                           1080103004     1 2.654132e-06
##                           1080103402    12 3.184959e-05
##                           10801XXXXX    20 5.308264e-05
##                           1080200401   827 2.194967e-03
##                           1080201001    19 5.042851e-05
##                           1080201003    55 1.459773e-04
##                           1080201009     1 2.654132e-06
##                           1080201011    67 1.778268e-04
##                           1080201012     5 1.327066e-05
##                           1080201016    19 5.042851e-05
##                           1080201017   156 4.140446e-04
##                           1080201018    13 3.450372e-05
##                           1080201020    30 7.962396e-05
##                           1080201021     2 5.308264e-06
##                           1080201025     4 1.061653e-05
##                           1080201031    16 4.246611e-05
##                           1080201703    72 1.910975e-04
##                           1080202701     3 7.962396e-06
##                           1080204001    16 4.246611e-05
##                           1080204002     3 7.962396e-06
##                           10802XXXXX   494 1.311141e-03
##                           1080300501   102 2.707215e-04
##                           1080300506    59 1.565938e-04
##                           1080300509     1 2.654132e-06
##                           10803XXXXX   236 6.263752e-04
##                           1080400701    32 8.493223e-05
##                           1080400703    16 4.246611e-05
##                           1080400707    18 4.777438e-05
##                           1080400709    64 1.698645e-04
##                           1080400712    73 1.937516e-04
##                           1080400713    46 1.220901e-04
##                           1080400715    17 4.512025e-05
##                           10804007XX   701 1.860547e-03
##                           1080401103   350 9.289462e-04
##                           1080402304     3 7.962396e-06
##                           1080402901     2 5.308264e-06
##                           1080600302     3 7.962396e-06
##                           1080702001     3 7.962396e-06
##                           1080800301     2 5.308264e-06
##                           1090100201    92 2.441802e-04
##                           1090100202    10 2.654132e-05
##                           1090100203    10 2.654132e-05
##                           1090100701     2 5.308264e-06
##                           1090100704  1027 2.725794e-03
##                           10901007XX    47 1.247442e-04
##                           1090100801   115 3.052252e-04
##                           1090100803    89 2.362178e-04
##                           1090100804    11 2.919545e-05
##                           1090101001    21 5.573677e-05
##                           1090101005     1 2.654132e-06
##                           10901010XX    29 7.696983e-05
##                           1090101401    51 1.353607e-04
##                           1090101403     5 1.327066e-05
##                           1090101601   106 2.813380e-04
##                           1090101602    42 1.114735e-04
##                           1090101702    23 6.104504e-05
##                           1090101801    56 1.486314e-04
##                           1090101901    25 6.635330e-05
##                           10901XXXXX   836 2.218854e-03
##                        10901XXXXX040   173 4.591649e-04
##                           10902004XX    13 3.450372e-05
##                           1090300401    61 1.619021e-04
##                           1090300404    41 1.088194e-04
##                           1090300406    76 2.017140e-04
##                           10903XXXXX   138 3.662702e-04
##                           1090500601    14 3.715785e-05
##                           1090500602     5 1.327066e-05
##                           1090600901     9 2.388719e-05
##                           109XXXXXXX     2 5.308264e-06
##                           1100100401    16 4.246611e-05
##                           1100100402    16 4.246611e-05
##                           1100100507     3 7.962396e-06
##                           1100100509    57 1.512855e-04
##                           1100100510    50 1.327066e-04
##                           1100100524     4 1.061653e-05
##                           11001XXXXX   158 4.193529e-04
##                           11002XXXXX    79 2.096764e-04
##                           1100400101    88 2.335636e-04
##                           1100400102   141 3.742326e-04
##                           1100400103    38 1.008570e-04
##                           1100400104    68 1.804810e-04
##                           1100400105    42 1.114735e-04
##                           1100400106    46 1.220901e-04
##                           1100400107    62 1.645562e-04
##                           1100400109    26 6.900743e-05
##                           1100400110    67 1.778268e-04
##                           1100400111    48 1.273983e-04
##                           1100400112     8 2.123306e-05
##                           1100400118     7 1.857892e-05
##                           1100400125    19 5.042851e-05
##                           1100400131     4 1.061653e-05
##                           1100400132    48 1.273983e-04
##                           1100400137     7 1.857892e-05
##                           1100400146     4 1.061653e-05
##                           1100400154     4 1.061653e-05
##                           1100400160     5 1.327066e-05
##                           1100400168     9 2.388719e-05
##                           1100400181     4 1.061653e-05
##                           1100400183     1 2.654132e-06
##                           1100400186     1 2.654132e-06
##                           1100400188     2 5.308264e-06
##                           11004001XX  1386 3.678627e-03
##                           1100400201    35 9.289462e-05
##                           1100400202    11 2.919545e-05
##                           1100400203    12 3.184959e-05
##                           1100400212    12 3.184959e-05
##                           1100400216     2 5.308264e-06
##                           1100400233     4 1.061653e-05
##                           1100400234     3 7.962396e-06
##                           11004002XX     8 2.123306e-05
##                           1100402001    12 3.184959e-05
##                           1100402002     4 1.061653e-05
##                           1100403001    12 3.184959e-05
##                           1100403201     4 1.061653e-05
##                           1100403601     4 1.061653e-05
##                           1100403602     4 1.061653e-05
##                           11004XXXXX    12 3.184959e-05
##                           1100500301    58 1.539397e-04
##                           1100500302     8 2.123306e-05
##                           1100500316     1 2.654132e-06
##                           1100500320     3 7.962396e-06
##                           1100500326    21 5.573677e-05
##                           11005003XX    14 3.715785e-05
##                           1100503407    15 3.981198e-05
##                           11005XXXXX    53 1.406690e-04
##                           1100700801    54 1.433231e-04
##                           1100702402     5 1.327066e-05
##                           1100702406     3 7.962396e-06
##                           11007XXXXX    60 1.592479e-04
##                           1100800702     2 5.308264e-06
##                           1100801007     9 2.388719e-05
##                           11008XXXXX    24 6.369917e-05
##                           1101001501    17 4.512025e-05
##                           1101001505     3 7.962396e-06
##                           110XXXXXXX  3706 9.836214e-03
##                           11101002XX    52 1.380149e-04
##                           1120100301    86 2.282554e-04
##                           1120100302     1 2.654132e-06
##                           1120100401    12 3.184959e-05
##                           1120100411    22 5.839091e-05
##                           11201004XX    41 1.088194e-04
##                           1120200101     2 5.308264e-06
##                           1120300101    81 2.149847e-04
##                           1120300102   140 3.715785e-04
##                           1120300103    37 9.820289e-05
##                           11203XXXXX     1 2.654132e-06
##                           112XXXXXXX    30 7.962396e-05
##                           1170100102    22 5.839091e-05
##                           1170100104     1 2.654132e-06
##                           1170100105    18 4.777438e-05
##                           1170100109    13 3.450372e-05
##                           1170100115    13 3.450372e-05
##                           1170100501    13 3.450372e-05
##                           11701XXXXX   319 8.466681e-04
##                           1210500105  1395 3.702514e-03
##                           1210500107   480 1.273983e-03
##                           1210500503    18 4.777438e-05
##                           1210501102   172 4.565107e-04
##                           1210501103   270 7.166157e-04
##                           1210501104    34 9.024049e-05
##                           1210501105    49 1.300525e-04
##                           1210501106   243 6.449541e-04
##                           1210501107    11 2.919545e-05
##                           1210501108     8 2.123306e-05
##                           12105011XX   434 1.151893e-03
##                           1210501203   127 3.370748e-04
##                           1210501204   327 8.679012e-04
##                           1210501210   763 2.025103e-03
##                           1210501217   284 7.537735e-04
##                           1210501222    37 9.820289e-05
##                           1210501223   126 3.344206e-04
##                           1210501224    85 2.256012e-04
##                           12105012XX  1942 5.154325e-03
##                           1210501301   165 4.379318e-04
##                           1210501302   142 3.768868e-04
##                           1210501303   158 4.193529e-04
##                           1210501305   192 5.095934e-04
##                           1210501309    22 5.839091e-05
##                           1210501801     8 2.123306e-05
##                           1210502301   181 4.803979e-04
##                           1210502401   124 3.291124e-04
##                           1210502402    37 9.820289e-05
##                           1210502403   137 3.636161e-04
##                           1210502404    63 1.672103e-04
##                           1210502901   179 4.750896e-04
##                           1210502902    53 1.406690e-04
##                           1210503002   617 1.637599e-03
##                           1210503101   166 4.405859e-04
##                           1210503104    74 1.964058e-04
##                           1210503307     2 5.308264e-06
##                           12105033XX   174 4.618190e-04
##                           1210503801   283 7.511194e-04
##                           1210503804   125 3.317665e-04
##                           1210504001    13 3.450372e-05
##                           1210504201    90 2.388719e-04
##                           1210504202   274 7.272322e-04
##                           1210504901    90 2.388719e-04
##                           1210505803    83 2.202930e-04
##                           1210505901   136 3.609620e-04
##                           1210506001    18 4.777438e-05
##                           1210506302     7 1.857892e-05
##                           1210506401  1655 4.392589e-03
##                           1210506601  1299 3.447718e-03
##                           1210506602    32 8.493223e-05
##                           1210506702   126 3.344206e-04
##                           1210507201    42 1.114735e-04
##                           1210507801    71 1.884434e-04
##                           1210600201  1656 4.395243e-03
##                           1210600202   173 4.591649e-04
##                           1210600206   120 3.184959e-04
##                           1210600207   163 4.326235e-04
##                           1210600208   137 3.636161e-04
##                           1210600212    77 2.043682e-04
##                           1210600703    10 2.654132e-05
##                           1210601501    49 1.300525e-04
##                           1210601503   139 3.689244e-04
##                           1210602003     2 5.308264e-06
##                           1210602005    26 6.900743e-05
##                           1210602011     9 2.388719e-05
##                           12106050XX   456 1.210284e-03
##                           12106XXXXX   571 1.515509e-03
##                           1211100201   193 5.122475e-04
##                           1211100202    34 9.024049e-05
##                           12111002XX   522 1.385457e-03
##                           1211200103    82 2.176388e-04
##                           1211200112   245 6.502624e-04
##                           1211200302     4 1.061653e-05
##                           1211200303   109 2.893004e-04
##                        121XXXXXXX019    97 2.574508e-04
##                        121XXXXXXX020  1955 5.188828e-03
##                           1220200101   337 8.944425e-04
##                           1230100401   958 2.542659e-03
##                           1230100402   400 1.061653e-03
##                           12301004XX     0 0.000000e+00
##                           1230100902   273 7.245781e-04
##                           1230100903   257 6.821119e-04
##                           1230100905    59 1.565938e-04
##                           1230100906   250 6.635330e-04
##                           1230100907   327 8.679012e-04
##                           1230100908   305 8.095103e-04
##                           1230100909    64 1.698645e-04
##                           12301009XX     8 2.123306e-05
##                           1230101005    70 1.857892e-04
##                           12301010XX    61 1.619021e-04
##                           1230400201   593 1.573900e-03
##                           1230400301   454 1.204976e-03
##                           1230400303   134 3.556537e-04
##                           1230400802    47 1.247442e-04
##                           1230401201   102 2.707215e-04
##                        12304XXXXX030   165 4.379318e-04
##                           1230501503    19 5.042851e-05
##                           1230501504    19 5.042851e-05
##                           12305015XX   554 1.470389e-03
##                           1230502901    69 1.831351e-04
##                           1231200101   124 3.291124e-04
##                           1231200102   233 6.184128e-04
##                           12312001XX   105 2.786839e-04
##                           1231400701    51 1.353607e-04
##                           12314007XX    14 3.715785e-05
##                           123XXXXXXX   332 8.811719e-04
##                           1250203001    15 3.981198e-05
##                           1250300801     1 2.654132e-06
##                           1290100302   141 3.742326e-04
##                           1290100304    88 2.335636e-04
##                           1290200401   211 5.600219e-04
##                           1290200402   111 2.946087e-04
##                           1300100501   154 4.087363e-04
##                           1300100601     6 1.592479e-05
##                           1310702201     2 5.308264e-06
##                           1311100701     1 2.654132e-06
##                           13111008XX     1 2.654132e-06
##                           13112XXXXX     4 1.061653e-05
##                           1311600102   320 8.493223e-04
##                           1311601003     4 1.061653e-05
##                           1311606801   304 8.068562e-04
##                           1311606804   127 3.370748e-04
##                           13116XXXXX   707 1.876471e-03
##                           1320801601    32 8.493223e-05
##                           1320801715     1 2.654132e-06
##                           1320802403    14 3.715785e-05
##                           1320803002     3 7.962396e-06
##                           1320803201     8 2.123306e-05
##                           13208XXXXX    71 1.884434e-04
##                           1400200102   389 1.032457e-03
##                           14002001XX    67 1.778268e-04
##                           1400200201    76 2.017140e-04
##                           1400200701    55 1.459773e-04
##                           1400201601    63 1.672103e-04
##                           1400201602     6 1.592479e-05
##                           1400201801   311 8.254351e-04
##                           14002018XX    63 1.672103e-04
##                           1400201901     4 1.061653e-05
##                           1400202001    73 1.937516e-04
##                           1400202502     0 0.000000e+00
##                           1400204301     2 5.308264e-06
##                           1400209701    69 1.831351e-04
##                           1400210001    76 2.017140e-04
##                           1400211501    24 6.369917e-05
##                           1400233301    11 2.919545e-05
##                           14002XXXXX   194 5.149016e-04
##                           1410200606    36 9.554876e-05
##                           1410204208     2 5.308264e-06
##                           14102XXXXX  2204 5.849707e-03
##                           14106064XX   144 3.821950e-04
##                           1430600701    21 5.573677e-05
##                           14306XXXXX    89 2.362178e-04
##                           1430901102   414 1.098811e-03
##                           14309011XX   230 6.104504e-04
##                           1430902102     7 1.857892e-05
##                           1431300101   980 2.601049e-03
##                           1431300102   138 3.662702e-04
##                           1431300104    60 1.592479e-04
##                           1431300105    45 1.194359e-04
##                           14313XXXXX   476 1.263367e-03
##                           14315XXXXX    26 6.900743e-05
##                           1431804501    12 3.184959e-05
##                           1470100101   917 2.433839e-03
##                           1470100801    28 7.431570e-05
##                           1470101208     7 1.857892e-05
##                           1470101308    19 5.042851e-05
##                           14701013XX   100 2.654132e-04
##                           14701XXXXX   324 8.599388e-04
##                           1470200201   111 2.946087e-04
##                           1470200701   217 5.759467e-04
##                           1470300311    56 1.486314e-04
##                           1470300406    98 2.601049e-04
##                           1470300413     9 2.388719e-05
##                           14703004XX   774 2.054298e-03
##                           1470401002    57 1.512855e-04
##                           14704XXXXX   961 2.550621e-03
##                           1480100101    37 9.820289e-05
##                           14801001XX    58 1.539397e-04
##                           1480200601     3 7.962396e-06
##                           1480201001    53 1.406690e-04
##                           1480201401   115 3.052252e-04
##                           1480201901    11 2.919545e-05
##                           1480203001   207 5.494053e-04
##                           1480204001   199 5.281723e-04
##                           14802XXXXX    82 2.176388e-04
##                           1480301801   162 4.299694e-04
##                           1480400101   784 2.080840e-03
##                           1480400202  2027 5.379926e-03
##                           1480400211   414 1.098811e-03
##                           1480400212    72 1.910975e-04
##                           1480400501   803 2.131268e-03
##                           1480400502   451 1.197014e-03
##                           1480400504     3 7.962396e-06
##                           14804005XX     8 2.123306e-05
##                           1480400601   444 1.178435e-03
##                           1480400602    38 1.008570e-04
##                           1480400604     5 1.327066e-05
##                           14804006XX   124 3.291124e-04
##                           1480400801   140 3.715785e-04
##                           1480400802   277 7.351946e-04
##                           1480400803   327 8.679012e-04
##                           1480401001  1451 3.851146e-03
##                           1480401201    62 1.645562e-04
##                           1480401202    63 1.672103e-04
##                           1480401301     7 1.857892e-05
##                           1480401302    63 1.672103e-04
##                           1480401501  1317 3.495492e-03
##                           1480401502   626 1.661487e-03
##                           1480401601   469 1.244788e-03
##                           1480401901   108 2.866463e-04
##                           1480402507     7 1.857892e-05
##                           1480402801     3 7.962396e-06
##                           14804028XX    54 1.433231e-04
##                           1480403201   310 8.227809e-04
##                           1480403202   101 2.680673e-04
##                           1480403203   537 1.425269e-03
##                           1480403301   915 2.428531e-03
##                           1480403302   390 1.035112e-03
##                           1480403401  1090 2.893004e-03
##                           1480404101     3 7.962396e-06
##                           1480500401  1780 4.724355e-03
##                           1480500402   273 7.245781e-04
##                           1480500403   184 4.883603e-04
##                           1480500404   346 9.183297e-04
##                           1480500405   137 3.636161e-04
##                           1480500406   448 1.189051e-03
##                           1480500407   230 6.104504e-04
##                           1480500408   111 2.946087e-04
##                           1480500412    17 4.512025e-05
##                           1480500414    11 2.919545e-05
##                           1480500419    49 1.300525e-04
##                           14805004XX   242 6.423000e-04
##                        14805004XX034   448 1.189051e-03
##                           1480501701   335 8.891342e-04
##                           1480501702   224 5.945256e-04
##                           1480600103   180 4.777438e-04
##                           1480600104    51 1.353607e-04
##                           1480600105    58 1.539397e-04
##                           1480600106     9 2.388719e-05
##                           14806001XX   319 8.466681e-04
##                           1480600401   663 1.759690e-03
##                           14806004XX     1 2.654132e-06
##                           1480600512     9 2.388719e-05
##                           1480600802     4 1.061653e-05
##                           1480601401     5 1.327066e-05
##                           1480602102     3 7.962396e-06
##                           1480603001    21 5.573677e-05
##                           14806XXXXX   107 2.839921e-04
##                           148XXXXXXX   931 2.470997e-03
##                           1500100101    74 1.964058e-04
##                           1500500901    59 1.565938e-04
##                           1510200101     7 1.857892e-05
##                           1510200103     7 1.857892e-05
##                           1510200104     2 5.308264e-06
##                           1510300401    71 1.884434e-04
##                           1510302204    11 2.919545e-05
##                           1510402101    19 5.042851e-05
##                           1520100102    93 2.468343e-04
##                           1520100103     5 1.327066e-05
##                           1520400202     3 7.962396e-06
##                           1520400203    26 6.900743e-05
##                           15204002XX    21 5.573677e-05
##                           1520500101    13 3.450372e-05
##                           1580200101   494 1.311141e-03
##                           1580200102    63 1.672103e-04
##                           1580200103    32 8.493223e-05
##                           1580200105   220 5.839091e-04
##                           15802001XX    66 1.751727e-04
##                           1580200502   134 3.556537e-04
##                           15802XXXXX    45 1.194359e-04
##                           1600200101     1 2.654132e-06
##                           1610100102     4 1.061653e-05
##                           1610200301    32 8.493223e-05
##                           1610200302    26 6.900743e-05
##                           16102003XX   450 1.194359e-03
##                           1610201201    59 1.565938e-04
##                           1610500201    11 2.919545e-05
##                           1610500202   294 7.803148e-04
##                           1610501301     2 5.308264e-06
##                           16105XXXXX    34 9.024049e-05
##                           1611101102    18 4.777438e-05
##                           16111XXXXX   146 3.875033e-04
##                           1620100101  1149 3.049598e-03
##                           1620100401    53 1.406690e-04
##                           1620100402    69 1.831351e-04
##                           1620100801     3 7.962396e-06
##                           1620101101     5 1.327066e-05
##                           1620101102    14 3.715785e-05
##                           16201XXXXX    18 4.777438e-05
##                           1620300201    29 7.696983e-05
##                           16203XXXXX     9 2.388719e-05
##                           1620400102    24 6.369917e-05
##                           1620400201    25 6.635330e-05
##                           1620400701    15 3.981198e-05
##                           1620400702     8 2.123306e-05
##                           16204XXXXX    88 2.335636e-04
##                           1630200201    63 1.672103e-04
##                           1630200204     3 7.962396e-06
##                           1630200301    76 2.017140e-04
##                           1630200302     2 5.308264e-06
##                           1630201302   101 2.680673e-04
##                           16302XXXXX   784 2.080840e-03
##                           1650100102   619 1.642908e-03
##                           1650100112   102 2.707215e-04
##                           1650100121    18 4.777438e-05
##                           1650100122     8 2.123306e-05
##                           1650100128    28 7.431570e-05
##                           1650100202     8 2.123306e-05
##                           1650100204    14 3.715785e-05
##                           1650101001    93 2.468343e-04
##                           1650101203    14 3.715785e-05
##                           1650101206    49 1.300525e-04
##                           1650101217    20 5.308264e-05
##                           1650104302    47 1.247442e-04
##                           16501XXXXX  4141 1.099076e-02
##                           17000XXXXX   349 9.262921e-04
##                           1700102510   113 2.999169e-04
##                           17001025XX   413 1.096157e-03
##                           1700116701   471 1.250096e-03
##                           1700200101    13 3.450372e-05
##                           1700200901     8 2.123306e-05
##                           1700204001    13 3.450372e-05
##                           1700204004    12 3.184959e-05
##                           1700204006    14 3.715785e-05
##                           1700204009    15 3.981198e-05
##                           1700204010    22 5.839091e-05
##                           17002040XX    71 1.884434e-04
##                           1700204201   415 1.101465e-03
##                           1700204202   164 4.352777e-04
##                           1700204211    18 4.777438e-05
##                           1700204219    35 9.289462e-05
##                           1700204220   102 2.707215e-04
##                           1700204221     1 2.654132e-06
##                           1700204222    40 1.061653e-04
##                           1700204223     1 2.654132e-06
##                           1700204224    14 3.715785e-05
##                           1700204225    95 2.521425e-04
##                           1700204228   164 4.352777e-04
##                           1700204229    12 3.184959e-05
##                           1700204230    12 3.184959e-05
##                           1700204232    13 3.450372e-05
##                           1700204233    14 3.715785e-05
##                           1700204234    20 5.308264e-05
##                           1700204235    13 3.450372e-05
##                           1700204236    17 4.512025e-05
##                           1700204240    13 3.450372e-05
##                           1700204255    13 3.450372e-05
##                           1700204257    36 9.554876e-05
##                           1700204269     3 7.962396e-06
##                           1700204273     3 7.962396e-06
##                           1700204274    13 3.450372e-05
##                           1700204277    13 3.450372e-05
##                           1700204284    14 3.715785e-05
##                           1700204285    13 3.450372e-05
##                           17002042XX  2430 6.449541e-03
##                           1700206101    18 4.777438e-05
##                           1700206102     5 1.327066e-05
##                           1700206113     2 5.308264e-06
##                           17002061XX     1 2.654132e-06
##                           1700207201    14 3.715785e-05
##                           1700208102   126 3.344206e-04
##                           1700211502    27 7.166157e-05
##                           1700211504    13 3.450372e-05
##                           1700211509    13 3.450372e-05
##                           1700211511    13 3.450372e-05
##                           1700211519   126 3.344206e-04
##                           1700212501    18 4.777438e-05
##                           1700220802    13 3.450372e-05
##                           1700220804    18 4.777438e-05
##                           1700220805    13 3.450372e-05
##                           1700225901    89 2.362178e-04
##                           1700240505    64 1.698645e-04
##                           17002405XX     8 2.123306e-05
##                           1700255701    19 5.042851e-05
##                           17002XXXXX  1918 5.090625e-03
##                           17004089XX    27 7.166157e-05
##                           1700420101     9 2.388719e-05
##                           1700505801   403 1.069615e-03
##                           1700505802    93 2.468343e-04
##                           1700522002    59 1.565938e-04
##                           1700600602   185 4.910144e-04
##                           1700600603     8 2.123306e-05
##                           1700634501   131 3.476913e-04
##                           1700634503   604 1.603096e-03
##                           17006345XX   208 5.520595e-04
##                           1700829701   126 3.344206e-04
##                           1701102605    70 1.857892e-04
##                           17011026XX   375 9.952995e-04
##                           17012XXXXX    61 1.619021e-04
##                           1701300701    10 2.654132e-05
##                           1701523304    31 8.227809e-05
##                           17015XXXXX   555 1.473043e-03
##                           1701600102    12 3.184959e-05
##                           1701600103    29 7.696983e-05
##                           1701600104    12 3.184959e-05
##                           1701640002   122 3.238041e-04
##                           17016XXXXX   346 9.183297e-04
##                           1701735702    14 3.715785e-05
##                           1701916502   296 7.856231e-04
##                           1702021301  1450 3.848492e-03
##                           1702222101   594 1.576554e-03
##                           1702300101    18 4.777438e-05
##                           1702300201    13 3.450372e-05
##                           1702300401   990 2.627591e-03
##                           1702300402    17 4.512025e-05
##                           1702300403   173 4.591649e-04
##                           1702300405   311 8.254351e-04
##                           1702300406   135 3.583078e-04
##                           1702300408   358 9.501793e-04
##                           1702300411    90 2.388719e-04
##                           1702300413   364 9.661041e-04
##                           1702300414   250 6.635330e-04
##                           1702300415    87 2.309095e-04
##                           17023004XX  1750 4.644731e-03
##                           1702301127   103 2.733756e-04
##                           1702304303     7 1.857892e-05
##                           1702304307    91 2.415260e-04
##                           1702304308   247 6.555706e-04
##                           17023043XX   826 2.192313e-03
##                           1702304405    60 1.592479e-04
##                           1702304408    13 3.450372e-05
##                           1702304411    13 3.450372e-05
##                           1702304426   139 3.689244e-04
##                           1702304429   189 5.016310e-04
##                           1702304431    33 8.758636e-05
##                           1702304442   101 2.680673e-04
##                           17023044XX  1730 4.591649e-03
##                           1702304604   106 2.813380e-04
##                           1702304605   251 6.661872e-04
##                           1702304609     7 1.857892e-05
##                           1702304610     3 7.962396e-06
##                           1702304701    16 4.246611e-05
##                           1702304703    82 2.176388e-04
##                           1702304706     4 1.061653e-05
##                           1702304721    16 4.246611e-05
##                           17023047XX   439 1.165164e-03
##                           1702304801   397 1.053690e-03
##                           1702304806   255 6.768037e-04
##                           1702304811     8 2.123306e-05
##                           1702304814    17 4.512025e-05
##                           1702304815     1 2.654132e-06
##                           17023048XX   830 2.202930e-03
##                           1702304903     8 2.123306e-05
##                           1702305001    12 3.184959e-05
##                           1702307202   542 1.438540e-03
##                           1702309003    43 1.141277e-04
##                           1702309901   439 1.165164e-03
##                           1702311402    55 1.459773e-04
##                           1702311408    13 3.450372e-05
##                           1702311412    26 6.900743e-05
##                           1702313401   371 9.846830e-04
##                           1702315101    78 2.070223e-04
##                           1702317901   463 1.228863e-03
##                           1702323101    38 1.008570e-04
##                           1702323102    10 2.654132e-05
##                           1702323104    13 3.450372e-05
##                           17023231XX   383 1.016533e-03
##                           1702326801   306 8.121644e-04
##                           1702326802    19 5.042851e-05
##                           1702328301    91 2.415260e-04
##                           1702329101   281 7.458111e-04
##                           1702342201   288 7.643900e-04
##                           1702342501    38 1.008570e-04
##                           1702352601    30 7.962396e-05
##                           17023XXXXX  2343 6.218631e-03
##                           1702632701   160 4.246611e-04
##                           1702700301   484 1.284600e-03
##                           1702700302    27 7.166157e-05
##                           1702700404     9 2.388719e-05
##                           17027XXXXX    22 5.839091e-05
##                           1702807101  1653 4.387280e-03
##                           1702905101    63 1.672103e-04
##                           1702905102   176 4.671272e-04
##                           1703001001    61 1.619021e-04
##                           1703028602    20 5.308264e-05
##                           17030XXXXX    41 1.088194e-04
##                           1703202702   178 4.724355e-04
##                           1703202707    16 4.246611e-05
##                           1703202713    29 7.696983e-05
##                           1703202716     2 5.308264e-06
##                           1703202717    18 4.777438e-05
##                           1703202720    91 2.415260e-04
##                           1703202722   243 6.449541e-04
##                           1703202724     9 2.388719e-05
##                           1703202725   118 3.131876e-04
##                           1703202727     8 2.123306e-05
##                           1703202728    27 7.166157e-05
##                           1703202729    15 3.981198e-05
##                           1703202733   180 4.777438e-04
##                           1703202734    15 3.981198e-05
##                           1703202742    15 3.981198e-05
##                           1703202745    13 3.450372e-05
##                           1703202750    13 3.450372e-05
##                           1703202753    13 3.450372e-05
##                           1703202757     8 2.123306e-05
##                           17032027XX  1309 3.474259e-03
##                           1703202801   350 9.289462e-04
##                           1703209801    13 3.450372e-05
##                           1703210001    11 2.919545e-05
##                           1703210102     9 2.388719e-05
##                           1703214001    11 2.919545e-05
##                           17032217XX    17 4.512025e-05
##                           1703222501    35 9.289462e-05
##                           1703235901     8 2.123306e-05
##                           17032XXXXX  1861 4.939340e-03
##                           1703318404    16 4.246611e-05
##                           1703318405    55 1.459773e-04
##                           1703318416     9 2.388719e-05
##                           17033184XX   675 1.791539e-03
##                           1703323010    13 3.450372e-05
##                           17033230XX   131 3.476913e-04
##                           17033XXXXX   150 3.981198e-04
##                           1703402901    31 8.227809e-05
##                           1703402902     3 7.962396e-06
##                           17035169XX   232 6.157586e-04
##                           17035XXXXX   345 9.156756e-04
##                           1703600201    20 5.308264e-05
##                           1703603001     5 1.327066e-05
##                           1703603010     8 2.123306e-05
##                           17036030XX    12 3.184959e-05
##                           1703603201    53 1.406690e-04
##                           1703616301   126 3.344206e-04
##                           1703619705     2 5.308264e-06
##                           1703620702    21 5.573677e-05
##                           1703620703    20 5.308264e-05
##                           1703620704     1 2.654132e-06
##                           1703620705   223 5.918715e-04
##                           1703620707    13 3.450372e-05
##                           1703620708     9 2.388719e-05
##                           17036207XX    18 4.777438e-05
##                           1703620901    18 4.777438e-05
##                           1703620904   145 3.848492e-04
##                           1703620918    35 9.289462e-05
##                           1703620919   224 5.945256e-04
##                           1703620923    16 4.246611e-05
##                           1703626303   493 1.308487e-03
##                           1703639501    71 1.884434e-04
##                           17036XXXXX  2035 5.401159e-03
##                           1703700501    28 7.431570e-05
##                           1703700921   100 2.654132e-04
##                           1703701601    11 2.919545e-05
##                           1703701604   119 3.158417e-04
##                           1703701605    65 1.725186e-04
##                           1703701606    11 2.919545e-05
##                           1703701607    11 2.919545e-05
##                           1703701609   179 4.750896e-04
##                           1703701614   126 3.344206e-04
##                           1703701617   126 3.344206e-04
##                           1703701618    11 2.919545e-05
##                           1703701632    11 2.919545e-05
##                           17037016XX   273 7.245781e-04
##                           1703702801    13 3.450372e-05
##                           1703703802   241 6.396458e-04
##                           1703703804   126 3.344206e-04
##                           17037038XX   157 4.166987e-04
##                           1703703901     4 1.061653e-05
##                           1703703907    60 1.592479e-04
##                           1703703908   102 2.707215e-04
##                           17037039XX    68 1.804810e-04
##                           1703707001   199 5.281723e-04
##                           1703707003   130 3.450372e-04
##                           1703707009   108 2.866463e-04
##                           1703709601   107 2.839921e-04
##                           1703710601   509 1.350953e-03
##                           1703710606   348 9.236380e-04
##                           1703710801   104 2.760297e-04
##                           1703710803    63 1.672103e-04
##                           1703714701    63 1.672103e-04
##                           1703716603    11 2.919545e-05
##                           1703716607   117 3.105335e-04
##                           1703718603    33 8.758636e-05
##                           1703719402    63 1.672103e-04
##                           1703721002   329 8.732095e-04
##                           1703729805    58 1.539397e-04
##                           1703730304   101 2.680673e-04
##                           1703730305   230 6.104504e-04
##                           1703731402    11 2.919545e-05
##                           1703736301   126 3.344206e-04
##                           1703741101    97 2.574508e-04
##                           1703745701    61 1.619021e-04
##                           1703745702   115 3.052252e-04
##                           1703745705   265 7.033450e-04
##                           17037457XX   724 1.921592e-03
##                           1703755301    63 1.672103e-04
##                           1703756101    73 1.937516e-04
##                           1703756105    16 4.246611e-05
##                           1703756501   126 3.344206e-04
##                           17037XXXXX  2440 6.476082e-03
##                           17038155XX    89 2.362178e-04
##                           1703817202    44 1.167818e-04
##                           1703817204    27 7.166157e-05
##                           1703817206    13 3.450372e-05
##                           1703817207    23 6.104504e-05
##                           1703817215    28 7.431570e-05
##                           1703817216    21 5.573677e-05
##                           1703817217     3 7.962396e-06
##                           1703817223    13 3.450372e-05
##                           1703817225    13 3.450372e-05
##                           1703817226    18 4.777438e-05
##                           1703818001    13 3.450372e-05
##                           17038XXXXX   998 2.648824e-03
##                           1703900801   296 7.856231e-04
##                           1703900802   527 1.398728e-03
##                           1703900803   257 6.821119e-04
##                           1703900807   239 6.343376e-04
##                           17039008XX   584 1.550013e-03
##                           1703903301    36 9.554876e-05
##                           1703903302    33 8.758636e-05
##                           1703903303   185 4.910144e-04
##                           1703903305    20 5.308264e-05
##                           1703903307     5 1.327066e-05
##                           17039033XX   544 1.443848e-03
##                           17039034XX   151 4.007739e-04
##                           1703906002   477 1.266021e-03
##                           1703906006   636 1.688028e-03
##                           1703906010    59 1.565938e-04
##                           1703906011    27 7.166157e-05
##                           17039060XX   626 1.661487e-03
##                           1703906302   624 1.656178e-03
##                           1703907601   320 8.493223e-04
##                           1703910201   102 2.707215e-04
##                           1703910202     7 1.857892e-05
##                           1703910501    89 2.362178e-04
##                           1703910701    61 1.619021e-04
##                           1703911802    56 1.486314e-04
##                           1703912601    21 5.573677e-05
##                           1703919101     1 2.654132e-06
##                           1703919103   686 1.820735e-03
##                           1703919115   448 1.189051e-03
##                           17039191XX   447 1.186397e-03
##                           1703920301    31 8.227809e-05
##                           1703922001   109 2.893004e-04
##                           1703922401    49 1.300525e-04
##                           1703922406    26 6.900743e-05
##                           1703923508   753 1.998561e-03
##                           1703926101  1105 2.932816e-03
##                           17039264XX    74 1.964058e-04
##                           1703926601    10 2.654132e-05
##                           1703927701    36 9.554876e-05
##                           1703927702   265 7.033450e-04
##                           17039277XX    22 5.839091e-05
##                           1703929301   488 1.295216e-03
##                           1703930001    26 6.900743e-05
##                           1703933001    22 5.839091e-05
##                           1703933004    24 6.369917e-05
##                           1703933005    64 1.698645e-04
##                           1703933006    51 1.353607e-04
##                           1703935301   120 3.184959e-04
##                           1703936701     5 1.327066e-05
##                           17039XXXXX  2923 7.758028e-03
##                           1704007501    55 1.459773e-04
##                           1704007502     2 5.308264e-06
##                           17040075XX   632 1.677411e-03
##                           1704100701   574 1.523472e-03
##                           1704100702   236 6.263752e-04
##                           1704100703    21 5.573677e-05
##                           17041007XX  1015 2.693944e-03
##                           1704118101    27 7.166157e-05
##                           17041251XX   706 1.873817e-03
##                           1704149903   337 8.944425e-04
##                           17041XXXXX   565 1.499585e-03
##                           1704200101     8 2.123306e-05
##                           17042XXXXX     9 2.388719e-05
##                           1704603611    19 5.042851e-05
##                           1704603612    15 3.981198e-05
##                           1704603613    10 2.654132e-05
##                           17046036XX   354 9.395628e-04
##                           1704603701    11 2.919545e-05
##                           1704614110     8 2.123306e-05
##                           17046XXXXX   325 8.625929e-04
##                           1704700302    42 1.114735e-04
##                           1704700303    13 3.450372e-05
##                           17047XXXXX    68 1.804810e-04
##                           1705013201   158 4.193529e-04
##                           1705013202   535 1.419961e-03
##                           1705700402    18 4.777438e-05
##                           1705700602    11 2.919545e-05
##                           1705700701    59 1.565938e-04
##                           1705700703    23 6.104504e-05
##                           17059051XX   107 2.839921e-04
##                           1706008301    54 1.433231e-04
##                           1706300501    28 7.431570e-05
##                           1706300506     2 5.308264e-06
##                           1706300801     2 5.308264e-06
##                           1706306501     8 2.123306e-05
##                           1706306601     9 2.388719e-05
##                           1706306901    10 2.654132e-05
##                           1706307901     8 2.123306e-05
##                           1706311703    18 4.777438e-05
##                           1706316401    22 5.839091e-05
##                           1706324301    63 1.672103e-04
##                           1706325002    63 1.672103e-04
##                           1706333102    15 3.981198e-05
##                           1706338702     8 2.123306e-05
##                           17063XXXXX   582 1.544705e-03
##                           1706505506    80 2.123306e-04
##                           1706505609    16 4.246611e-05
##                           1706505611    13 3.450372e-05
##                           1706543701    13 3.450372e-05
##                           17065XXXXX   418 1.109427e-03
##                           1706600704    28 7.431570e-05
##                           17066XXXXX    23 6.104504e-05
##                           1706902102     9 2.388719e-05
##                           1707027002    87 2.309095e-04
##                           1707027003    68 1.804810e-04
##                           1707030504    87 2.309095e-04
##                           17070305XX   167 4.432401e-04
##                           17071XXXXX   123 3.264582e-04
##                           1707700109   202 5.361347e-04
##                           1707700201   138 3.662702e-04
##                           1707700302   481 1.276638e-03
##                           1707700401   187 4.963227e-04
##                           1707700601     5 1.327066e-05
##                           17077XXXXX  1003 2.662094e-03
##                           1708800101    16 4.246611e-05
##                           1709100301    16 4.246611e-05
##                           1709200702   157 4.166987e-04
##                           1709201501   151 4.007739e-04
##                           1709201502   675 1.791539e-03
##                           1709201902   116 3.078793e-04
##                           1709201903    75 1.990599e-04
##                           1709201904     6 1.592479e-05
##                           1709201906   124 3.291124e-04
##                           1709201909     2 5.308264e-06
##                           1709201910     7 1.857892e-05
##                           1709201911     9 2.388719e-05
##                           1709243001     9 2.388719e-05
##                           1709243002    22 5.839091e-05
##                           1709243003     6 1.592479e-05
##                           1709243004     1 2.654132e-06
##                           1709244001    40 1.061653e-04
##                           1709244002    59 1.565938e-04
##                           1709244801     4 1.061653e-05
##                           17092448XX     5 1.327066e-05
##                           1709252901    11 2.919545e-05
##                           1709253501    29 7.696983e-05
##                           17092XXXXX   155 4.113905e-04
##                           1709345201     8 2.123306e-05
##                           1709400101    15 3.981198e-05
##                           1709400901     2 5.308264e-06
##                           1709441601    74 1.964058e-04
##                           1709441701   184 4.883603e-04
##                           1709441702    10 2.654132e-05
##                           1709441801    65 1.725186e-04
##                           1709446601    12 3.184959e-05
##                           1709446602     5 1.327066e-05
##                           1709446603     1 2.654132e-06
##                           1709447001    31 8.227809e-05
##                           1709448001    21 5.573677e-05
##                           17094XXXXX    79 2.096764e-04
##                           17095XXXXX    44 1.167818e-04
##                           1709637301    98 2.601049e-04
##                           17096373XX    43 1.141277e-04
##                           170XXXXXXX   546 1.449156e-03
##                           1710200101   569 1.510201e-03
##                           1710200102    17 4.512025e-05
##                           1710200103    84 2.229471e-04
##                           17102001XX   857 2.274591e-03
##                           1711500401   134 3.556537e-04
##                           1711501202    76 2.017140e-04
##                           17115024XX    25 6.635330e-05
##                           1720400204   108 2.866463e-04
##                           17204002XX   498 1.321758e-03
##                           1720820201    89 2.362178e-04
##                           1720900501    63 1.672103e-04
##                           1720900602    77 2.043682e-04
##                           1720919602    53 1.406690e-04
##                           1720928801     6 1.592479e-05
##                           1720928802     9 2.388719e-05
##                           1721201002   291 7.723524e-04
##                           17212010XX    26 6.900743e-05
##                           17212XXXXX     8 2.123306e-05
##                           1721335202    31 8.227809e-05
##                           17213352XX     1 2.654132e-06
##                           1721348401    45 1.194359e-04
##                           1727210301   121 3.211500e-04
##                           1732100401    13 3.450372e-05
##                           1732101702     3 7.962396e-06
##                           1732116201     5 1.327066e-05
##                        17321XXXXX023   602 1.597788e-03
##                           1740200416    13 3.450372e-05
##                           1740200802    13 3.450372e-05
##                           17402XXXXX   296 7.856231e-04
##                           17405206XX    62 1.645562e-04
##                           1740526702     3 7.962396e-06
##                           17405XXXXX   118 3.131876e-04
##                           17406330XX    43 1.141277e-04
##                           17407001XX   775 2.056952e-03
##                           1750100101  1923 5.103896e-03
##                           1750100102    56 1.486314e-04
##                           1750100104   258 6.847661e-04
##                           1750100201  3026 8.031404e-03
##                           1750100205  1749 4.642077e-03
##                           1750100207   108 2.866463e-04
##                           17501002XX   156 4.140446e-04
##                           1750100601   213 5.653301e-04
##                           1750101001  1216 3.227425e-03
##                           1750101202    65 1.725186e-04
##                           1750101401   179 4.750896e-04
##                           1750101403   688 1.826043e-03
##                           17501014XX   419 1.112081e-03
##                           1750101503  1169 3.102680e-03
##                           1750101504   528 1.401382e-03
##                           1750101505   185 4.910144e-04
##                           1750101506   442 1.173126e-03
##                           1750101507   185 4.910144e-04
##                           1750101508   133 3.529996e-04
##                           1750101509   228 6.051421e-04
##                           1750101511   255 6.768037e-04
##                           1750101512   186 4.936686e-04
##                           1750101515   215 5.706384e-04
##                           17501015XX  1070 2.839921e-03
##                           1750101801    12 3.184959e-05
##                           1750102301    97 2.574508e-04
##                           1750102303     8 2.123306e-05
##                        17501023XX018  2167 5.751504e-03
##                           1750102401  1451 3.851146e-03
##                           1750102404   245 6.502624e-04
##                           1750102406  1276 3.386673e-03
##                           1750102501  5785 1.535415e-02
##                           1750102601  2057 5.459550e-03
##                           1750102602   658 1.746419e-03
##                           1750102603   917 2.433839e-03
##                           1750102604   577 1.531434e-03
##                           1750102605  4441 1.178700e-02
##                           1750102608   865 2.295824e-03
##                           1750102610  6866 1.822327e-02
##                           1750102612  5341 1.417572e-02
##                           1750102701    21 5.573677e-05
##                           17501XXXXX   645 1.711915e-03
##                           1750300402  1526 4.050206e-03
##                           1750300404  1323 3.511417e-03
##                           1750300505  3212 8.525072e-03
##                           1750300507  1431 3.798063e-03
##                           1750300901    21 5.573677e-05
##                           1750300903  1526 4.050206e-03
##                           1750300904  1216 3.227425e-03
##                           1750300905   153 4.060822e-04
##                           1750300906   166 4.405859e-04
##                           1750300907     5 1.327066e-05
##                           17503XXXXX  1549 4.111251e-03
##                           1750400301  5143 1.365020e-02
##                           1750500101   454 1.204976e-03
##                           1750500201     1 2.654132e-06
##                           1750500501   135 3.583078e-04
##                           1750500701   210 5.573677e-04
##                           1750500901   136 3.609620e-04
##                           1750501701    19 5.042851e-05
##                           17505XXXXX   118 3.131876e-04
##                           17506002XX    15 3.981198e-05
##                           1750600302  1748 4.639423e-03
##                           1750600601   438 1.162510e-03
##                           1750601201   194 5.149016e-04
##                           1750601202     1 2.654132e-06
##                           17506XXXXX   646 1.714569e-03
##                           175XXXXXXX  3457 9.175335e-03
##                           1760300401   237 6.290293e-04
##                           1760300405     7 1.857892e-05
##                           1760300901   434 1.151893e-03
##                           17603009XX    35 9.289462e-05
##                           1760301102   127 3.370748e-04
##                           1760301104    94 2.494884e-04
##                           1760301105    30 7.962396e-05
##                           17603011XX    52 1.380149e-04
##                           17603XXXXX   796 2.112689e-03
##                           1760401201    58 1.539397e-04
##                           1760600104     3 7.962396e-06
##                           1760800101     3 7.962396e-06
##                           1760800302    11 2.919545e-05
##                           1760800309    15 3.981198e-05
##                           1760800310    14 3.715785e-05
##                           1760801001    21 5.573677e-05
##                           1760801002    40 1.061653e-04
##                           1760801004    79 2.096764e-04
##                           1760801005    26 6.900743e-05
##                           17608010XX   182 4.830520e-04
##                           1760801502    52 1.380149e-04
##                           1760801503    13 3.450372e-05
##                           1760801504     4 1.061653e-05
##                           1760802001   170 4.512025e-04
##                           17608XXXXX   136 3.609620e-04
##                           1771000101    35 9.289462e-05
##                           1771000103    29 7.696983e-05
##                           1771000104    14 3.715785e-05
##                           1771000107   139 3.689244e-04
##                           1771000108     4 1.061653e-05
##                           17710001XX  2675 7.099803e-03
##                           1772301101     1 2.654132e-06
##                           1780100101   172 4.565107e-04
##                           1780100102     7 1.857892e-05
##                           1780100103    34 9.024049e-05
##                           1780100104    35 9.289462e-05
##                           1780100109   338 8.970966e-04
##                           1780100110    32 8.493223e-05
##                           1780100112   225 5.971797e-04
##                           1780100115    32 8.493223e-05
##                           1780100116    32 8.493223e-05
##                           1780100122     3 7.962396e-06
##                           1780100132    13 3.450372e-05
##                           1780100147    12 3.184959e-05
##                           1780100148     4 1.061653e-05
##                           17801001XX  1417 3.760905e-03
##                           1780100901     2 5.308264e-06
##                           1780100902    24 6.369917e-05
##                           1780101703   328 8.705553e-04
##                           1780101902    13 3.450372e-05
##                           1780107901    21 5.573677e-05
##                           1780108003    11 2.919545e-05
##                           17801XXXXX  1414 3.752943e-03
##                           1780200301   324 8.599388e-04
##                           1780200302    74 1.964058e-04
##                           1780200304    13 3.450372e-05
##                           1780200307    73 1.937516e-04
##                           1780200403   137 3.636161e-04
##                           1780200803    11 2.919545e-05
##                           17802020XX   160 4.246611e-04
##                           1780202501    88 2.335636e-04
##                           1780202502    18 4.777438e-05
##                           1780207001   250 6.635330e-04
##                           17802XXXXX  1131 3.001823e-03
##                           1780700501   189 5.016310e-04
##                           1780701402   193 5.122475e-04
##                           1780701403    85 2.256012e-04
##                           1780702902     7 1.857892e-05
##                           1780800101     1 2.654132e-06
##                           1780800401   291 7.723524e-04
##                           1780900302    15 3.981198e-05
##                           1780901801    65 1.725186e-04
##                           17809XXXXX   220 5.839091e-04
##                           1781103001     2 5.308264e-06
##                           1781301203     1 2.654132e-06
##                           17813012XX    10 2.654132e-05
##                           1781303001    30 7.962396e-05
##                           17813XXXXX    46 1.220901e-04
##                           1781602205    21 5.573677e-05
##                           1782000301   374 9.926454e-04
##                           1782400201    12 3.184959e-05
##                           1830101805    34 9.024049e-05
##                           18301XXXXX   123 3.264582e-04
##                           1830200201  1324 3.514071e-03
##                           1830200202   200 5.308264e-04
##                           1830200405   892 2.367486e-03
##                           1830200408    32 8.493223e-05
##                           1830200415    30 7.962396e-05
##                           1830200501  1147 3.044290e-03
##                           1830200801   131 3.476913e-04
##                           1830200802   141 3.742326e-04
##                           1830201001    32 8.493223e-05
##                           1830201102  1003 2.662094e-03
##                           1830201103    30 7.962396e-05
##                           1830201401   766 2.033065e-03
##                           1830201404   108 2.866463e-04
##                           1830201801    10 2.654132e-05
##                           1830202402    77 2.043682e-04
##                           1830202404   299 7.935855e-04
##                           1830202405   616 1.634945e-03
##                           1830204301    92 2.441802e-04
##                           1830204503    32 8.493223e-05
##                           1830204504   633 1.680066e-03
##                           1830204802   802 2.128614e-03
##                           1830204804    13 3.450372e-05
##                           1830204901    30 7.962396e-05
##                           1830205001    63 1.672103e-04
##                           1830205003   150 3.981198e-04
##                           18302053XX    99 2.627591e-04
##                           1830205902    13 3.450372e-05
##                           18302XXXXX    13 3.450372e-05
##                           1830300701  1473 3.909537e-03
##                           1830300704   142 3.768868e-04
##                           1830300708    14 3.715785e-05
##                           1830301701   142 3.768868e-04
##                           1830305701   105 2.786839e-04
##                           1830305702    44 1.167818e-04
##                           18303057XX    90 2.388719e-04
##                           18303081XX    43 1.141277e-04
##                           18303XXXXX   307 8.148186e-04
##                           18304XXXXX   944 2.505501e-03
##                           1830500301   652 1.730494e-03
##                           1830500302    17 4.512025e-05
##                           18305003XX    69 1.831351e-04
##                           1830506401   637 1.690682e-03
##                           1830506402    39 1.035112e-04
##                           1830509201  1126 2.988553e-03
##                           18305XXXXX    46 1.220901e-04
##                           18306XXXXX    26 6.900743e-05
##                           1830700101   297 7.882772e-04
##                           1830700102    14 3.715785e-05
##                           1830800902    11 2.919545e-05
##                           1830804601   128 3.397289e-04
##                           1830804603    27 7.166157e-05
##                           1830804606    94 2.494884e-04
##                           1830804607     6 1.592479e-05
##                           18308046XX   200 5.308264e-04
##                           1831000201     8 2.123306e-05
##                           183XXXXXXX  3236 8.588771e-03
##                           19001XXXXX    48 1.273983e-04
##                           1900200505     3 7.962396e-06
##                           1900200612    64 1.698645e-04
##                           19002006XX    31 8.227809e-05
##                           19002XXXXX   161 4.273153e-04
##                           1900300601    11 2.919545e-05
##                           1900800201    28 7.431570e-05
##                           19009004XX    60 1.592479e-04
##                           1900901001    41 1.088194e-04
##                           1900901801    50 1.327066e-04
##                           19009XXXXX   129 3.423830e-04
##                           1901000201    91 2.415260e-04
##                           19010XXXXX   758 2.011832e-03
##                           1930100101    11 2.919545e-05
##                           1930100601     5 1.327066e-05
##                           19301XXXXX    30 7.962396e-05
##                           1950100101   567 1.504893e-03
##                           1950100102    19 5.042851e-05
##                           1950100103   263 6.980367e-04
##                           1950100105    12 3.184959e-05
##                           1950100106   147 3.901574e-04
##                           1950100107    21 5.573677e-05
##                           19501001XX   709 1.881780e-03
##                           19501XXXXX    54 1.433231e-04
##                        199XXXXXXX007   578 1.534088e-03
##                        199XXXXXXX008   235 6.237210e-04
##                        199XXXXXXX009  1102 2.924854e-03
##                        199XXXXXXX010 14289 3.792489e-02
##                        199XXXXXXX012  1478 3.922807e-03
##                        199XXXXXXX013   840 2.229471e-03
##                        199XXXXXXX053   294 7.803148e-04
##                        199XXXXXXX054  6405 1.699972e-02
##                           2020200101    25 6.635330e-05
##                           2090100101     3 7.962396e-06
##                           21302007XX    17 4.512025e-05
##                           2130301201    37 9.820289e-05
##                           2130500101    37 9.820289e-05
##                           2250100102   135 3.583078e-04
##                           2250100402     4 1.061653e-05
##                           22501XXXXX    53 1.406690e-04
##                           225XXXXXXX    50 1.327066e-04
##                           2280100101    92 2.441802e-04
##                           2280100103   309 8.201268e-04
##                           2280100104   139 3.689244e-04
##                           2280100105   136 3.609620e-04
##                           2280100108     2 5.308264e-06
##                           2280100109   183 4.857062e-04
##                           2280100110    27 7.166157e-05
##                           2280100111    90 2.388719e-04
##                           2280100112   453 1.202322e-03
##                           2280100116    86 2.282554e-04
##                           2280100117   305 8.095103e-04
##                           2280100119    55 1.459773e-04
##                           2280100120   208 5.520595e-04
##                           2280100122    91 2.415260e-04
##                           2280100123   235 6.237210e-04
##                           2280100125    11 2.919545e-05
##                           2280100128    99 2.627591e-04
##                           2280100129    56 1.486314e-04
##                           2280100130    42 1.114735e-04
##                           2280100131   216 5.732925e-04
##                           2280100132    39 1.035112e-04
##                           2280100133     4 1.061653e-05
##                           22801001XX  2506 6.651255e-03
##                           2280100301     6 1.592479e-05
##                           2280101601    27 7.166157e-05
##                           2280101606    56 1.486314e-04
##                           2280101607    43 1.141277e-04
##                           22801016XX   398 1.056345e-03
##                           2280101701   611 1.621675e-03
##                           2280101902    13 3.450372e-05
##                           22801019XX    54 1.433231e-04
##                           2280102201   170 4.512025e-04
##                           2280102202    49 1.300525e-04
##                           2280104302    92 2.441802e-04
##                           2280106701    65 1.725186e-04
##                        22801XXXXX027   238 6.316834e-04
##                           2280202101    61 1.619021e-04
##                           2280203001    46 1.220901e-04
##                           2280203101   130 3.450372e-04
##                           2280203102    53 1.406690e-04
##                           22802031XX     1 2.654132e-06
##                           22802XXXXX    19 5.042851e-05
##                           2280400201    16 4.246611e-05
##                           2280400202     5 1.327066e-05
##                           2280400203   948 2.516117e-03
##                           2280400204    29 7.696983e-05
##                           2280400205    11 2.919545e-05
##                           2280400207    14 3.715785e-05
##                           2280400208    16 4.246611e-05
##                           22804002XX   132 3.503454e-04
##                           2280400501    60 1.592479e-04
##                           2280400508     9 2.388719e-05
##                           2280403201     3 7.962396e-06
##                           2280403702    15 3.981198e-05
##                           2280700901     7 1.857892e-05
##                           2280700903   148 3.928115e-04
##                           22807XXXXX   204 5.414429e-04
##                           2281200301    12 3.184959e-05
##                           2281200302    16 4.246611e-05
##                           2281201801     3 7.962396e-06
##                           2281201806    13 3.450372e-05
##                           2281201810   229 6.077962e-04
##                        22812XXXXX046    63 1.672103e-04
##                           2282300303   593 1.573900e-03
##                           22823006XX    15 3.981198e-05
##                           22823XXXXX    15 3.981198e-05
##                           2282802801    45 1.194359e-04
##                           2282802806    15 3.981198e-05
##                           2282900601    75 1.990599e-04
##                           2282900603    59 1.565938e-04
##                           2282907201    19 5.042851e-05
##                           2282907301    86 2.282554e-04
##                           2282907302     7 1.857892e-05
##                           2282907303    28 7.431570e-05
##                           228XXXXXXX  3315 8.798448e-03
##                           2290100101   137 3.636161e-04
##                           2290100106     3 7.962396e-06
##                           2290100108  1298 3.445063e-03
##                           2290100113    63 1.672103e-04
##                           2290100115    63 1.672103e-04
##                           2290100116   157 4.166987e-04
##                           22901001XX  1963 5.210061e-03
##                           2290100201   106 2.813380e-04
##                           2290100202    54 1.433231e-04
##                           2290100203    88 2.335636e-04
##                           2290100205    63 1.672103e-04
##                           2290100206    63 1.672103e-04
##                           2290100207    55 1.459773e-04
##                           2290100208    63 1.672103e-04
##                           2290100802    50 1.327066e-04
##                           2290100804   304 8.068562e-04
##                           2290100805    49 1.300525e-04
##                           2290100806    41 1.088194e-04
##                           22901008XX   767 2.035719e-03
##                           2290119701     7 1.857892e-05
##                           22901XXXXX    96 2.547967e-04
##                           2291500104    24 6.369917e-05
##                           2291500501   177 4.697814e-04
##                           2291504101    32 8.493223e-05
##                           2291504102     4 1.061653e-05
##                           22915XXXXX   277 7.351946e-04
##                           2294200502    55 1.459773e-04
##                           2294200503     9 2.388719e-05
##                           2294200504    23 6.104504e-05
##                           22942005XX    19 5.042851e-05
##                           2294200602  1364 3.620236e-03
##                           2294200701   153 4.060822e-04
##                           2294200718  1087 2.885042e-03
##                           2294200901     1 2.654132e-06
##                           2294900103    13 3.450372e-05
##                           22959001XX    14 3.715785e-05
##                           229XXXXXXX    74 1.964058e-04
##                           2301900101    26 6.900743e-05
##                           2301900102    32 8.493223e-05
##                           2301900206    10 2.654132e-05
##                           2301900301    34 9.024049e-05
##                           23019XXXXX    99 2.627591e-04
##                           2302001801   168 4.458942e-04
##                           2302001802    17 4.512025e-05
##                           2302001803    17 4.512025e-05
##                           23020018XX   191 5.069392e-04
##                           2302007001   139 3.689244e-04
##                           2302007002    16 4.246611e-05
##                           2302007005    17 4.512025e-05
##                           23020070XX     3 7.962396e-06
##                           2302012301    76 2.017140e-04
##                           2302012302     8 2.123306e-05
##                           2302012303    21 5.573677e-05
##                           2302012304    11 2.919545e-05
##                           2302012306     2 5.308264e-06
##                           23020123XX     3 7.962396e-06
##                           23020XXXXX    61 1.619021e-04
##                           2310300302     6 1.592479e-05
##                           2310901003   109 2.893004e-04
##                           2310901004   189 5.016310e-04
##                           2310901006   673 1.786231e-03
##                           2310901007    39 1.035112e-04
##                           2310901008    59 1.565938e-04
##                           2310901010    19 5.042851e-05
##                           2311000201     4 1.061653e-05
##                           2311001001    19 5.042851e-05
##                           2311005001   213 5.653301e-04
##                           23111003XX    10 2.654132e-05
##                           2311100401   658 1.746419e-03
##                           2311100404   132 3.503454e-04
##                           23111004XX   161 4.273153e-04
##                           2311101202   255 6.768037e-04
##                           2311101205    53 1.406690e-04
##                           2311109001   221 5.865632e-04
##                           2311109002   118 3.131876e-04
##                           2311114001   526 1.396073e-03
##                           2311119501    44 1.167818e-04
##                           2312100102    15 3.981198e-05
##                           2312100501   466 1.236826e-03
##                           2312114501    95 2.521425e-04
##                           2312114503    18 4.777438e-05
##                           23121145XX   177 4.697814e-04
##                           2312300101    17 4.512025e-05
##                           2312400101     3 7.962396e-06
##                           2314300102   112 2.972628e-04
##                           2314300109    29 7.696983e-05
##                           2314300112    41 1.088194e-04
##                           2314300113    34 9.024049e-05
##                           2314300114    15 3.981198e-05
##                           23143001XX    57 1.512855e-04
##                           2314308802     9 2.388719e-05
##                           231XXXXXXX  2982 7.914622e-03
##                        299XXXXXXX013  2614 6.937901e-03
##                           3070100101   107 2.839921e-04
##                           30701001XX   341 9.050590e-04
##                           30702002XX    90 2.388719e-04
##                           30702018XX    72 1.910975e-04
##                           3070202301    85 2.256012e-04
##                           3070300109    63 1.672103e-04
##                           3070300111    62 1.645562e-04
##                           3070300113   115 3.052252e-04
##                           3070300114    30 7.962396e-05
##                           30703001XX   405 1.074923e-03
##                           3070400603    18 4.777438e-05
##                           3070500202   112 2.972628e-04
##                           30706002XX   930 2.468343e-03
##                           3070800101   331 8.785177e-04
##                           3070800603     9 2.388719e-05
##                           30709003XX    89 2.362178e-04
##                           3072300201     7 1.857892e-05
##                           3074200401     3 7.962396e-06
##                           30742004XX    20 5.308264e-05
##                           3074200701    59 1.565938e-04
##                           307XXXXXXX   513 1.361570e-03
##                           3160400103     2 5.308264e-06
##                           3160400106     5 1.327066e-05
##                           31604001XX   159 4.220070e-04
##                           3160400508    57 1.512855e-04
##                           3160407101   246 6.529165e-04
##                           3160407116    19 5.042851e-05
##                           31604071XX    92 2.441802e-04
##                           3160700203    61 1.619021e-04
##                           3160700205   543 1.441194e-03
##                           3160700220    63 1.672103e-04
##                           3160700801   373 9.899913e-04
##                           3160700802   169 4.485483e-04
##                           3160700803   249 6.608789e-04
##                           3160700811    36 9.554876e-05
##                           31607008XX   422 1.120044e-03
##                           3160701102    14 3.715785e-05
##                           3160800105   247 6.555706e-04
##                           3160800309   491 1.303179e-03
##                           3160800311    67 1.778268e-04
##                           3160800313    49 1.300525e-04
##                           3160801404   185 4.910144e-04
##                           3160803001    34 9.024049e-05
##                           3160803002   111 2.946087e-04
##                           3160803003    89 2.362178e-04
##                           3160803004    29 7.696983e-05
##                           3160803603   116 3.078793e-04
##                           3160806601    44 1.167818e-04
##                           3160806607   184 4.883603e-04
##                           3160806701    19 5.042851e-05
##                           3160806702    76 2.017140e-04
##                           31608XXXXX   599 1.589825e-03
##                           3160904501   119 3.158417e-04
##                           3161000101    63 1.672103e-04
##                           3161000103    77 2.043682e-04
##                           3161000105   413 1.096157e-03
##                           3161000108   123 3.264582e-04
##                           3161000112   347 9.209838e-04
##                           3161000117    69 1.831351e-04
##                           3161002601    33 8.758636e-05
##                           31610028XX    61 1.619021e-04
##                           3161003201    52 1.380149e-04
##                           3161003202   122 3.238041e-04
##                           3161003801   144 3.821950e-04
##                           31610XXXXX   287 7.617359e-04
##                           3161100105   280 7.431570e-04
##                           3161100301   132 3.503454e-04
##                           3161100303     8 2.123306e-05
##                           3161100601    33 8.758636e-05
##                           3161100704    18 4.777438e-05
##                           3161101701   157 4.166987e-04
##                           31611017XX   100 2.654132e-04
##                           3161102001   272 7.219239e-04
##                           3161102002   163 4.326235e-04
##                           31611020XX    17 4.512025e-05
##                           3161102104     7 1.857892e-05
##                           3161102401    13 3.450372e-05
##                           3161102502    17 4.512025e-05
##                           3161102701     2 5.308264e-06
##                           3161103702    79 2.096764e-04
##                           31611041XX   130 3.450372e-04
##                           3161105502    12 3.184959e-05
##                           3161105503    63 1.672103e-04
##                           3161107501   130 3.450372e-04
##                           31611XXXXX   244 6.476082e-04
##                           3161200102    99 2.627591e-04
##                           31612005XX    13 3.450372e-05
##                           3161202001    88 2.335636e-04
##                           3161202002    69 1.831351e-04
##                           3161202005    43 1.141277e-04
##                           3161202006     3 7.962396e-06
##                           31612020XX    11 2.919545e-05
##                           31612040XX    19 5.042851e-05
##                           3161300102    40 1.061653e-04
##                           31615002XX   142 3.768868e-04
##                           31616003XX   142 3.768868e-04
##                           3161600502    49 1.300525e-04
##                           3161600503     8 2.123306e-05
##                           3161600505     5 1.327066e-05
##                           3161600701    44 1.167818e-04
##                           31616XXXXX    31 8.227809e-05
##                           3161700601   142 3.768868e-04
##                           3161808901    57 1.512855e-04
##                           3162300203   395 1.048382e-03
##                           3162300402    15 3.981198e-05
##                           3162301004     5 1.327066e-05
##                           31623XXXXX    51 1.353607e-04
##                           3162400201    67 1.778268e-04
##                           3162403901    78 2.070223e-04
##                           3163900103    19 5.042851e-05
##                           3164000501    10 2.654132e-05
##                           31642002XX     4 1.061653e-05
##                           316XXXXXXX  1153 3.060214e-03
##                           3210200202   699 1.855238e-03
##                           3210200229   200 5.308264e-04
##                        32102XXXXX026  2605 6.914014e-03
##                           3210400102   281 7.458111e-04
##                           3210400103    28 7.431570e-05
##                           3210400105   165 4.379318e-04
##                           3210400109    53 1.406690e-04
##                           3210400111     3 7.962396e-06
##                           3210400112    72 1.910975e-04
##                           3210400113    14 3.715785e-05
##                           32104001XX  1424 3.779484e-03
##                           3210400702    34 9.024049e-05
##                           3210500301    40 1.061653e-04
##                           3210501001   460 1.220901e-03
##                           3210501002   101 2.680673e-04
##                           3210501003   413 1.096157e-03
##                           3210502301   215 5.706384e-04
##                           3210505801   165 4.379318e-04
##                           3210505802     1 2.654132e-06
##                           3210505803   186 4.936686e-04
##                           3210505901   112 2.972628e-04
##                           3210506001    67 1.778268e-04
##                        32105XXXXX036  3072 8.153494e-03
##                           3210603301    22 5.839091e-05
##                           3210603305     3 7.962396e-06
##                           32109001XX     1 2.654132e-06
##                           3210900507   611 1.621675e-03
##                           3210900519     8 2.123306e-05
##                           3210902401    23 6.104504e-05
##                           3210902402     1 2.654132e-06
##                           32109024XX    86 2.282554e-04
##                           32109XXXXX  2935 7.789878e-03
##                           3211400102     9 2.388719e-05
##                           32114XXXXX     2 5.308264e-06
##                           321XXXXXXX   421 1.117390e-03
##                        399XXXXXXX016  3516 9.331928e-03
##                           6180200101     2 5.308264e-06
##                           61841007XX   433 1.149239e-03
##                           649XXXXXXX   114 3.025711e-04
##                           6560100102    80 2.123306e-04
##                           689XXXXXXX   269 7.139615e-04
##                           6910500101    18 4.777438e-05
##                           691XXXXXXX   137 3.636161e-04
##                           69302004XX   604 1.603096e-03
##                           6930400701   104 2.760297e-04
##                           6930401401    64 1.698645e-04
##                           6930401701    63 1.672103e-04
##                           693XXXXXXX     4 1.061653e-05
##                           6940100302    11 2.919545e-05
##                           6940100303    12 3.184959e-05
##                           6940100305    12 3.184959e-05
##                           6941400201    12 3.184959e-05
##                           6941400401   126 3.344206e-04
##                           694XXXXXXX   904 2.399335e-03
##                           699XXXXXXX   487 1.292562e-03
```

6. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy%>%
  filter(year==2000)%>%
  slice_max(catch)
```

```
## # A tibble: 1 × 10
##   country common_n…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##   <fct>   <chr>      <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
## 1 China   Marine fi… 39      Marine… 199XXX… Osteic… 61      Quanti…  2000  9068
## # … with abbreviated variable names ¹​common_name, ²​isscaap_group_number,
## #   ³​isscaap_taxonomic_group, ⁴​asfis_species_number, ⁵​asfis_species_name,
## #   ⁶​fao_major_fishing_area
```

```r
#China had the biggest catch of 2000 with a catch of 9068
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

```r
fisheries_tidy%>%
  filter(between(year,1990,2000))%>%
  filter(asfis_species_name=="Sardina pilchardus")%>%
  slice_max(catch)
```

```
## # A tibble: 1 × 10
##   country common_n…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##   <fct>   <chr>      <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
## 1 Morocco European … 35      Herrin… 121050… Sardin… 34      Quanti…  1994   947
## # … with abbreviated variable names ¹​common_name, ²​isscaap_group_number,
## #   ³​isscaap_taxonomic_group, ⁴​asfis_species_number, ⁵​asfis_species_name,
## #   ⁶​fao_major_fishing_area
```

```r
#Morocco with a catch of 947 in 1994
```

8. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy%>%
  filter(between(year,2008,2012))%>%
  filter(asfis_species_name=="Cephalopoda")%>%
  slice_max(catch, n=12)
```

```
## # A tibble: 12 × 10
##    country common_…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##    <fct>   <chr>     <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
##  1 India   Cephalop… 57      Squids… 321XXX… Cephal… 51      Quanti…  2011    94
##  2 India   Cephalop… 57      Squids… 321XXX… Cephal… 57      Quanti…  2010    93
##  3 India   Cephalop… 57      Squids… 321XXX… Cephal… 57      Quanti…  2012    88
##  4 China   Cephalop… 57      Squids… 321XXX… Cephal… 61      Quanti…  2008    86
##  5 China   Cephalop… 57      Squids… 321XXX… Cephal… 61      Quanti…  2010    74
##  6 Italy   Cephalop… 57      Squids… 321XXX… Cephal… 34      Quanti…  2012    66
##  7 India   Cephalop… 57      Squids… 321XXX… Cephal… 51      Quanti…  2009    62
##  8 India   Cephalop… 57      Squids… 321XXX… Cephal… 57      Quanti…  2009    61
##  9 India   Cephalop… 57      Squids… 321XXX… Cephal… 51      Quanti…  2010    60
## 10 Spain   Cephalop… 57      Squids… 321XXX… Cephal… 34      Quanti…  2008    57
## 11 India   Cephalop… 57      Squids… 321XXX… Cephal… 51      Quanti…  2012    56
## 12 Algeria Cephalop… 57      Squids… 321XXX… Cephal… 37      Quanti…  2011    54
## # … with abbreviated variable names ¹​common_name, ²​isscaap_group_number,
## #   ³​isscaap_taxonomic_group, ⁴​asfis_species_number, ⁵​asfis_species_name,
## #   ⁶​fao_major_fishing_area
```

```r
#India, China, Italy, Spain, and Algeria were the 5 countries that had the biggest catches of cephalopods (India had the top 3 spots, China had the top 4 and 5 spots)
```


```r
tabyl(fisheries_tidy$common_name)
```

```
##      fisheries_tidy$common_name     n      percent
##        [Aplodactylus punctatus]     9 2.388719e-05
##          [Calanus finmarchicus]     3 7.962396e-06
##       [Chionobathyscus dewitti]    15 3.981198e-05
##           [Chionodraco hamatus]     5 1.327066e-05
##                  [Haemulon spp]    12 3.184959e-05
##                 [Notolepis spp]     1 2.654132e-06
##         [Nototheniops nybelini]     1 2.654132e-06
##            [Odontesthes smitti]     3 7.962396e-06
##   [Parachaenichthys georgianus]     8 2.123306e-05
##                [Paralabrax spp]     8 2.123306e-05
##                 [Paralomis spp]     3 7.962396e-06
##                     [Raja taaf]     7 1.857892e-05
##                    Abalones nei   405 1.074923e-03
##                 Acoupa weakfish    11 2.919545e-05
##                    Aesop shrimp    11 2.919545e-05
##        African forktail snapper     9 2.388719e-05
##                African moonfish   251 6.661872e-04
##              African sicklefish   535 1.419961e-03
##           African striped grunt     2 5.308264e-06
##             Akiami paste shrimp   148 3.928115e-04
##                   Alaska plaice    32 8.493223e-05
##  Alaska pollock(=Walleye poll.)   469 1.244788e-03
##                        Albacore  4441 1.178700e-02
##                         Alewife   243 6.449541e-04
##              Alexandria pompano    43 1.141277e-04
##                       Alfonsino    32 8.493223e-05
##                  Alfonsinos nei   450 1.194359e-03
##                      Allis shad    34 9.024049e-05
##                  Amberjacks nei   830 2.202930e-03
##   Amer. plaice(=Long rough dab)   766 2.033065e-03
##                 American angler   263 6.980367e-04
##                 American conger    60 1.592479e-04
##          American cupped oyster   249 6.608789e-04
##           American gizzard shad     8 2.123306e-05
##            American harvestfish   127 3.370748e-04
##                American lobster   153 4.060822e-04
##            American sea scallop   185 4.910144e-04
##                   American shad   270 7.166157e-04
##          American yellow cockle     5 1.327066e-05
##               Anadara clams nei    92 2.441802e-04
##    Anchoveta(=Peruvian anchovy)   137 3.636161e-04
##             Anchovies, etc. nei   571 1.515509e-03
##                 Andaman lobster     9 2.388719e-05
##                 Angelfishes nei    23 6.104504e-05
##                      Angelshark    61 1.619021e-04
##    Angelsharks, sand devils nei   138 3.662702e-04
##                   Angler(=Monk)   567 1.504893e-03
##                Anglerfishes nei    54 1.433231e-04
##                  Angolan dentex    59 1.565938e-04
##              Angular roughshark    14 3.715785e-05
##                 Angulate volute    59 1.565938e-04
##                Annular seabream    33 8.758636e-05
##      Antarctic armless flounder     8 2.123306e-05
##          Antarctic flying squid     1 2.654132e-06
##             Antarctic horsefish     2 5.308264e-06
##             Antarctic octopuses     1 2.654132e-06
##  Antarctic rockcods, noties nei   155 4.113905e-04
##            Antarctic silverfish    29 7.696983e-05
##          Antarctic starry skate    48 1.273983e-04
##            Antarctic stone crab    21 5.573677e-05
##             Antarctic toothfish   151 4.007739e-04
##       Aquatic invertebrates nei   487 1.292562e-03
##            Arabian whip lobster     7 1.857892e-05
##              Araucanian herring    71 1.884434e-04
##                     Arctic char    70 1.857892e-04
##                    Arctic skate     9 2.388719e-05
##                Areolate grouper    13 3.450372e-05
##                       Argentine    19 5.042851e-05
##               Argentine anchovy   120 3.184959e-04
##            Argentine angelshark    41 1.088194e-04
##                Argentine conger   138 3.662702e-04
##               Argentine croaker   130 3.450372e-04
##              Argentine goatfish    21 5.573677e-05
##                  Argentine hake   448 1.189051e-03
##              Argentine menhaden    37 9.820289e-05
##            Argentine red shrimp    75 1.990599e-04
##               Argentine seabass    89 2.362178e-04
##        Argentine shortfin squid   413 1.096157e-03
##       Argentine stiletto shrimp    65 1.725186e-04
##                      Argentines   554 1.470389e-03
##           Argentinian sandperch    77 2.043682e-04
##            Aristeid shrimps nei    19 5.042851e-05
##            Aristeus shrimps nei     1 2.654132e-06
##                   Ark clams nei   159 4.220070e-04
##               Arrowhead dogfish     5 1.327066e-05
##             Arrowtooth flounder   131 3.476913e-04
##                             Asp    24 6.369917e-05
##                   Atka mackerel    85 2.256012e-04
##  Atl.jackknife(=Atl.razor clam)    49 1.300525e-04
##              Atlantic anchoveta    49 1.300525e-04
##            Atlantic bay scallop   111 2.946087e-04
##           Atlantic bluefin tuna  2057 5.459550e-03
##                 Atlantic bonito  1923 5.103896e-03
##                 Atlantic bumper   306 8.121644e-04
##             Atlantic butterfish    94 2.494884e-04
##                    Atlantic cod  2027 5.379926e-03
##                Atlantic croaker   126 3.344206e-04
##                Atlantic emperor    27 7.166157e-05
##     Atlantic goldeneye tilefish    12 3.184959e-05
##                Atlantic halibut  1324 3.514071e-03
##                Atlantic herring  1395 3.702514e-03
##         Atlantic horse mackerel   990 2.627591e-03
##             Atlantic lizardfish     4 1.061653e-05
##               Atlantic mackerel  1749 4.642077e-03
##               Atlantic menhaden   137 3.636161e-04
##               Atlantic moonfish   106 2.813380e-04
##             Atlantic needlefish     7 1.857892e-05
##                Atlantic pomfret   484 1.284600e-03
##            Atlantic puffers nei    31 8.227809e-05
##          Atlantic redfishes nei  1417 3.760905e-03
##              Atlantic rock crab   109 2.893004e-04
##               Atlantic sailfish  1323 3.511417e-03
##                 Atlantic salmon   958 2.542659e-03
##                  Atlantic saury   111 2.946087e-04
##                 Atlantic seabob   170 4.512025e-04
##              Atlantic searobins   160 4.246611e-04
##        Atlantic sharpnose shark    16 4.246611e-05
##             Atlantic silverside   101 2.680673e-04
##       Atlantic Spanish mackerel   185 4.910144e-04
##              Atlantic surf clam    88 2.335636e-04
##         Atlantic thread herring   274 7.272322e-04
##                 Atlantic tomcod    63 1.672103e-04
##           Atlantic weasel shark     3 7.962396e-06
##           Atlantic white marlin  1216 3.227425e-03
##               Atlantic wolffish   569 1.510201e-03
##               Australian mussel    69 1.831351e-04
##             Australian pilchard    22 5.839091e-05
##               Australian salmon   176 4.671272e-04
##        Australian spiny lobster    63 1.672103e-04
##               Axillary seabream   257 6.821119e-04
##               Baird's slickhead    51 1.353607e-04
##                  Balao halfbeak     9 2.388719e-05
##                 Bali sardinella   126 3.344206e-04
##                   Ballan wrasse    28 7.431570e-05
##               Ballyhoo halfbeak    98 2.601049e-04
##                    Baltic prawn     3 7.962396e-06
##                    Banana prawn   309 8.201268e-04
##             Banded carpet shell     8 2.123306e-05
##               Banded rudderfish     1 2.654132e-06
##               Banded yellowfish    19 5.042851e-05
##                        Bar jack    33 8.758636e-05
##             Barbeled houndshark     3 7.962396e-06
##                        Barnacle    37 9.820289e-05
##                  Barracudas nei  2675 7.099803e-03
##     Barramundi(=Giant seaperch)   471 1.250096e-03
##                    Barred grunt    71 1.884434e-04
##                      Barrelfish     4 1.061653e-05
##                Bartail flathead    65 1.725186e-04
##                   Basket cockle    15 3.981198e-05
##                  Basketwork eel    12 3.184959e-05
##                   Basking shark   119 3.158417e-04
##                   Bastard grunt    35 9.289462e-05
##                 Bastard halibut   128 3.397289e-04
##            Bastard halibuts nei   200 5.308264e-04
##                       Batfishes    62 1.645562e-04
##              Bathyraja rays nei     8 2.123306e-05
##              Batwing coral crab     4 1.061653e-05
##                  Beaked redfish   225 5.971797e-04
##                      Bean solen    10 2.654132e-05
##                 Bearded brotula   134 3.556537e-04
##                          Beluga    13 3.450372e-05
##                   Benguela hake   111 2.946087e-04
##                  Bigeye croaker    16 4.246611e-05
##                Bigeye grenadier     9 2.388719e-05
##                    Bigeye grunt   493 1.308487e-03
##                     Bigeye scad   281 7.458111e-04
##                 Bigeye thresher    71 1.884434e-04
##                 Bigeye trevally    13 3.450372e-05
##                     Bigeye tuna  5341 1.417572e-02
##                     Bigeyes nei   375 9.952995e-04
##               Bigfin reef squid    34 9.024049e-05
##                    Biglip grunt     1 2.654132e-06
##                Bignose fanskate     4 1.061653e-05
##             Bigscale sand smelt    76 2.017140e-04
##              Bigspined boarfish    11 2.919545e-05
##                Bigtooth corvina    11 2.919545e-05
##                Birdbeak dogfish    51 1.353607e-04
##     Black and Caspian Sea sprat   136 3.609620e-04
##             Black cardinal fish    98 2.601049e-04
##                   Black cuskeel    32 8.493223e-05
##                   Black dogfish    25 6.635330e-05
##                 Black driftfish    13 3.450372e-05
##                      Black drum   329 8.732095e-04
##                   Black grouper    13 3.450372e-05
##                    Black marlin  1431 3.798063e-03
##             Black musselcracker    21 5.573677e-05
##                      Black oreo    15 3.981198e-05
##                   Black pomfret   439 1.165164e-03
##                   Black rockcod     2 5.308264e-06
##                  Black rockfish    13 3.450372e-05
##              Black scabbardfish   194 5.149016e-04
##              Black scorpionfish     2 5.308264e-06
##                   Black seabass   126 3.344206e-04
##                  Black seabream   624 1.656178e-03
##                  Black skipjack   245 6.502624e-04
##                Black stone crab   213 5.653301e-04
##                  Black teatfish    12 3.184959e-05
##            Blackbanded trevally    38 1.008570e-04
##             Blackbellied angler    19 5.042851e-05
##             Blackbelly rosefish   328 8.705553e-04
##            Blackchin guitarfish     3 7.962396e-06
##              Blackfin goosefish    21 5.573677e-05
##                Blackfin icefish    74 1.964058e-04
##                Blackfin snapper     9 2.388719e-05
##                   Blackfin tuna   577 1.531434e-03
##              Blackhead seabream    24 6.369917e-05
##                Blacklip abalone   115 3.052252e-04
##             Blackmouth catshark    60 1.592479e-04
##              Blackmouth croaker    63 1.672103e-04
##             Blackmouth splitfin    10 2.654132e-05
##                 Blacknose shark     1 2.654132e-06
##        Blackspot(=red) seabream   296 7.856231e-04
##          Blackspotted rubberlip    13 3.450372e-05
##     Blackstreaked monocle bream    13 3.450372e-05
##                Blacktail comber     2 5.308264e-06
##                Blacktip grouper    14 3.715785e-05
##                  Blacktip shark    55 1.459773e-04
##            Bloch's gizzard shad    13 3.450372e-05
##                      Blonde ray    42 1.114735e-04
##                       Blood ark    19 5.042851e-05
##                    Blood cockle   246 6.529165e-04
##                Blotched picarel    55 1.459773e-04
##             Blue and red shrimp   130 3.450372e-04
##                   Blue antimora   207 5.494053e-04
##                 Blue butterfish   237 6.290293e-04
##                       Blue crab   255 6.768037e-04
##                  Blue grenadier   224 5.945256e-04
##              Blue jack mackerel    17 4.512025e-05
##                  Blue king crab    17 4.512025e-05
##                       Blue ling   451 1.197014e-03
##                   Blue mackerel   108 2.866463e-04
##                     Blue marlin  3212 8.525072e-03
##                 Blue mud shrimp    13 3.450372e-05
##                     Blue mussel   413 1.096157e-03
##                     Blue runner   139 3.689244e-04
##                      Blue shark   827 2.194967e-03
##                     Blue shrimp    27 7.166157e-05
##                      Blue skate    88 2.335636e-04
##              Blue squat lobster    34 9.024049e-05
##              Blue swimming crab   658 1.746419e-03
##        Blue whiting(=Poutassou)   915 2.428531e-03
##                   Blueback shad    11 2.919545e-05
##           Bluebarred parrotfish    13 3.450372e-05
##                 Bluefin gurnard   324 8.599388e-04
##                Bluefin trevally    13 3.450372e-05
##                        Bluefish  1450 3.848492e-03
##                Bluenose warehou    52 1.380149e-04
##           Bluespine unicornfish    13 3.450372e-05
##                 Bluespot mullet    47 1.247442e-04
##          Bluespotted cornetfish     2 5.308264e-06
##            Bluespotted seabream     1 2.654132e-06
##              Bluestripe herring    42 1.114735e-04
##                 Blunt scalyhead     4 1.061653e-05
##         Bluntnose sixgill shark    45 1.194359e-04
##                        Boarfish    29 7.696983e-05
##                  Boarfishes nei     9 2.388719e-05
##                    Bobo croaker   265 7.033450e-04
##                     Bobo mullet    93 2.468343e-04
##               Bocaccio rockfish    32 8.493223e-05
##                  Bocon toadfish    11 2.919545e-05
##                        Boe drum   117 3.105335e-04
##                           Bogue  1105 2.932816e-03
##                      Bombayduck   320 8.493223e-04
##                        Bonefish   154 4.087363e-04
##                      Bonga shad   617 1.637599e-03
##                      Bonnethead     1 2.654132e-06
##    Bonnetmouths, rubyfishes nei    41 1.088194e-04
##                   Boxfishes nei    48 1.273983e-04
##                   Bramble shark     9 2.388719e-05
##               Brazilian codling   140 3.715785e-04
##              Brazilian flathead    89 2.362178e-04
##          Brazilian groupers nei    71 1.884434e-04
##              Brazilian menhaden   124 3.291124e-04
##             Brazilian sandperch     6 1.592479e-05
##            Brazilian sardinella    85 2.256012e-04
##                           Brill   637 1.690682e-03
##                    Brine shrimp    25 6.635330e-05
##             Broadgilled hagfish    10 2.654132e-05
##       Broadnose sevengill shark    26 6.900743e-05
##                 Broadnose skate     4 1.061653e-05
##            Broadstriped anchovy     9 2.388719e-05
##        Broadtail shortfin squid   101 2.680673e-04
##               Broomtail grouper    22 5.839091e-05
##                 Brown king crab    17 4.512025e-05
##                    Brown meagre   100 2.654132e-04
##                       Brown ray     1 2.654132e-06
##               Brown smoothhound    18 4.777438e-05
##                    Brown wrasse     2 5.308264e-06
##            Brownmarbled grouper    13 3.450372e-05
##            Brownspotted grouper    13 3.450372e-05
##         Brownstripe red snapper     2 5.308264e-06
##           Brushtooth lizardfish   127 3.370748e-04
##               Buccaneer anchovy    10 2.654132e-05
##                      Bull shark    13 3.450372e-05
##                     Bullet tuna     8 2.123306e-05
##                     Butter clam    79 2.096764e-04
##      Butterfishes, pomfrets nei   796 2.112689e-03
##              Butterfly kingfish    12 3.184959e-05
##                         Cabezon    30 7.962396e-05
##                   Cabinza grunt   126 3.344206e-04
##                  Calico scallop    34 9.024049e-05
##        California butterfly ray     3 7.962396e-06
##             California flounder    27 7.166157e-05
##             California pilchard   142 3.768868e-04
##            California sheephead    15 3.981198e-05
##             Californian anchovy   163 4.326235e-04
##              Camouflage grouper     3 7.962396e-06
##          Canary drum(=Baardman)   108 2.866463e-04
##                 Canary rockfish    32 8.493223e-05
##            Cannonball jellyfish     2 5.308264e-06
##                Cape bonnetmouth    61 1.619021e-04
##               Cape elephantfish    37 9.820289e-05
##                    Cape fathead     3 7.962396e-06
##                    Cape gurnard    73 1.937516e-04
##                      Cape hakes   448 1.189051e-03
##                 Cape Hope squid    72 1.910975e-04
##             Cape horse mackerel   364 9.661041e-04
##               Cape rock lobster   106 2.813380e-04
##                         Capelin   593 1.573900e-03
##                      Capro dory     3 7.962396e-06
##                  Caramote prawn   305 8.095103e-04
##                   Carangids nei  2343 6.218631e-03
##             Cardinal fishes nei    43 1.141277e-04
##        Cardinalfishes, etc. nei    61 1.619021e-04
##         Caribbean spiny lobster  1298 3.445063e-03
##              Carpenter seabream    61 1.619021e-04
##               Carpet shells nei    17 4.512025e-05
##            Carrot squat lobster    32 8.493223e-05
##                 Cassava croaker   115 3.052252e-04
##                       Castaneta    87 2.309095e-04
##             Catsharks, etc. nei    20 5.308264e-05
##      Catsharks, nursehounds nei   103 2.733756e-04
##                 Cephalopods nei   421 1.117390e-03
##                            Cero   133 3.529996e-04
##             Chaceon geryons nei    57 1.512855e-04
##           Chacunda gizzard shad   181 4.803979e-04
##             Channel bull blenny    16 4.246611e-05
##                       Chars nei    61 1.619021e-04
##             Charybdis crabs nei    10 2.654132e-05
##             Chilean flat oyster    61 1.619021e-04
##               Chilean grenadier     9 2.388719e-05
##           Chilean jack mackerel   311 8.254351e-04
##            Chilean knife shrimp    28 7.431570e-05
##                  Chilean mussel    77 2.043682e-04
##            Chilean nylon shrimp    60 1.592479e-04
##               Chilean sandperch     9 2.388719e-05
##              Chilean sea urchin    63 1.672103e-04
##                  Chilean semele    19 5.042851e-05
##              Chilean silverside    63 1.672103e-04
##            Chilipepper rockfish    32 8.493223e-05
##             Chimaeras, etc. nei    30 7.962396e-05
##            Chinese gizzard shad    83 2.202930e-04
##    Chinook(=Spring=King) salmon   327 8.679012e-04
##                  Chocolate hind   126 3.344206e-04
##                     Choicy ruff    21 5.573677e-05
##                Chola guitarfish    57 1.512855e-04
##                   Cholga mussel   144 3.821950e-04
##                    Choro mussel    33 8.758636e-05
##                   Chub mackerel  3026 8.031404e-03
##          Chum(=Keta=Dog) salmon   257 6.821119e-04
##                   Citharids nei    26 6.900743e-05
##                 Clams, etc. nei  1153 3.060214e-03
##                   Clupeoids nei  1955 5.188828e-03
##                           Cobia   594 1.576554e-03
##                     Cockles nei    51 1.353607e-04
##            Coho(=Silver) salmon   305 8.095103e-04
##                          Comber    18 4.777438e-05
##                     Combers nei     1 2.654132e-06
##                   Comet grouper    13 3.450372e-05
##                  Commercial top    18 4.777438e-05
##       Common Atlantic grenadier     3 7.962396e-06
##       Common bluestripe snapper    13 3.450372e-05
##                     Common carp    76 2.017140e-04
##               Common cuttlefish   699 1.855238e-03
##                      Common dab   616 1.634945e-03
##                   Common dentex   636 1.688028e-03
##              Common dolphinfish  1653 4.387280e-03
##                Common eagle ray    54 1.433231e-04
##            Common edible cockle   395 1.048382e-03
##     Common European bittersweet    40 1.061653e-04
##                     Common goby     3 7.962396e-06
##               Common guitarfish     4 1.061653e-05
##                     Common mora    53 1.406690e-04
##                  Common octopus   611 1.621675e-03
##                  Common pandora   527 1.398728e-03
##               Common periwinkle   107 2.839921e-04
##                    Common prawn   229 6.077962e-04
##                   Common shrimp   593 1.573900e-03
##              Common silverbiddy    19 5.042851e-05
##                    Common snook   113 2.999169e-04
##                     Common sole  1473 3.909537e-03
##            Common spiny lobster   304 8.068562e-04
##               Common squids nei  1424 3.779484e-03
##                 Common stingray    21 5.573677e-05
##       Common twobanded seabream    20 5.308264e-05
##                  Common warehou    40 1.061653e-04
##                           Coney    27 7.166157e-05
##           Conger eels, etc. nei   476 1.263367e-03
##                    Congo dentex    27 7.166157e-05
##               Coonstripe shrimp    16 4.246611e-05
##                    Copper shark    30 7.962396e-05
##                      Coral hind    13 3.450372e-05
##                 Corkwing wrasse     8 2.123306e-05
##                      Cornetfish     7 1.857892e-05
##                    Corvina drum   126 3.344206e-04
##                     Cownose ray     5 1.327066e-05
##           Crangonid shrimps nei    15 3.981198e-05
##        Craylets, squat lobsters    99 2.627591e-04
##                   Creole wrasse     2 5.308264e-06
##              Crested bellowfish    11 2.919545e-05
##                   Crevalle jack   189 5.016310e-04
##                    Croakers nei   157 4.166987e-04
##             Croakers, drums nei  2440 6.476082e-03
##         Crocodile icefishes nei    79 2.096764e-04
##                 Crocodile shark     1 2.654132e-06
##                    Crucian carp    63 1.672103e-04
##                  Crystal shrimp   235 6.237210e-04
##                  Cubera snapper     8 2.123306e-05
##                      Cuckoo ray    67 1.778268e-04
##           Cunene horse mackerel   250 6.635330e-04
##                          Cunner    63 1.672103e-04
##              Cupped oysters nei   422 1.120044e-03
##                    Curlfin sole    13 3.450372e-05
##                    Cuskeels nei    66 1.751727e-04
##          Cuskeels, brotulas nei    45 1.194359e-04
##  Cuttlefish, bobtail squids nei  2605 6.914014e-03
##                   Cyprinids nei   194 5.149016e-04
##           Daggerhead breams nei    74 1.964058e-04
##         Daggertooth pike conger   414 1.098811e-03
##                   Dana swimcrab    53 1.406690e-04
##         Danube sturgeon(=Osetr)    22 5.839091e-05
##                Dark ghost shark    22 5.839091e-05
##                 Darkbelly skate     2 5.308264e-06
##           Darkblotched rockfish    12 3.184959e-05
##                        Dealfish    26 6.900743e-05
##                      Dealfishes    21 5.573677e-05
##                Deepsea red crab    29 7.696983e-05
##                   Deepsea smelt    69 1.831351e-04
##           Deepwater rose shrimp   611 1.621675e-03
##                Delicate scallop    19 5.042851e-05
##                     Delta prawn    13 3.450372e-05
##        Demersal percomorphs nei  1478 3.922807e-03
##                      Dentex nei   626 1.661487e-03
##                Devil anglerfish   147 3.901574e-04
##                      Devil fish     9 2.388719e-05
##        Diadromous clupeoids nei    97 2.574508e-04
##              Dogfish sharks nei   836 2.218854e-03
##        Dogfish sharks, etc. nei     2 5.308264e-06
##        Dogfishes and hounds nei   173 4.591649e-04
##                   Dogfishes nei    47 1.247442e-04
##              Dogtooth grenadier     5 1.327066e-05
##                Dogtooth grouper    13 3.450372e-05
##                   Dogtooth tuna    65 1.725186e-04
##                     Donax clams   142 3.768868e-04
##               Dorab wolfherring   193 5.122475e-04
##                      Dories nei    18 4.777438e-05
##             Dotted gizzard shad    18 4.777438e-05
##         Doublespotted queenfish    10 2.654132e-05
##                      Dover sole    32 8.493223e-05
##             Draughtsboard shark    12 3.184959e-05
##            Duckbill barracudina     1 2.654132e-06
##                  Dungat grouper    20 5.308264e-05
##                  Dungeness crab   189 5.016310e-04
##                  Dusky catshark     1 2.654132e-06
##                   Dusky grouper   415 1.101465e-03
##                     Dusky shark    19 5.042851e-05
##               Dusky smoothhound    16 4.246611e-05
##                  Eagle rays nei    60 1.592479e-04
##          Eastern Pacific bonito   258 6.847661e-04
##                   Eaton's skate    35 9.289462e-05
##                     Echinoderms   269 7.139615e-04
##                     Edible crab   673 1.786231e-03
##                         Eelpout   134 3.556537e-04
##                        Eelpouts    25 6.635330e-05
##               Eeltail catfishes   144 3.821950e-04
##           Electron subantarctic     3 7.962396e-06
##        Elephantfishes, etc. nei     1 2.654132e-06
##                 Elongate ilisha    82 2.176388e-04
##       Emperors(=Scavengers) nei   998 2.648824e-03
##                Endeavour shrimp    56 1.486314e-04
##                    English sole    30 7.962396e-05
##                         Escolar   135 3.583078e-04
##                        Eulachon   102 2.707215e-04
##                European anchovy  1656 4.395243e-03
##              European barracuda    35 9.289462e-05
##                 European conger   980 2.601049e-03
##      European edible sea urchin    64 1.698645e-04
##            European flat oyster   543 1.441194e-03
##               European flounder   802 2.128614e-03
##           European flying squid   165 4.379318e-04
##                   European hake  1780 4.724355e-03
##                European lobster  1087 2.885042e-03
##     European pilchard(=Sardine)  1655 4.392589e-03
##                 European plaice   892 2.367486e-03
##                European seabass   604 1.603096e-03
##                  European smelt   454 1.204976e-03
##                  European sprat  1299 3.447718e-03
##                  European squid    53 1.406690e-04
##              European whitefish   233 6.184128e-04
##                   Eyespot skate     4 1.061653e-05
##                  Falkland sprat    32 8.493223e-05
##                   False abalone    85 2.256012e-04
##                      False scad   101 2.680673e-04
##                  False trevally   296 7.856231e-04
##                  Filefishes nei    60 1.592479e-04
##  Filefishes, leatherjackets nei   129 3.423830e-04
##                 Finetooth shark     4 1.061653e-05
##                   Finfishes nei  1102 2.924854e-03
##               Fivelined snapper    13 3.450372e-05
##                 Flagfin mojarra     8 2.123306e-05
##                 Flat needlefish    28 7.431570e-05
##                  Flatfishes nei  3236 8.588771e-03
##            Flathead grey mullet   619 1.642908e-03
##                Flathead lobster   177 4.697814e-04
##                   Flathead sole   108 2.866463e-04
##                   Flatheads nei   220 5.839091e-04
##                    Fleshy prawn    86 2.282554e-04
##                 Florida pompano    82 2.176388e-04
##                  Flying gurnard    12 3.184959e-05
##                Flyingfishes nei   961 2.550621e-03
##                       Forkbeard    38 1.008570e-04
##                  Forkbeards nei   124 3.291124e-04
##              Fourbeard rockling     3 7.962396e-06
##            Fourfinger threadfin   138 3.662702e-04
##               Fourlined terapon     9 2.388719e-05
##               Fourspot flounder     6 1.592479e-05
##                 Fourspot megrim    17 4.512025e-05
##                Freshwater bream   389 1.032457e-03
##           Freshwater breams nei    67 1.778268e-04
##        Frigate and bullet tunas  2167 5.751504e-03
##                    Frigate tuna    97 2.574508e-04
##                     Frostfishes    15 3.981198e-05
##                   Fusiliers nei   349 9.262921e-04
##                  Gadiformes nei   931 2.470997e-03
##                             Gag    12 3.184959e-05
##                         Garfish   917 2.433839e-03
##                  Gastropods nei   513 1.361570e-03
##              Gay's little venus    13 3.450372e-05
##                     Gazami crab   132 3.503454e-04
##                 Geelbek croaker   104 2.760297e-04
##                     Ghost shark    81 2.149847e-04
##               Ghost shrimps nei    14 3.715785e-05
##                   Giant abalone    63 1.672103e-04
##         Giant African threadfin   202 5.361347e-04
##                  Giant barnacle    37 9.820289e-05
##                  Giant boarfish    18 4.777438e-05
##                   Giant catfish    36 9.554876e-05
##                Giant guitarfish    16 4.246611e-05
##                     Giant manta     2 5.308264e-06
##                Giant red shrimp    46 1.220901e-04
##                   Giant seabass    59 1.565938e-04
##                 Giant stargazer    45 1.194359e-04
##                Giant stone crab    19 5.042851e-05
##               Giant tiger prawn   453 1.202322e-03
##                  Giant trevally    60 1.592479e-04
##               Gilthead seabream   753 1.998561e-03
##                     Glassfishes    44 1.167818e-04
##               Globose king crab    11 2.919545e-05
##                      Goatfishes   706 1.873817e-03
##     Goatfishes, red mullets nei   565 1.499585e-03
##                      Gobies nei   602 1.597788e-03
##             Golden deepsea crab    15 3.981198e-05
##              Golden grey mullet    14 3.715785e-05
##                Golden king crab    17 4.512025e-05
##                  Golden redfish   172 4.565107e-04
##                   Golden shrimp     3 7.962396e-06
##          Golden threadfin bream    55 1.459773e-04
##                 Golden trevally    78 2.070223e-04
##                        Goldfish     6 1.592479e-05
##               Goldsilk seabream    22 5.839091e-05
##                 Goldsinnywrasse    10 2.654132e-05
##           Goldstripe sardinella   127 3.370748e-04
##               Gonate squids nei     2 5.308264e-06
##             Goose barnacles nei    17 4.512025e-05
##                  Greasy grouper    35 9.289462e-05
##          Great Atlantic scallop   491 1.303179e-03
##                 Great barracuda   139 3.689244e-04
##              Great lanternshark     1 2.654132e-06
##     Great Mediterranean scallop    67 1.778268e-04
##         Great Northern tilefish   122 3.238041e-04
##               Great white shark    27 7.166157e-05
##               Greater amberjack   397 1.053690e-03
##               Greater argentine    19 5.042851e-05
##               Greater forkbeard   444 1.178435e-03
##            Greater hooked squid    22 5.839091e-05
##              Greater lizardfish   304 8.068562e-04
##                  Greater weever   291 7.723524e-04
##                      Green crab   221 5.865632e-04
##       Green humphead parrotfish    13 3.450372e-05
##                   Green jobfish    11 2.919545e-05
##                    Green mussel   122 3.238041e-04
##              Green rock lobster    88 2.335636e-04
##             Green spiny lobster   157 4.166987e-04
##                  Green sturgeon    13 3.450372e-05
##               Green tiger prawn   208 5.520595e-04
##                  Green weakfish    11 2.919545e-05
##        Greenback horse mackerel    87 2.309095e-04
##                       Greeneyes     4 1.061653e-05
##                   Greenland cod    72 1.910975e-04
##               Greenland halibut  1147 3.044290e-03
##                 Greenland shark    92 2.441802e-04
##                   Grenadier cod    11 2.919545e-05
##                  Grenadiers nei   319 8.466681e-04
##        Grenadiers, rattails nei   107 2.839921e-04
##       Grenadiers, whiptails nei     1 2.654132e-06
##                    Grey gurnard   250 6.635330e-04
##                    Grey rockcod   124 3.291124e-04
##                    Grey snapper    27 7.166157e-05
##                   Grey tilefish    12 3.184959e-05
##                Grey triggerfish    91 2.415260e-04
##            Grooved carpet shell   272 7.219239e-04
##                Groundfishes nei   578 1.534088e-03
##                    Groupers nei  2430 6.449541e-03
##         Groupers, seabasses nei  1918 5.090625e-03
##           Grunts, sweetlips nei  2035 5.401159e-03
##                   Guinea shrimp    13 3.450372e-05
##         Guinean striped mojarra    10 2.654132e-05
##          Guitarfishes, etc. nei   158 4.193529e-04
##     Gulf butterfishes, etc. nei    52 1.380149e-04
##                Gulf kingcroaker   102 2.707215e-04
##                   Gulf menhaden    63 1.672103e-04
##                 Gulf parrotfish    16 4.246611e-05
##                    Gulper shark   115 3.052252e-04
##                     Gummy shark    32 8.493223e-05
##         Gurnards, searobins nei  1131 3.001823e-03
##                         Haddock  1451 3.851146e-03
##                Haffara seabream    26 6.900743e-05
##                   Hagfishes nei    54 1.433231e-04
##                       Hair crab    17 4.512025e-05
##   Hairtails, scabbardfishes nei   646 1.714569e-03
##                       Hakes nei   242 6.423000e-04
##                   Halfbeaks nei   774 2.054298e-03
##                Halfcrenated ark    57 1.512855e-04
##     Hammerhead sharks, etc. nei   236 6.263752e-04
##                Hapuku wreckfish    93 2.468343e-04
##              Harbour spidercrab    15 3.981198e-05
##                  Hard clams nei   100 2.654132e-04
##            Hector's lanternfish    32 8.493223e-05
##                      Helmet ton     7 1.857892e-05
##                    Hickory shad     8 2.123306e-05
##                      Hilsa shad   283 7.511194e-04
##                         Hogfish    22 5.839091e-05
##                   Hokkai shrimp    16 4.246611e-05
##               Honeycomb grouper    18 4.777438e-05
##                 Honnibe croaker    58 1.539397e-04
##      Horned and musky octopuses    86 2.282554e-04
##                  Horned octopus    23 6.104504e-05
##                   Horned turban   112 2.972628e-04
##               Horse mussels nei    61 1.619021e-04
##                  Horseshoe crab    80 2.123306e-04
##                Hound needlefish    19 5.042851e-05
##                Humpback grouper    18 4.777438e-05
##            Humpback red snapper    13 3.450372e-05
##                  Humped rockcod    75 1.990599e-04
##                 Humphead wrasse    18 4.777438e-05
##           Humpnose bigeye bream    13 3.450372e-05
##                    Humpy shrimp    14 3.715785e-05
##                 Iceland scallop   116 3.078793e-04
##              Imperial blackfish    11 2.919545e-05
##              Imperial surf clam    99 2.627591e-04
##                Indian driftfish    58 1.539397e-04
##                  Indian halibut   297 7.882772e-04
##                 Indian mackerel   688 1.826043e-03
##            Indian mackerels nei   419 1.112081e-03
##              Indian oil sardine   327 8.679012e-04
##                  Indian pellona   109 2.893004e-04
##                  Indian pompano    16 4.246611e-05
##                     Indian scad   247 6.555706e-04
##                    Indian squid     3 7.962396e-06
##                Indian threadfin     5 1.327066e-05
##              Indian white prawn    11 2.919545e-05
##       IndoPacific king mackerel   528 1.401382e-03
##            IndoPacific sailfish  1526 4.050206e-03
##          IndoPacific swamp crab   526 1.396073e-03
##              IndoPacific tarpon   111 2.946087e-04
##       Intermediate scabbardfish     1 2.654132e-06
##                   Irish mojarra    11 2.919545e-05
##    Jack and horse mackerels nei  1750 4.644731e-03
##                Jackknife shrimp     7 1.857892e-05
##            Jacks, crevalles nei  1730 4.591649e-03
##                Jamaica weakfish    11 2.919545e-05
##                Japanese anchovy   173 4.591649e-04
##           Japanese carpet shell   163 4.326235e-04
##            Japanese fan lobster    24 6.369917e-05
##           Japanese flying squid   186 4.936686e-04
##             Japanese flyingfish    57 1.512855e-04
##               Japanese halfbeak    56 1.486314e-04
##              Japanese hard clam   157 4.166987e-04
##          Japanese jack mackerel   173 4.591649e-04
##               Japanese pilchard   165 4.379318e-04
##               Japanese sandfish   121 3.211500e-04
##             Japanese sardinella    37 9.820289e-05
##                   Japanese scad    91 2.415260e-04
##           Japanese sea cucumber   126 3.344206e-04
##                Japanese seabass   126 3.344206e-04
##       Japanese Spanish mackerel   186 4.936686e-04
##        Japanese threadfin bream    16 4.246611e-05
##              Japanese topeshark     2 5.308264e-06
##                 Javelin grunter    16 4.246611e-05
##                 Jellyfishes nei   433 1.149239e-03
##                   Jobfishes nei    17 4.512025e-05
##                  John's snapper    16 4.246611e-05
##                       John dory  1149 3.049598e-03
##                 Jonah's icefish     2 5.308264e-06
##                      Jonah crab    39 1.035112e-04
##     Juan Fernandez rock lobster    54 1.433231e-04
##              Jumbo flying squid   215 5.706384e-04
##              Kamchatka flounder   141 3.742326e-04
##              Karanteen seabream    10 2.654132e-05
##                        Kawakawa  1276 3.386673e-03
##                  Kelp greenling     7 1.857892e-05
##       Kerguelen sandpaper skate    12 3.184959e-05
##                      King crabs   191 5.069392e-04
##                  King crabs nei     3 7.962396e-06
##     King crabs, stone crabs nei    61 1.619021e-04
##                       King dory    14 3.715785e-05
##                   King mackerel   442 1.173126e-03
##                King of herrings    13 3.450372e-05
##              King soldier bream    89 2.362178e-04
##                   King weakfish   107 2.839921e-04
##                Kingcroakers nei    68 1.804810e-04
##                        Kingklip   220 5.839091e-04
##                   Kitefin shark    56 1.486314e-04
##             Klunzinger's mullet    20 5.308264e-05
##                    Knife shrimp    86 2.282554e-04
##              Knifetooth dogfish    23 6.104504e-05
##                      Knout goby     5 1.327066e-05
##                  Kolibri shrimp    19 5.042851e-05
##                   Korean mussel    63 1.672103e-04
##                Korean sandlance    59 1.565938e-04
##                    Kuruma prawn   183 4.857062e-04
##                        Ladyfish   141 3.742326e-04
##                    Lampreys nei    23 6.104504e-05
##                    Lane snapper   180 4.777438e-04
##                    Lantern fish     1 2.654132e-06
##               Lanternfishes nei    71 1.884434e-04
##               Lanternsharks nei    29 7.696983e-05
##            Large yellow croaker   101 2.680673e-04
##                 Largeeye breams    89 2.362178e-04
##                 Largeeye dentex   477 1.266021e-03
##              Largehead hairtail  1748 4.639423e-03
##     Latchet(=Sharpbeak gurnard)    88 2.335636e-04
##                     Law croaker    61 1.619021e-04
##          Leafscale gulper shark    89 2.362178e-04
##                  Leaping mullet    49 1.300525e-04
##                Lebranche mullet   102 2.707215e-04
##                        Leerfish   542 1.438540e-03
##           Lefteye flounders nei   123 3.264582e-04
##                     Lemon shark     3 7.962396e-06
##                      Lemon sole   633 1.680066e-03
##            Leopard coralgrouper    18 4.777438e-05
##                Leopard flounder    34 9.024049e-05
##        Lesser African threadfin   481 1.276638e-03
##                Lesser amberjack     8 2.123306e-05
##                            Ling   803 2.131268e-03
##                         Lingcod   189 5.016310e-04
##                       Lings nei     8 2.123306e-05
##                    Little skate     5 1.327066e-05
##            Little sleeper shark    10 2.654132e-05
##  Little tunny(=Atl.black skipj)  1451 3.851146e-03
##                Live sharksucker     8 2.123306e-05
##                Lizardfishes nei   707 1.876471e-03
##                    Lobsters nei    74 1.964058e-04
##         Long snouted lancetfish     2 5.308264e-06
##              Longbill spearfish   166 4.405859e-04
##                Longfin bonefish     6 1.592479e-05
##                 Longfin codling     3 7.962396e-06
##                    Longfin hake     5 1.327066e-05
##                    Longfin mako    38 1.008570e-04
##                   Longfin squid   165 4.379318e-04
##              Longfin yellowtail    17 4.512025e-05
##        Longlegged spiny lobster   137 3.636161e-04
##                Longnose anchovy    26 6.900743e-05
##                Longnose spurdog     2 5.308264e-06
##         Longnose velvet dogfish    42 1.114735e-04
##                 Longnosed skate    48 1.273983e-04
##              Longspine burrfish    11 2.919545e-05
##             Longspine snipefish    71 1.884434e-04
##           Longtail Southern cod    59 1.565938e-04
##               Longtail stingray     3 7.962396e-06
##                   Longtail tuna   917 2.433839e-03
##                        Lookdown     3 7.962396e-06
##             Lowfin gulper shark    11 2.919545e-05
##           Lumpfish(=Lumpsucker)   374 9.926454e-04
##          Lusitanian cownose ray     3 7.962396e-06
##             Lusitanian toadfish     5 1.327066e-05
##                      Macha clam    78 2.070223e-04
##                Mackerel icefish   184 4.883603e-04
##  Mackerel sharks,porbeagles nei    17 4.512025e-05
##                   Mackerels nei   645 1.711915e-03
##                    Madeiran ray     1 2.654132e-06
##             Madeiran sardinella   284 7.537735e-04
##                     Mako sharks    34 9.024049e-05
##           Malabar blood snapper    29 7.696983e-05
##                Malabar trevally    26 6.900743e-05
##          Mangrove cupped oyster   169 4.485483e-04
##             Mangrove ghost crab     6 1.592479e-05
##            Mangrove red snapper   178 4.724355e-04
##          Mantas, devil rays nei    24 6.369917e-05
##                 Marbled rockcod   116 3.078793e-04
##                Marine crabs nei  2982 7.914622e-03
##          Marine crustaceans nei  2614 6.937901e-03
##               Marine fishes nei 14289 3.792489e-02
##             Marine molluscs nei  3516 9.331928e-03
##                    Marine worms   114 3.025711e-04
##                Marini's anchovy     2 5.308264e-06
##     Marlins,sailfishes,etc. nei  1549 4.111251e-03
##            Masu(=Cherry) salmon    59 1.565938e-04
##                  McCain's skate    11 2.919545e-05
##                          Meagre   509 1.350953e-03
##          Mediterranean dealfish     3 7.962396e-06
##            Mediterranean geryon     9 2.388719e-05
##    Mediterranean horse mackerel   358 9.501793e-04
##             Mediterranean moray    21 5.573677e-05
##            Mediterranean mussel   347 9.209838e-04
##        Mediterranean sand smelt     2 5.308264e-06
##        Mediterranean shore crab   118 3.131876e-04
##         Mediterranean slimehead    11 2.919545e-05
##   Mediterranean slipper lobster    32 8.493223e-05
##         Mediterranean spearfish    21 5.573677e-05
##        Mediterranean starry ray     7 1.857892e-05
##                          Megrim   652 1.730494e-03
##                     Megrims nei    69 1.831351e-04
##       Metanephrops lobsters nei    19 5.042851e-05
##         Metapenaeus shrimps nei   398 1.056345e-03
##               Mexican barracuda     4 1.061653e-05
##          Mexican barred snapper     8 2.123306e-05
##        Mexican foureyed octopus     8 2.123306e-05
##           Miiuy (brown) croaker    13 3.450372e-05
##                      Milk shark     3 7.962396e-06
##                        Milkfish   337 8.944425e-04
##              Minstrel sweetlips    20 5.308264e-05
##                     Mirror dory    69 1.831351e-04
##                   Misty grouper    12 3.184959e-05
##    Mojarras(=Silverbiddies) nei   354 9.395628e-04
##              Mojarras, etc. nei   325 8.625929e-04
##                  Mola rock crab    19 5.042851e-05
##                  Monkfishes nei   709 1.881780e-03
##                  Monocle breams   131 3.476913e-04
##                        Moonfish   160 4.246611e-04
##                       Moras nei    82 2.176388e-04
##                  Moray cods nei    58 1.539397e-04
##                      Morays nei    89 2.362178e-04
##                 Morotoge shrimp    15 3.981198e-05
##                        Morwongs   167 4.432401e-04
##                    Mote sculpin    21 5.573677e-05
##                  Mouse catshark     5 1.327066e-05
##              Mozambique lobster    55 1.459773e-04
##                        Mud sole    44 1.167818e-04
##                     Mullets nei  4141 1.099076e-02
##                           Murex    90 2.388719e-04
##                  Murray's skate    12 3.184959e-05
##                   Musky octopus     1 2.654132e-06
##                  Mutton snapper    18 4.777438e-05
##                  Myers' icefish     1 2.654132e-06
##   Narrowbarred Spanish mackerel  1169 3.102680e-03
##          Narrownose smoothhound    73 1.937516e-04
##                  Nassau grouper   102 2.707215e-04
##             Natal spiny lobster    49 1.300525e-04
##          Natantian decapods nei  3315 8.798448e-03
##             Navaga(=Wachna cod)    62 1.645562e-04
##                Needlefishes nei   100 2.654132e-04
##          Needlefishes, etc. nei   324 8.599388e-04
##          Needlescaled queenfish    13 3.450372e-05
##               Neon flying squid    40 1.061653e-04
##            New Zealand blue cod    53 1.406690e-04
##                New Zealand dory     5 1.327066e-05
##       New Zealand dredge oyster    63 1.672103e-04
##             New Zealand lobster    23 6.104504e-05
##         New Zealand rough skate    12 3.184959e-05
##             New Zealand scallop    49 1.300525e-04
##        New Zealand smooth skate    12 3.184959e-05
##            Nichol's lanternfish     8 2.123306e-05
##                      Noah's ark     2 5.308264e-06
##              North Pacific hake   230 6.104504e-04
##           Northern brown shrimp    92 2.441802e-04
##               Northern kingfish    60 1.592479e-04
##           Northern nylon shrimp     9 2.388719e-05
##            Northern pink shrimp   136 3.609620e-04
##                  Northern prawn   948 2.516117e-03
##                 Northern puffer    64 1.698645e-04
##     Northern quahog(=Hard clam)   130 3.450372e-04
##            Northern red snapper   118 3.131876e-04
##         Northern shortfin squid   460 1.220901e-03
##           Northern white shrimp    91 2.415260e-04
##               Northern wolffish    17 4.512025e-05
##                  Norway lobster  1364 3.620236e-03
##                     Norway pout   310 8.227809e-04
##                  Norway redfish     7 1.857892e-05
##                 Norwegian skate     2 5.308264e-06
##                     Nurse shark    50 1.327066e-04
##                      Nursehound    60 1.592479e-04
##                Obtuse barracuda    14 3.715785e-05
##                      Ocean pout    76 2.017140e-04
##                    Ocean quahog   119 3.158417e-04
##                    Ocean shrimp    29 7.696983e-05
##                   Ocean sunfish    28 7.431570e-05
##                 Ocean whitefish    29 7.696983e-05
##          Oceanic whitetip shark    67 1.778268e-04
##               Ocellated icefish    12 3.184959e-05
##             Octopuses, etc. nei  2935 7.789878e-03
##               Offshore rockfish    13 3.450372e-05
##            Offshore silver hake    17 4.512025e-05
##                         Oilfish   210 5.573677e-04
##           Okhotsk atka mackerel   193 5.122475e-04
##                  Olympia oyster    14 3.715785e-05
##                            Opah    93 2.468343e-04
##        Opalescent inshore squid    28 7.431570e-05
##                         Opaleye    13 3.450372e-05
##                    Orange perch    14 3.715785e-05
##                   Orange roughy   294 7.803148e-04
##           Orangespotted grouper    36 9.554876e-05
##          Orangespotted trevally    55 1.459773e-04
##           Orangestriped emperor    13 3.450372e-05
##                 Oreo dories nei    88 2.335636e-04
##                      Orfe(=Ide)    73 1.937516e-04
##            Ornate spiny lobster     3 7.962396e-06
##               Pacific anchoveta   139 3.689244e-04
##              Pacific angelshark    76 2.017140e-04
##            Pacific bluefin tuna   658 1.746419e-03
##                  Pacific bumper    19 5.042851e-05
##          Pacific calico scallop    29 7.696983e-05
##                     Pacific cod   414 1.098811e-03
##              Pacific cornetfish     7 1.857892e-05
##           Pacific cupped oyster   373 9.899913e-04
##        Pacific flatiron herring     2 5.308264e-06
##                 Pacific geoduck    57 1.512855e-04
##              Pacific guitarfish    50 1.327066e-04
##                 Pacific halibut   200 5.308264e-04
##                 Pacific herring   480 1.273983e-03
##         Pacific horse clams nei    13 3.450372e-05
##           Pacific jack mackerel   135 3.583078e-04
##         Pacific littleneck clam    12 3.184959e-05
##                Pacific menhaden   126 3.344206e-04
##             Pacific ocean perch   338 8.970966e-04
##              Pacific piquitinga     7 1.857892e-05
##                 Pacific pompano    30 7.962396e-05
##              Pacific razor clam    44 1.167818e-04
##             Pacific red snapper     8 2.123306e-05
##               Pacific rock crab    59 1.565938e-04
##             Pacific rock shrimp    15 3.981198e-05
##              Pacific rudderfish   170 4.512025e-04
##             Pacific salmons nei     8 2.123306e-05
##               Pacific sand sole    30 7.962396e-05
##                 Pacific sanddab    11 2.919545e-05
##               Pacific sandlance   108 2.866463e-04
##               Pacific sandperch    63 1.672103e-04
##                   Pacific saury   217 5.759467e-04
##                  Pacific seabob    49 1.300525e-04
##                 Pacific seabobs   238 6.316834e-04
##                  Pacific sierra   228 6.051421e-04
##           Pacific sleeper shark    10 2.654132e-05
##               Pacific spadefish     3 7.962396e-06
##          Pacific thread herring    90 2.388719e-04
##                  Pacific tomcod     7 1.857892e-05
##              Pacific tripletail     3 7.962396e-06
##                  Painted comber     5 1.327066e-05
##                   Painted notie     9 2.388719e-05
##               Painted sweetlips    20 5.308264e-05
##          Palaemonid shrimps nei    63 1.672103e-04
##    Palinurid spiny lobsters nei   767 2.035719e-03
##                     Panama hake    11 2.919545e-05
##            Pandalus shrimps nei   132 3.503454e-04
##                    Pandoras nei   584 1.550013e-03
##                  Panga seabream   109 2.893004e-04
##      Parapenaeopsis shrimps nei    54 1.433231e-04
##                  Parassi mullet     8 2.123306e-05
##                Pargo breams nei   447 1.186397e-03
##            Parona leatherjacket    91 2.415260e-04
##                          Parore    42 1.114735e-04
##                      Parrotfish    80 2.123306e-04
##                Parrotfishes nei   418 1.109427e-03
##              Patagonian blennie   157 4.166987e-04
##            Patagonian grenadier   335 8.891342e-04
##              Patagonian redfish     4 1.061653e-05
##              Patagonian rockcod    40 1.061653e-04
##              Patagonian scallop    76 2.017140e-04
##                Patagonian skate     3 7.962396e-06
##                Patagonian squid   281 7.458111e-04
##            Patagonian toothfish   675 1.791539e-03
##                    Peacock hind    13 3.450372e-05
##                Pearly razorfish     8 2.123306e-05
##              Pelagic armourhead    59 1.565938e-04
##              Pelagic fishes nei   235 6.237210e-04
##         Pelagic percomorphs nei   840 2.229471e-03
##                Pelagic red crab    26 6.900743e-05
##                Pelagic stingray     1 2.654132e-06
##                Pelagic thresher     3 7.962396e-06
##               Pemarco blackfish    14 3.715785e-05
##             Penaeus shrimps nei  2506 6.651255e-03
##                    Percoids nei   546 1.449156e-03
##                 Periwinkles nei   341 9.050590e-04
##               Perlemoen abalone    62 1.645562e-04
##         Peruvian banded croaker    63 1.672103e-04
##         Peruvian calico scallop    89 2.362178e-04
##               Peruvian moonfish     7 1.857892e-05
##                Peruvian morwong    68 1.804810e-04
##           Peruvian rock seabass    64 1.698645e-04
##               Peruvian weakfish   119 3.158417e-04
##                    Petrale sole    32 8.493223e-05
##              Pharaoh cuttlefish   200 5.308264e-04
##                         Picarel     2 5.308264e-06
##                    Picarels nei   632 1.677411e-03
##                  Picked dogfish  1027 2.725794e-03
##            Pickhandle barracuda    29 7.696983e-05
##              Pig's snout volute     3 7.962396e-06
##                         Pigfish    53 1.406690e-04
##                    Pike icefish    10 2.654132e-05
##                 Pikecongers nei   230 6.104504e-04
##                       Pilotfish    12 3.184959e-05
##                         Pinfish     5 1.327066e-05
##                    Pink cuskeel   494 1.311141e-03
##                Pink ear emperor    28 7.431570e-05
##                     Pink maomao     8 2.123306e-05
##              Pink spiny lobster    50 1.327066e-04
##          Pink(=Humpback) salmon   273 7.245781e-04
##                 Pipi wedge clam    67 1.778268e-04
##                    Plain bonito   213 5.653301e-04
##               Plownose chimaera   140 3.715785e-04
##                     Plunderfish    16 4.246611e-05
##                 Pod razor shell     8 2.123306e-05
##                       Polar cod   108 2.866463e-04
##                         Pollack   626 1.661487e-03
##      Pomfrets, ocean breams nei    22 5.839091e-05
##                         Pompano     4 1.061653e-05
##                    Pompanos nei   439 1.165164e-03
##                     Pontic shad   172 4.565107e-04
##         Ponyfishes(=Slipmouths)   232 6.157586e-04
##     Ponyfishes(=Slipmouths) nei   345 9.156756e-04
##                        Poor cod   101 2.680673e-04
##                       Porbeagle   690 1.831351e-03
##                         Porgies   151 4.007739e-04
##          Porgies, seabreams nei  2923 7.758028e-03
##              Portly spider crab     3 7.962396e-06
##              Portuguese dogfish   106 2.813380e-04
##          Portunus swimcrabs nei   161 4.273153e-04
##                   Pouting(=Bib)   537 1.425269e-03
##                 Prickly redfish    12 3.184959e-05
##                     Puffers nei   161 4.273153e-04
##             Pullet carpet shell   132 3.503454e-04
##                      Queen crab    95 2.521425e-04
##                   Queen scallop   247 6.555706e-04
##                   Queen snapper    11 2.919545e-05
##                     Queenfishes   383 1.016533e-03
##                     Rabbit fish    86 2.282554e-04
##                  Rainbow runner   371 9.846830e-04
##                 Rainbow sardine   179 4.750896e-04
##                   Rainbow smelt   134 3.556537e-04
##                   Rainbow trout    64 1.698645e-04
##                  Rainbow wrasse     9 2.388719e-05
##                   Raja rays nei  1386 3.678627e-03
##       Randall's threadfin bream     9 2.388719e-05
##                   Ratfishes nei    41 1.088194e-04
##             Rays and skates nei    12 3.184959e-05
##     Rays, stingrays, mantas nei  3706 9.836214e-03
##    Razor clams, knife clams nei    31 8.227809e-05
##                    Red bandfish    54 1.433231e-04
##                      Red bigeye    70 1.857892e-04
##                     Red codling   115 3.052252e-04
##                        Red crab    41 1.088194e-04
##                     Red cuskeel    63 1.672103e-04
##                        Red drum    97 2.574508e-04
##                     Red grouper   164 4.352777e-04
##                     Red gurnard   137 3.636161e-04
##                        Red hake   277 7.351946e-04
##                        Red hind    95 2.521425e-04
##                   Red king crab   168 4.458942e-04
##                      Red mullet   236 6.263752e-04
##                     Red pandora   239 6.343376e-04
##                 Red pike conger     7 1.857892e-05
##                       Red porgy   686 1.820735e-03
##                Red rock lobster    63 1.672103e-04
##                Red scorpionfish    24 6.369917e-05
##           Red sea mantis shrimp     4 1.061653e-05
##                   Red snow crab    18 4.777438e-05
##                    Red starfish    18 4.777438e-05
##                   Red steenbras    31 8.227809e-05
##                  Red stone crab     8 2.123306e-05
##             Red vermillion crab     2 5.308264e-06
##            Redeye round herring   166 4.405859e-04
##                         Redfish    59 1.565938e-04
##                Redmouth grouper    13 3.450372e-05
##               Redspotted shrimp    55 1.459773e-04
##                   Redtail prawn    42 1.114735e-04
##              Requiem sharks nei   494 1.311141e-03
##                        Rex sole    30 7.962396e-05
##            Ridge scaled rattail    58 1.539397e-04
##          Righteye flounders nei    13 3.450372e-05
##                       Rio skate     4 1.061653e-05
##                   River lamprey     2 5.308264e-06
##              River Plata mussel   123 3.264582e-04
##                           Roach   311 8.254351e-04
##                     Roaches nei    63 1.672103e-04
##           Robust clubhook squid     3 7.962396e-06
##                       Rock cook     8 2.123306e-05
##                       Rock hind     1 2.654132e-06
##                     Rock shrimp    45 1.194359e-04
##                       Rock sole    92 2.441802e-04
##                   Rocklings nei    54 1.433231e-04
##                  Rostrate pitar     7 1.857892e-05
##                   Roudi escolar    19 5.042851e-05
##                      Rough scad    90 2.388719e-04
##             Roughhead grenadier   180 4.777438e-04
##            Roughsnout grenadier     4 1.061653e-05
##                       Round ray     4 1.061653e-05
##                Round sardinella   763 2.025103e-03
##             Roundnose grenadier   663 1.759690e-03
##            Roundscale spearfish     5 1.327066e-05
##             Roving coralgrouper    13 3.450372e-05
##                Royal red shrimp    59 1.565938e-04
##                 Royal threadfin   187 4.963227e-04
##                 Rubberlip grunt   223 5.918715e-04
##                        Rubyfish    20 5.308264e-05
##                            Rudd     4 1.061653e-05
##                      Rudderfish     3 7.962396e-06
##                            Ruff    63 1.672103e-04
##         Ruffs, barrelfishes nei   136 3.609620e-04
##                   Rusty jobfish    13 3.450372e-05
##                       Sablefish   291 7.723524e-04
##              Sabre squirrelfish    18 4.777438e-05
##                Saddled seabream   320 8.493223e-04
##                     Saffron cod    63 1.672103e-04
##              Sailfin roughshark     5 1.327066e-05
##                         Sailray     4 1.061653e-05
##                Saithe(=Pollock)  1317 3.495492e-03
##                          Salema   488 1.295216e-03
##                  Salmonoids nei   332 8.811719e-04
##                       Sand fish    11 2.919545e-05
##              Sand flounders nei    99 2.627591e-04
##                      Sand gaper   142 3.768868e-04
##                       Sand sole   142 3.768868e-04
##                  Sand steenbras   265 7.033450e-04
##                Sand tiger shark    23 6.104504e-05
##                   Sand tilefish    14 3.715785e-05
##                   Sand weakfish    65 1.725186e-04
##                   Sandbar shark    19 5.042851e-05
##       Sandeels(=Sandlances) nei   498 1.321758e-03
##                  Sandpaper fish     2 5.308264e-06
##                       Sandy ray    46 1.220901e-04
##                 Santer seabream    56 1.486314e-04
##                Sao Paulo shrimp    39 1.035112e-04
##                 Sardinellas nei  1942 5.154325e-03
##                Sargo breams nei   544 1.443848e-03
##                       Sawfishes    79 2.096764e-04
##                   Sawsharks nei    13 3.450372e-05
##                       Scads nei   826 2.192313e-03
##                 Scaled sardines   174 4.618190e-04
##            Scalloped hammerhead    59 1.565938e-04
##         Scalloped spiny lobster    63 1.672103e-04
##                    Scallops nei   599 1.589825e-03
##                   Scaly gurnard    11 2.919545e-05
##                           Scamp    14 3.715785e-05
##                  Scarlet shrimp    61 1.619021e-04
##                           Scats    43 1.141277e-04
##       Schoolmaster gonate squid     9 2.388719e-05
##           Scomber mackerels nei   156 4.140446e-04
##              Scorpionfishes nei  1414 3.752943e-03
##                        Sculpins    10 2.654132e-05
##                    Sculpins nei    46 1.220901e-04
##          Sculptured shrimps nei    15 3.981198e-05
##                            Scup   120 3.184959e-04
##               Sea catfishes nei  2204 5.849707e-03
##                   Sea chubs nei    68 1.804810e-04
##               Sea cucumbers nei   904 2.399335e-03
##                     Sea lamprey   103 2.733756e-04
##                 Sea mussels nei   287 7.617359e-04
##                      Sea snails    72 1.910975e-04
##                       Sea trout   400 1.061653e-03
##                 Sea urchins nei   604 1.603096e-03
##           Sea urchins, etc. nei     4 1.061653e-05
##                   Seabasses nei   208 5.520595e-04
##                  Seerfishes nei  1070 2.839921e-03
##                 Senegalese hake   273 7.245781e-04
##                 Senegalese sole    14 3.715785e-05
##           Sergestid shrimps nei   204 5.414429e-04
##          Serra Spanish mackerel   215 5.706384e-04
##          Sevenstar flying squid    67 1.778268e-04
##                       Shads nei   434 1.151893e-03
##                    Shagreen ray    62 1.645562e-04
##          Shallowwater Cape hake    49 1.300525e-04
##  Sharks, rays, skates, etc. nei  6405 1.699972e-02
##       Sharpnose sevengill shark     4 1.061653e-05
##              Sharpnose stingray    15 3.981198e-05
##             Sharpsnout seabream     5 1.327066e-05
##           Sharptooth houndshark     3 7.962396e-06
##                      Sheepshead   102 2.707215e-04
##                        Shi drum   199 5.281723e-04
##                    Shiba shrimp    43 1.141277e-04
##                  Short mackerel   179 4.750896e-04
##            Short neck clams nei   130 3.450372e-04
##             Shortbill spearfish   153 4.060822e-04
##                   Shortfin mako   801 2.125960e-03
##                   Shortfin scad     7 1.857892e-05
##                  Shorthead drum    11 2.919545e-05
##               Shorthorn sculpin     1 2.654132e-06
##          Shortjaw leatherjacket     8 2.123306e-05
##       Shortspine African angler    12 3.184959e-05
##           Shortspine thornyhead    21 5.573677e-05
##                     Shrimp scad    18 4.777438e-05
##                          Sichel    76 2.017140e-04
##                  Sickle pomfret     9 2.388719e-05
##                    Silk snapper    15 3.981198e-05
##                     Silky shark   156 4.140446e-04
##                 Sillagowhitings   555 1.473043e-03
##                     Silver carp     2 5.308264e-06
##                 Silver chimaera     1 2.654132e-06
##                  Silver croaker    73 1.937516e-04
##                  Silver gemfish   136 3.609620e-04
##                    Silver grunt   145 3.848492e-04
##                     Silver hake   346 9.183297e-04
##                  Silver pomfret   434 1.151893e-03
##             Silver pomfrets nei    35 9.289462e-05
##             Silver scabbardfish   438 1.162510e-03
##                 Silver seabream   448 1.189051e-03
##                  Silver sillago    31 8.227809e-05
##                  Silver warehou    79 2.096764e-04
##          Silvercheeked toadfish     3 7.962396e-06
##   Silversides(=Sand smelts) nei   784 2.080840e-03
##      Silverstripe round herring    90 2.388719e-04
##               Silvery John dory    53 1.406690e-04
##               Silvery lightfish    15 3.981198e-05
##                    Silvery pout     7 1.857892e-05
##                        Skilfish     1 2.654132e-06
##         Skinnycheek lanternfish    14 3.715785e-05
##                   Skipjack tuna  5785 1.535415e-02
##                     Sky emperor    23 6.104504e-05
##               Slender armorhead    23 6.104504e-05
##         Slender rainbow sardine    53 1.406690e-04
##             Slender silverbiddy    15 3.981198e-05
##             Slender smoothhound     2 5.308264e-06
##                    Slender tuna    21 5.573677e-05
##                  Slickheads nei    14 3.715785e-05
##                  Slimeheads nei    34 9.024049e-05
##           Slipper cupped oyster    36 9.554876e-05
##            Slipper lobsters nei   277 7.351946e-04
##              Smalleye moray cod    37 9.820289e-05
##                   Smalleyed ray    26 6.900743e-05
##              Smallnose fanskate     4 1.061653e-05
##             Smallscaled grouper    14 3.715785e-05
##           Smallspotted catshark    99 2.627591e-04
##                 Smalltail shark     5 1.327066e-05
##              Smalltooth emperor    21 5.573677e-05
##                      Smelts nei   165 4.379318e-04
##                 Smooth callista    33 8.758636e-05
##               Smooth hammerhead   102 2.707215e-04
##                Smooth oreo dory    25 6.635330e-05
##                 Smooth weakfish    11 2.919545e-05
##                     Smoothhound    46 1.220901e-04
##                Smoothhounds nei   701 1.860547e-03
##                    Snaggletooth     1 2.654132e-06
##                  Snake eels nei    26 6.900743e-05
##   Snake mackerels, escolars nei   118 3.131876e-04
##                    Snappers nei  1309 3.474259e-03
##         Snappers, jobfishes nei  1861 4.939340e-03
##                           Snoek   454 1.204976e-03
##            Snooks(=Robalos) nei   413 1.096157e-03
##                   Snowy grouper    12 3.184959e-05
##                Snubnose emperor    18 4.777438e-05
##                Snubnose pompano    16 4.246611e-05
##                Sobaity seabream    26 6.900743e-05
##            Sockeye(=Red) salmon   250 6.635330e-04
##              Softshell red crab    76 2.017140e-04
##               Sohal surgeonfish    13 3.450372e-05
##           Soiny (redlip) mullet    14 3.715785e-05
##                    Soiuy mullet    28 7.431570e-05
##           Solen razor clams nei   142 3.768868e-04
##                       Soles nei   307 8.148186e-04
##                 Solid surf clam    43 1.141277e-04
##                    Sompat grunt   224 5.945256e-04
##                Sordid rubberlip     9 2.388719e-05
##         South American pilchard   158 4.193529e-04
##      South American rock mussel    52 1.380149e-04
##     South American silver porgy    36 9.554876e-05
##           South Georgia icefish    65 1.725186e-04
##              South Pacific hake   137 3.636161e-04
##    Southeast Atlantic soles nei    90 2.388719e-04
##        Southern African anchovy    77 2.043682e-04
##       Southern African pilchard   192 5.095934e-04
##           Southern blue whiting   390 1.035112e-03
##           Southern bluefin tuna   865 2.295824e-03
##           Southern brown shrimp     4 1.061653e-05
##                   Southern hake   184 4.883603e-04
##              Southern king crab   139 3.689244e-04
##            Southern kingcroaker     4 1.061653e-05
##             Southern lemon sole    10 2.654132e-05
##            Southern lobsterette     1 2.654132e-06
##      Southern meagre(=Mulloway)   348 9.236380e-04
##                   Southern opah     5 1.327066e-05
##            Southern pink shrimp   216 5.732925e-04
##             Southern rays bream    27 7.166157e-05
##            Southern red snapper   243 6.449541e-04
##           Southern rock lobster    55 1.459773e-04
##           Southern rough shrimp    92 2.441802e-04
##          Southern spiny lobster    41 1.088194e-04
##               Southern stingray     8 2.123306e-05
##           Southern white shrimp     2 5.308264e-06
##   Southwest Atlantic butterfish     7 1.857892e-05
##     Southwest Atlantic red crab    34 9.024049e-05
##                 Spadefishes nei   118 3.131876e-04
##                Spangled emperor    44 1.167818e-04
##                    Spanish ling     3 7.962396e-06
##         Spanish slipper lobster     4 1.061653e-05
##                   Speckled hind     1 2.654132e-06
##                 Speckled shrimp    27 7.166157e-05
##                      Spiky oreo    24 6.369917e-05
##    Spinefeet(=Rabbitfishes) nei   775 2.056952e-03
##                   Spinner shark     2 5.308264e-06
##             Spinous spider crab   466 1.236826e-03
##             Spiny butterfly ray    17 4.512025e-05
##                   Spiny icefish    21 5.573677e-05
##              Spiny lobsters nei    96 2.547967e-04
##              Spiny scorpionfish    11 2.919545e-05
##                  Spiral babylon     9 2.388719e-05
##              Splendid alfonsino    26 6.900743e-05
##              Splitnose rockfish     3 7.962396e-06
##                    Spot croaker   126 3.344206e-04
##                     Spot shrimp     5 1.327066e-05
##                  Spotback skate     4 1.061653e-05
##                Spotfin flathead    15 3.981198e-05
##        Spottail mantis squillid   135 3.583078e-04
##                  Spottail shark    16 4.246611e-05
##           Spottail spiny turbot    14 3.715785e-05
##     Spotted estuary smoothhound    64 1.698645e-04
##                 Spotted grouper    40 1.061653e-04
##                 Spotted gurnard    18 4.777438e-05
##                 Spotted ratfish    12 3.184959e-05
##                     Spotted ray    68 1.804810e-04
##            Spotted rose snapper    15 3.981198e-05
##              Spotted sardinella    18 4.777438e-05
##                 Spotted seabass   131 3.476913e-04
##              Spotted sicklefish   158 4.193529e-04
##                Spotted weakfish   179 4.750896e-04
##                Spotted wolffish    84 2.229471e-04
##         Squaretail coralgrouper    13 3.450372e-05
##      Squeteague(=Gray weakfish)   126 3.344206e-04
##                   Squillids nei    53 1.406690e-04
##              Squirrelfishes nei   146 3.875033e-04
##            St.Paul rock lobster    63 1.672103e-04
##                  Starfishes nei   137 3.636161e-04
##                       Stargazer    31 8.227809e-05
##                      Stargazers     1 2.654132e-06
##                 Starry flounder    13 3.450372e-05
##                      Starry ray    38 1.008570e-04
##              Starry smoothhound    17 4.512025e-05
##                 Starry sturgeon    18 4.777438e-05
##                Steenbrasses nei    22 5.839091e-05
##                Sterlet sturgeon     1 2.654132e-06
##            Stimpson's surf clam    69 1.831351e-04
##                   Stingrays nei    14 3.715785e-05
##   Stingrays, butterfly rays nei    53 1.406690e-04
##       Stolephorus anchovies nei   456 1.210284e-03
##                 Stomatopods nei    50 1.327066e-04
##                Stony sea urchin   104 2.760297e-04
##                 Stout beardfish     4 1.061653e-05
##         Straightnose rabbitfish     2 5.308264e-06
##                Streaked gurnard    13 3.450372e-05
##               Streaked seerfish   185 4.910144e-04
##                    Striped bass   185 4.910144e-04
##                  Striped bonito    56 1.486314e-04
##                  Striped marlin  1526 4.050206e-03
##                   Striped piggy    18 4.777438e-05
##              Striped red shrimp    53 1.406690e-04
##                 Striped rockcod    11 2.919545e-05
##                   Striped venus   280 7.431570e-04
##                Striped weakfish   126 3.344206e-04
##             Stripedeyed rockcod     7 1.857892e-05
##               Stripped weakfish    11 2.919545e-05
##            Stromboid conchs nei   930 2.468343e-03
##                   Sturgeons nei   319 8.466681e-04
##              Stutchbury's venus    18 4.777438e-05
##         Subantarctic stone crab    16 4.246611e-05
##           Subtruncate surf clam     3 7.962396e-06
##       Suckerfishes, remoras nei     9 2.388719e-05
##                  Summan grouper    13 3.450372e-05
##                 Summer flounder    94 2.494884e-04
##                  Surf clams nei    11 2.919545e-05
##                      Surf smelt    47 1.247442e-04
##               Surgeonfishes nei   296 7.856231e-04
##                       Surmullet   574 1.523472e-03
##    Surmullets(=Red mullets) nei  1015 2.693944e-03
##          Swarming squat lobster    10 2.654132e-05
##       Sweetlips, rubberlips nei    18 4.777438e-05
##               Sword razor shell     5 1.327066e-05
##                       Swordfish  5143 1.365020e-02
##                       Taca clam    63 1.672103e-04
##                 Tadpole codling   199 5.281723e-04
##                Talang queenfish    38 1.008570e-04
##                Tanner crabs nei   177 4.697814e-04
##                  Taquilla clams    19 5.042851e-05
##                        Tarakihi    87 2.309095e-04
##                          Tarpon   211 5.600219e-04
##                          Tautog    63 1.672103e-04
##                     Tellins nei     4 1.061653e-05
##                           Tench    55 1.459773e-04
##             Terapon perches nei    27 7.166157e-05
##             Thickback soles nei    43 1.141277e-04
##            Thicklip grey mullet     8 2.123306e-05
##                   Thornback ray   141 3.742326e-04
##            Thorntooth grenadier    21 5.573677e-05
##  Threadfin and dwarf breams nei   150 3.981198e-04
##            Threadfin breams nei   675 1.791539e-03
##              Threadfin rockling     3 7.962396e-06
##    Threadfins, tasselfishes nei  1003 2.662094e-03
##             Threadsail filefish    41 1.088194e-04
##         Threespined stickleback    74 1.964058e-04
##                        Thresher   208 5.520595e-04
##             Thresher sharks nei   116 3.078793e-04
##              Thumbprint emperor    13 3.450372e-05
##                     Tiger shark    72 1.910975e-04
##              Tigertooth croaker    33 8.758636e-05
##                    Tilapias nei   107 2.839921e-04
##                  Tilefishes nei   346 9.183297e-04
##                     Titi shrimp     6 1.592479e-05
##                      Toad notie     6 1.592479e-05
##            Toadfishes, etc. nei    30 7.962396e-05
##                       Toli shad   125 3.317665e-04
##                    Tonguefishes   944 2.505501e-03
##                      Tope shark   350 9.289462e-04
##                    Torpedo rays    52 1.380149e-04
##                    Torpedo scad   463 1.228863e-03
##                         Totoaba    28 7.431570e-05
##                Transparent goby    13 3.450372e-05
##                  Trematomus nei     5 1.327066e-05
##              Triangular rockcod     9 2.388719e-05
##               Triangular tivela    17 4.512025e-05
##      Triggerfishes, durgons nei   758 2.011832e-03
##                      Tripletail    31 8.227809e-05
##   Tristan da Cunha rock lobster    63 1.672103e-04
##     Tropical spiny lobsters nei  1963 5.210061e-03
##                 Trout sweetlips    21 5.573677e-05
##                 Trumpet emperor     3 7.962396e-06
##                  Trumpeters nei   123 3.264582e-04
##        Tsivakihini paste shrimp     7 1.857892e-05
##                     Tub gurnard    74 1.964058e-04
##             Tuberculate abalone    30 7.962396e-05
##             Tunalike fishes nei  3457 9.175335e-03
##                          Turbot  1126 2.988553e-03
##                     Turbots nei    46 1.220901e-04
##                     Turkey wing     5 1.327066e-05
##                     Tusk(=Cusk)   784 2.080840e-03
##                     Twaite shad    49 1.300525e-04
##                 Twobar seabream    51 1.353607e-04
##             Twospot red snapper    15 3.981198e-05
##                    Undulate ray     8 2.123306e-05
##                     Unicorn cod   162 4.299694e-04
##                 Unicorn icefish    31 8.227809e-05
##                          Vadigo    30 7.962396e-05
##              Various sharks nei   294 7.803148e-04
##              Various squids nei  3072 8.153494e-03
##                    Veined squid    14 3.715785e-05
##                    Velvet belly    21 5.573677e-05
##            Velvet leatherjacket    50 1.327066e-04
##                 Velvet swimcrab    44 1.167818e-04
##                Velvet whalefish     1 2.654132e-06
##                         Vendace   124 3.291124e-04
##                 Venus clams nei   244 6.476082e-04
##               Vermilion snapper    35 9.289462e-05
##                     Vimba bream    69 1.831351e-04
##                  Violet warehou    15 3.981198e-05
##                     Volutes nei    20 5.308264e-05
##                           Wahoo  1216 3.227425e-03
##                     Warehou nei   182 4.830520e-04
##                  Warsaw grouper    17 4.512025e-05
##                 Warthead blenny     1 2.654132e-06
##                      Warty dory     8 2.123306e-05
##                     Warty venus     2 5.308264e-06
##                  Weakfishes nei   273 7.245781e-04
##             Weathervane scallop    44 1.167818e-04
##                      Wedge sole   142 3.768868e-04
##                Weeverfishes nei     8 2.123306e-05
##                     Weevers nei    26 6.900743e-05
##         Wellington flying squid   112 2.972628e-04
##       West African croakers nei   724 1.921592e-03
##    West African estuarine prawn    12 3.184959e-05
##             West African geryon   112 2.972628e-04
##           West African goatfish   337 8.944425e-04
##             West African ilisha   245 6.502624e-04
##           West African ladyfish    88 2.335636e-04
##   West African Spanish mackerel   255 6.768037e-04
##                 West coast sole   105 2.786839e-04
##       Western Atlantic seabream     7 1.857892e-05
##              Western king prawn    99 2.627591e-04
##            Western white shrimp    56 1.486314e-04
##                           Whelk   331 8.785177e-04
##                          Whelks    89 2.362178e-04
##                   Whip stingray    58 1.539397e-04
##                    White barbel     2 5.308264e-06
##                     White bream    11 2.919545e-05
##                   White croaker    63 1.672103e-04
##                   White grouper   164 4.352777e-04
##                     White grunt     8 2.123306e-05
##                      White hake   327 8.679012e-04
##                   White margate     5 1.327066e-05
##                    White mullet    18 4.777438e-05
##                     White perch     8 2.123306e-05
##                  White seabream   185 4.910144e-04
##                     White skate    19 5.042851e-05
##            White snake mackerel     1 2.654132e-06
##                 White steenbras    36 9.554876e-05
##                 White stumpnose    49 1.300525e-04
##                  White sturgeon    13 3.450372e-05
##                  White teatfish    12 3.184959e-05
##                  White trevally   103 2.733756e-04
##                   White warehou    26 6.900743e-05
##                  White weakfish    63 1.672103e-04
##                Whitebelly prawn    16 4.246611e-05
##           Whiteblotched grouper    13 3.450372e-05
##            Whitefin wolfherring    34 9.024049e-05
##                 Whitefishes nei   105 2.786839e-04
##       Whitehead's round herring    74 1.964058e-04
##                 Whiteleg shrimp    90 2.388719e-04
##              Whitemouth croaker   241 6.396458e-04
##             Whitespotted conger    45 1.194359e-04
##            Whitespotted grouper     3 7.962396e-06
##          Whitespotted wedgefish    16 4.246611e-05
##                         Whiting  1090 2.893004e-03
##             Whitson's grenadier    51 1.353607e-04
##                  Widow rockfish    34 9.024049e-05
##             Windowpane flounder    39 1.035112e-04
##                 Winter flounder   150 3.981198e-04
##                  Witch flounder  1003 2.662094e-03
##      Wolffishes(=Catfishes) nei   857 2.274591e-03
##                Wolfherrings nei   522 1.385457e-03
##    Wrasses, hogfishes, etc. nei   582 1.544705e-03
##                       Wreckfish   403 1.069615e-03
##                  Yellow croaker   230 6.104504e-04
##                  Yellow snapper    91 2.415260e-04
##         Yellow striped flounder    63 1.672103e-04
##             Yellowbar angelfish    28 7.431570e-05
##             Yellowbelly rockcod     6 1.592479e-05
##              Yellowedge grouper    14 3.715785e-05
##            Yellowedged lyretail    19 5.042851e-05
##               Yellowfin grouper    15 3.981198e-05
##                  Yellowfin hind    13 3.450372e-05
##                 Yellowfin notie    22 5.839091e-05
##         Yellowfin river pellona     4 1.061653e-05
##              Yellowfin seabream    64 1.698645e-04
##                  Yellowfin sole    77 2.043682e-04
##                  Yellowfin tuna  6866 1.822327e-02
##                Yellowleg shrimp   139 3.689244e-04
##               Yellowlip emperor    13 3.450372e-05
##                Yellownose skate     4 1.061653e-05
##          Yellowspotted trevally    13 3.450372e-05
##           Yellowstripe goatfish    27 7.166157e-05
##               Yellowstripe scad   288 7.643900e-04
##            Yellowtail amberjack   255 6.768037e-04
##             Yellowtail flounder   299 7.935855e-04
##             Yellowtail rockfish    35 9.289462e-05
##                 Yellowtail scad    13 3.450372e-05
##              Yellowtail snapper   350 9.289462e-04
##                   Yesso scallop   184 4.883603e-04
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

```r
fisheries_tidy%>%
  filter(between(year,2008,2012))%>%
  slice_max(catch,n=4)
```

```
## # A tibble: 4 × 10
##   country  common_…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##   <fct>    <chr>     <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
## 1 Viet Nam Marine f… 39      Marine… 199XXX… Osteic… 71      Quanti…  2010  9806
## 2 Myanmar  Marine f… 39      Marine… 199XXX… Osteic… 57      Quanti…  2012  9613
## 3 Viet Nam Marine f… 39      Marine… 199XXX… Osteic… 71      Quanti…  2009  8898
## 4 China    Largehea… 34      Miscel… 175060… Trichi… 61      Quanti…  2011  8221
## # … with abbreviated variable names ¹​common_name, ²​isscaap_group_number,
## #   ³​isscaap_taxonomic_group, ⁴​asfis_species_number, ⁵​asfis_species_name,
## #   ⁶​fao_major_fishing_area
```

```r
#First 3 were fish not identified, the largest catch of an identified species was Trichiurus lepturus in 2011 in China
```

10. Use the data to do at least one analysis of your choice.

Which country caught the most sharks/rays/chimaeras between 2000-2005 and which species was caught the most?

```r
fisheries_tidy%>%
  filter(isscaap_taxonomic_group=="Sharks, rays, chimaeras")%>%
  filter(between(year,2000,2005))%>%
  slice_max(catch)
```

```
## # A tibble: 3 × 10
##   country    commo…¹ issca…² issca…³ asfis…⁴ asfis…⁵ fao_m…⁶ measure  year catch
##   <fct>      <chr>   <fct>   <chr>   <fct>   <chr>   <fct>   <chr>   <dbl> <dbl>
## 1 Liberia    Silky … 38      Sharks… 108020… Carcha… 34      Quanti…  2000    99
## 2 Spain      Lanter… 38      Sharks… 109010… Etmopt… 27      Quanti…  2002    99
## 3 Taiwan Pr… Sharks… 38      Sharks… 199XXX… Elasmo… 71      Quanti…  2003    99
## # … with abbreviated variable names ¹​common_name, ²​isscaap_group_number,
## #   ³​isscaap_taxonomic_group, ⁴​asfis_species_number, ⁵​asfis_species_name,
## #   ⁶​fao_major_fishing_area
```

```r
#There are 3 species sharks, rays, and chimaeras that were caught the most (99) between 2000-2005, the silky shark in Liberia, lanternsharks in Spain, and sharks,etc. in Taiwan.
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
