# tidyfst: Tidy Verbs for Fast Data Manipulation<img src="man/figures/hex-tidyfst_url.png" align="right" alt="" width="120" />

 [![](https://www.r-pkg.org/badges/version/tidyfst?color=orange)](https://cran.r-project.org/package=tidyfst) [![](https://img.shields.io/badge/devel%20version-0.9.9-purple.svg)](https://github.com/hope-data-science/tidyfst) ![](https://img.shields.io/badge/lifecycle-stable-deepgreen.svg)  [![downloads](http://cranlogs.r-pkg.org/badges/grand-total/tidyfst?color=yellow)](https://r-pkg.org/pkg/tidyfst) 

 [![download](https://cranlogs.r-pkg.org/badges/tidyfst?color=red)](https://rdrr.io/cran/tidyfst/) [![downloads](https://cranlogs.r-pkg.org/badges/last-week/tidyfst?color=9cf)](https://crantastic.org/packages/tidyfst) [![DOI](https://zenodo.org/badge/240626994.svg)](https://zenodo.org/badge/latestdoi/240626994)



## Overview

*tidyfst* is a toolkit of tidy data manipulation verbs with *data.table* as the backend . Combining the merits of syntax elegance from *dplyr* and computing performance from *data.table*,  *tidyfst* intends to provide users with state-of-the-art data manipulation tools with least pain. This package is an extension of *data.table*, while enjoying a tidy syntax, it also wraps combinations of efficient functions to facilitate frequently-used data operations.  Also, *tidyfst* would introduce more tidy data verbs from other packages, including but not limited to *tidyverse* and *data.table*. If you are a *dplyr* user but have to use *data.table* for speedy computation,  or *data.table* user looking for readable coding syntax, *tidyfst* is designed for you (and me of course). For further details and tutorials, see [vignettes](https://hope-data-science.github.io/tidyfst/). Both [Chinese](https://hope-data-science.github.io/tidyfst/articles/chinese_tutorial.html) and [English](https://hope-data-science.github.io/tidyfst/articles/english_tutorial.html) tutorials could be found there.

Till now, *tidyfst* has an API that might even transcend its predecessors (e.g. [`select_dt`](https://hope-data-science.github.io/tidyfst/reference/select.html) could accept nearly anything for super column selection). Enjoy the efficient data operations in *tidyfst* !

PS: For extreme performance in tidy syntax, try *tidyfst*'s mirror package [tidyft](https://github.com/hope-data-science/tidyft). 



## Features

- Receives any data.frame (tibble/data.table/data.frame) and returns a data.table.
- Show the variable class of data.table as default.
- Never use in place replacement (also known as modification by reference, which means the original variable would not be modified without notification).
- Use suffix ("_dt") rather than prefix to increase the efficiency (especially when you have IDE with automatic code completion).
- More flexible verbs for big data manipulation.
- Supporting data importing and parsing with *fst*, which saves both time and memory. Details see [parse_fst/select_fst/filter_fst](https://hope-data-science.github.io/tidyfst/reference/fst.html) and [import_fst/export_fst](https://hope-data-science.github.io/tidyfst/reference/fst_io.html).
- Flagship functions: [group_dt](https://hope-data-science.github.io/tidyfst/reference/group_dt.html), [nest_dt](https://hope-data-science.github.io/tidyfst/reference/nest.html), [mutate_when](https://hope-data-science.github.io/tidyfst/reference/mutate_when.html), etc.



## Installation

```R
install.packages("tidyfst")
```



## Example

```R
library(tidyfst)

iris %>%
  mutate_dt(group = Species,sl = Sepal.Length,sw = Sepal.Width) %>%
  select_dt(group,sl,sw) %>%
  filter_dt(sl > 5) %>%
  arrange_dt(group,sl) %>%
  distinct_dt(sl,.keep_all = T) %>%
  summarise_dt(sw = max(sw),by = group)
#>         group  sw
#>        <fctr> <num>
#> 1:     setosa 4.4
#> 2: versicolor 3.4
#> 3:  virginica 3.8

mtcars %>%
  group_dt(
      by =.(vs,am),
      summarise_dt(avg = mean(mpg))
   )
#>    vs am      avg
#>   <num> <num>    <num>
#> 1:  0  1 19.75000
#> 2:  1  1 28.37143
#> 3:  1  0 20.74286
#> 4:  0  0 15.05000

iris[3:8,] %>%
  mutate_when(Petal.Width == .2,
              one = 1,Sepal.Length=2)
#>    Sepal.Length Sepal.Width Petal.Length Petal.Width Species one
#>          <num>       <num>        <num>       <num>  <fctr> <num>
#> 1:          2.0         3.2          1.3         0.2  setosa   1
#> 2:          2.0         3.1          1.5         0.2  setosa   1
#> 3:          2.0         3.6          1.4         0.2  setosa   1
#> 4:          5.4         3.9          1.7         0.4  setosa  NA
#> 5:          4.6         3.4          1.4         0.3  setosa  NA
#> 6:          2.0         3.4          1.5         0.2  setosa   1


```



## Future plans

*tidyfst* will keep up with the [updates](https://github.com/Rdatatable/data.table/blob/master/NEWS.md) of *data.table* , in the next step would introduce more new features to improve the performance and flexibility to facilitate fast data manipulation in tidy syntax. 



## Vignettes
- [Example 1: Basic usage](https://hope-data-science.github.io/tidyfst/articles/example1_intro.html)
- [Example 2: Join tables](https://hope-data-science.github.io/tidyfst/articles/example2_join.html)
- [Example 3: Reshape](https://hope-data-science.github.io/tidyfst/articles/example3_reshape.html)
- [Example 4: Nest](https://hope-data-science.github.io/tidyfst/articles/example4_nest.html)
- [Example 5: Fst](https://hope-data-science.github.io/tidyfst/articles/example5_fst.html) 
- [Example 6: Dt](https://hope-data-science.github.io/tidyfst/articles/example6_dt.html) 

## Related work

- [data.table](https://github.com/Rdatatable/data.table)
- [fst](https://github.com/fstpackage/fst)
- [tidyr](https://github.com/tidyverse/tidyr)
- [dplyr](https://github.com/tidyverse/dplyr)
- [dtplyr](https://github.com/tidyverse/dtplyr)
- [tidyfast](https://github.com/TysonStanley/tidyfast)
- [tidytable](https://github.com/markfairbanks/tidytable)

## Acknowledgement

The author of [maditr](https://github.com/gdemin/maditr), [Gregory Demin](https://github.com/gdemin) and the author of [fst](https://github.com/fstpackage/fst), [Marcus Klik](https://github.com/MarcusKlik) have helped me a lot in the development of this work. It is so lucky to have them (and many other selfless contributors) in the same open source community of R.

