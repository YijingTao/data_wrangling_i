Data manipulation
================

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.4     v dplyr   1.0.7
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   2.0.1     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

\#\#Load in the FAS Litters Data

``` r
litters_df = read_csv("./data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
```

    ## Warning in FUN(X[[i]], ...): strings not representable in native encoding will
    ## be translated to UTF-8

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00C4>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00D6>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00E4>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00F6>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00DF>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00C6>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00E6>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00D8>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00F8>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00C5>' to native encoding

    ## Warning in FUN(X[[i]], ...): unable to translate '<U+00E5>' to native encoding

``` r
pups_df = read_csv("data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df = janitor::clean_names(pups_df)
```

\#\#\#learning assessment

``` r
select(pups_df, litter_number, sex, pd_ears)
```

    ## # A tibble: 313 x 3
    ##    litter_number   sex pd_ears
    ##    <chr>         <dbl>   <dbl>
    ##  1 #85               1       4
    ##  2 #85               1       4
    ##  3 #1/2/95/2         1       5
    ##  4 #1/2/95/2         1       5
    ##  5 #5/5/3/83/3-3     1       5
    ##  6 #5/5/3/83/3-3     1       5
    ##  7 #5/4/2/95/2       1      NA
    ##  8 #4/2/95/3-3       1       4
    ##  9 #4/2/95/3-3       1       4
    ## 10 #2/2/95/3-2       1       4
    ## # ... with 303 more rows

``` r
pull(litters_df, group)
```

    ##  [1] "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con7" "Con8" "Con8" "Con8"
    ## [11] "Con8" "Con8" "Con8" "Con8" "Con8" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7"
    ## [21] "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Mod7" "Low7" "Low7" "Low7"
    ## [31] "Low7" "Low7" "Low7" "Low7" "Low7" "Mod8" "Mod8" "Mod8" "Mod8" "Mod8"
    ## [41] "Mod8" "Mod8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8" "Low8"

## `select`

Choose some columns and not others.

``` r
select(litters_df, group, litter_number)#tell select what column I want to keep__only keep the 'litter_number' column
```

    ## # A tibble: 49 x 2
    ##    group litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ... with 39 more rows

``` r
select(litters_df, group, gd0_weight,gd18_weight)
```

    ## # A tibble: 49 x 3
    ##    group gd0_weight gd18_weight
    ##    <chr>      <dbl>       <dbl>
    ##  1 Con7        19.7        34.7
    ##  2 Con7        27          42  
    ##  3 Con7        26          41.4
    ##  4 Con7        28.5        44.1
    ##  5 Con7        NA          NA  
    ##  6 Con7        NA          NA  
    ##  7 Con7        NA          NA  
    ##  8 Con8        NA          NA  
    ##  9 Con8        NA          NA  
    ## 10 Con8        28.5        NA  
    ## # ... with 39 more rows

``` r
select(litters_df, -litter_number)
```

    ## # A tibble: 49 x 7
    ##    group gd0_weight gd18_weight gd_of_birth pups_born_alive pups_dead_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>           <dbl>           <dbl>
    ##  1 Con7        19.7        34.7          20               3               4
    ##  2 Con7        27          42            19               8               0
    ##  3 Con7        26          41.4          19               6               0
    ##  4 Con7        28.5        44.1          19               5               1
    ##  5 Con7        NA          NA            20               6               0
    ##  6 Con7        NA          NA            20               6               0
    ##  7 Con7        NA          NA            20               9               0
    ##  8 Con8        NA          NA            20               9               1
    ##  9 Con8        NA          NA            20               8               0
    ## 10 Con8        28.5        NA            20               8               0
    ## # ... with 39 more rows, and 1 more variable: pups_survive <dbl>

``` r
select(litters_df, group, gd0_weight:gd_of_birth)#save the columns from `gd0_weight` to `gd_of_birth`
```

    ## # A tibble: 49 x 4
    ##    group gd0_weight gd18_weight gd_of_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>
    ##  1 Con7        19.7        34.7          20
    ##  2 Con7        27          42            19
    ##  3 Con7        26          41.4          19
    ##  4 Con7        28.5        44.1          19
    ##  5 Con7        NA          NA            20
    ##  6 Con7        NA          NA            20
    ##  7 Con7        NA          NA            20
    ##  8 Con8        NA          NA            20
    ##  9 Con8        NA          NA            20
    ## 10 Con8        28.5        NA            20
    ## # ... with 39 more rows

``` r
select(litters_df, -litter_number)#keep everything else except `litter_number` column
```

    ## # A tibble: 49 x 7
    ##    group gd0_weight gd18_weight gd_of_birth pups_born_alive pups_dead_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>           <dbl>           <dbl>
    ##  1 Con7        19.7        34.7          20               3               4
    ##  2 Con7        27          42            19               8               0
    ##  3 Con7        26          41.4          19               6               0
    ##  4 Con7        28.5        44.1          19               5               1
    ##  5 Con7        NA          NA            20               6               0
    ##  6 Con7        NA          NA            20               6               0
    ##  7 Con7        NA          NA            20               9               0
    ##  8 Con8        NA          NA            20               9               1
    ##  9 Con8        NA          NA            20               8               0
    ## 10 Con8        28.5        NA            20               8               0
    ## # ... with 39 more rows, and 1 more variable: pups_survive <dbl>

Renaming columns???

``` r
select(litters_df, GROUP = group, LITTer_NUmBer = litter_number)#pick out the columns and change the name of the column
```

    ## # A tibble: 49 x 2
    ##    GROUP LITTer_NUmBer  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ... with 39 more rows

``` r
rename(litters_df, GROUP = group, LITTer_NUmBer = litter_number)#save all the columns and rename one or several of them
```

    ## # A tibble: 49 x 8
    ##    GROUP LITTer_NUmBer   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

Select helpers

``` r
select(litters_df, starts_with("gd"))#select all the columns whose name starts with gd
```

    ## # A tibble: 49 x 3
    ##    gd0_weight gd18_weight gd_of_birth
    ##         <dbl>       <dbl>       <dbl>
    ##  1       19.7        34.7          20
    ##  2       27          42            19
    ##  3       26          41.4          19
    ##  4       28.5        44.1          19
    ##  5       NA          NA            20
    ##  6       NA          NA            20
    ##  7       NA          NA            20
    ##  8       NA          NA            20
    ##  9       NA          NA            20
    ## 10       28.5        NA            20
    ## # ... with 39 more rows

``` r
select(litters_df, starts_with("pups"))
```

    ## # A tibble: 49 x 3
    ##    pups_born_alive pups_dead_birth pups_survive
    ##              <dbl>           <dbl>        <dbl>
    ##  1               3               4            3
    ##  2               8               0            7
    ##  3               6               0            5
    ##  4               5               1            4
    ##  5               6               0            6
    ##  6               6               0            4
    ##  7               9               0            9
    ##  8               9               1            8
    ##  9               8               0            8
    ## 10               8               0            8
    ## # ... with 39 more rows

``` r
select(litters_df, litter_number, everything()) #a way to relocate, put"litter_number" to the 1st column
```

    ## # A tibble: 49 x 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
relocate(litters_df, litter_number)#put `litter_number` to the 1st column
```

    ## # A tibble: 49 x 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

\#\#`filter` \#\#\#remove rows and keep rows

``` r
filter(litters_df, gd0_weight < 22)#only save the gd0_weight data which is less than 22
```

    ## # A tibble: 8 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Mod7  #59                 17          33.4          19               8
    ## 3 Mod7  #103                21.4        42.1          19               9
    ## 4 Mod7  #106                21.7        37.8          20               5
    ## 5 Mod7  #62                 19.5        35.9          19               7
    ## 6 Low8  #53                 21.8        37.2          20               8
    ## 7 Low8  #100                20          39.2          20               8
    ## 8 Low8  #4/84               21.8        35.2          20               4
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, gd_of_birth == 20)#==is a test, whether they are equal or not, save the datas whivh birth is exactly equal to 20
```

    ## # A tibble: 32 x 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  3 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  4 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  5 Con8  #3/83/3-3             NA          NA            20               9
    ##  6 Con8  #2/95/3               NA          NA            20               8
    ##  7 Con8  #3/5/2/2/95           28.5        NA            20               8
    ##  8 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ##  9 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ## 10 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ## # ... with 22 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
filter(litters_df, group == "Con7")
```

    ## # A tibble: 7 x 8
    ##   group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                   19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2             27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3           NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2           NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, !(gd_of_birth == 20))#give all the datas that birth is not equal to 20
```

    ## # A tibble: 17 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #1/2/95/2           27          42            19               8
    ##  2 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  3 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  4 Con8  #5/4/3/83/3         28          NA            19               9
    ##  5 Con8  #2/2/95/2           NA          NA            19               5
    ##  6 Mod7  #59                 17          33.4          19               8
    ##  7 Mod7  #103                21.4        42.1          19               9
    ##  8 Mod7  #1/82/3-2           NA          NA            19               6
    ##  9 Mod7  #3/83/3-2           NA          NA            19               8
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## 11 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## 12 Mod7  #94/2               24.4        42.9          19               7
    ## 13 Mod7  #62                 19.5        35.9          19               7
    ## 14 Low7  #112                23.9        40.5          19               6
    ## 15 Mod8  #5/93/2             NA          NA            19               8
    ## 16 Mod8  #7/110/3-2          27.5        46            19               8
    ## 17 Low8  #79                 25.4        43.8          19               8
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group == "Con7")
```

    ## # A tibble: 7 x 8
    ##   group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Con7  #85                   19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2             27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3           NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2           NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group %in% c("con7","Mod8"))
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ## 1 Mod8  #97                 24.5        42.8          20               8
    ## 2 Mod8  #5/93               NA          41.1          20              11
    ## 3 Mod8  #5/93/2             NA          NA            19               8
    ## 4 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 5 Mod8  #7/110/3-2          27.5        46            19               8
    ## 6 Mod8  #2/95/2             28.5        44.5          20               9
    ## 7 Mod8  #82/4               33.4        52.7          20               8
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, pups_survive != 4)#######???????????
```

    ## # A tibble: 44 x 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  5 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  6 Con8  #3/83/3-3             NA          NA            20               9
    ##  7 Con8  #2/95/3               NA          NA            20               8
    ##  8 Con8  #3/5/2/2/95           28.5        NA            20               8
    ##  9 Con8  #5/4/3/83/3           28          NA            19               9
    ## 10 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ## # ... with 34 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
filter(litters_df, group %in% c("Con7","Con8"))#only interested in con7 and con8
```

    ## # A tibble: 15 x 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## 11 Con8  #5/4/3/83/3           28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ## 14 Con8  #2/2/95/2             NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
filter(litters_df, group == "Con7" | group == "Con8")
```

    ## # A tibble: 15 x 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## 11 Con8  #5/4/3/83/3           28          NA            19               9
    ## 12 Con8  #1/6/2/2/95-2         NA          NA            20               7
    ## 13 Con8  #3/5/3/83/3-3-2       NA          NA            20               8
    ## 14 Con8  #2/2/95/2             NA          NA            19               5
    ## 15 Con8  #3/6/2/2/95-3         NA          NA            20               7
    ## # ... with 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
drop_na(litters_df)
```

    ## # A tibble: 31 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Mod7  #59                 17          33.4          19               8
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #3/82/3-2           28          45.9          20               5
    ##  8 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  9 Mod7  #106                21.7        37.8          20               5
    ## 10 Mod7  #94/2               24.4        42.9          19               7
    ## # ... with 21 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
drop_na(litters_df, gd_of_birth)##delete na
```

    ## # A tibble: 49 x 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

## `mutate`

``` r
mutate(
  litters_df, 
  wt_gain = gd18_weight - gd0_weight,
  group = str_to_lower("group")##make the group lower
  )
```

    ## # A tibble: 49 x 9
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 group #85                   19.7        34.7          20               3
    ##  2 group #1/2/95/2             27          42            19               8
    ##  3 group #5/5/3/83/3-3         26          41.4          19               6
    ##  4 group #5/4/2/95/2           28.5        44.1          19               5
    ##  5 group #4/2/95/3-3           NA          NA            20               6
    ##  6 group #2/2/95/3-2           NA          NA            20               6
    ##  7 group #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 group #3/83/3-3             NA          NA            20               9
    ##  9 group #2/95/3               NA          NA            20               8
    ## 10 group #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows, and 3 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>, wt_gain <dbl>

\#\#`arrange`

``` r
arrange(litters_df,pups_born_alive)#arrange based on pups_born_alive order(small number to large number)
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Low7  #111                25.5        44.6          20               3
    ##  3 Low8  #4/84               21.8        35.2          20               4
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #2/2/95/2           NA          NA            19               5
    ##  6 Mod7  #3/82/3-2           28          45.9          20               5
    ##  7 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  8 Mod7  #106                21.7        37.8          20               5
    ##  9 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 10 Con7  #4/2/95/3-3         NA          NA            20               6
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

## `%>%`

``` r
litters_data_raw = read_csv("./data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_clean_name = janitor::clean_names(litters_data_raw)
litters_data_selected = select(litters_clean_name, -pups_survive)
litters_mutated = mutate(litters_data_selected, wt_gain = gd18_weight - gd0_weight)
litters_without_missing = drop_na(litters_mutated, gd0_weight)
```

Use the PIPE OPERATOR instead(more brief)

``` r
litters_df = (
  read_csv("./data/FAS_litters.csv") %>% #shift+ctrl+m----%>%---don't need to repeat anything
    janitor::clean_names() %>% 
    select(-pups_survive) %>% 
    drop_na(gd0_weight)
)
```

    ## Rows: 49 Columns: 8

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
