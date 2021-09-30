Superbowl Ads
================
The Outliers

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    ## Loading required package: viridisLite

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

    ## 
    ## Attaching package: 'scales'

    ## The following object is masked from 'package:viridis':
    ## 
    ##     viridis_pal

    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard

    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

    ## New names:
    ## * `` -> ...1

    ## Warning: One or more parsing issues, see `problems()` for details

## Introduction

\[add in Hebron’s work\]

## Exploring how Super Bowl commercial content trends change over time

### Introduction

\[add in Hebron’s work\]

### Approach

\[(1-2 paragraphs) Describe what types of plots you are going to make to
address your question. For each plot, provide a clear explanation as to
why this plot (e.g. boxplot, barplot, histogram, etc.) is best for
providing the information you are asking about. The two plots should be
of different types, and at least one of the two plots needs to use
either color mapping or facets.\]

### Analysis

#### Wrangling data

``` r
q1_p1_data <- superbowl_data %>%
  group_by(year) %>%
  summarise(funny_count = sum(funny),
            show_product_quickly_count = sum(show_product_quickly),
            patriotic_count = sum(patriotic),
            celebrity_count = sum(celebrity),
            danger_count = sum(danger),
            animals_count = sum(animals),
            use_sex_count = sum(use_sex)) %>%
  pivot_longer(cols = c(funny_count, show_product_quickly_count, patriotic_count, celebrity_count, danger_count, animals_count, use_sex_count), names_to = "type")
```

#### Visualization one

``` r
ggplot(data = q1_p1_data, aes(x = year, y = value, color = type)) +
  geom_line() +
  labs(title = "Prevelance of Different Types of Ads Over Time", x = "Year", y = "Count")
```

![](README_files/figure-gfm/q1_p1_graph-1.png)<!-- -->

#### Visualization two

``` r
q1_p2_data <- superbowl_data %>%
  filter(show_product_quickly  == TRUE, 
         danger == TRUE, 
         celebrity == TRUE)
```

``` r
ggplot(data = q1_p2_data, aes(x = like_count, y = view_count, color = brand)) +
  geom_point() + 
  labs(title = "Proportion of Likes/Dislikes Over time for ads containing danger,
       celebrities, and shows_product_quickly", x = "Like_Count", y = "View_Count") + theme_minimal()
```

    ## Warning: Removed 1 rows containing missing values (geom_point).

![](README_files/figure-gfm/q1_p2_graph-1.png)<!-- -->

\[(2-3 code blocks, 2 figures, text/code comments as needed) In this
section, provide the code that generates your plots. Use scale functions
to provide nice axis labels and guides. You are welcome to use theme
functions to customize the appearance of your plot, but you are not
required to do so. All plots must be made with ggplot2. Do not use base
R or lattice plotting functions.\]

### Discussion

\[(1-3 paragraphs) In the Discussion section, interpret the results of
your analysis. Identify any trends revealed (or not revealed) by the
plots. Speculate about why the data looks the way it does.\]

## Exploring the most popular Super Bowl commercial brands

### Introduction

\[Hebron’s work here\]

### Approach

\[(1-2 paragraphs) Describe what types of plots you are going to make to
address your question. For each plot, provide a clear explanation as to
why this plot (e.g. boxplot, barplot, histogram, etc.) is best for
providing the information you are asking about. The two plots should be
of different types, and at least one of the two plots needs to use
either color mapping or facets.\]

### Analysis

``` r
q2_p1_data <- filter(superbowl_data, like_count != is.na(like_count) & dislike_count != is.na(dislike_count)) %>%
  group_by(brand) %>%
  mutate(likes_total = sum(like_count),
         dislikes_total = sum(dislike_count),
         proportion_likes_total = likes_total / (dislikes_total + likes_total))
```

![](README_files/figure-gfm/q2_p1_graph-1.png)<!-- -->

``` r
q2_p2_data <- superbowl_data %>%
  filter(brand == c("Kia", "NFL", "Pepsi", "E-Trade"))%>%
  group_by(year, brand) %>%
  mutate(proportion_likes_yearly = like_count / (like_count + dislike_count))
```

    ## Warning in brand == c("Kia", "NFL", "Pepsi", "E-Trade"): longer object length is
    ## not a multiple of shorter object length

``` r
ggplot(data = q2_p2_data, aes(x = year, y = proportion_likes_yearly, color = brand)) +
  geom_point() + 
  labs(title = "Proportion of Likes/Dislikes over time for the top 3 Brands", x = "Year", y = "Count") + theme_minimal()
```

    ## Warning: Removed 2 rows containing missing values (geom_point).

![](README_files/figure-gfm/q2_p2_graph-1.png)<!-- -->

\[(2-3 code blocks, 2 figures, text/code comments as needed) In this
section, provide the code that generates your plots. Use scale functions
to provide nice axis labels and guides. You are welcome to use theme
functions to customize the appearance of your plot, but you are not
required to do so. All plots must be made with ggplot2. Do not use base
R or lattice plotting functions.\]

### Discussion

(1-3 paragraphs) In the Discussion section, interpret the results of
your analysis. Identify any trends revealed (or not revealed) by the
plots. Speculate about why the data looks the way it does.

## Presentation

Our presentation can be found [here](presentation/presentation.html).

## Data

Include a citation for your data here. See
<http://libraryguides.vu.edu.au/c.php?g=386501&p=4347840> for guidance
on proper citation for datasets. If you got your data off the web, make
sure to note the retrieval date.

## References

List any references here. You should, at a minimum, list your data
source.
