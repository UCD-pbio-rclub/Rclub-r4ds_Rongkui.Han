# HW_July_12
Rongkui Han  
July 11, 2017  
###Strings  
####14.1.1 Prerequisites  

```r
library(tidyverse)
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```

```r
library(stringr)
```

###14.2 String basics  

```r
string1 = "This is a string"
string2 = 'If I want to include a "quote" inside a string, I use single quotes'
"This is a string without a closing quote
HELP I'M STUCK"
```

```
## [1] "This is a string without a closing quote\nHELP I'M STUCK"
```

```r
#press escape to escape. 
double_quote = "\""
double_quote
```

```
## [1] "\""
```

```r
single_quote = '\''
single_quote
```

```
## [1] "'"
```

```r
x = c("\"", "\\")
x
```

```
## [1] "\"" "\\"
```

```r
writeLines(x) #weird.
```

```
## "
## \
```


