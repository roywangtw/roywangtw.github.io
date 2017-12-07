## 1. Introduction

Taiwan's society has been going through massive fundamental shifts during the past decade, and changes to its population structure is one of them. Here, we analyze Taiwan population data from 2004 to 2016 for interesting, noteworthy trends and phenomena.

Our pick of 2004 as the beginning year is mainly because it was when the data started to become available for classification of children population based on their biological mothers' nationalities.

***

## 2. Data retrieval and manipulation

The Taiwan population data for our analysis are published and updated periodically by the Ministry of the Interior, Taiwan (R.O.C.) and can be downloaded [here](http://sowf.moi.gov.tw/stat/month/m1-02.xls).  

Since the complete annual data for 2017 are not yet available, we cannot make fair, meaningful comparison with data from previous years. In this case, the data we use will be up till 2016 only.

A quick scan of the original raw data online offers some critical information:

- The entire spreadsheet follows a mostly consistent format with only slight differences.

- Data in the rows of the Taiwan Province and Fuchien Province are just aggregations of their respective constituent counties, rendering them redundant here and therefore will be removed from our dataset when we read the spreadsheet data into R.

- The first column of each sheet contains all the names of Taiwan administrative regions, i.e. the chief subjects of our data exploration later on.

- Towards the end of 2010 and 2014, several changes in Taiwan administrative structure led to the merging and upgrading of several cities and counties. Hence, the resulting mismatches in administrative naming and row ordering will have to be handled, before we combine everything together for further exploration.

The first column of each year's dataset contains both the Chinese and English names of Taiwan's administrative regions, thus requiring some cleaning.

```
for(i in list(df2004, df2011, df2015)){
  print(i[, 1])
}
```

The results above also show the mismatches in administrative naming and ordering caused by past changes to Taiwan administrative structure as mentioned earlier. Therefore, we create 3 different character vectors of administrative region names based on the data from 2004, 2011, and 2015.

```
library(stringr)
library(dplyr)
adm.names.2004 <- str_split(df2004[, 1], fixed(", "), simplify = TRUE) %>% # Extract only the English names
  str_extract_all("[A-Z].*\\s[A-Z].*") %>% 
  str_replace_all("\"[:punct:]?", "") %>% 
  print()
adm.names.2011 <- str_split(df2011[, 1], fixed(", "), simplify = TRUE) %>% # Extract only the English names
  str_extract_all("[A-Z].*\\s[A-Z].*") %>% 
  str_replace_all("\"[:punct:]?", "") %>% 
  print()
adm.names.2015 <- str_split(df2015[, 1], fixed(", "), simplify = TRUE) %>% # Extract only the English names
  str_extract_all("[A-Z].*\\s[A-Z].*") %>% 
  str_replace_all("\"[:punct:]?", "") %>% 
  print()
```

We then replace the first column in each year's dataset with the appropriate version of English administrative region names.
