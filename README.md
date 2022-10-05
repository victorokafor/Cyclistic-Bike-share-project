---
title: "Bike Share Analysis from May 2021 - April 2022"
author: "Victor Okafor"
date: '2022-06-24'
output: html_document
---

![bike_share](C:\Users\user\Desktop\Bike_share.png)

## About the company
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.


#### Business Task
We are going to take an in depth look at these data sets to understand how the two user types groups (Annual members and casual users) make use of the cyclystic bikes differently.

#### About the Data
You will use Cyclistic’s historical trip data to analyze and identify trends. [Download the previous 12 months of Cyclistic trip data here.](https://divvy-tripdata.s3.amazonaws.com/index.html) Note: The datasets have a different name because Cyclistic is a fictional company. For the purposes of this case study,the datasets are appropriate and will enable you to answer the business questions. The data has been made available by Motivate International Inc. under this [license.](https://ride.divvybikes.com/data-license-agreement))
This is public data that you can use to explore how different customer types are using Cyclistic bikes. But note that data-privacy issues prohibit you from using riders’ personally identifiable information. This means that you won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.


#### Key Stakeholders
*  Lily Moreno: The director of marketing and your manager
* Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting,    analyzing, andreporting data that helps guide Cyclistic marketing strategy.

#### Load packages
```{r echo=FALSE}
library(tidyverse)
library(readr)
library(tidyr)
library(dplyr)
library(lubridate)
library(ggplot2)
```


#### Import datasets
The data is a combination of 12months of data recorded monthly. from May 2021 - April 2022
```{r show_col_types=FALSE, echo=FALSE}
X202105_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202105-divvy-tripdata.csv")
X202106_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202106-divvy-tripdata.csv")
X202107_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202107-divvy-tripdata.csv")
X202108_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202108-divvy-tripdata.csv")
X202109_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202109-divvy-tripdata.csv")
X202110_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202110-divvy-tripdata.csv")
X202111_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202111-divvy-tripdata.csv")
X202112_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202112-divvy-tripdata.csv")
X202201_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202201-divvy-tripdata.csv")
X202202_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202202-divvy-tripdata.csv")
X202203_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202203-divvy-tripdata.csv")
X202204_divvy_tripdata <- read_csv("C:/Users/user/Downloads/My-second-R-project/202204-divvy-tripdata.csv")
```

#### Assigning aliases to datasets
```{r}
yy2105 <- X202105_divvy_tripdata
yy2106 <- X202106_divvy_tripdata
yy2107 <- X202107_divvy_tripdata
yy2108 <- X202108_divvy_tripdata
yy2109 <- X202109_divvy_tripdata
yy2110 <- X202110_divvy_tripdata
yy2111 <- X202111_divvy_tripdata
yy2112 <- X202112_divvy_tripdata
yy2201 <- X202201_divvy_tripdata
yy2202 <- X202202_divvy_tripdata
yy2203 <- X202203_divvy_tripdata
yy2204 <- X202204_divvy_tripdata
```

#### Data wrangling and combination
```{r May, 2021}
colnames(yy2105)
```

```{r June, 2021 }
colnames(yy2106)
```

```{r July, 2021}
colnames(yy2107)
```

```{r August, 2021}
colnames(yy2108)
```

```{r September, 2021}
colnames(yy2109)
```

```{r October, 2021}
colnames(yy2110)
```

```{r November, 2021}
 colnames(yy2111)
```

```{r December, 2021}
colnames(yy2112)
```

```{r January, 2022}
colnames(yy2201)
```

```{r February, 2022}
colnames(yy2202)
```

```{r March, 2022}
colnames(yy2203)
```

```{r April, 2022}
colnames(yy2204)
```

#### Rename colums
we will rename some colums in data set. This is to make all column names consistent.
```{r}
(yy2105 <- rename(yy2105
                   ,trip_id = ride_id
                   ,bikeid = rideable_type
                   ,start_time = started_at  
                   ,end_time = ended_at  
                   ,from_station_name = start_station_name 
                   ,from_station_id = start_station_id 
                   ,to_station_name = end_station_name 
                   ,to_station_id = end_station_id 
                   ,usertype = member_casual))
(yy2106 <- rename(yy2106
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2107 <- rename(yy2107
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2108 <- rename(yy2108
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2109 <- rename(yy2109
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2110 <- rename(yy2110
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2111 <- rename(yy2111
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2112 <- rename(yy2112
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2201 <- rename(yy2201
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2202 <- rename(yy2202
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2203 <- rename(yy2203
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
(yy2204 <- rename(yy2204
                  ,trip_id = ride_id
                  ,bikeid = rideable_type
                  ,start_time = started_at  
                  ,end_time = ended_at  
                  ,from_station_name = start_station_name 
                  ,from_station_id = start_station_id 
                  ,to_station_name = end_station_name 
                  ,to_station_id = end_station_id 
                  ,usertype = member_casual))
```

###### Inspect columns
```{r}
str(yy2105)
```

```{r}
str(yy2106)
```

```{r}
str(yy2107)
```

```{r}
str(yy2108)
```

```{r}
str(yy2109)
```

```{r}
str(yy2110)
```

```{r}
str(yy2111)
```

```{r}
str(yy2112)
```

```{r}
str(yy2201)
```

```{r}
str(yy2202)
```

```{r}
str(yy2203)
```

```{r}
str(yy2204)
```

#### Convert trip_id colum to character so that they can stack correctly.
```{r}
yy2105 <-  mutate(yy2105, trip_id = as.character(trip_id))
yy2106 <-  mutate(yy2106, trip_id = as.character(trip_id))
yy2107 <-  mutate(yy2107, trip_id = as.character(trip_id))
yy2108 <-  mutate(yy2108, trip_id = as.character(trip_id))                   
yy2109 <-  mutate(yy2109, trip_id = as.character(trip_id))
yy2110 <-  mutate(yy2110, trip_id = as.character(trip_id))
yy2111 <-  mutate(yy2111, trip_id = as.character(trip_id))
yy2112 <-  mutate(yy2112, trip_id = as.character(trip_id))
yy2201 <-  mutate(yy2201, trip_id = as.character(trip_id))
yy2202 <-  mutate(yy2202, trip_id = as.character(trip_id))
yy2203 <-  mutate(yy2203, trip_id = as.character(trip_id))
yy2204 <-  mutate(yy2204, trip_id = as.character(trip_id))
```

# We will stack individual month's data frames into one big data frame
```{r}
all_trips <- bind_rows(yy2105,
                       yy2106,
                       yy2107,
                       yy2108,
                       yy2109,
                       yy2110,
                       yy2111,
                       yy2112,
                       yy2201,
                       yy2202,
                       yy2203,
                       yy2204)
```


### Clean up data and prepare for analysis

Inspect the new created table
```{r}
colnames(all_trips)
nrow(all_trips)
dim(all_trips)
head(all_trips)
str(all_trips)
summary(all_trips)
```

##### Add columns that list the hour, date, month, day, and year of each ride
This will allow us to aggregate ride data for each hour, day, month or year before completing these operations we could only aggregate at the ride level
```{r}
all_trips$start_time=as.POSIXct(all_trips$start_time, format="%Y-%m-%d %H:%M:%S", tz= "UTC")
all_trips$date <- as.Date(all_trips$start_time) 
all_trips$month <- format(as.Date(all_trips$date), "%b/%y")
all_trips$day <- format(as.Date(all_trips$date), "%d")
all_trips$year <- format(as.Date(all_trips$date), "%Y")
all_trips$day_of_week <- format(as.Date(all_trips$date), "%A")
all_trips$Hour <- format(all_trips$start_time, format = "%H")
all_trips$Hour <- as.POSIXct(all_trips$Hour, format = "%H")
```


##### Add a "ride_length" calculation to all_trips (in seconds)
```{r}
all_trips$ride_length <- difftime(all_trips$end_time,all_trips$start_time)
```

# Inspect the structure of the columns
```{r}
str(all_trips)
```

#### Convert "ride_length" from Factor to numeric so we can run calculations on the data
```{r}
is.factor(all_trips$ride_length)
all_trips$ride_length <- as.numeric(as.character(all_trips$ride_length))
is.numeric(all_trips$ride_length)
```

#### Remove "bad" data
 The data frame includes a few hundred entries when bikes were taken out of docks and checked for quality by Divvy or ride length was negative.
 
#### We will create a new version of the dataframe (v2) since data is being removed
```{r}
all_trips_v2 <- all_trips[!(all_trips$from_station_name == "HQ QR" | all_trips$ride_length<0),]
```


## Analysis and Visualizations

#### Conduct descriptive analysis
```{r}
summary(all_trips_v2$ride_length)
```

# Compare members and casual users
```{r}
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = mean)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = median)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = max)
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype, FUN = min)
```


#### Analysis of usertypes
This is to help us quantify the different customer groups patronage within the last 12months.
```{r}
usage<- all_trips %>% 
  group_by(usertype) %>%
  count(usertype) %>% 
  drop_na() %>% 
  mutate(freq = n / 5757551) %>% 
  mutate(percentage = scales::percent(freq))
head(usage)
```



```{r}
usage %>% ggplot(aes(x="", y=percentage, fill=usertype))+
  geom_bar(stat = "identity", width = 1)+
  coord_polar(theta = "y",  start=0)+
  theme_minimal()+
  theme(axis.title.x = element_blank(),
        axis.title.y = element_blank(),
        panel.border = element_blank(),
        panel.grid = element_blank(),
        axis.ticks = element_blank(),
        axis.text.x = element_blank(),
        plot.title = element_text(hjust = 1, size=14, face = "bold"))+
  scale_fill_manual(values = c("light green", "dark green"))+
  geom_text(aes(label = percentage), 
            position = position_stack(vjust = 0.5))+
  labs(title = "User Type Distribution", subtitle = "This chart shows the user types and their patronage in the last 12months")
```
#### Observation
The chart above shows the member usertype (3,221,193) makes up a major part(56%) of our 
customers  while the casual(2,536,358) users make up 44% of our patronage in the last 12 months.While is impressive i believe more can still be done to convince our casual users
to convert to a more profitable user model.  


#### We will see the average ride time by each day for members vs casual users
```{r eval=FALSE}
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype + all_trips_v2$day_of_week, FUN = mean)  
```

#### Notice that the days of the week and months of the last 12 months are out of order. 
lets fix that.
```{r}
all_trips_v2$day_of_week <- ordered(all_trips_v2$day_of_week, levels=c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"))
all_trips_v2$month <- ordered(all_trips_v2$month, levels = c("May/21", "Jun/21",
                                                             "Jul/21", "Aug/21",
                                                             "Sep/21", "Oct/21",
                                                             "Nov/21", "Dec/21",
                                                             "Jan/22", "Feb/22",
                                                             "Mar/22", "Apr/22"))
```

#### Now, let's run the average ride time by each day for members vs casual users
```{r eval=FALSE}
aggregate(all_trips_v2$ride_length ~ all_trips_v2$usertype + all_trips_v2$day_of_week, FUN = mean)
```


#### Analyze ridership data by type and weekday
```{r}
all_trips_v2 %>% 
  mutate(weekday = wday(start_time, label = TRUE)) %>% 
  group_by(usertype, weekday) %>% drop_na() %>% 
  summarise(number_of_rides = n() ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, weekday) 
```


#### Let's visualize the number of rides by rider type
```{r}
all_trips_v2 %>% 
  mutate(weekday = wday(start_time, label = TRUE)) %>% 
  group_by(usertype, weekday) %>% 
  drop_na() %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, weekday)  %>% 
  ggplot(aes(x = weekday, y = number_of_rides, fill = usertype)) +
  geom_col(position = "dodge")+
  labs(title = "Number of rides vs Weekday", subtitle = "This graph captures how users utilize our services by weekdays.")
```

#### Observation
From the visualization above it can be observed that member usertypes use cyclistic more of often than the casual usertypes during the mid-week but on weekends the causual usertypes make use of cyclistic more often.This trend could be interpreted to mean that member usertypes are working class who use bikes to commute to and or from work in order to keep fit.


#### Let's visualize the Rider type by Ride duration
```{r}
all_trips_v2 %>% 
  mutate(weekday = wday(start_time, label = TRUE)) %>% 
  group_by(usertype, weekday) %>% 
  drop_na() %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, weekday)  %>% 
  ggplot(aes(x = weekday, y = average_duration/60, fill = usertype)) +
  geom_col(position = "dodge")+
  labs(title = "Average Ride duration vs Weekday", subtitle = "This visualization expresses the time span of bike useage by weekday for the usertypes.", y = "Average Duration")
```

#### Observation
The visualization above shows weekday trends that reveal that casual usertypes use cyclistic for average more duration than member usertypes.This means that our casual usertypes find our bikes more appealing for long trips.

#### Let's Analyze bike usage by time of the day
```{r}
all_trips_v2 %>% 
  group_by(usertype, Hour ) %>% 
  summarise(number_of_rides = n()) %>% 
  drop_na() %>% 
  ggplot(aes(x = Hour, y = number_of_rides, color = usertype, group = usertype)) +
  geom_line(size = 1)+ scale_x_datetime(date_breaks = "1 hour",
                            date_labels =  "%H", expand = c(0,0))+
  theme(axis.text.x = element_text(angle = 45))+
  labs(title = "Number of rides vs Time of the day", subtitle = "The graphic below captures the hour of the day and frequency of bike useage by the user types.", x = "Time of Day",y = "Number of Rides")
  
```

#### Oberservations
The visual above captures the hourly usage of bikes by our user types. from the above we can infer that member peak usage is 5:00 PM in the evening.Apart for that it can also be observed that there is a rapid increase in demand for bikes by casual usertypes from 6:00AM till 5:00PM.

#### Let's visualize rides by months covered in this analysis
```{r}
all_trips_v2 %>% 
  mutate(Month = month(start_time, label = TRUE)) %>% 
  group_by(usertype, Month) %>% drop_na() %>% 
  summarise(number_of_rides = n() ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, Month)
```


```{r}
all_trips_v2 %>% 
  group_by(usertype, month) %>% 
  drop_na() %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, month)  %>% 
  ggplot(aes(x = month, y = number_of_rides, fill = usertype)) +
  geom_col(position = "dodge")+
  theme(axis.text.x = element_text(angle = 45))+
  labs(title = "Number of Rides by Months", 
       subtitle = "This visual covers the bike patronage by the users over the last 12 months",
       x = "Months",
       y = "Number of Rides")
```

#### Observation
Scrutiny of this graph reveals that patronage by the casual usertype peaks 
in summer months. According to the national geographic website, summer begins
June 1. This visualization signals that the casual usertypes begin to make use
of our bikes more often from the end of spring till autum when casual patronage
begins to decline again. This means their is a correlation between bike usage and seasonality  

#### Average duration by months
```{r}
all_trips_v2 %>% 
  group_by(usertype, month) %>% 
  drop_na() %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length)) %>% 
  arrange(usertype, month)  %>% 
  ggplot(aes(x = month, y = average_duration/60 , fill = usertype)) +
  geom_col(position = "dodge")+
  theme(axis.text.x = element_text(angle = 45))+
  labs(title = "Average Ride Duration by Months",
       subtitle = "This barchart visualizes the average time span of bike usage by users over the past 12 Months",
       x = "Months",
       y = "Average Duration")
```

#### Observation
The graphic above expresses that the duration of ride by members are relatively 
stable all year round while that of the casual users are higher all year round
and peaks around summer months. 

#### Analysis of type of bike used by customer types
```{r}
bike_usage<- all_trips_v2 %>% 
  group_by(usertype, bikeid) %>% 
  count() %>% drop_na()
head(bike_usage)
```

```{r}
bike_usage %>% 
  ggplot(aes(x=bikeid, y=n, fill = usertype))+
  geom_col(position = "dodge")+
  labs(title = "Bike type by Usertype", subtitle = "A chart to show how users interact with the various bike types.",x="Bike type", y="Number of Bikes")
```

#### Observation
The visual above conveys that both usertypes make use of the classic bikes more
then the other bike types and the members did not make use of the docked bike which is perplexing.



## Summary and recommendations for Cyclistic membership:

![Bike_man](C:\Users\user\Desktop\Bike_man.jfif)


**What is Cyclistic annual membership?**
Cyclistic Annual membership is one of the user type group offered by cyclistic which enable users to pay a one time fee that allows them unlimited access rides all year round. 


## Insights from the data
* Majority of our bike users are Annual members.
* Casual users make use of bikes more often on weekends but there is a stable usage of
  bikes by annual members weekdays and increases a little on weekends. This a signal that our         members commute to work with their bikes a lot.
* Casual users begin to ride demand begins to rise during spring, peaks during summer and begins to   decline during fall. For annual members it is almost the same except demand doesn't decline as
  quickly during fall.
* Annual users tend to use bikes for shorter trips than casual users. The average trip duration 
  of casual users is more than double that of Annual members in peak months of summer and few
  steps shy double all year round.
* Generally, members pick more rides through the day but bike usage peaks around 05:00PM daily       for the member user type groups however there is smaller peak during morning rush hours.            while casual users demand rise gradually till it peaks in the evening as well.
* while it is perplexing, it is still worthy of note that the member usertype did not make use of
  docked bike in the last 12months. The favourite bike of the both users is the classic bike.


#### Recommendations 

**Target Audience:** : 9 - 5 Workers

* Ad campaigns should be targeted towards single young adults and middle age workers whose work       place is not too far from their homes.
* Casual users of middle age should be targeted with digital ads from afternoon to evening period    because that's when they are most active.
* Ads should emphasize why taking bikes during colder months is very necessary and how a membership
  will help casual users stick to bikes.
* Ads should help users know that short trips over long periods will keep them fit always and        enrolling for memberships will help them ensure they take those trips
* pricing should reflect that it is economically smarter to enroll for membership for regular  casuals.
* It could also not hurt to introduce monthly memberships.

