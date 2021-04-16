Progect Proposal Group 3 - Video Games Sales Dataset
================
Krist Adofo \| Taylor Memon \| Roey Stern \| Nicholas Metzger \|
Nicholas McKenna

**<u>Introduction</u>**

For our Data final project, we chose the “Video Game Sales” dataset from
**Kaggle.com.** All of the group members are fond of video games and we
thought it would be an interesting task to analyze data about video
games and explore relationships of video game characteristics and sales.

“Video Game Sales” was published by Gregory Smith on Kaggle in
2017PerPe. The dataset has a list of video games with sales of over
100,000 copies worldwide between the years 2007-2011. The data was
collected from the website VGChartz, which is a business intelligence
research firm that was founded in 2005 by Brett Walton. VGChartz offers
consumers access to their 55,000+ large database on video games which
includes sales data, reviews, news, and a forum.

The dataset is comprised of 11,493 variables (video games) and the
fields of the data set are:

-   <u>Rank</u> - Ranking of overall sales
-   <u>Name</u> - The games’ names
-   <u>Platform</u> - Platform of the games release (i.e. PC,PS4, etc.)
-   <u>Year</u> - Year of the game’s release
-   <u>Genre</u> - Genre of the game
-   <u>Publisher</u> - Publisher of the game
-   <u>NA\_Sales</u> - Sales in North America (in millions)
-   <u>EU\_Sales</u> - Sales in Europe (in millions)
-   <u>JP\_Sales</u> - Sales in Japan (in millions)
-   <u>Other\_Sales</u> - Sales in the rest of the world (in millions)
-   <u>Global\_Sales</u> - Total worldwide sales.

Looking at the data, we thought it would be interesting to find what was
the relationship between the genre of the video game and its sales
worldwide between the years 2007-2011.

**<u>Data</u>**

``` r
library(tidyverse)
library(skimr)
```

``` r
vgsales <- read_csv ("https://raw.githubusercontent.com/MU-DATA325/Group3/main/data/vgsales.csv")
 
skim(vgsales)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | vgsales |
| Number of rows                                   | 16598   |
| Number of columns                                | 11      |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 5       |
| numeric                                          | 6       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim\_variable | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
|:---------------|-----------:|---------------:|----:|----:|------:|----------:|-----------:|
| Name           |          0 |              1 |   1 | 132 |     0 |     11493 |          0 |
| Platform       |          0 |              1 |   2 |   4 |     0 |        31 |          0 |
| Year           |          0 |              1 |   3 |   4 |     0 |        40 |          0 |
| Genre          |          0 |              1 |   4 |  12 |     0 |        12 |          0 |
| Publisher      |          0 |              1 |   3 |  38 |     0 |       579 |          0 |

**Variable type: numeric**

| skim\_variable | n\_missing | complete\_rate |    mean |      sd |   p0 |     p25 |     p50 |      p75 |     p100 | hist  |
|:---------------|-----------:|---------------:|--------:|--------:|-----:|--------:|--------:|---------:|---------:|:------|
| Rank           |          0 |              1 | 8300.61 | 4791.85 | 1.00 | 4151.25 | 8300.50 | 12449.75 | 16600.00 | ▇▇▇▇▇ |
| NA\_Sales      |          0 |              1 |    0.26 |    0.82 | 0.00 |    0.00 |    0.08 |     0.24 |    41.49 | ▇▁▁▁▁ |
| EU\_Sales      |          0 |              1 |    0.15 |    0.51 | 0.00 |    0.00 |    0.02 |     0.11 |    29.02 | ▇▁▁▁▁ |
| JP\_Sales      |          0 |              1 |    0.08 |    0.31 | 0.00 |    0.00 |    0.00 |     0.04 |    10.22 | ▇▁▁▁▁ |
| Other\_Sales   |          0 |              1 |    0.05 |    0.19 | 0.00 |    0.00 |    0.01 |     0.04 |    10.57 | ▇▁▁▁▁ |
| Global\_Sales  |          0 |              1 |    0.54 |    1.56 | 0.01 |    0.06 |    0.17 |     0.47 |    82.74 | ▇▁▁▁▁ |

``` r
glimpse(vgsales)
```

    ## Rows: 16,598
    ## Columns: 11
    ## $ Rank         <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17…
    ## $ Name         <chr> "Wii Sports", "Super Mario Bros.", "Mario Kart Wii", "Wii…
    ## $ Platform     <chr> "Wii", "NES", "Wii", "Wii", "GB", "GB", "DS", "Wii", "Wii…
    ## $ Year         <chr> "2006", "1985", "2008", "2009", "1996", "1989", "2006", "…
    ## $ Genre        <chr> "Sports", "Platform", "Racing", "Sports", "Role-Playing",…
    ## $ Publisher    <chr> "Nintendo", "Nintendo", "Nintendo", "Nintendo", "Nintendo…
    ## $ NA_Sales     <dbl> 41.49, 29.08, 15.85, 15.75, 11.27, 23.20, 11.38, 14.03, 1…
    ## $ EU_Sales     <dbl> 29.02, 3.58, 12.88, 11.01, 8.89, 2.26, 9.23, 9.20, 7.06, …
    ## $ JP_Sales     <dbl> 3.77, 6.81, 3.79, 3.28, 10.22, 4.22, 6.50, 2.93, 4.70, 0.…
    ## $ Other_Sales  <dbl> 8.46, 0.77, 3.31, 2.96, 1.00, 0.58, 2.90, 2.85, 2.26, 0.4…
    ## $ Global_Sales <dbl> 82.74, 40.24, 35.82, 33.00, 31.37, 30.26, 30.01, 29.02, 2…

**<u>Data Analysis Plan</u>**

-   <u>Outcome (y)</u>: Global Sales
-   <u>Predictor (x)</u>: Genre
-   <u>Preliminary Exploratory Data Analysis</u>:
    -   Count all genres
    -   Find the most produced genre.
    -   Count sales worldwide between the years of 2007-2011
-   <u>Hypothesis</u>: The most produced genre also had the highest
    amount of sales worldwide.
-   <u>Methods</u>:
    -   1.  Find total sales for each genre

    -   2.  Compare total sales of each genre.

    -   3.  Find the most popular genre in the world.

***In order to not reject our hypothesis, our results should indicate
that the most produced genre also has the highest amount of sales.***
