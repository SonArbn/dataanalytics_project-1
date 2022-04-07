# Data analytics: Dating apps
Data Analytics Project'22
```{r}
library(tidytext)
library(tidyverse)
library(tibble)
```
Loading the datasets, organizing columns and merging into one data set: 
```{r}
tinder <- data.frame()
tinder <- read.csv(file = "tinder.csv")
okcupid <- data.frame()
okcupid <- read.csv(file = "okcupid.csv")
bumble <- data.frame()
bumble <- read.csv(file = "bumble.csv")
hinge <- data.frame()
hinge <- read.csv(file = "hinge.csv")
  
filter_col <- function(mydata){
  mydata %>% select (userName, content, score,reviewCreatedVersion, at, replyContent)
  }

tinder <- filter_col(tinder)
appName <- rep(c("Tinder"))
tinder <- cbind(tinder, appName)

okcupid <- filter_col(okcupid)
appName <- rep(c("okcupid"))
okcupid <- cbind(okcupid, appName)

bumble <- filter_col(bumble)
appName <- rep(c("bumble"))
bumble <- cbind(bumble, appName)

hinge <- filter_col(hinge)
appName <- rep(c("hinge"))
hinge <- cbind(hinge, appName)

all_reviews <- rbind(tinder,okcupid,bumble,hinge)
```
Calculating mean score for each app:
```{r}

t_meanscore <- mean(tinder$score)
ok_meanscore <- mean(okcupid$score)
b_meanscore <- mean(bumble$score)
h_meanscore <- mean(hinge$score)
```
Creating a subset from the last 2 years:
```{r}
tinder_time <- filter(tinder[tinder$at > as.POSIXct("2020-01-01 00:00:00", tz="UTC"),])
ok_time <- filter(okcupid[okcupid$at > as.POSIXct("2020-01-01 00:00:00", tz="UTC"),])
b_time <- filter(bumble[bumble$at > as.POSIXct("2020-01-01 00:00:00", tz="UTC"),])
h_time <- filter(hinge[hinge$at > as.POSIXct("2020-01-01 00:00:00", tz="UTC"),])

all_subset <- rbind(tinder_time,ok_time,b_time,h_time)
saveRDS(all_subset, file = "cleaned_data.rds")
```
