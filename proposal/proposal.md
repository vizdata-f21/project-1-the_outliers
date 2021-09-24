Project proposal
================
The Outliers

## Load Packages

``` r
library(tidyverse)
library(dplyr)
```

## Dataset

``` r
youtube <- readr::read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-03-02/youtube.csv")
```

    ## Rows: 247 Columns: 25

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (10): brand, superbowl_ads_dot_com_url, youtube_url, id, kind, etag, ti...
    ## dbl   (7): year, view_count, like_count, dislike_count, favorite_count, comm...
    ## lgl   (7): funny, show_product_quickly, patriotic, celebrity, danger, animal...
    ## dttm  (1): published_at

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
summary(youtube)
```

    ##       year         brand           superbowl_ads_dot_com_url youtube_url       
    ##  Min.   :2000   Length:247         Length:247                Length:247        
    ##  1st Qu.:2005   Class :character   Class :character          Class :character  
    ##  Median :2010   Mode  :character   Mode  :character          Mode  :character  
    ##  Mean   :2010                                                                  
    ##  3rd Qu.:2015                                                                  
    ##  Max.   :2020                                                                  
    ##                                                                                
    ##    funny         show_product_quickly patriotic       celebrity      
    ##  Mode :logical   Mode :logical        Mode :logical   Mode :logical  
    ##  FALSE:76        FALSE:78             FALSE:206       FALSE:176      
    ##  TRUE :171       TRUE :169            TRUE :41        TRUE :71       
    ##                                                                      
    ##                                                                      
    ##                                                                      
    ##                                                                      
    ##    danger         animals         use_sex             id           
    ##  Mode :logical   Mode :logical   Mode :logical   Length:247        
    ##  FALSE:172       FALSE:155       FALSE:181       Class :character  
    ##  TRUE :75        TRUE :92        TRUE :66        Mode  :character  
    ##                                                                    
    ##                                                                    
    ##                                                                    
    ##                                                                    
    ##      kind               etag             view_count          like_count    
    ##  Length:247         Length:247         Min.   :       10   Min.   :     0  
    ##  Class :character   Class :character   1st Qu.:     6431   1st Qu.:    19  
    ##  Mode  :character   Mode  :character   Median :    41379   Median :   130  
    ##                                        Mean   :  1407556   Mean   :  4146  
    ##                                        3rd Qu.:   170016   3rd Qu.:   527  
    ##                                        Max.   :176373378   Max.   :275362  
    ##                                        NA's   :16          NA's   :22      
    ##  dislike_count     favorite_count comment_count    
    ##  Min.   :    0.0   Min.   :0      Min.   :   0.00  
    ##  1st Qu.:    1.0   1st Qu.:0      1st Qu.:   1.00  
    ##  Median :    7.0   Median :0      Median :  10.00  
    ##  Mean   :  833.5   Mean   :0      Mean   : 188.64  
    ##  3rd Qu.:   24.0   3rd Qu.:0      3rd Qu.:  50.75  
    ##  Max.   :92990.0   Max.   :0      Max.   :9190.00  
    ##  NA's   :22        NA's   :16     NA's   :25       
    ##   published_at                    title           description       
    ##  Min.   :2006-02-06 10:02:36   Length:247         Length:247        
    ##  1st Qu.:2009-02-02 03:59:35   Class :character   Class :character  
    ##  Median :2013-01-31 09:13:55   Mode  :character   Mode  :character  
    ##  Mean   :2012-12-23 22:41:37                                        
    ##  3rd Qu.:2016-04-09 11:09:50                                        
    ##  Max.   :2021-01-27 13:11:29                                        
    ##  NA's   :16                                                         
    ##   thumbnail         channel_title       category_id   
    ##  Length:247         Length:247         Min.   : 1.00  
    ##  Class :character   Class :character   1st Qu.:17.00  
    ##  Mode  :character   Mode  :character   Median :23.00  
    ##                                        Mean   :19.32  
    ##                                        3rd Qu.:24.00  
    ##                                        Max.   :29.00  
    ##                                        NA's   :16

``` r
glimpse(youtube)
```

    ## Rows: 247
    ## Columns: 25
    ## $ year                      <dbl> 2018, 2020, 2006, 2018, 2003, 2020, 2020, 20…
    ## $ brand                     <chr> "Toyota", "Bud Light", "Bud Light", "Hynudai…
    ## $ superbowl_ads_dot_com_url <chr> "https://superbowl-ads.com/good-odds-toyota/…
    ## $ youtube_url               <chr> "https://www.youtube.com/watch?v=zeBZvwYQ-hA…
    ## $ funny                     <lgl> FALSE, TRUE, TRUE, FALSE, TRUE, TRUE, TRUE, …
    ## $ show_product_quickly      <lgl> FALSE, TRUE, FALSE, TRUE, TRUE, TRUE, FALSE,…
    ## $ patriotic                 <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FA…
    ## $ celebrity                 <lgl> FALSE, TRUE, FALSE, FALSE, FALSE, TRUE, TRUE…
    ## $ danger                    <lgl> FALSE, TRUE, TRUE, FALSE, TRUE, TRUE, FALSE,…
    ## $ animals                   <lgl> FALSE, FALSE, TRUE, FALSE, TRUE, TRUE, TRUE,…
    ## $ use_sex                   <lgl> FALSE, FALSE, FALSE, FALSE, TRUE, FALSE, FAL…
    ## $ id                        <chr> "zeBZvwYQ-hA", "nbbp0VW7z8w", "yk0MQD5YgV8",…
    ## $ kind                      <chr> "youtube#video", "youtube#video", "youtube#v…
    ## $ etag                      <chr> "rn-ggKNly38Cl0C3CNjNnUH9xUw", "1roDoK-SYqSp…
    ## $ view_count                <dbl> 173929, 47752, 142310, 198, 13741, 23636, 30…
    ## $ like_count                <dbl> 1233, 485, 129, 2, 20, 115, 1470, 78, 342, 7…
    ## $ dislike_count             <dbl> 38, 14, 15, 0, 3, 11, 384, 6, 7, 0, 14, 0, 2…
    ## $ favorite_count            <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    ## $ comment_count             <dbl> NA, 14, 9, 0, 2, 13, 227, 6, 30, 0, 8, 1, 13…
    ## $ published_at              <dttm> 2018-02-03 11:29:14, 2020-01-31 21:04:13, 2…
    ## $ title                     <chr> "Toyota Super Bowl Commercial 2018 Good Odds…
    ## $ description               <chr> "Toyota Super Bowl Commercial 2018 Good Odds…
    ## $ thumbnail                 <chr> "https://i.ytimg.com/vi/zeBZvwYQ-hA/sddefaul…
    ## $ channel_title             <chr> "Funny Commercials", "VCU Brandcenter", "Joh…
    ## $ category_id               <dbl> 1, 27, 17, 22, 24, 1, 24, 2, 24, 24, 24, 24,…

``` r
names(youtube)
```

    ##  [1] "year"                      "brand"                    
    ##  [3] "superbowl_ads_dot_com_url" "youtube_url"              
    ##  [5] "funny"                     "show_product_quickly"     
    ##  [7] "patriotic"                 "celebrity"                
    ##  [9] "danger"                    "animals"                  
    ## [11] "use_sex"                   "id"                       
    ## [13] "kind"                      "etag"                     
    ## [15] "view_count"                "like_count"               
    ## [17] "dislike_count"             "favorite_count"           
    ## [19] "comment_count"             "published_at"             
    ## [21] "title"                     "description"              
    ## [23] "thumbnail"                 "channel_title"            
    ## [25] "category_id"

We chose to use the Superbowl Ad dataset which contains a list of ads
from the 10 brands that had the most advertisements in Super Bowls from
2000 to 2020. The dataset came from FiveThirtyEight, but it was
originally sourced from superbowl-ads.com. The dataset has 247 rows and
25 columns. Each row represents an Superbowl ad aired between 2000 to
2020 with 25 characteristics. We chose to use this dataset because we
all love Superbowl ads, and we were initially interested in viewing
trends over time. This dataset has a variable dedicated to the ad’s
published date and several variables surrounding viewer preferences.

## Questions

#### Question 1

We would like to explore how content trends change over time. We will
leverage the following variables to answer this question: `funny`,
`show_product_quickly`, `patriotic`, `celebrity`, `danger`, `animals`,
`use_sex`, `like_count year`. By examining the prevalence of these
characteristics over time, we should be able to see how companies have
changed their approach to advertising. It is difficult to say how all of
these different content types have changed over time, but we do believe
that use patriotic marketing has likely decreased recently. We look
forward to exploring whether this hypothesis is correct and seeing how
the patterns of the variables have changed as well.

``` r
Q1data <- youtube %>%
  select(funny, show_product_quickly, patriotic, celebrity, danger, animals, use_sex, like_count, year)

glimpse(Q1data)
```

    ## Rows: 247
    ## Columns: 9
    ## $ funny                <lgl> FALSE, TRUE, TRUE, FALSE, TRUE, TRUE, TRUE, FALSE…
    ## $ show_product_quickly <lgl> FALSE, TRUE, FALSE, TRUE, TRUE, TRUE, FALSE, FALS…
    ## $ patriotic            <lgl> FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, FALSE, …
    ## $ celebrity            <lgl> FALSE, TRUE, FALSE, FALSE, FALSE, TRUE, TRUE, TRU…
    ## $ danger               <lgl> FALSE, TRUE, TRUE, FALSE, TRUE, TRUE, FALSE, FALS…
    ## $ animals              <lgl> FALSE, FALSE, TRUE, FALSE, TRUE, TRUE, TRUE, FALS…
    ## $ use_sex              <lgl> FALSE, FALSE, FALSE, FALSE, TRUE, FALSE, FALSE, F…
    ## $ like_count           <dbl> 1233, 485, 129, 2, 20, 115, 1470, 78, 342, 7, 46,…
    ## $ year                 <dbl> 2018, 2020, 2006, 2018, 2003, 2020, 2020, 2020, 2…

We chose not to use published\_date for our time series analyses because
some of the videos were uploaded years later than they initially ran on
live television.

#### Question 2

For our second question, we would like to explore which brands are most
popular among viewers on Youtube. Specifically, for each brand
represented in the data, we plan to look at what proportion of the
reactions (likes + dislikes) each brand receives on their Super Bowl
commercials. We plan to look at the proportion of likes, on average,
over the history of the dataset. We may also explore how the proportion
of likes changes over time, as some brands may have increased /
decreased in popularity over time.

We would like to explore this question because we are interested in
discovering which brands are received best by those who watch Super Bowl
commercials. That way, next time we all watch the Super Bowl, we know
which ads are likely to be best. This analysis should also provide some
insight into which brands are more popular generally, which should be
interesting to see as well.

``` r
Q2data <- youtube %>%
  select(brand, like_count, dislike_count, year)

glimpse(Q2data)
```

    ## Rows: 247
    ## Columns: 4
    ## $ brand         <chr> "Toyota", "Bud Light", "Bud Light", "Hynudai", "Bud Ligh…
    ## $ like_count    <dbl> 1233, 485, 129, 2, 20, 115, 1470, 78, 342, 7, 46, 9, 133…
    ## $ dislike_count <dbl> 38, 14, 15, 0, 3, 11, 384, 6, 7, 0, 14, 0, 24, 10, 7445,…
    ## $ year          <dbl> 2018, 2020, 2006, 2018, 2003, 2020, 2020, 2020, 2020, 20…

We chose not to use `published_date` for our time series analyses
because some of the videos were uploaded years later than they initially
ran on live television.

## Analysis plan

To address Question 1, we plan on creating two plots:

To address Question 1, we will first have to create a new variable that
counts the occurrence of different content types for each year in the
dataset. There are 7 different content types (`funny`,
`show_product_quickly`, `patriotic`, `celebrity`, `danger`, `animals`,
or `use_sex`) and so we will generate 7 new variables (`funny_count`,
`show_product_quickly_count`, `patriotic_count`, `celebrity_count`,
`danger_count`, `animals_count`, `use_sex_count`) that count the
occurrence of each of these content tags. For example, if there are 7
commercials in 2000 that are tagged as `funny`, the new variable
`funny_count` will equal 7 for that year. Videos that do not have
content tags will be completely omitted from the analysis. This plot is
best for our question because it will clearly show how the use of
different content types has changed over time. The second plot will be a
deep dive into one content area. After creating the first plot and
conducting a simple analysis, we will choose a content area that has an
interesting trend (prevalence has increased / decreased significantly,
prevalence fluctuates significantly, etc.). For all the videos that
contain the category we choose, we will use `geom_point` to look at the
relationship between `like_count` (x-axis) and `view_count` (y-axis). In
addition, we will color the observations by `brand` to see if there is
any interaction there with respect to this relationship. This way we can
identify any brands that have unique relationships between `like_counts`
and `view_counts` in the content area of our choosing, which may help
explain whatever pattern we originally identify.

To address Question 2, we plan on creating two plots:

For the first step of our analysis, we will look at the proportion of
likes each brand receives in a new variable called
`proportion_likes_total`. To calculate this variable, we first need to
sum the total number of likes and dislikes each brand receives across
all of its advertisements in the dataset. We will then calculate
`proportion_likes_total` for each brand based on the cumulative
proportion of likes to total reactions (likes + dislikes). To visualize
this information, each of the 10 brand’s proportion of likes will be
represented in a stacked bar chart. We will determine the appropriate
axis orientation for this information once we have started our analysis.

Our second plot will explore like/dislike trends by brand over time. We
are going to pick the top three brands based on our previous analysis
(highest proportion of likes). To see how brand popularity has changed
over time, we will need to create a new variable for the brands we
select: `proportion_likes_yearly`. Unlike the variable used in the first
visualization, this variable will look at the proportion of likes each
brand receives for each year they are represented in the dataset. In
this case, `proportion_likes_yearly` will be on the y-axis, and `year`
will be on the x-axis. This graph will show us trends in the proportion
of likes for the three most popular brands. One issue we may run into is
that every brand we select may not have a commercial from each year. We
may have to carefully select the time period we represent in our
analysis so that each brand has an observation for every year we plot.

Both of our questions use the variables in the original dataset:
Superbowl Ads. Therefore, we do not need to merge any external data.
