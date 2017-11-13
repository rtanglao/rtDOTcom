---
layout: post
title: "Cleaning dates and removing outliers with R using lubridate and other R packages using the Kaggle Taxis dataset"
---
From [Kaggle - Taxis](http://rpubs.com/jackh08/298981):

* 1\. Shouldn't this be using pipes i.e. ```%>%```?:

```R
train_kaggle$distance = distance(train_kaggle$pickup_latitude, train_kaggle$pickup_longitude, 
    train_kaggle$dropoff_latitude, train_kaggle$dropoff_longitude)
```

* 2\. Some ```lubridate``` code:

**QUOTE**

<blockquote>
The hour of day of the pick up is added and a daytime boolean (between 8:00 and 20:00) is added.
</blockquote>

```R
# Add time of pickup----
t.lub.train <- ymd_hms(train_kaggle$pickup_datetime)

train_kaggle$pickup_hour <- as.numeric(format(t.lub.train, "%H")) + as.numeric(format(t.lub.train, 
    "%M"))/60

# Add daytime
train_kaggle$Daytime = (train_kaggle$pickup_hour < 20) & train_kaggle$pickup_hour > 
    8
test_kaggle$Daytime = (test_kaggle$pickup_hour < 20) & test_kaggle$pickup_hour > 
    8
```

**END QUOTE**

* 3\. How to remove outliers:

**QUOTE**

<blockquote>
Outliers are removed as follows:<br />
Trips with distance of 0 km.<br />
Trips over 40 km<br />
Trips over 20000 seconds<br />
Trips with average speed over 50 km/ hour<br />
</blockquote>

```R
train_kaggle = train_kaggle[train_kaggle$distance != 0, ]
train_kaggle = train_kaggle[train_kaggle$distance < 40, ]
train_kaggle = train_kaggle[train_kaggle$trip_duration < 20000, ]
train_kaggle = train_kaggle[train_kaggle$speed < 50, ]
```

**END QUOTE**