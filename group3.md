group3
================

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
