Author: Matthew Jensen Date: 3/18/2023

### Introduction

Bellabeat is a high-tech company that manufactures health-focused smart
products and develops beautifully designed technology that informs and
inspires women around the world. Collecting data on activity, sleep,
stress, and reproductive health has allowed Bellabeat to empower women
with knowledge about their own health and habits. Since it was founded
in 2013, Bellabeat has grown rapidly and quickly positioned itself as a
tech-driven wellness company for women. By 2016, Bellabeat had opened
offices around the world and launched multiple products. Bellabeat
products became available through a growing number of online retailers
in addition to their own e-commerce channel on their website. The
company has invested in traditional advertising media, such as radio,
out-of-home billboards, print, and television, but focuses on digital
marketing extensively. Bellabeat invests year-round in Google Search,
maintaining active Facebook and Instagram pages, and consistently
engages consumers on Twitter. Additionally, Bellabeat runs video ads on
Youtube and display ads on the Google Display Network to support
campaigns around key marketing dates.

### Ask

*What is the problem you are trying to solve?*

Finding patterns about the users of the smart devices daily habits to
see if there are any edges and/or angles that will be useful to
Bellabeat’s marketing strategy.

*How can your insights drive business decisions?*

The data may contain insights that will be useful to the company in the
way that they advertise their products. It can also help the company see
when and how their product is being used.

### Prepare

The data used in this case study is from FitBit Fitness Tracker Data \|
Kaggle. It contains data collected from 30 fitbit users that consented
to their data being recorded. It includes information about daily steps,
heart rate, physical activity, sleeping habits, and general daily
activity.

*Where is your data stored?*

The dataset was downloaded onto my computer from Kaggle at the site
linked above.

*How is the data organized?*

The data is organized throughout 18 files on a zip file. The files are:

-   dailyActivity_merged.csv
-   dailyCalories_merged.csv
-   dailyIntensities_merged.csv
-   dailySteps_merged.csv
-   Heartrate_seconds_merged.csv
-   hourlyCalories_merged.csv
-   hourlyIntensities_merged.csv
-   hourlySteps_merged.csv
-   minuteCaloriesNarrow_merged.csv
-   minuteCaloriesWide_merged.csv
-   minuteIntensitiesNarrow_merged.csv
-   minuteIntensitiesWide_merged.csv
-   minuteMETsNarrow_merged.csv
-   minuteSleep_merged.csv
-   minuteStepsNarrow_merged.csv
-   minuteStepsWide_merged.csv
-   sleepDay_merged.csv
-   weightLogInfo_merged.csv

*Is it in long or wide format?*

The data is in wide format.

*Does your data ROCCC?*

For a case study where we will be analyzing data, we want the data to be
unbiased and credible, and that it fits ROCCC. ROCCC stands for
reliable, original, comprehensive, current, and cited. Using it is the
best way to figure out if the data is useful and will not give
misleading results.

Reliable: The data is from real FitBit users which is reliable. However,
surveying only 30 people over a month is too small of a sample size to
find any clear trends in the data. The end results might be a little
noisy which could be improved upon if more people were surveyed (for
example, 100-1000 people) and the data was collected over a longer
period of time (3-6 months).

Original: The data was submitted via Amazon Mechanical Turk. It is
original because it comes from real people and is credible because it is
quantitative data that comes from the Fitbit the person is using.
However, it would have been better if the data had come from the FitBit
device itself and not a survey.

Comprehensive: The data is somewhat comprehensive. It does a good job of
tracking things like sleep and user activity which can give a good idea
of how the people surveyed are using their devices. However, the
concerns about reliability also apply here because the data could use a
longer time period and a larger sample size to remove noise from the
dataset. People’s habits change a lot from month to month, and even
though the data gives a clear picture of habits of the people surveyed
in April 2016, it might not be for another season where the weather is
worse or the days are shorter or longer.

Current: The data is from March 2016 to May 2016. This data would have
been useful in 2016 or 2017, but at this point it might be outdated. Due
to the rapid developments in technology it could be argued that this
data is obsolete due to FitBit updating and improving their devices over
the past 6 years. However, it’s not too far in the past therefore it
could still be worth a look.

Cited: Yes, the data is cited.

Overall, the data itself is decent however it could be updated and
improved upon. It doesn’t check every box of ROCCC yet there’s still
enough useful data to complete the case study. The dataset’s strength is
that it is original and cited, yet it could be a little more reliable
and comprehensive.

### Process

I chose R Studio to complete this case study in because I was familiar
with it and thought that the graphing features through the ggplot
library would work well with the data that I had been given.

I also decided the files that I thought would give the clearest picture
on trends within the data for Bellabeat:

-   dailyActivity_merged
-   hourlyCalories_merged
-   hourlySteps_merged
-   sleepDay_merged

The first step I took is loading in the libraries that I need, then I
read in the files into R:

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.2.2

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.4.0      ✔ purrr   0.3.5 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.3      ✔ forcats 0.5.2

    ## Warning: package 'ggplot2' was built under R version 4.2.2

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(here)
```

    ## Warning: package 'here' was built under R version 4.2.2

    ## here() starts at C:/Users/Matthew/Documents/Bellabeat-Case-Study

``` r
library(skimr)
```

    ## Warning: package 'skimr' was built under R version 4.2.2

``` r
library(janitor)
```

    ## Warning: package 'janitor' was built under R version 4.2.2

    ## 
    ## Attaching package: 'janitor'
    ## 
    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'
    ## 
    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
library(ggrepel)
```

    ## Warning: package 'ggrepel' was built under R version 4.2.2

``` r
library(ggplot2)
library(reshape2)
```

    ## Warning: package 'reshape2' was built under R version 4.2.2

    ## 
    ## Attaching package: 'reshape2'
    ## 
    ## The following object is masked from 'package:tidyr':
    ## 
    ##     smiths

``` r
library(scales)
```

    ## Warning: package 'scales' was built under R version 4.2.2

    ## 
    ## Attaching package: 'scales'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

``` r
# read in files

daily_activity <- read.csv("/Users/Matthew/Documents/fitbit/Fitabase Data 4.12.16-5.12.16/dailyActivity_merged.csv")
hourly_calories <- read.csv("/Users/Matthew/Documents/fitbit/Fitabase Data 4.12.16-5.12.16/hourlyCalories_merged.csv")
hourly_steps <- read.csv('/Users/Matthew/Documents/fitbit/Fitabase Data 4.12.16-5.12.16/hourlySteps_merged.csv')
sleep_day <- read.csv("/Users/Matthew/Documents/fitbit/Fitabase Data 4.12.16-5.12.16/sleepDay_merged.csv")
```

The next step in cleaning the dataset is getting rid of any duplicates
and dropping any blank cells.

``` r
# Removing duplicates and dropping NA 

daily_activity <- daily_activity %>% 
    drop_na()

hourly_calories <- hourly_calories %>% 
    drop_na()

hourly_steps <- hourly_steps %>% 
    drop_na()

sleep_day <- sleep_day %>% 
    drop_na() %>% 
    unique()
```

Then I converted the time data in the ActivityHour, ActivityDate, and
Sleep_day variable in each of the files to date/time and set new columns
for month, date, and time.

``` r
# Convert ActivityDate column to POSIXct format
daily_activity$ActivityDate <- as.POSIXct(daily_activity$ActivityDate, format="%m/%d/%Y", tz=Sys.timezone())

# Create new columns for date, month, day, and weekday
daily_activity <- daily_activity %>% 
  mutate(date = format(ActivityDate, format = "%m/%d/%y"),
         month = format(ActivityDate, format = "%B"),
         day = format(ActivityDate, format = "%d"),
         weekday = format(ActivityDate, format = "%A"))

# Convert hourly calories to POSIXct format
hourly_calories$ActivityHour=as.POSIXct(hourly_calories$ActivityHour, format="%m/%d/%Y %I:%M:%S %p", tz=Sys.timezone())
hourly_calories$time <- format(hourly_calories$ActivityHour, format = "%H:%M:%S")
hourly_calories$date <- format(hourly_calories$ActivityHour, format = "%m/%d/%y")
hourly_calories$month <- format(hourly_calories$ActivityHour, format = "%B")

# Convert hourly steps to POSIXct format
hourly_steps$ActivityHour=as.POSIXct(hourly_calories$ActivityHour, format="%m/%d/%Y %I:%M:%S %p", tz=Sys.timezone())
hourly_steps$time <- format(hourly_calories$ActivityHour, format = "%H:%M:%S")
hourly_steps$date <- format(hourly_calories$ActivityHour, format = "%m/%d/%y")
hourly_steps$month <- format(hourly_calories$ActivityHour, format = "%B")

# Convert the SleepDay column to POSIXct format
sleep_day$SleepDay <- as.POSIXct(sleep_day$SleepDay, format="%m/%d/%Y %I:%M:%S %p", tz=Sys.timezone())

# Create new columns for date and month
sleep_day <- sleep_day %>% 
  mutate(date = format(SleepDay, format = "%m/%d/%y"),
         month = format(SleepDay, format = "%B"))
```

Attached below is the data read in and cleaned from the four files:

``` r
head(daily_activity)
```

    ##           Id ActivityDate TotalSteps TotalDistance TrackerDistance
    ## 1 1503960366   2016-04-12      13162          8.50            8.50
    ## 2 1503960366   2016-04-13      10735          6.97            6.97
    ## 3 1503960366   2016-04-14      10460          6.74            6.74
    ## 4 1503960366   2016-04-15       9762          6.28            6.28
    ## 5 1503960366   2016-04-16      12669          8.16            8.16
    ## 6 1503960366   2016-04-17       9705          6.48            6.48
    ##   LoggedActivitiesDistance VeryActiveDistance ModeratelyActiveDistance
    ## 1                        0               1.88                     0.55
    ## 2                        0               1.57                     0.69
    ## 3                        0               2.44                     0.40
    ## 4                        0               2.14                     1.26
    ## 5                        0               2.71                     0.41
    ## 6                        0               3.19                     0.78
    ##   LightActiveDistance SedentaryActiveDistance VeryActiveMinutes
    ## 1                6.06                       0                25
    ## 2                4.71                       0                21
    ## 3                3.91                       0                30
    ## 4                2.83                       0                29
    ## 5                5.04                       0                36
    ## 6                2.51                       0                38
    ##   FairlyActiveMinutes LightlyActiveMinutes SedentaryMinutes Calories     date
    ## 1                  13                  328              728     1985 04/12/16
    ## 2                  19                  217              776     1797 04/13/16
    ## 3                  11                  181             1218     1776 04/14/16
    ## 4                  34                  209              726     1745 04/15/16
    ## 5                  10                  221              773     1863 04/16/16
    ## 6                  20                  164              539     1728 04/17/16
    ##   month day   weekday
    ## 1 April  12   Tuesday
    ## 2 April  13 Wednesday
    ## 3 April  14  Thursday
    ## 4 April  15    Friday
    ## 5 April  16  Saturday
    ## 6 April  17    Sunday

``` r
head(hourly_calories)
```

    ##           Id        ActivityHour Calories     time     date month
    ## 1 1503960366 2016-04-12 00:00:00       81 00:00:00 04/12/16 April
    ## 2 1503960366 2016-04-12 01:00:00       61 01:00:00 04/12/16 April
    ## 3 1503960366 2016-04-12 02:00:00       59 02:00:00 04/12/16 April
    ## 4 1503960366 2016-04-12 03:00:00       47 03:00:00 04/12/16 April
    ## 5 1503960366 2016-04-12 04:00:00       48 04:00:00 04/12/16 April
    ## 6 1503960366 2016-04-12 05:00:00       48 05:00:00 04/12/16 April

``` r
head(hourly_steps)
```

    ##           Id        ActivityHour StepTotal     time     date month
    ## 1 1503960366 2016-04-12 00:00:00       373 00:00:00 04/12/16 April
    ## 2 1503960366 2016-04-12 01:00:00       160 01:00:00 04/12/16 April
    ## 3 1503960366 2016-04-12 02:00:00       151 02:00:00 04/12/16 April
    ## 4 1503960366 2016-04-12 03:00:00         0 03:00:00 04/12/16 April
    ## 5 1503960366 2016-04-12 04:00:00         0 04:00:00 04/12/16 April
    ## 6 1503960366 2016-04-12 05:00:00         0 05:00:00 04/12/16 April

``` r
head(sleep_day)
```

    ##           Id   SleepDay TotalSleepRecords TotalMinutesAsleep TotalTimeInBed
    ## 1 1503960366 2016-04-12                 1                327            346
    ## 2 1503960366 2016-04-13                 2                384            407
    ## 3 1503960366 2016-04-15                 1                412            442
    ## 4 1503960366 2016-04-16                 2                340            367
    ## 5 1503960366 2016-04-17                 1                700            712
    ## 6 1503960366 2016-04-19                 1                304            320
    ##       date month
    ## 1 04/12/16 April
    ## 2 04/13/16 April
    ## 3 04/15/16 April
    ## 4 04/16/16 April
    ## 5 04/17/16 April
    ## 6 04/19/16 April

After that, I merged the daily_activity dataframe with the sleep_day
dataframe by the ID and date to find the averages of how much people
slept. Later on I did the same to find the average calories and steps
per day of the week.

``` r
# merge daily activity with sleep data by the Id and date
combined_activity <- merge(daily_activity, sleep_day, by=c ("Id", "date"))
combined_activity <- combined_activity %>% select(-c("month.y"))
glimpse(combined_activity)
```

    ## Rows: 410
    ## Columns: 23
    ## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036…
    ## $ date                     <chr> "04/12/16", "04/13/16", "04/15/16", "04/16/16…
    ## $ ActivityDate             <dttm> 2016-04-12, 2016-04-13, 2016-04-15, 2016-04-…
    ## $ TotalSteps               <int> 13162, 10735, 9762, 12669, 9705, 15506, 10544…
    ## $ TotalDistance            <dbl> 8.50, 6.97, 6.28, 8.16, 6.48, 9.88, 6.68, 6.3…
    ## $ TrackerDistance          <dbl> 8.50, 6.97, 6.28, 8.16, 6.48, 9.88, 6.68, 6.3…
    ## $ LoggedActivitiesDistance <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ VeryActiveDistance       <dbl> 1.88, 1.57, 2.14, 2.71, 3.19, 3.53, 1.96, 1.3…
    ## $ ModeratelyActiveDistance <dbl> 0.55, 0.69, 1.26, 0.41, 0.78, 1.32, 0.48, 0.3…
    ## $ LightActiveDistance      <dbl> 6.06, 4.71, 2.83, 5.04, 2.51, 5.03, 4.24, 4.6…
    ## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ VeryActiveMinutes        <int> 25, 21, 29, 36, 38, 50, 28, 19, 41, 39, 73, 3…
    ## $ FairlyActiveMinutes      <int> 13, 19, 34, 10, 20, 31, 12, 8, 21, 5, 14, 23,…
    ## $ LightlyActiveMinutes     <int> 328, 217, 209, 221, 164, 264, 205, 211, 262, …
    ## $ SedentaryMinutes         <int> 728, 776, 726, 773, 539, 775, 818, 838, 732, …
    ## $ Calories                 <int> 1985, 1797, 1745, 1863, 1728, 2035, 1786, 177…
    ## $ month.x                  <chr> "April", "April", "April", "April", "April", …
    ## $ day                      <chr> "12", "13", "15", "16", "17", "19", "20", "21…
    ## $ weekday                  <chr> "Tuesday", "Wednesday", "Friday", "Saturday",…
    ## $ SleepDay                 <dttm> 2016-04-12, 2016-04-13, 2016-04-15, 2016-04-…
    ## $ TotalSleepRecords        <int> 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ TotalMinutesAsleep       <int> 327, 384, 412, 340, 700, 304, 360, 325, 361, …
    ## $ TotalTimeInBed           <int> 346, 407, 442, 367, 712, 320, 377, 364, 384, …

``` r
# new dataframe for measuring average 

dfweekdaysleep <- combined_activity %>%
  mutate(weekday = weekdays(ActivityDate))

# Create vector for the weekdays
dfweekdaysleep$weekday <-ordered(dfweekdaysleep$weekday, levels=c("Monday", "Tuesday", "Wednesday", "Thursday",
"Friday", "Saturday", "Sunday"))

weekday_activity <- dfweekdaysleep%>%
  group_by(weekday) %>%
  summarize(daily_steps = mean(TotalSteps), daily_calories = mean(Calories), daily_sedentary = mean(SedentaryMinutes), daily_sleep = mean(TotalMinutesAsleep)/60)

head(weekday_activity)
```

    ## # A tibble: 6 × 5
    ##   weekday   daily_steps daily_calories daily_sedentary daily_sleep
    ##   <ord>           <dbl>          <dbl>           <dbl>       <dbl>
    ## 1 Monday          9273.          2432.            718.        6.99
    ## 2 Tuesday         9183.          2496.            740.        6.74
    ## 3 Wednesday       8023.          2378.            714.        7.24
    ## 4 Thursday        8184.          2307.            698.        6.69
    ## 5 Friday          7901.          2330.            743.        6.76
    ## 6 Saturday        9871.          2507.            680.        6.98

``` r
# average calories in a day

weekday_calories <- ggplot(weekday_activity) +
    geom_col(aes(weekday, daily_calories), fill = "darkgreen") +
    labs(title = "Daily calories burned per day of week", x= "", y = "") +
    theme(axis.text.x = element_text(angle = 90,vjust = 0.5, hjust = 0.5))

weekday_calories
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-8-1.png)

This graph examines if there is any particular day that people burn the
most calories. While there isn’t a big difference, Saturday being the
day with the most calories burned makes sense because of it being the
weekend where people might have more free time to get active.

``` r
# average steps in a day 

weekday_steps <- ggplot(weekday_activity) +
    geom_col(aes(weekday, daily_steps), fill = "orangered4") +
    labs(title = "Daily steps per day of week", x= "", y = "") +
    theme(axis.text.x = element_text(angle = 90,vjust = 0.5, hjust = 0.5))

weekday_steps
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-9-1.png)

This graph plots the relationship between a person’s daily steps with
each day of the week to show which day has the most activity. This does
compare well to the last graph as the days where people took more steps
are also the days where people burned more calories. The top 3 days for
steps and calories burned are both Saturday, Monday, and Tuesday.

``` r
# average sleep per day of week 

weekday_sleep <- ggplot(weekday_activity) +
    geom_col(aes(weekday, daily_sleep), fill = "dodgerblue4") +
    labs(title = "Average hours asleep per day of week", x= "", y = "") +
    theme(axis.text.x = element_text(angle = 90,vjust = 0.5, hjust = 0.5))

weekday_sleep
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-10-1.png)

This graph also shows which days of the week people typically sleep the
most, graphing this can show which day or days people are the most well
rested, as well as see if people are getting the recommended amount of
sleep each night. The recommended amount of sleep is at least 6-8 hours
per night. While the people surveyed are on the low end of that
recommendation, they are still getting enough on average. However this
graph does not show anything about sleep leading to more step activity
or burning calories.

``` r
# calories burned for every step taken

cal_burned <- ggplot(data=daily_activity, mapping=aes(x=TotalSteps, y=Calories)) + 
geom_point(color="seagreen4") + geom_smooth(method = 'lm', formula = y ~ x) + 
labs(title="Daily Steps vs. Calories Burned", x="Total Steps", y="Calories Burned")

cal_burned
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-11-1.png)

This graph shows the correlation between the amount of steps a person
has in a day and how many calories they burn. On average, when they take
more steps, they burn more calories. This is shown by the blue line of
best fit. This also goes along with the previous graphs where the days
on which more steps were taken were the ones with more calories burned.

``` r
# Create new df with daily active minutes
total_activity <- daily_activity %>%
mutate(TotalActiveMinutes = VeryActiveMinutes+FairlyActiveMinutes+LightlyActiveMinutes)

# Plot relationship between number of daily steps and minutes active during the day
active_steps <- ggplot(data=total_activity, aes(x=TotalSteps, y=TotalActiveMinutes)) + 
geom_point(color="dodgerblue4") + 
geom_smooth(method = 'lm', formula = y ~ x) +
labs(title="Total Steps vs Daily Activity", x="Total Daily Steps", y="Time Active in Minutes")

active_steps
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-12-1.png)

``` r
# merge daily activity with hourly steps by the Id and date
step_activity <- merge(daily_activity, hourly_steps, by=c('Id', 'date'))
glimpse(step_activity)
```

    ## Rows: 22,099
    ## Columns: 23
    ## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036…
    ## $ date                     <chr> "04/12/16", "04/12/16", "04/12/16", "04/12/16…
    ## $ ActivityDate             <dttm> 2016-04-12, 2016-04-12, 2016-04-12, 2016-04-…
    ## $ TotalSteps               <int> 13162, 13162, 13162, 13162, 13162, 13162, 131…
    ## $ TotalDistance            <dbl> 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.5…
    ## $ TrackerDistance          <dbl> 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.5…
    ## $ LoggedActivitiesDistance <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ VeryActiveDistance       <dbl> 1.88, 1.88, 1.88, 1.88, 1.88, 1.88, 1.88, 1.8…
    ## $ ModeratelyActiveDistance <dbl> 0.55, 0.55, 0.55, 0.55, 0.55, 0.55, 0.55, 0.5…
    ## $ LightActiveDistance      <dbl> 6.06, 6.06, 6.06, 6.06, 6.06, 6.06, 6.06, 6.0…
    ## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ VeryActiveMinutes        <int> 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 2…
    ## $ FairlyActiveMinutes      <int> 13, 13, 13, 13, 13, 13, 13, 13, 13, 13, 13, 1…
    ## $ LightlyActiveMinutes     <int> 328, 328, 328, 328, 328, 328, 328, 328, 328, …
    ## $ SedentaryMinutes         <int> 728, 728, 728, 728, 728, 728, 728, 728, 728, …
    ## $ Calories                 <int> 1985, 1985, 1985, 1985, 1985, 1985, 1985, 198…
    ## $ month.x                  <chr> "April", "April", "April", "April", "April", …
    ## $ day                      <chr> "12", "12", "12", "12", "12", "12", "12", "12…
    ## $ weekday                  <chr> "Tuesday", "Tuesday", "Tuesday", "Tuesday", "…
    ## $ ActivityHour             <dttm> 2016-04-12 00:00:00, 2016-04-12 01:00:00, 20…
    ## $ StepTotal                <int> 373, 160, 151, 0, 0, 0, 0, 0, 250, 1864, 676,…
    ## $ time                     <chr> "00:00:00", "01:00:00", "02:00:00", "03:00:00…
    ## $ month.y                  <chr> "April", "April", "April", "April", "April", …

``` r
# steps by hour

avg_steps <- step_activity %>%
  group_by(time) %>%
  drop_na() %>%
  summarise(mean_total_int = mean(StepTotal))

steps_per_hour <- ggplot(data=avg_steps, aes(x=time, y=mean_total_int)) + 
geom_bar(stat = "identity", fill="blue") +
theme(axis.text.x = element_text(angle = 90)) +
labs(title="Average Steps per Hour", x="Hour", y="Average Steps")

steps_per_hour
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-14-1.png)

This graph illustrates the time of day in which people are most active.
When people are asleep in the early morning there isn’t much activity
however as the day goes on people become more active. There are also
relative peaks around noon (lunchtime) and 4 pm to 7 pm (dinnertime).

``` r
# merge daily activity with hourly calories by the Id and date
calorie_activity <- merge(daily_activity, hourly_calories, by=c('Id', 'date'))
glimpse(calorie_activity)
```

    ## Rows: 22,099
    ## Columns: 23
    ## $ Id                       <dbl> 1503960366, 1503960366, 1503960366, 150396036…
    ## $ date                     <chr> "04/12/16", "04/12/16", "04/12/16", "04/12/16…
    ## $ ActivityDate             <dttm> 2016-04-12, 2016-04-12, 2016-04-12, 2016-04-…
    ## $ TotalSteps               <int> 13162, 13162, 13162, 13162, 13162, 13162, 131…
    ## $ TotalDistance            <dbl> 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.5…
    ## $ TrackerDistance          <dbl> 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.50, 8.5…
    ## $ LoggedActivitiesDistance <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ VeryActiveDistance       <dbl> 1.88, 1.88, 1.88, 1.88, 1.88, 1.88, 1.88, 1.8…
    ## $ ModeratelyActiveDistance <dbl> 0.55, 0.55, 0.55, 0.55, 0.55, 0.55, 0.55, 0.5…
    ## $ LightActiveDistance      <dbl> 6.06, 6.06, 6.06, 6.06, 6.06, 6.06, 6.06, 6.0…
    ## $ SedentaryActiveDistance  <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ VeryActiveMinutes        <int> 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 25, 2…
    ## $ FairlyActiveMinutes      <int> 13, 13, 13, 13, 13, 13, 13, 13, 13, 13, 13, 1…
    ## $ LightlyActiveMinutes     <int> 328, 328, 328, 328, 328, 328, 328, 328, 328, …
    ## $ SedentaryMinutes         <int> 728, 728, 728, 728, 728, 728, 728, 728, 728, …
    ## $ Calories.x               <int> 1985, 1985, 1985, 1985, 1985, 1985, 1985, 198…
    ## $ month.x                  <chr> "April", "April", "April", "April", "April", …
    ## $ day                      <chr> "12", "12", "12", "12", "12", "12", "12", "12…
    ## $ weekday                  <chr> "Tuesday", "Tuesday", "Tuesday", "Tuesday", "…
    ## $ ActivityHour             <dttm> 2016-04-12 00:00:00, 2016-04-12 01:00:00, 20…
    ## $ Calories.y               <int> 81, 61, 59, 47, 48, 48, 48, 47, 68, 141, 99, …
    ## $ time                     <chr> "00:00:00", "01:00:00", "02:00:00", "03:00:00…
    ## $ month.y                  <chr> "April", "April", "April", "April", "April", …

``` r
# calories by hour 

hourly_cal <- calorie_activity %>%
  group_by(time) %>%
  drop_na() %>%
  summarise(mean_total_int = mean(Calories.y))

# Plot relationship between average intensity and time of day
bar_calories <- ggplot(data=hourly_cal, aes(x=time, y=mean_total_int)) + 
geom_bar(stat = "identity", fill='purple') +
theme(axis.text.x = element_text(angle = 90)) +
labs(title="Average Calories Burned vs Time of Day", y="Average Calories Burned", x="Hour of day")

bar_calories
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-16-1.png)

This graph illustrates what time of day people are burning the most
calories. One of the most interesting things is how much people are
presumably burning calories in their sleep. This graph also correlated
with the last graph of hourly steps, where the most calories are getting
burned around dinnertime. The number of calories burned also increases
throughout the day, similar to the last graph.

``` r
# Graph of sedentary minutes 

sed_minutes <- ggplot(weekday_activity) +
    geom_col(aes(weekday, daily_sedentary), fill = "orangered4") +
    labs(title = "Sedentary Minutes Per Day of Week", x= "", y = "") +
    theme(axis.text.x = element_text(angle = 90,vjust = 0.5, hjust = 0.5))

sed_minutes
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-17-1.png)

This graph shows how much time people are sedentay, or not staying
active during the week. It is spread out evenly, however Tuesday and
Friday are the least active days, with the weekend having the least
amount of sedentary minutes.

``` r
#slicing the individual segments
veryactive_min <- sum(daily_activity$VeryActiveMinutes)
fairlyactive_min <- sum(daily_activity$FairlyActiveMinutes)
lightlyactive_min <- sum(daily_activity$LightlyActiveMinutes)
sedentary_min <- sum(daily_activity$SedentaryMinutes)
total_min <- veryactive_min + fairlyactive_min + lightlyactive_min + sedentary_min

# plotting the pie
slices <- c(veryactive_min,fairlyactive_min,lightlyactive_min,sedentary_min)
activity_type <- c("Very Active","Fairly Active","Lightly Active","Sedentary")
active_percentage <- round(slices/sum(slices)*100)
activity_type <- paste(activity_type, active_percentage)
activity_type <- paste(activity_type, "%", sep="")
pie(slices, labels = activity_type, col = rainbow(length(activity_type)), main = "Percentage of Activity Type in Minutes")
```

![](bellabeatgit_files/figure-markdown_github/unnamed-chunk-18-1.png)

This graph illustrates how most of the time people are spending is
sedentary and not doing any activity. Lightly active is the type of
activity that people do the most, vastly more than both fairly and very
active, which have a very small chunk of all the activity that is
tracked.

### Act

Trends shown within the data:

-   Saturday is the day of the week with the most steps taken and the
    most calories burned.
-   The hour of the day with the most calories burned is 7 pm, and the
    people surveyed generally get more exercise around the lunchtime
    (12-2 pm) and dinnertime hours.
-   People are still burning calories when they are asleep as well as
    the less active times of the day.
-   Generally, the more steps a person takes the more calories they will
    burn.

Recommendations:

-   Pool data from a larger and more diverse dataset.
-   Create a feature where users can compete and compare their
    statistics to gain the most steps or be the most active with their
    friends and family, somewhat like a game.
-   Partner with a health company to develop personal exercise and sleep
    plans for specific people.
