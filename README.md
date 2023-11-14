# Bellabeat-Data-Analysis-Case-Study

Bellabeat is a wellness brand for women with a variety of products and services focused on women’s health. The company develops wearables and accompanying products that monitor biometric and lifestyle data to help women better understand how their bodies work and make healthier choices. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women. By 2016, Bellabeat had opened offices around the world and launched multiple products. Bellabeat products became available through a growing number of online retailers in addition to their own e-commerce channel on their website. The company has invested in traditional advertising media, such as radio, out-of-home billboards, print, and television, but focuses on digital marketing extensively.(https://bellabeat.com/)

### **Characters:**
* **Urška Sršen**: Bellabeat’s co-founder and Chief Creative Officer
* **Sando Mur**: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
* **Bellabeat marketing analytics team**: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. You joined this team six months ago and have been busy learning about Bellabeat’s mission and business goals — as well as how you, as a junior data analyst, can help Bellabeat achieve them.

### **Products:**
* **Bellabeat app**: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
* **Leaf**: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf Tracker connects to the Bellabeat app to track activity, sleep, and stress.
* **Time**: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
* **Spring**: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.
* **Bellabeat membership**: Bellabeat also offers a subscription-based membership program for users. Membership gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health, beauty, and mindfulness based on their lifestyle and goals.

## **ASK**

### **Scenario**:
Urška Sršen, co-founder and Chief Creative Officer of Bellabeat believes that analyzing smart device fitness data could help unlock new growth opportunities for the company. As a Junior Data Analyst, I have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. 

### **There are three main questions that need to be answered**:
1. What are some trends in smart device usage? 
2. How could these trends apply to Bellabeat customers? 
3. How could these trends help influence Bellabeat's marketing strategy?

### **Business task**
Perform data analysis on non-Beallabeat's products to discover consumer usage trends and provide founded insights and high-level recommendations to Bellabeat’s stakeholders Urška Sršen CCO and Sando Mur: Mathematician and Bellabeat’s cofounder.

## **PREPARE**

### **About the data**

The data source used in this analysis is a Kaggle data set. The crowd-sourced Fitbit dataset, dated 03.12.2016-05.12.2016, is in the form of 18 CSV files that were generated by respondents to a distributed survey via Amazon Mechanical Turk. It was placed in Zenodo, where it got a DOI and had a license of CC0: Public Domain.

The Digital Object Identifier DOI of this data is 10.5281/zenodo.53894. It was posted on Zenodo by Furberg, Robert; Brinton, Julia; Keating, Michael; Ortiz, Alexa. The data was collected through a survey so there are limitations on verifying its integrity, however, the data was used and uploaded in Zenodo, which is a safe and credible website operated by CERN and OpenAIRE to ensure that everyone can join in Open Science.

There are some issues with bias or credibility in this data. Data could be biased since there is no information about consumers who submitted the responses, we are not aware of their gender, age, and so on. The data is not from Bellabeat's product and the usage of FitBit could slightly differ from BellaBeat's products. Ideally, to make data-driven decisions and have data analysis for BellaBeat, we would have the data from the BellaBeat product.

### **Evaluation of ROCCC**

* **Reliable** - Data is not necessarily very reliable since it’s not Bellabeat’s data and it’s only 30 consumers' data.
* **Original** - The data is not original and was produced by a third party - Amazon Mechanical Turk.
* **Comprehensive** - The data is somewhat comprehensive since it has 18 datasets, that include calories, steps, sleep and so on which are relevant to our analysis.
* **Current** - The data is from 2016 so it’s not super current. At the time of the analysis, it’s 7 years old, which could mean that usage and trends during this time have changed.
* **Cited** – The data on Kaggle has been used many times by various analysts, in Zenodo, where it got the DOI, it was cited 3 times.

## **PROCESS**

### **Tools for the process**

To clean, manipulate, and analyze the data I have chosen **R programming language**. I will ensure data integrity by not making any changes to the actual data, but rather creating new data frames and manipulating data that way. Also, I will be keeping notes of all changes made and actions taken regarding this data.

### **Start of data processing**

I have uploaded the dataset to **RStudio**. Once all 18 CSV files have been uploaded, I have installed and uploaded tidyverse package and set the working directory.
```
# installing and uploading tidyverse
install.packages("tidyverse")
library(tidyverse)
# setting working directory
setwd("/cloud/project/Fitabase Data 4.12.16-5.12.16")
```

### Choosing the files to work with

I looked through the CSV files in the File pane and immediately decided not to use the following files: 

hourlyCalories_merged.csv, hourlySteps_merged.csv, minuteCaloriesNarrow_merged.csv, minuteCaloriesWide_merged.csv, minuteIntensitiesNarrow_merged.csv, minuteIntensitiesWide_merged.csv, minuteSleep_merged.csv, minuteStepsNarrow_merged.csv, minuteStepsWide_merged.csv, minuteMETsNarrow_merged.csv.

I chose to analyze daily patterns rather than minute and hour ones because I believe they will provide more useful insights. Then, I read the remaining CSV files and assigned them data frames.

```
#reading files in the data set and assigning them data frames
daily_activity<-read.csv('dailyActivity_merged.csv')
daily_calories <- read.csv('dailyCalories_merged.csv')
daily_intensities <- read.csv('dailyIntensities_merged.csv')
daily_steps <- read.csv('dailySteps_merged.csv')
heartrate_seconds <- read_csv('heartrate_seconds_merged.csv')
hourly_intensities <-read.csv('hourlyIntensities_merged.csv')
minute_METs <- read.csv('minuteMETsNarrow_merged.csv')
sleep_day <- read.csv('sleepDay_merged.csv')
weight_log_info <- read.csv('weightLogInfo_merged.csv')
```

After assigning CSV files data frames, I got familiar with the data, to see which CSV files I would be using for the analysis. I used head() and n_distinct() functions to get familiar with data frames daily_activity, daily_calories, daily_intensities, daily_steps.

```
#trying to get familiar with data 
head(daily_activity)
head(daily_calories)
head(daily_intensities)
head(daily_steps)
n_distinct(daily_activity$Id)
n_distinct(daily_calories$Id)
n_distinct(daily_intensities$Id)
n_distinct(daily_steps$Id)
```

<img width="651" alt="head1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/c815230a-dd72-4fac-acf5-b920303ff82f">
<img width="671" alt="head 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/e1323a5d-ad88-4e5a-99b5-025df65e4424">

From performing this code, it was obvious that daily_calories, daily_intensities, and daily_steps are already in the daily_activity data frame, so I will be using daily_activity data frame for further analysis. There are also 33 distinct Ids in all 4 data frames, where it should be 30.

Next, I got familiar with the remaining data frames.

```
# getting familiar with heartrate_seconds data frame
head(heartrate_seconds)
n_distinct(heartrate_seconds$Id)
```

<img width="192" alt="heart" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/28adee23-8a1e-439c-9e3b-f947c2ba103b">

After executing the code it was clear that there are less than half unique Id's than it should be, so this data frame will not be used for further analysis. Next, I got familiar with hourly_intensities and sleep_day data frames.

```
# getting familiar with hourly_intensities and sleep_day data frames
head(hourly_intensities)
n_distinct(hourly_intensities$Id) 
head(sleep_day)
n_distinct(sleep_day$Id)
```

<img width="429" alt="head 3" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/14c2efd2-1a71-4afb-9c88-1e20457cf62c">

After executing the code, it looks like these two data sets can be useful for further analysis.

```
# getting familiar with weight_log_info data frame
head(weight_log_info)
n_distinct(weight_log_info$Id)
```

<img width="434" alt="head 4" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/7b252bd1-0456-475f-bab1-25b78ba87551">

Unfortunately, after running the code it was clear that I could not use the data frame weight_log_info, since there are only 8 distinct Ids in this data frame. 

### **Files that will be used for processing and analysis:**

After reviewing all data frames, I have decided to use the following for further processing and analysis:

* **daily_activity**
* **hourly_intensities**
* **sleep_day**

### Cleaning selected data frames - Daily Activity

First, I've started with the **daily_activity** data frame. Running glimpse() and str() functions gave me basic information like the data frame has 940 rows and 15 columns, I was also presented with the data type of each variable. That is where I've noticed that ActivityDate is a character and not a date type of variable, which I would need to change.

```
# gathering basic information about daily_activity data frame
glimpse(daily_activity)
str(daily_activity)
```

<img width="642" alt="daily activity 1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/38c39c34-ea55-4b71-96fa-5c320629e2c6">

I've checked to see how many distinct Ids there were, also if there were any NA values or duplicates. Distinct 33 Id, no NA or duplicate values were found.

```
# number of distinct Id in the daily_activity data frame
n_distinct(daily_activity$Id)

# checking to see if there is any null values in the data frame 
sum(is.na(daily_activity))

# checking for duplicates
sum(duplicated(daily_activity))
```
<img width="290" alt="daily activity 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/b216ba0c-6ab6-49fa-8152-d9b3e46b9c7c">

Since there were no NA values, and no duplicates, it was time to change the data type of ActivityDate. I've installed the necessary package lubridate and changed the data type.

```
# installing and leading needed package
install.packages("lubridate")
library(lubridate)
​
#changing ActivityDate data type
daily_activity$Date <- mdy(daily_activity$ActivityDate)
​
#checking to see if the data type has been changed correctly
str(daily_activity)
```

<img width="491" alt="daily activity 3" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/5f2b571a-3d6a-46cb-a73c-7abc33db86a0">

The next step was creating a new column from Date that would showcase Date in Weekday format. Also creating new columns transforming minutes to hours, changing data type of Calories and Total_Steps cleaning up column names, and making them neater. At last, I created a new data frame with only those columns that I intended to use.

```
# now I will be creating a new column for weekdays
daily_activity$Weekday <- wday(daily_activity$Date, label=TRUE)
head(daily_activity)

# creating active hours column combining all activities
daily_activity$ActiveHours <-((daily_activity$VeryActiveMinutes)+(daily_activity$FairlyActiveMinutes)+
                                (daily_activity$LightlyActiveMinutes))/60

# creating sedentary hours column
daily_activity$SedentaryHours <-(daily_activity$SedentaryMinutes)/60

# creating different active hours columns
daily_activity$VeryActiveHours <-(daily_activity$VeryActiveMinutes)/60
daily_activity$FairlyActiveHours <-(daily_activity$FairlyActiveMinutes)/60
daily_activity$LightlyActiveHours <-(daily_activity$LightlyActiveMinutes)/60

# making the column names neat
colnames(daily_activity) <- gsub("([a-z])([A-Z])", "\\1_\\2", colnames(daily_activity))

#making calories and total steps as numeric 
daily_activity$Calories <- as.numeric(daily_activity$Calories)
daily_activity$Total_Steps <- as.numeric(daily_activity$Total_Steps)

# creating data frame from daily_activity with only columns that I will use
library(dplyr)
daily_activity2 <- daily_activity %>%
  select(Id, Date, Weekday, Calories, Total_Steps, Total_Distance, Very_Active_Distance, Moderately_Active_Distance, Light_Active_Distance, Active_Hours, Sedentary_Hours, Very_Active_Hours, Fairly_Active_Hours, Lightly_Active_Hours) 
head(daily_activity2)
```
<img width="691" alt="daily activity 4" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/5bcda388-d4f2-4fd2-86fb-12b9f74d4ad4">
<img width="712" alt="daily activity 5" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/b212e277-af6a-40ad-965e-1a0c4629f632">
<img width="742" alt="daily activity 6" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/42638763-f7a4-40fa-8eed-652fa2d1c62c">

Cleaning and manipulating daily activity was done. Next, it was time for another data frame.

### Cleaning selected data frames - Hourly Intensities

I've run head(), glimpse(), and str() for basic information about the data frame. The hourly intensities data frame consists of 4 columns and 22099 rows. ActivityHour contains date and time in one column, so I will separate them and change the data type of Time. Also, column names need some manipulation to make them neater.

```
# now lets dive in to another data set - hourly intensities
head(hourly_intensities)
str(hourly_intensities)
glimpse(hourly_intensities)

#checking for distinct Ids
n_distinct(hourly_intensities$Id)

# check if there is na values
sum(is.na(hourly_intensities))

# checking for duplicates
sum(duplicated(hourly_intensities))
```

I've also checked for unique Ids, NA values, and duplicates. The number of unique Ids is 33, and no Null values or duplicates were found. Then, I manipulated the column names and separated Activity_Hour column into 2 using the str_split_fixed() function. I've changed the Time data type and formatted it so that when I will need to make a chart the hours will go in order.

```
# after looking at the data set, we can see that we need to make col names neat

colnames(hourly_intensities) <- gsub("([a-z])([A-Z])", "\\1_\\2", colnames(hourly_intensities))
glimpse(hourly_intensities)

# create two separate columns from activity hour to have only hours and only date

library(stringr)

hourly_intensities[c('Date', 'Time')] <- str_split_fixed(hourly_intensities$Activity_Hour, ' ', 2)

#changing the format of new column Time

install.packages("chron")
library(chron)

hourly_intensities$Time <- strptime(hourly_intensities$Time, format = "%I:%M:%S %p")

# extract only the hours and format the result to include AM/PM
hourly_intensities$Time <- factor(format(hourly_intensities$Time, format = "%I %p"),
                                  levels = c("12 AM", "01 AM", "02 AM", "03 AM", "04 AM", "05 AM", 
                                         "06 AM", "07 AM", "08 AM", "09 AM", "10 AM", "11 AM", 
                                         "12 PM", "01 PM", "02 PM", "03 PM", "04 PM", "05 PM", 
                                         "06 PM", "07 PM", "08 PM", "09 PM", "10 PM", "11 PM"))

glimpse(hourly_intensities)
```
<img width="725" alt="hourly intensities 1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/278ed693-bb40-4f4b-b4db-e150f1cecb80">
<img width="733" alt="hourly intensities 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/a451ebfe-8289-4f0e-acfe-d60b877d3990">

Cleaning and manipulating of **hourly intensities** data frame was done. Next, it was time to clean and manipulate **sleep day** data frame.

### Cleaning selected data frames - Sleep Day

I've run head(), glimpse(), and str() for basic information about the data frame. The sleep day data frame  consists of 5 columns and 413 rows. I've also checked for unique Ids, NA values, and duplicates. The number of unique Ids is 24, no Null values but 3 duplicates were found. I've removed duplicates with distinct() functions and manipulated column names.

```
# cleaning the sleep data data frame
head(sleep_day)
glimpse(sleep_day)
str(sleep_day)

# unique Ids
n_distinct(sleep_day$Id)

#checking for NA values
sum(is.na(sleep_day))

# checking for duplicates
sum(duplicated(sleep_day))

#removing duplicates
sleep_day <- distinct(sleep_day)
sum(duplicated(sleep_day))

#making col names neat
colnames(sleep_day) <- gsub("([a-z])([A-Z])", "\\1_\\2", colnames(sleep_day))
View(sleep_day)
```

<img width="734" alt="sleep day" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/bdac6788-ceb2-4058-962b-c0550d42c834">
<img width="347" alt="sleep day 1" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/eb30edfa-1a87-414d-b1ac-efa45901b553">
<img width="360" alt="sleep day 2" src="https://github.com/xgabrielex/Bellabeat-Data-Analysis-Case-Study/assets/150829287/05e70d11-a160-4d76-9891-7ecaa929b521">

Cleaning of all three selected data frames was done. Now the time has come for analysis of the data.

## **ANALYZE**








