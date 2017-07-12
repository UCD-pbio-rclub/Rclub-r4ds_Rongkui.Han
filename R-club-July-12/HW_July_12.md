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

```r
writeLines("\n") #new line
```

```r
writeLines("\t") #tab
```

	

```r
writeLines("\u00b5")
```

```
## µ
```

```r
c("one","two","three")
```

```
## [1] "one"   "two"   "three"
```

####14.2.1 String length  

```r
str_length(c("a","R for data science", NA)) #space counts as length too
```

```
## [1]  1 18 NA
```

####14.2.2 Combining stings  


```r
str_c("x","y") #wow
```

```
## [1] "xy"
```

```r
str_c("x","y","z")
```

```
## [1] "xyz"
```

```r
str_c("x","y", sep = ", ")
```

```
## [1] "x, y"
```

```r
x = c("abc",NA)
str_c("|-",x,"-|")
```

```
## [1] "|-abc-|" NA
```

```r
str_c("|-",str_replace_na(x),"-|")
```

```
## [1] "|-abc-|" "|-NA-|"
```

```r
str_replace_na(x) #turns NA into literal "NA"
```

```
## [1] "abc" "NA"
```

```r
str_c("prefix-", c("a", "b", "c"), "-suffix")
```

```
## [1] "prefix-a-suffix" "prefix-b-suffix" "prefix-c-suffix"
```


```r
name = "Hadley"
time_of_day = "morning"
birthday = FALSE
str_c("Good ",time_of_day, " ", name, if (birthday) " and HAPPY BIRTHDAY", ".")
```

```
## [1] "Good morning Hadley."
```

```r
birthday2 = TRUE
str_c("Good ",time_of_day, " ", name, if (birthday2) " and HAPPY BIRTHDAY", ".")
```

```
## [1] "Good morning Hadley and HAPPY BIRTHDAY."
```

```r
str_c(c("x", "y", "z"), collapse = ",") #to collapse a vector into a single string. 
```

```
## [1] "x,y,z"
```

####14.2.3 Subsetting strings  

```r
x = c("Apple","Banana","Pear")
str_sub(x,1,3)
```

```
## [1] "App" "Ban" "Pea"
```

```r
str_sub(x, -3, -1) #negative numbers count backwards from end
```

```
## [1] "ple" "ana" "ear"
```

```r
str_sub("a", 1, 5) #won't fail if string is too short
```

```
## [1] "a"
```

```r
str_sub(x, 1, 1) = str_to_lower(str_sub(x,1,1))
x
```

```
## [1] "apple"  "banana" "pear"
```

```r
#accidentally found this fun thing:
str_sub(x, 1, 1) = str_to_lower(str_sub(x,1,3))
x
```

```
## [1] "apppple"  "bananana" "peaear"
```

####14.2.4 Locales  


```r
x = c("apple", "eggplant", "banana")
str_sort(x, locale = "en")
```

```
## [1] "apple"    "banana"   "eggplant"
```

```r
str_sort(x, locale = "haw")
```

```
## [1] "apple"    "eggplant" "banana"
```

####14.2.5 Exercises  
1. In code that doesn’t use stringr, you’ll often see paste() and paste0(). What’s the difference between the two functions? What stringr function are they equivalent to? How do the functions differ in their handling of NA?

```r
paste(c(2,"R", NA))
```

```
## [1] "2"  "R"  "NA"
```

```r
paste0(c(2,"R", NA))
```

```
## [1] "2"  "R"  "NA"
```

```r
#no difference here.

## If you pass several vectors to paste0, they are concatenated in a vectorized way.
(nth <- paste0(1:12, c("st", "nd", "rd", rep("th", 9))))
```

```
##  [1] "1st"  "2nd"  "3rd"  "4th"  "5th"  "6th"  "7th"  "8th"  "9th"  "10th"
## [11] "11th" "12th"
```

```r
(nth2 <- paste(1:12, c("st", "nd", "rd", rep("th", 9))))
```

```
##  [1] "1 st"  "2 nd"  "3 rd"  "4 th"  "5 th"  "6 th"  "7 th"  "8 th" 
##  [9] "9 th"  "10 th" "11 th" "12 th"
```

```r
#So it looks like paste() has a default space when concatinating things. 

## To collapse the output into a single string, pass a collapse argument.
paste0(nth, collapse = ", ")
```

```
## [1] "1st, 2nd, 3rd, 4th, 5th, 6th, 7th, 8th, 9th, 10th, 11th, 12th"
```

```r
paste(nth, collapse = ", ")
```

```
## [1] "1st, 2nd, 3rd, 4th, 5th, 6th, 7th, 8th, 9th, 10th, 11th, 12th"
```

```r
#no difference here. 
```

2. In your own words, describe the difference between the sep and collapse arguments to str_c().  
*sep is when the input is multiple elements and the output is one element. collapse is when the input is one vector of multiple elements and the output is one element.*  

3. Use str_length() and str_sub() to extract the middle character from a string. What will you do if the string has an even number of characters?    

```r
a = "This is a string in R" #odd number
str_sub(a, ceiling(str_length(a)/2), ceiling(str_length(a)/2))
```

```
## [1] "s"
```

```r
b = "This a string in R" #even number
#I think it depends on what you mean by the middle character. WHen there length is even technically there is no middle character... assuming the middle two characters are the middle characters:
str_sub(b, str_length(b)/2, (str_length(b)/2 + 1))
```

```
## [1] "tr"
```

4. What does str_wrap() do? When might you want to use it?  

```r
?str_wrap()
harry = "But he understood at last what Dumbledore had been trying to tell him. It was, he thought, the difference between being dragged into the arena to face a battle to the death and walking into the arena with your head held high. Some people, perhaps, would say that there was little to choose between the two ways, but Dumbledore knew - and so do I, thought Harry, with a rush of fierce pride, and so did my parents - that there was all the difference in the world."
writeLines(str_wrap(harry, width = 45, indent = 4))
```

```
##     But he understood at last what Dumbledore had
## been trying to tell him. It was, he thought,
## the difference between being dragged into
## the arena to face a battle to the death and
## walking into the arena with your head held
## high. Some people, perhaps, would say that
## there was little to choose between the two
## ways, but Dumbledore knew - and so do I,
## thought Harry, with a rush of fierce pride,
## and so did my parents - that there was all
## the difference in the world.
```
Formatting a paragraph I guess?  

5. What does str_trim() do? What’s the opposite of str_trim()?  

```r
?str_trim()
str_trim("  String with trailing and leading white space\t")
```

```
## [1] "String with trailing and leading white space"
```

```r
str_pad("String needing trailing and leading white space", width = 55, side = "both")
```

```
## [1] "    String needing trailing and leading white space    "
```

6. Write a function that turns (e.g.) a vector c("a", "b", "c") into the string a, b, and c. Think carefully about what it should do if given a vector of length 0, 1, or 2.


```r
AddAnd = function(x) {
  if (length(x) == 0) {
    print("and")
  } else if (length(x) == 1) {
    print(x)
  } else {
    library(stringr)
    b = str_c(x[1:(length(x)-1)], collapse = ", ")
    c = str_c(" and ", x[length(x)], sep = "")
    d = str_c(b, c, sep = "")
    print(d)
  }  
}
AddAnd(c("Apple", "Banana", "Orange"))
```

```
## [1] "Apple, Banana and Orange"
```

```r
AddAnd(c("Apple", "Orange"))
```

```
## [1] "Apple and Orange"
```

```r
AddAnd("Orange")
```

```
## [1] "Orange"
```

```r
AddAnd(character())
```

```
## [1] "and"
```

###RegExpOne exercises  
Lesson 1: abc  
Lesson 1 1/2: 123  
Lesson 2:  ...\\.


