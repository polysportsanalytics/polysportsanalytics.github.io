---
layout: post
title: Lahman Package in R
tags: [Baseball]
---

Exploratory Data Analysis
=========================

Traditionally the first step in any good data analysis is to "explore the data". In this step, the researcher will take the data and experiment with any possible relationships that they think might be present in the data. In the following notebook we will provide a brief example of exploratory data analysis with the Lahman Batting data.

Lahman Data
-----------

Sean Lahman has compiled historical baseball data for the years 1871 - 2015 for both Batting and Pitching. In this notebook we will first install the neccesary packages to work with the data and then we will take a closer look at the Batting data available through the Lahman package for R.

### Installing the Lahman Package

To be able to access the Batting data we first must install the Lahman package and then load it into our R session. Then we will load the Batting dataframe from the Lahman package using the data command.

``` r
install.packages("Lahman")
library(Lahman)

data(Batting)
```

Exploring the Data
------------------

### Individual Player Statistics

Now that we have the Batting dataframe loaded into our R session let's take a look and see what the data has to offer. First we will look to see the dimensions of the data, this is the number of variables and entires that constitute the data. We will then next look at a number of the entries to see what types of variables are being recorded.

``` r
# This will output the number of rows and columns in the dataset
dim(Batting)
```

    ## [1] 101332     22

From the output we can see that we have over 100,000 entries and 22 variables collected. Next we will take a look at the names of the variables.

``` r
# This will dsiplay the names of the columns
names(Batting)
```

    ##  [1] "playerID" "yearID"   "stint"    "teamID"   "lgID"     "G"       
    ##  [7] "AB"       "R"        "H"        "X2B"      "X3B"      "HR"      
    ## [13] "RBI"      "SB"       "CS"       "BB"       "SO"       "IBB"     
    ## [19] "HBP"      "SH"       "SF"       "GIDP"

If you want to learn more about what each of the column names represent you can use the following command which will open the help file for the Batting dataframe.

``` r
?Batting
```

Here we will look to see what type of data is contained for each column. In R the different columns of a dataframe do not have to have the same type of data, but the entries in the column will all have the same data type. To illustrate this we use the following command to check the data type of each column.

``` r
# This will display the type of each variable
sapply(Batting, class)
```

    ##    playerID      yearID       stint      teamID        lgID           G
    ## "character"   "integer"   "integer"    "factor"    "factor"   "integer"
    ##          AB           R           H         X2B         X3B          HR
    ##   "integer"   "integer"   "integer"   "integer"   "integer"   "integer"
    ##         RBI          SB          CS          BB          SO         IBB
    ##   "integer"   "integer"   "integer"   "integer"   "integer"   "integer"
    ##         HBP          SH          SF        GIDP
    ##   "integer"   "integer"   "integer"   "integer"

Looking at the data types of the columns we see that ost of our variables are of the type integer. The rest are of the cahracter type (This is R's name for strings) or are of the factor type. Factor variables are those that have a natural ordering to them. An example of this would be the cardinal numbers. We can check the order that is set for the variables using the `levels()` command.

``` r
levels(Batting$teamID)
```

    ##   [1] "ALT" "ANA" "ARI" "ATL" "BAL" "BFN" "BFP" "BL1" "BL2" "BL3" "BL4"
    ##  [12] "BLA" "BLF" "BLN" "BLU" "BOS" "BR1" "BR2" "BR3" "BR4" "BRF" "BRO"
    ##  [23] "BRP" "BS1" "BS2" "BSN" "BSP" "BSU" "BUF" "CAL" "CH1" "CH2" "CHA"
    ##  [34] "CHF" "CHN" "CHP" "CHU" "CIN" "CL1" "CL2" "CL3" "CL4" "CL5" "CL6"
    ##  [45] "CLE" "CLP" "CN1" "CN2" "CN3" "CNU" "COL" "DET" "DTN" "ELI" "FLO"
    ##  [56] "FW1" "HAR" "HOU" "HR1" "IN1" "IN2" "IN3" "IND" "KC1" "KC2" "KCA"
    ##  [67] "KCF" "KCN" "KCU" "KEO" "LAA" "LAN" "LS1" "LS2" "LS3" "MIA" "MID"
    ##  [78] "MIL" "MIN" "ML1" "ML2" "ML3" "ML4" "MLA" "MLU" "MON" "NEW" "NH1"
    ##  [89] "NY1" "NY2" "NY3" "NY4" "NYA" "NYN" "NYP" "OAK" "PH1" "PH2" "PH3"
    ## [100] "PH4" "PHA" "PHI" "PHN" "PHP" "PHU" "PIT" "PRO" "PT1" "PTF" "PTP"
    ## [111] "RC1" "RC2" "RIC" "SDN" "SE1" "SEA" "SFN" "SL1" "SL2" "SL3" "SL4"
    ## [122] "SL5" "SLA" "SLF" "SLN" "SLU" "SPU" "SR1" "SR2" "TBA" "TEX" "TL1"
    ## [133] "TL2" "TOR" "TRN" "TRO" "WAS" "WIL" "WOR" "WS1" "WS2" "WS3" "WS4"
    ## [144] "WS5" "WS6" "WS7" "WS8" "WS9" "WSU"

``` r
levels(Batting$lgID)
```

    ## [1] "AA" "AL" "FL" "NA" "NL" "PL" "UA"

``` r
# The knitr::kable() function is used to output as a table
# The head() function dsiplays the first couple of enties from a dataframe
knitr::kable(head(Batting))
```

| playerID  |  yearID|  stint| teamID | lgID |    G|   AB|    R|    H|  X2B|  X3B|   HR|  RBI|   SB|   CS|   BB|   SO|  IBB|  HBP|   SH|   SF|  GIDP|
|:----------|-------:|------:|:-------|:-----|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|----:|-----:|
| abercda01 |    1871|      1| TRO    | NA   |    1|    4|    0|    0|    0|    0|    0|    0|    0|    0|    0|    0|   NA|   NA|   NA|   NA|    NA|
| addybo01  |    1871|      1| RC1    | NA   |   25|  118|   30|   32|    6|    0|    0|   13|    8|    1|    4|    0|   NA|   NA|   NA|   NA|    NA|
| allisar01 |    1871|      1| CL1    | NA   |   29|  137|   28|   40|    4|    5|    0|   19|    3|    1|    2|    5|   NA|   NA|   NA|   NA|    NA|
| allisdo01 |    1871|      1| WS3    | NA   |   27|  133|   28|   44|   10|    2|    2|   27|    1|    1|    0|    2|   NA|   NA|   NA|   NA|    NA|
| ansonca01 |    1871|      1| RC1    | NA   |   25|  120|   29|   39|   11|    3|    0|   16|    6|    2|    2|    1|   NA|   NA|   NA|   NA|    NA|
| armstbo01 |    1871|      1| FW1    | NA   |   12|   49|    9|   11|    2|    1|    0|    5|    0|    1|    0|    1|   NA|   NA|   NA|   NA|    NA|

To get a summary of all of the variables we use the `summarize()` function which will return the max, min 1st Quartile, Mean, Median, 3rd Quartile, and the count of entries with no data for that variable (NA's).

``` r
summary(Batting)
```

    ##    playerID             yearID         stint           teamID     
    ##  Length:101332      Min.   :1871   Min.   :1.000   CHN    : 4818  
    ##  Class :character   1st Qu.:1933   1st Qu.:1.000   PHI    : 4721  
    ##  Mode  :character   Median :1972   Median :1.000   PIT    : 4667  
    ##                     Mean   :1964   Mean   :1.078   SLN    : 4627  
    ##                     3rd Qu.:1997   3rd Qu.:1.000   CIN    : 4488  
    ##                     Max.   :2015   Max.   :5.000   CLE    : 4451  
    ##                                                    (Other):73560  
    ##  lgID             G                AB             R         
    ##  AA: 1890   Min.   :  0.00   Min.   :  0    Min.   :  0.00  
    ##  AL:46371   1st Qu.: 13.00   1st Qu.:  7    1st Qu.:  0.00  
    ##  FL:  470   Median : 34.00   Median : 57    Median :  5.00  
    ##  NA:  737   Mean   : 51.40   Mean   :150    Mean   : 19.89  
    ##  NL:51385   3rd Qu.: 80.25   3rd Qu.:251    3rd Qu.: 30.00  
    ##  PL:  147   Max.   :165.00   Max.   :716    Max.   :192.00  
    ##  UA:  332                    NA's   :5149   NA's   :5149    
    ##        H               X2B              X3B               HR        
    ##  Min.   :  0.00   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:  1.00   1st Qu.: 0.000   1st Qu.: 0.000   1st Qu.: 0.000  
    ##  Median : 11.00   Median : 1.000   Median : 0.000   Median : 0.000  
    ##  Mean   : 39.26   Mean   : 6.637   Mean   : 1.373   Mean   : 2.949  
    ##  3rd Qu.: 63.00   3rd Qu.:10.000   3rd Qu.: 2.000   3rd Qu.: 3.000  
    ##  Max.   :262.00   Max.   :67.000   Max.   :36.000   Max.   :73.000  
    ##  NA's   :5149     NA's   :5149     NA's   :5149     NA's   :5149    
    ##       RBI               SB                CS               BB        
    ##  Min.   :  0.00   Min.   :  0.000   Min.   : 0.000   Min.   :  0.00  
    ##  1st Qu.:  0.00   1st Qu.:  0.000   1st Qu.: 0.000   1st Qu.:  0.00  
    ##  Median :  4.00   Median :  0.000   Median : 0.000   Median :  3.00  
    ##  Mean   : 17.96   Mean   :  3.158   Mean   : 1.324   Mean   : 13.81  
    ##  3rd Qu.: 27.00   3rd Qu.:  2.000   3rd Qu.: 1.000   3rd Qu.: 20.00  
    ##  Max.   :191.00   Max.   :138.000   Max.   :42.000   Max.   :232.00  
    ##  NA's   :5573     NA's   :6449      NA's   :28603    NA's   :5149    
    ##        SO              IBB              HBP               SH        
    ##  Min.   :  0.00   Min.   :  0.00   Min.   : 0.000   Min.   : 0.000  
    ##  1st Qu.:  2.00   1st Qu.:  0.00   1st Qu.: 0.000   1st Qu.: 0.000  
    ##  Median : 10.00   Median :  0.00   Median : 0.000   Median : 1.000  
    ##  Mean   : 21.63   Mean   :  1.21   Mean   : 1.113   Mean   : 2.458  
    ##  3rd Qu.: 30.00   3rd Qu.:  1.00   3rd Qu.: 1.000   3rd Qu.: 3.000  
    ##  Max.   :223.00   Max.   :120.00   Max.   :51.000   Max.   :67.000  
    ##  NA's   :12987    NA's   :41712    NA's   :7959     NA's   :11487   
    ##        SF             GIDP      
    ##  Min.   : 0.00   Min.   : 0.00  
    ##  1st Qu.: 0.00   1st Qu.: 0.00  
    ##  Median : 0.00   Median : 1.00  
    ##  Mean   : 1.15   Mean   : 3.21  
    ##  3rd Qu.: 2.00   3rd Qu.: 5.00  
    ##  Max.   :19.00   Max.   :36.00  
    ##  NA's   :41181   NA's   :31257

We can see some interesting things here. Some poor sap was hit by a pitch 51 times in a season.

### Team Statistics

In this section we will aggregate the data for the individuals and use them to create team level data. To do this we will make use of the tidyverse package created by Hadley Wickham. This package was designed to simplify the "tidying up" of datasaets. To learn more about this package from Hadley Wickham himself just read his book available for free at the following link <http://r4ds.had.co.nz/>.

### Installing tidyverse

Since tidyverse is not a built-in package we need to install it with the `install.packages()` command. We then need to load it using `library()`.

``` r
install.packages("tidyverse")
library(tidyverse)
```

One of the features od the tidyverse package that we would like to focus on is the pipe operator `%>%`. The easiest way to think of this operator is to compare it to how functions are composed mathematically. That is, it takes the ouptut of one function as the input for the next. We will give break down an example of how to use the pipe operator.

``` r
Teams <- Batting %>%
  filter(!is.na(H)) %>%
  group_by(teamID, yearID, lgID) %>%
  summarise(
    Hits = sum(H),
    AtBats = sum(AB),
    AVG = Hits / AtBats
  ) %>%
  arrange(desc(AVG))
```

In the the first line we take our Batting dataframe and pipe it into our filter function. We use the filter to take from the list the players that did not have an official hit in a year. We then group it by team, year, and league. We then summarise the data, by creating the Hits, Atbats, and AVG variables.

``` r
knitr::kable(head(Teams))
```

| teamID |  yearID| lgID |  Hits|  AtBats|        AVG|
|:-------|-------:|:-----|-----:|-------:|----------:|
| PHI    |    1894| NL   |  1732|    4967|  0.3487014|
| BLN    |    1894| NL   |  1647|    4799|  0.3431965|
| BS1    |    1873| NA   |   930|    2755|  0.3375681|
| CHN    |    1876| NL   |   926|    2748|  0.3369723|
| BSN    |    1894| NL   |  1658|    5011|  0.3308721|
| PHI    |    1895| NL   |  1664|    5037|  0.3303554|

``` r
knitr::kable(tail(Teams))
```

| teamID |  yearID| lgID |  Hits|  AtBats|        AVG|
|:-------|-------:|:-----|-----:|-------:|----------:|
| BR2    |    1875| NA   |   304|    1562|  0.1946223|
| WS6    |    1875| NA   |   194|    1004|  0.1932271|
| KEO    |    1875| NA   |    81|     449|  0.1804009|
| SPU    |    1884| UA   |    49|     272|  0.1801471|
| WIL    |    1884| UA   |    91|     521|  0.1746641|
| BL4    |    1873| NA   |    33|     211|  0.1563981|

Looking at the top and bottom six teams for bating average we can see that all of them happened before the turn of the 20th century. We can also see that all of the bottom teams were from leagues other than the current AL or NL. Let us filter these results so that we have teams from the current Major Leagues.

``` r
Teams_Modern <- filter(Teams, lgID == "AL" | lgID == "NL")
```

``` r
knitr::kable(head(Teams_Modern))
```

| teamID |  yearID| lgID |  Hits|  AtBats|        AVG|
|:-------|-------:|:-----|-----:|-------:|----------:|
| PHI    |    1894| NL   |  1732|    4967|  0.3487014|
| BLN    |    1894| NL   |  1647|    4799|  0.3431965|
| CHN    |    1876| NL   |   926|    2748|  0.3369723|
| BSN    |    1894| NL   |  1658|    5011|  0.3308721|
| PHI    |    1895| NL   |  1664|    5037|  0.3303554|
| BLN    |    1896| NL   |  1548|    4719|  0.3280356|

``` r
knitr::kable(tail(Teams_Modern))
```

| teamID |  yearID| lgID |  Hits|  AtBats|        AVG|
|:-------|-------:|:-----|-----:|-------:|----------:|
| NYA    |    1968| AL   |  1137|    5310|  0.2141243|
| BRO    |    1908| NL   |  1044|    4897|  0.2131918|
| CHA    |    1910| AL   |  1058|    5024|  0.2105892|
| WS8    |    1886| NL   |   856|    4082|  0.2097011|
| DTN    |    1884| NL   |   825|    3970|  0.2078086|
| WS8    |    1888| NL   |   944|    4546|  0.2076551|

Looking at the top and bottom 6 for our filtered results we can see some changes, but overall the pattern remains the same with most of the highest and lowest values coming before the turn of the 20th century. We will examine this pattern further using a scatterplot of Year vs. Batting Average.

``` r
ggplot(Teams_Modern, aes(yearID, AVG)) + geom_point() +
         theme(legend.position =  "none")
```

![](/polysportsanalytics.github.io/public/img/unnamed-chunk-15-1.png)

From this plot we can get a general sense of the change in team batting averages over time, but there are still many ways that we can modify the plots to give us more insight into what is happening.

``` r
ggplot(Teams_Modern, aes(yearID, AVG)) + geom_point() + geom_smooth() +
         theme(legend.position =  "none")
```

    ## `geom_smooth()` using method = 'gam'

![](/polysportsanalytics.github.io/public/img/unnamed-chunk-16-1.png)

The `geom_smooth` adds a smooth curve to the data this helps us to see the trend a little mre readily than in our previous graph, but this tells us nothing about the league specific trends. To do this we will add one more option to our graph.

``` r
ggplot(Teams_Modern, aes(yearID, AVG, color = lgID)) + geom_point() + geom_smooth()
```

    ## `geom_smooth()` using method = 'gam'

![](/polysportsanalytics.github.io/public/img/unnamed-chunk-17-1.png)
