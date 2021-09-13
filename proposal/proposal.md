Project proposal
================
The Outliers

``` r
library(tidyverse)
```

    ## Warning in system("timedatectl", intern = TRUE): running command 'timedatectl'
    ## had status 1

``` r
library(dplyr)
```

## Dataset

``` r
youtube <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-03-02/youtube.csv')
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
head(youtube)
```

    ## # A tibble: 6 × 25
    ##    year brand     superbowl_ads_do… youtube_url funny show_product_qu… patriotic
    ##   <dbl> <chr>     <chr>             <chr>       <lgl> <lgl>            <lgl>    
    ## 1  2018 Toyota    https://superbow… https://ww… FALSE FALSE            FALSE    
    ## 2  2020 Bud Light https://superbow… https://ww… TRUE  TRUE             FALSE    
    ## 3  2006 Bud Light https://superbow… https://ww… TRUE  FALSE            FALSE    
    ## 4  2018 Hynudai   https://superbow… https://ww… FALSE TRUE             FALSE    
    ## 5  2003 Bud Light https://superbow… https://ww… TRUE  TRUE             FALSE    
    ## 6  2020 Toyota    https://superbow… https://ww… TRUE  TRUE             FALSE    
    ## # … with 18 more variables: celebrity <lgl>, danger <lgl>, animals <lgl>,
    ## #   use_sex <lgl>, id <chr>, kind <chr>, etag <chr>, view_count <dbl>,
    ## #   like_count <dbl>, dislike_count <dbl>, favorite_count <dbl>,
    ## #   comment_count <dbl>, published_at <dttm>, title <chr>, description <chr>,
    ## #   thumbnail <chr>, channel_title <chr>, category_id <dbl>

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

We chose to use the Superbowl Ad dataset. The dataset came from
FiveThirtyEight, but it was originally sourced from superbowl-ads.com.
The dataset has 247 rows and 25 columns. The variable names include
year, brand, superbowl\_ads\_dot\_com\_url, youtube\_url, funny,
show\_product\_quickly, patriotic, celebrity, danger, animals, use\_sex,
id, kind, etag, view\_count, like\_count, dislike\_count,
favorite\_count, comment\_count, published\_at, title, description,
thumbnail, channel\_title, and category\_id. We chose to use this
dataset because we all love Superbowl ads, and we were initially
interested in viewing trends over time. This dataset has a variable
dedicated to the ad’s published date and several variables surrounding
viewer preferences.

## Questions

#### Question 1

Question 1:

We would like to explore how content trends change over time. We will
leverage the following variables to answer this question funny,
show\_product\_quickly, patriotic, celebrity, danger, animals, use\_sex,
like\_count year. Specifically we will explore the distribution of
certain commercial content categories (funny, show\_product\_quickly
patriotic, celebrity, danger, animlas, use\_sex) over time. We are
interested in seeing the changes in commercial advertising over time. We
predict that patriotic themes in commericals would decrease over time.

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
popular amongst viewers on Youtube. Specifically, for each brand
represented in the data, we plan to look at what proportion of the
reactions (likes + dislikes) each brand receives on their Super Bowl
commercials. We plan to look at the proportion of likes and dislikes, on
average, over the history of the dataset. We may also explore how the
proportion of likes and dislikes changes over time, as some brands may
have increased / decreased in popularity over time.

We would like to explore this question, because we are interested in
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

We chose not to use published\_date for our time series analyses because
some of the videos were uploaded years later than they initially ran on
live television.

## Analysis plan

To address Question 1, we plan on creating two plots. The first plot
will be a geom\_line plot with year on the x-axis and like\_count on the
y-axis. We will color the lines by type of video, after creating a
variable type that encompasses whether the video is categorized as
“funny,” “show\_product\_quickly,” “patriotic,” “celebrity,” “danger,”
“animals,” or “use\_sex.” This plot is best for our question because it
will clearly show trends over time faceted by category, which is exactly
what we are trying to analyze. The second plot will be a deep dive into
one content area. After creating the first plot and conducting a simple
analysis, we will choose a content area that has an interesting trend
(e.g., very high likes in some years, very low likes in others). We will
dive into this category and analyze like\_count, view\_count, and
dislike\_count over the years with a faceted barplot.

To address Question 2, we plan on creating two plots:

For the first step of our analysis, we will look at the average
proportion of likes and dislikes for each brand across all the time
periods. To view this visually, we will create a new variable that first
finds the proportion of likes and dislikes out of total reactions (likes
and dislikes). We will then take the average of this proportion for each
brand across all time periods. The graph we plan to use to represent
this will be a 100% stacked bar chart. This should show which brands are
most well received on average.

Our second plot will explore like/dislike trends over time. We are going
to pick the top three brands based on our previous analysis (highest
proportion of likes). We will use geom\_line and color the lines by
brand. We will create a new variable called proportion\_likes, which
divides the number of likes (like\_count) by total reactions
(like\_count + dislike\_count). The proportion\_likes will be on the
y-axis, and the year will be on the x-axis. This graph will show us
trends in the proportion of likes for the three most popular brands.

Both of our questions use the variables in the original dataset:
Superbowl Ads. Therefore, we do not need to merge any external data.
