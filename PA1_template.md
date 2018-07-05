#Load the activity.csv file
> 
> ```{r}
Error: attempt to use zero-length variable name
> library(tidyverse)
-- Attaching packages --------------------------------------- tidyverse 1.2.1 --
v ggplot2 3.0.0     v purrr   0.2.5
v tibble  1.4.2     v dplyr   0.7.6
v tidyr   0.8.1     v stringr 1.3.1
v readr   1.1.1     v forcats 0.3.0
-- Conflicts ------------------------------------------ tidyverse_conflicts() --
x dplyr::filter() masks stats::filter()
x dplyr::lag()    masks stats::lag()
> library(knitr)
> library(dplyr)
> library(ggplot2)
> act <- read.csv("activity.csv", header = TRUE, sep = ",")
> summary(act)
     steps                date          interval     
 Min.   :  0.00   2012-10-01:  288   Min.   :   0.0  
 1st Qu.:  0.00   2012-10-02:  288   1st Qu.: 588.8  
 Median :  0.00   2012-10-03:  288   Median :1177.5  
 Mean   : 37.38   2012-10-04:  288   Mean   :1177.5  
 3rd Qu.: 12.00   2012-10-05:  288   3rd Qu.:1766.2  
 Max.   :806.00   2012-10-06:  288   Max.   :2355.0  
 NA's   :2304     (Other)   :15840                   
> ```
Error: attempt to use zero-length variable name
> 
> 
> #calculate the total no of steps taken per day and plotting them by using histogram
> 
> ```{r}
Error: attempt to use zero-length variable name
> act_byDay <- act %>% 
+                        group_by(date)%>%
+                        summarise(total_steps = sum(steps))
> act_byDay$date <- as.Date(act_byDay$date)
> ggplot(act_byDay, aes(x = date, y = total_steps)) +
+         geom_histogram(stat = "identity")
Warning: Ignoring unknown parameters: binwidth, bins, pad
Warning message:
Removed 8 rows containing missing values (position_stack). 
> ```
Error: attempt to use zero-length variable name
> 
> #claculate the mean and median off total no of steps taken per day
> 
> ```{r}
Error: attempt to use zero-length variable name
> mean(act_byDay$total_steps, na.rm = TRUE)
[1] 10766.19
> 
> median(act_byDay$total_steps, na.rm = TRUE)
[1] 10765
> 
> act_mean <- act %>%
+         group_by(interval) %>%
+         summarise(mean_steps = mean(steps, na.rm = TRUE))
> ```
Error: attempt to use zero-length variable name
> 
> 
> #find the average steps over time series plot
> 
> 
> 
> ```{r}
Error: attempt to use zero-length variable name
> ggplot(act_mean, aes(x = interval, y = mean_steps)) +
+         geom_line()
> ```
Error: attempt to use zero-length variable name
> 
> #calculate the number of rows containing in activity data
> 
> ```{r}
Error: attempt to use zero-length variable name
> sum(is.na(act))
[1] 2304
> ```
Error: attempt to use zero-length variable name
> 
> 
> #impute the NA vlaues by using mean_steps fill in the NA-containing rows
> 
> ```{r}
Error: attempt to use zero-length variable name
> for(i in 1:nrow(act)){
+         if(is.na(act$steps[i])){
+                 act$steps[i] = act_mean$mean_steps[which(act_mean$interval == act$interval[i])]
+         }
+ }
> sum(is.na(act$steps))
[1] 0
> ```
Error: attempt to use zero-length variable name
> 
> 
> #after imputing ploting the histogram of total no of steps per day
> 
> ```{r}
Error: attempt to use zero-length variable name
> act$date = as.Date(act$date)
> ggplot(act, aes(x = date, y = steps))+
+         geom_histogram(stat = "identity")
Warning: Ignoring unknown parameters: binwidth, bins, pad
> ```
Error: attempt to use zero-length variable name
> 
> 
> #find mean and median of the total number of steps per day(after imputing)
> 
> ```{r}
Error: attempt to use zero-length variable name
> newAct_byDay <- act %>% 
+                        group_by(date)%>%
+                        summarise(total_steps = sum(steps))
> 
> mean(newAct_byDay$total_steps)
[1] 10766.19
> median(newAct_byDay$total_steps)
[1] 10766.19
> ```
Error: attempt to use zero-length variable name
> 
> 
> #create new variable containing weekday and weekend
> 
> ```{r}
Error: attempt to use zero-length variable name
> act <- act %>% mutate(typeofDay = ifelse(weekdays(act$date) == "Saturday" | weekdays(act$date) == "Sunday", "weekend", "weekday"))
> table(act$typeofDay)

weekday weekend 
  12960    4608 
> newAct_mean <- act %>%
+         group_by(interval, typeofDay) %>%
+         summarise(mean_steps = mean(steps, na.rm = TRUE))
> ```
Error: attempt to use zero-length variable name
> 
> 
> #plot the avg no of steps taken per each day using panels weekday and weekend
> 
> ```{r}
Error: attempt to use zero-length variable name
> ggplot(newAct_mean, aes(x = interval, y = mean_steps)) +
+         geom_line() +
+         facet_grid(typeofDay~.)
> ```
Error: attempt to use zero-length variable name
