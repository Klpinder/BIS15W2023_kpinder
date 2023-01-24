---
title: "Lab 4 Homework"
author: "Kat Pinder"
date: "2023-01-24"
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

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  


```r
dim(homerange)
```

```
## [1] 569  24
```

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", …
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3…
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car…
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3…
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N…
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, …
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20…
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```


**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
taxon_f <- as.factor(homerange$taxon)
taxon_f
```

```
##   [1] lake fishes   river fishes  river fishes  river fishes  river fishes 
##   [6] river fishes  marine fishes marine fishes marine fishes marine fishes
##  [11] marine fishes marine fishes marine fishes lake fishes   lake fishes  
##  [16] lake fishes   river fishes  river fishes  lake fishes   lake fishes  
##  [21] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [26] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [31] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [36] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [41] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [46] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [51] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [56] marine fishes marine fishes marine fishes marine fishes lake fishes  
##  [61] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [66] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [71] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [76] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [81] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [86] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [91] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [96] marine fishes river fishes  river fishes  river fishes  river fishes 
## [101] lake fishes   river fishes  river fishes  river fishes  marine fishes
## [106] marine fishes marine fishes marine fishes marine fishes lake fishes  
## [111] marine fishes marine fishes marine fishes birds         birds        
## [116] birds         birds         birds         birds         birds        
## [121] birds         birds         birds         birds         birds        
## [126] birds         birds         birds         birds         birds        
## [131] birds         birds         birds         birds         birds        
## [136] birds         birds         birds         birds         birds        
## [141] birds         birds         birds         birds         birds        
## [146] birds         birds         birds         birds         birds        
## [151] birds         birds         birds         birds         birds        
## [156] birds         birds         birds         birds         birds        
## [161] birds         birds         birds         birds         birds        
## [166] birds         birds         birds         birds         birds        
## [171] birds         birds         birds         birds         birds        
## [176] birds         birds         birds         birds         birds        
## [181] birds         birds         birds         birds         birds        
## [186] birds         birds         birds         birds         birds        
## [191] birds         birds         birds         birds         birds        
## [196] birds         birds         birds         birds         birds        
## [201] birds         birds         birds         birds         birds        
## [206] birds         birds         birds         birds         birds        
## [211] birds         birds         birds         birds         birds        
## [216] birds         birds         birds         birds         birds        
## [221] birds         birds         birds         birds         birds        
## [226] birds         birds         birds         birds         birds        
## [231] birds         birds         birds         birds         birds        
## [236] birds         birds         birds         birds         birds        
## [241] birds         birds         birds         birds         birds        
## [246] birds         birds         birds         birds         birds        
## [251] birds         birds         birds         mammals       mammals      
## [256] mammals       mammals       mammals       mammals       mammals      
## [261] mammals       mammals       mammals       mammals       mammals      
## [266] mammals       mammals       mammals       mammals       mammals      
## [271] mammals       mammals       mammals       mammals       mammals      
## [276] mammals       mammals       mammals       mammals       mammals      
## [281] mammals       mammals       mammals       mammals       mammals      
## [286] mammals       mammals       mammals       mammals       mammals      
## [291] mammals       mammals       mammals       mammals       mammals      
## [296] mammals       mammals       mammals       mammals       mammals      
## [301] mammals       mammals       mammals       mammals       mammals      
## [306] mammals       mammals       mammals       mammals       mammals      
## [311] mammals       mammals       mammals       mammals       mammals      
## [316] mammals       mammals       mammals       mammals       mammals      
## [321] mammals       mammals       mammals       mammals       mammals      
## [326] mammals       mammals       mammals       mammals       mammals      
## [331] mammals       mammals       mammals       mammals       mammals      
## [336] mammals       mammals       mammals       mammals       mammals      
## [341] mammals       mammals       mammals       mammals       mammals      
## [346] mammals       mammals       mammals       mammals       mammals      
## [351] mammals       mammals       mammals       mammals       mammals      
## [356] mammals       mammals       mammals       mammals       mammals      
## [361] mammals       mammals       mammals       mammals       mammals      
## [366] mammals       mammals       mammals       mammals       mammals      
## [371] mammals       mammals       mammals       mammals       mammals      
## [376] mammals       mammals       mammals       mammals       mammals      
## [381] mammals       mammals       mammals       mammals       mammals      
## [386] mammals       mammals       mammals       mammals       mammals      
## [391] mammals       mammals       mammals       mammals       mammals      
## [396] mammals       mammals       mammals       mammals       mammals      
## [401] mammals       mammals       mammals       mammals       mammals      
## [406] mammals       mammals       mammals       mammals       mammals      
## [411] mammals       mammals       mammals       mammals       mammals      
## [416] mammals       mammals       mammals       mammals       mammals      
## [421] mammals       mammals       mammals       mammals       mammals      
## [426] mammals       mammals       mammals       mammals       mammals      
## [431] mammals       mammals       mammals       mammals       mammals      
## [436] mammals       mammals       mammals       mammals       mammals      
## [441] mammals       mammals       mammals       mammals       mammals      
## [446] mammals       mammals       mammals       mammals       mammals      
## [451] mammals       mammals       mammals       mammals       mammals      
## [456] mammals       mammals       mammals       mammals       mammals      
## [461] mammals       mammals       mammals       mammals       mammals      
## [466] mammals       mammals       mammals       mammals       mammals      
## [471] mammals       mammals       mammals       mammals       mammals      
## [476] mammals       mammals       mammals       mammals       mammals      
## [481] mammals       mammals       mammals       mammals       mammals      
## [486] mammals       mammals       mammals       mammals       mammals      
## [491] mammals       lizards       snakes        snakes        snakes       
## [496] snakes        snakes        snakes        snakes        snakes       
## [501] snakes        snakes        snakes        snakes        snakes       
## [506] snakes        snakes        snakes        snakes        snakes       
## [511] snakes        snakes        snakes        snakes        snakes       
## [516] snakes        snakes        lizards       lizards       lizards      
## [521] lizards       lizards       lizards       lizards       lizards      
## [526] lizards       snakes        lizards       snakes        snakes       
## [531] snakes        snakes        snakes        snakes        snakes       
## [536] snakes        snakes        snakes        snakes        snakes       
## [541] snakes        snakes        snakes        turtles       turtles      
## [546] turtles       turtles       turtles       turtles       turtles      
## [551] turtles       turtles       turtles       turtles       turtles      
## [556] turtles       tortoises     tortoises     tortoises     tortoises    
## [561] tortoises     tortoises     tortoises     tortoises     tortoises    
## [566] tortoises     tortoises     tortoises     turtles      
## 9 Levels: birds lake fishes lizards mammals marine fishes ... turtles
```

```r
order_f <- as.factor(homerange$order)
order_f
```

```
##   [1] anguilliformes        cypriniformes         cypriniformes        
##   [4] cypriniformes         cypriniformes         esociformes          
##   [7] gadiformes            gadiformes            perciformes          
##  [10] perciformes           perciformes           perciformes          
##  [13] perciformes           perciformes           perciformes          
##  [16] perciformes           perciformes           perciformes          
##  [19] perciformes           perciformes           perciformes          
##  [22] perciformes           perciformes           perciformes          
##  [25] perciformes           perciformes           perciformes          
##  [28] perciformes           perciformes           perciformes          
##  [31] perciformes           perciformes           perciformes          
##  [34] perciformes           perciformes           perciformes          
##  [37] perciformes           perciformes           perciformes          
##  [40] perciformes           perciformes           perciformes          
##  [43] perciformes           perciformes           perciformes          
##  [46] perciformes           perciformes           perciformes          
##  [49] perciformes           perciformes           perciformes          
##  [52] perciformes           perciformes           perciformes          
##  [55] perciformes           perciformes           perciformes          
##  [58] perciformes           perciformes           perciformes          
##  [61] perciformes           perciformes           perciformes          
##  [64] perciformes           perciformes           perciformes          
##  [67] perciformes           perciformes           perciformes          
##  [70] perciformes           perciformes           perciformes          
##  [73] perciformes           perciformes           perciformes          
##  [76] perciformes           perciformes           perciformes          
##  [79] perciformes           perciformes           perciformes          
##  [82] perciformes           perciformes           perciformes          
##  [85] perciformes           perciformes           perciformes          
##  [88] perciformes           perciformes           perciformes          
##  [91] perciformes           perciformes           perciformes          
##  [94] perciformes           perciformes           perciformes          
##  [97] salmoniformes         salmoniformes         salmoniformes        
## [100] salmoniformes         salmoniformes         scorpaeniformes      
## [103] scorpaeniformes       scorpaeniformes       scorpaeniformes      
## [106] scorpaeniformes       scorpaeniformes       scorpaeniformes      
## [109] scorpaeniformes       siluriformes          syngnathiformes      
## [112] syngnathiformes       tetraodontiformes\xa0 accipitriformes      
## [115] accipitriformes       accipitriformes       accipitriformes      
## [118] accipitriformes       accipitriformes       anseriformes         
## [121] apterygiformes        caprimulgiformes      charadriiformes      
## [124] columbidormes         columbiformes         columbiformes        
## [127] coraciiformes         coraciiformes         cuculiformes         
## [130] cuculiformes          cuculiformes          cuculiformes         
## [133] falconiformes         falconiformes         falconiformes        
## [136] falconiformes         falconiformes         falconiformes        
## [139] falconiformes         falconiformes         falconiformes        
## [142] falconiformes         falconiformes         falconiformes        
## [145] falconiformes         falconiformes         falconiformes        
## [148] falconiformes         falconiformes         galliformes          
## [151] galliformes           galliformes           galliformes          
## [154] galliformes           galliformes           galliformes          
## [157] galliformes           gruiformes            gruiformes           
## [160] gruiformes            passeriformes         passeriformes        
## [163] passeriformes         passeriformes         passeriformes        
## [166] passeriformes         passeriformes         passeriformes        
## [169] passeriformes         passeriformes         passeriformes        
## [172] passeriformes         passeriformes         passeriformes        
## [175] passeriformes         passeriformes         passeriformes        
## [178] passeriformes         passeriformes         passeriformes        
## [181] passeriformes         passeriformes         passeriformes        
## [184] passeriformes         passeriformes         passeriformes        
## [187] passeriformes         passeriformes         passeriformes        
## [190] passeriformes         passeriformes         passeriformes        
## [193] passeriformes         passeriformes         passeriformes        
## [196] passeriformes         passeriformes         passeriformes        
## [199] passeriformes         passeriformes         passeriformes        
## [202] passeriformes         passeriformes         passeriformes        
## [205] passeriformes         passeriformes         passeriformes        
## [208] passeriformes         passeriformes         passeriformes        
## [211] passeriformes         passeriformes         passeriformes        
## [214] passeriformes         passeriformes         passeriformes        
## [217] passeriformes         passeriformes         passeriformes        
## [220] passeriformes         passeriformes         passeriformes        
## [223] passeriformes         passeriformes         passeriformes        
## [226] passeriformes         passeriformes         passeriformes        
## [229] passeriformes         passeriformes         pelecaniformes       
## [232] pelecaniformes        piciformes            piciformes           
## [235] piciformes            piciformes            piciformes           
## [238] piciformes            piciformes            psittaciformes       
## [241] rheiformes            rheiformes            strigiformes         
## [244] strigiformes          strigiformes          strigiformes         
## [247] strigiformes          strigiformes          strigiformes         
## [250] strigiformes          strigiformes          struthioniformes     
## [253] tinamiformes          afrosoricida          afrosoricida         
## [256] artiodactyla          artiodactyla          artiodactyla         
## [259] artiodactyla          artiodactyla          artiodactyla         
## [262] artiodactyla          artiodactyla          artiodactyla         
## [265] artiodactyla          artiodactyla          artiodactyla         
## [268] artiodactyla          artiodactyla          artiodactyla         
## [271] artiodactyla          artiodactyla          artiodactyla         
## [274] artiodactyla          artiodactyla          artiodactyla         
## [277] artiodactyla          artiodactyla          artiodactyla         
## [280] artiodactyla          artiodactyla          artiodactyla         
## [283] artiodactyla          artiodactyla          artiodactyla         
## [286] artiodactyla          artiodactyla          artiodactyla         
## [289] artiodactyla          artiodactyla          artiodactyla         
## [292] artiodactyla          artiodactyla          artiodactyla         
## [295] carnivora             carnivora             carnivora            
## [298] carnivora             carnivora             carnivora            
## [301] carnivora             carnivora             carnivora            
## [304] carnivora             carnivora             carnivora            
## [307] carnivora             carnivora             carnivora            
## [310] carnivora             carnivora             carnivora            
## [313] carnivora             carnivora             carnivora            
## [316] carnivora             carnivora             carnivora            
## [319] carnivora             carnivora             carnivora            
## [322] carnivora             carnivora             carnivora            
## [325] carnivora             carnivora             carnivora            
## [328] carnivora             carnivora             carnivora            
## [331] carnivora             carnivora             carnivora            
## [334] carnivora             carnivora             carnivora            
## [337] carnivora             carnivora             carnivora            
## [340] carnivora             carnivora             carnivora            
## [343] carnivora             carnivora             carnivora            
## [346] carnivora             carnivora             carnivora            
## [349] carnivora             carnivora             dasyuromorpha        
## [352] dasyuromorpha         dasyuromorpha         dasyuromorpia        
## [355] didelphimorphia       didelphimorphia       diprodontia          
## [358] diprodontia           diprodontia           diprodontia          
## [361] diprodontia           diprodontia           diprodontia          
## [364] diprodontia           diprodontia           diprodontia          
## [367] diprodontia           diprodontia           diprotodontia        
## [370] diprotodontia         diprotodontia         diprotodontia        
## [373] diprotodontia         diprotodontia         diprotodontia        
## [376] erinaceomorpha        erinaceomorpha        lagomorpha           
## [379] lagomorpha            lagomorpha            lagomorpha           
## [382] lagomorpha            lagomorpha            lagomorpha           
## [385] lagomorpha            lagomorpha            lagomorpha           
## [388] lagomorpha            lagomorpha            lagomorpha           
## [391] lagomorpha            macroscelidea         macroscelidea        
## [394] macroscelidea         monotrematae          peramelemorphia      
## [397] peramelemorphia       perissodactyla        perissodactyla       
## [400] perissodactyla        pilosa                proboscidea          
## [403] proboscidea           roden                 rodentia             
## [406] rodentia              rodentia              rodentia             
## [409] rodentia              rodentia              rodentia             
## [412] rodentia              rodentia              rodentia             
## [415] rodentia              rodentia              rodentia             
## [418] rodentia              rodentia              rodentia             
## [421] rodentia              rodentia              rodentia             
## [424] rodentia              rodentia              rodentia             
## [427] rodentia              rodentia              rodentia             
## [430] rodentia              rodentia              rodentia             
## [433] rodentia              rodentia              rodentia             
## [436] rodentia              rodentia              rodentia             
## [439] rodentia              rodentia              rodentia             
## [442] rodentia              rodentia              rodentia             
## [445] rodentia              rodentia              rodentia             
## [448] rodentia              rodentia              rodentia             
## [451] rodentia              rodentia              rodentia             
## [454] rodentia              rodentia              rodentia             
## [457] rodentia              rodentia              rodentia             
## [460] rodentia              rodentia              rodentia             
## [463] rodentia              rodentia              rodentia             
## [466] rodentia              rodentia              rodentia             
## [469] rodentia              rodentia              rodentia             
## [472] rodentia              rodentia              rodentia             
## [475] rodentia              rodentia              rodentia             
## [478] rodentia              rodentia              rodentia             
## [481] rodentia              soricomorpha          soricomorpha         
## [484] soricomorpha          soricomorpha          soricomorpha         
## [487] soricomorpha          soricomorpha          soricomorpha         
## [490] soricomorpha          soricomorpha          squamata             
## [493] squamata              squamata              squamata             
## [496] squamata              squamata              squamata             
## [499] squamata              squamata              squamata             
## [502] squamata              squamata              squamata             
## [505] squamata              squamata              squamata             
## [508] squamata              squamata              squamata             
## [511] squamata              squamata              squamata             
## [514] squamata              squamata              squamata             
## [517] squamata              squamata              squamata             
## [520] squamata              squamata              squamata             
## [523] squamata              squamata              squamata             
## [526] squamata              squamata              squamata             
## [529] squamata              squamata              squamata             
## [532] squamata              squamata              squamata             
## [535] squamata              squamata              squamata             
## [538] squamata              squamata              squamata             
## [541] squamata              squamata              squamata             
## [544] testudines            testudines            testudines           
## [547] testudines            testudines            testudines           
## [550] testudines            testudines            testudines           
## [553] testudines            testudines            testudines           
## [556] testudines            testudines            testudines           
## [559] testudines            testudines            testudines           
## [562] testudines            testudines            testudines           
## [565] testudines            testudines            testudines           
## [568] testudines            testudines           
## 51 Levels: accipitriformes afrosoricida anguilliformes ... tetraodontiformes\xa0
```


**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa <- select(homerange, "taxon", "common.name","class", "order","family","genus","species")
view(taxa)
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
carnivore <- filter(homerange, trophic.guild=="carnivore")
table(carnivore$species)
```

```
## 
##                adspersus                    aedon                     alba 
##                        1                        1                        2 
##                albicauda                    aluco                americana 
##                        1                        1                        2 
##               americanus                   analis                annularis 
##                        1                        1                        1 
##                 anomalum                   apodus                aquaticus 
##                        1                        1                        1 
##                  arborea                 arcticus                areolatus 
##                        2                        1                        1 
##                    argus                  aruanus                    asper 
##                        1                        1                        1 
##             atricapillus                    atrox                  auratus 
##                        2                        1                        2 
##                  auritus             aurocapillus                australis 
##                        1                        1                        1 
##                   bairdi                  barbata                baronessa 
##                        1                        1                        1 
##                    belli              bengalensis                 bergylta 
##                        1                        1                        1 
##                 bewickiI                biarmicus              bifasciatum 
##                        1                        1                        1 
##               bivittatus               blandingii                   bonaci 
##                        1                        1                        1 
##                  bonelli                     bubo              bungaroides 
##                        1                        1                        1 
##                    buteo                  butleri                 cabrilla 
##                        1                        1                        1 
##            californianus               canadensis                  canorus 
##                        1                        2                        1 
##                    canus                  caracal                carolinae 
##                        1                        1                        1 
##             carolinensis               cataractae                catenifer 
##                        1                        1                        1 
##                    catus                 caudatus                 caurinus 
##                        1                        1                        1 
##                 cerastes                 cheriway               chrysaetos 
##                        1                        1                        1 
##              chrysopygus                chrysurus                 cinereus 
##                        1                        1                        1 
##                   citrea                   clarki               clathratus 
##                        1                        1                        1 
##                  coelebs                 collurio                 concolor 
##                        1                        1                        1 
##              constrictor constrictor flaviventris               contortrix 
##                        1                        1                        1 
##                 cooperii                    corax                coronatus 
##                        1                        1                        1 
##                  couperi                 cristata                cristatus 
##                        1                        1                        1 
##                cruentata                 culpaeus                   cyanea 
##                        1                        1                        1 
##                  cyaneus                    dahli                    dalli 
##                        1                        1                        1 
##               decussatus               dimidiatus                 dolomieu 
##                        1                        1                        1 
##                  elegans                    epops                  erminea 
##                        2                        1                        1 
##            erythrogaster                 europaea                europaeus 
##                        1                        2                        2 
##                   exilis                    falco               familiaris 
##                        1                        1                        1 
##                 fasciata                fasciatus                    ferox 
##                        1                        1                        1 
##                flagellum                    flava               flavescens 
##                        1                        1                        1 
##            flavimaculata            flavolineatus                    foina 
##                        1                        1                        1 
##                  frenata              funduloides                 funereus 
##                        1                        1                        1 
##                     furo                    fusca               fuscicauda 
##                        1                        1                        1 
##                 gallicus                  garnoti                 garrulus 
##                        1                        1                        1 
##                  genetta                 gentilis                geoffroii 
##                        1                        1                        1 
##                geoffroyi            getula getula                 gibbosus 
##                        1                        1                        1 
##                    gigal                    gilae               glandarius 
##                        1                        1                        1 
##                    gobio               gossypinus              gracillimus 
##                        1                        1                        1 
##                   granti                  griseus                     gulo 
##                        1                        3                        1 
##           guttata emoryi                 guttatus               guttulatus 
##                        1                        1                        1 
##                    harak              hemistiktos                 hipoliti 
##                        1                        1                        1 
##                 horridus                   huntii             ignicapillus 
##                        1                        1                        1 
##                ignobilis               inchneumon                  inermis 
##                        1                        1                        1 
##                inornatus              jamaicensis                 japonica 
##                        1                        1                        1 
##                  jubatus                    julis                 juncidis 
##                        1                        1                        1 
##                kirtlandi                   labrax                  lagopus 
##                        1                        1                        1 
##                 latastei                leopardus                 leucopus 
##                        1                        1                        1 
##                 leucotos                 lineatus               lineolatus 
##                        1                        1                        1 
##              longicollis              longipinnis              longissimus 
##                        1                        1                        1 
##             ludovicianus           lumbriciformis                   lunare 
##                        2                        1                        1 
##                  luridus                 lutreola                     lynx 
##                        1                        1                        1 
##              maccullochi              macrochirus                  macroti 
##                        1                        1                        1 
##                maculatus              maculipinna                    magna 
##                        1                        1                        1 
##                 magnolia                  maliger               marginatus 
##                        1                        1                        1 
##               marmoratus                   martes                  martius 
##                        1                        1                        1 
##              masquinongy                   medius                megalotis 
##                        1                        1                        1 
##             melanoleucus                 melanops                mexicanus 
##                        1                        1                        1 
##                   milvus                  miniata                  minimus 
##                        1                        1                        1 
##                    minor           minor peltifer                 molossus 
##                        1                        1                        1 
##                    morio                 mustinus                   mykiss 
##                        1                        1                        1 
##                  natalis                   natrix                nebulifer 
##                        1                        1                        1 
##                 neglecta                nicholsii                 nigripes 
##                        1                        1                        1 
##                    nisus                  nivalis                   noctua 
##                        1                        1                        1 
##                 obesulus                 obsoleta                 odoratus 
##                        1                        1                        1 
##                 oenanthe                olivaceus                     onca 
##                        1                        1                        1 
##              orbicularis        oreganus concolor               ostralegus 
##                        1                        1                        1 
##                     otus              paludinosus                palustris 
##                        1                        1                        1 
##                 pardalis                 pardinus                   pardus 
##                        1                        1                        1 
##                  parvula                passerina               passerinum 
##                        1                        1                        1 
##              penicillata                 pennanti                 pennatus 
##                        1                        1                        1 
##             pensylvanica             percnopterus               peregrinus 
##                        1                        1                        1 
##                 petechia             philadelphia              phoenicurus 
##                        1                        1                        1 
##          picta marginata                    pinos              piscivorous 
##                        1                        1                        1 
##              platirhinos                poecilura                    poeyi 
##                        1                        1                        1 
##               pollachius               polyglotta              polyglottos 
##                        1                        1                        1 
##               porphyreus             porphyriacus                   pricei 
##                        1                        1                        1 
##                 princeps                  pulcher                punctatus 
##                        1                        1                        1 
##                 pygargus                   raddei               radiolosus 
##                        1                        1                        1 
##                  regulus              reticularia                   romana 
##                        1                        1                        1 
##                 rostrata                  rubetra                   rubica 
##                        2                        1                        1 
##                rubrubrum                rufescens             rufodorsatus 
##                        1                        1                        1 
##                    rufus                rupestris                 ruppelli 
##                        2                        1                        1 
##                  russula                ruticilla                    salar 
##                        1                        1                        1 
##                salmoides                    sarda               savannarum 
##                        1                        1                        1 
##                scandiaca               schneideri                   scriba 
##                        1                        1                        1 
##                 scutatus               scutulatus                  senator 
##                        1                        1                        1 
##                  serinus               serpentina                   serval 
##                        1                        1                        1 
##              shedaoensis                   sialis                 sibirica 
##                        1                        1                        1 
##                 simensis                 sipeodon               sparverius 
##                        1                        1                        1 
##             spectrabilis        spilota imbricata                spinifera 
##                        1                        1                        1 
##                splendens                stellaris                  striata 
##                        1                        1                        1 
##                 striatus                 stuartii                swainsoni 
##                        2                        1                        1 
##               sylvestris                  tauvina                    taxus 
##                        1                        1                        1 
##            tetradactylus                  tigrina                   tigris 
##                        1                        1                        2 
##              tinnunculus                torquilla                 torridus 
##                        1                        1                        1 
##               trevelyani               triangulum                  trichas 
##                        1                        1                        1 
##                trichrous              tridactylus             trifascialis 
##                        1                        1                        1 
##             trifasciatus              troglodytes                   trutta 
##                        1                        1                        1 
##                 tyrannus                    uncia                   undata 
##                        1                        1                        1 
##                undulatus             unguiculatus             unimaculatus 
##                        1                        1                        1 
##                  ursinus                    velox                   vermis 
##                        1                        1                        1 
##                   virens              virginianus             viridiflavus 
##                        4                        1                        1 
##                  viridis                  vittata                   wiedii 
##                        2                        1                        1 
##                    wolfi                 wrightii             yagouaroundi 
##                        1                        1                        1 
##                  zibetha 
##                        1
```

```r
herbivore <- filter(homerange, trophic.guild=="herbivore")
table(herbivore$species)
```

```
## 
##           aberti        aegyptius      aethiopicus africaeaustralis 
##                2                1                1                1 
##         africana        africanus        agassizii         agrestis 
##                1                1                1                1 
##            alces        americana       americanus            ammon 
##                1                2                2                1 
##          amoenus      antilopinus         antimena         apicalis 
##                1                1                1                1 
##        aquaticus         arcticus argenteocinereus             argi 
##                2                1                1                1 
##        assimilis       atlanticus        audeberti     aurofrenatum 
##                1                1                1                1 
##     avellanarius             axis         beecheyi      bezoarticus 
##                1                1                1                1 
##          bicolor         bicornis       biocellata            bison 
##                1                1                1                1 
##          bonasia          bonasus           bottae       buselaphus 
##                1                1                1                1 
##         caballus     californicus       callipygus   camelopardalis 
##                1                3                1                1 
##          camelus       campestris       canadensis        cannabina 
##                1                1                1                1 
##         capensis        capreolus       carbonaria     carolinensis 
##                2                1                1                1 
##    caryocatactes          chromis     chrysopterum          cinerea 
##                1                1                1                1 
##      columbianus          cooperi             crex        cuniculus 
##                1                1                1                1 
##  cupido pinnatus        curzoniae          cuvieri           cyanus 
##                1                1                1                1 
##          cyclura             dama       damarensis     dentirostris 
##                1                1                1                1 
##         dorsalis         dorsatum          elaphus       erythropus 
##                3                1                1                1 
##        europaeus      flagellifer      flavicollis     flaviventris 
##                1                1                1                1 
##           flavus       floridanus         fraenata       franklinii 
##                1                1                1                1 
##          fulgens      fuliginosus         fuscipes           fuscus 
##                1                1                1                2 
##         gaimardi          galloti          gazella        giganteus 
##                1                1                1                1 
##           glaber           graeca        guentheri      habroptilus 
##                1                1                1                1 
##         hemionus         hermanii           hircus         hispidua 
##                1                1                1                1 
##       horsfieldi      hottentotus       hudsonicus        hurrianae 
##                1                1                1                1 
##       idahoensis         impressa             inca           indica 
##                1                1                1                1 
##           ingens            iseri        johnstoni       kleinmanni 
##                1                1                1                1 
##         krefftii          lagopus           lepida          leprosa 
##                1                1                1                1 
##           lervia           lewisi         lineatus              lis 
##                1                1                1                1 
##        lituratus         longipes        lumholtzi            major 
##                1                1                1                1 
##          maximus     megacephalus         melampus      melanoleuca 
##                2                1                1                1 
##         merriami         micropus      microrhinos          minimus 
##                1                1                1                1 
##            monax         montanus            niger      nigricollis 
##                1                1                1                1 
##           nippon           obesus         obscurus      ochrogaster 
##                1                1                1                1 
##         ocularis            ordii           ornata             oryx 
##                1                1                2                1 
##        palliatus         pallidus         palumbus        palustris 
##                1                1                1                1 
##         pardalis          parryii         partitus        patagonus 
##                1                1                1                1 
##           pecari         pennanti          pennata   pennsylvanicus 
##                1                1                1                1 
##           perdix        pinetorum          pinguis       polyphemus 
##                1                1                1                1 
##      prehensilis         princeps             puda          pumilio 
##                1                1                1                1 
##        pyrenaica   quadrivittatus        raimondii      raviventris 
##                1                1                1                1 
##          reevesi      richardsoni        rivulatus         robustus 
##                1                1                1                1 
##       rubripinne             rufa      rufogriseus            rufus 
##                1                1                1                2 
##        rupicapra         sabrinus            salpa     schisticolor 
##                1                1                1                1 
##         scriptus        sectatrix     semispinosus        sibiricus 
##                1                1                1                2 
##            simum      spectabilis           spekii        spilosoma 
##                1                1                1                1 
##        stephensi       stigmatica         strepera     strepsiceros 
##                1                1                1                1 
##          suillus       sylvaticus           tajacu         tarandus 
##                1                1                1                1 
##            telum        tentorius           tetrix           thetis 
##                1                1                1                1 
##          timidus        torquatus     travancorica tridecemlineatus 
##                1                1                1                1 
##           turtur         umbrinus        unicornis        urogallus 
##                1                1                1                1 
##     urophasianus          ursinus       variabilis       variegatus 
##                1                1                1                1 
##      virginianus           viride           volans         vulgaris 
##                1                1                2                1 
##        vulpecula          wagneri            wardi        zibethica 
##                1                1                1                1
```


**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivore <- filter(homerange, trophic.guild=="carnivore")
```

```r
herbivore <- filter(homerange, trophic.guild=="herbivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
mean(herbivore$mean.hra.m2, na.rm=T)
```

```
## [1] 34137012
```

```r
mean(carnivore$mean.hra.m2, na.rm=T)
```

```
## [1] 13039918
```

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
deer <- filter(homerange, family=="cervidae")
deer_updated <- select(deer, "mean.mass.g","log10.mass","family", "genus", "species")
view(deer_updated)
#alces alces is the largest species
```

```r
view(deer)
#common name for alces alces is moose
```


**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**  

```r
snakes <- filter(homerange, taxon=="snakes")
view(snakes)
#arranging the data by mean.hra.m2 in ascending order, you'll see that the namaqua dwarf adder has the smallest homerange with its mean.hra.m2 = 200
#namaqua dwarf adders are considered threatened due to mining, off-road driving and illegal collecting. They are also mildly venomous.They are found in the coastal dunes of Namaqualand and southern Namibia. They eat lizards and rain frogs
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
