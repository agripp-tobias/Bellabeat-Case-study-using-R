# Bellabeat-Case-study-using-R
Bellabeat Time Wellness Project
## Loading packages
library(tidyverse)
library(lubridate)
library(janitor)
library(broom)
library(data.table)
library(scales)
library(readxl)
## Change date formats
if(!"ActivityDate" %in% names(activity)) stop("Check activity file: column ActivityDate expected")
activity <- activity %>% mutate(date = mdy(ActivityDate))

if(!"SleepDay" %in% names(sleepday)) stop("Check sleepday file: column SleepDay expected")
sleepday <- sleepday %>% mutate(SleepDay = parse_date_time(SleepDay, orders = c("mdy HMS","mdy","ymd HMS","ymd")),
                          date = as_date(SleepDay),
                          sleep_hours = TotalMinutesAsleep/60,
                          time_in_bed_hours = TotalTimeInBed/60)
if(!"ActivityHour" %in% names(hourlysteps)) stop("Check hourlySteps file: column ActivityHour expected")
hourlysteps <- hourlysteps %>%
  mutate(ActivityHour = parse_date_time(ActivityHour, orders = c("ymd HMS","mdy HMS","ymd HM","mdy HM")),
         hour = hour(ActivityHour),
         date = as_date(ActivityHour))
intensity <- intensity %>%
  mutate(ActivityHour = parse_date_time(ActivityHour, orders = c("ymd HMS","mdy HMS","ymd HM","mdy HM")),
         hour = hour(ActivityHour),
         date = as_date(ActivityHour))
  ## Standardize column names
  library(janitor)
activity <- clean_names(activity)
sleepday <- clean_names(sleepday)
hourlysteps <- clean_names(hourlysteps)
intensity <- clean_names(intensity)
colnames(activity)
# Summarize daily totals
daily_user_summary <- activity %>%
  group_by(date) %>%
  summarise(
    daily_steps = sum(total_steps, na.rm = TRUE),
    daily_active_minutes = sum(active_minutes, na.rm = TRUE),
    daily_calories = sum(calories, na.rm = TRUE),
    daily_sedentary = sum(sedentary_minutes, na.rm = TRUE)
  )
  # Plot daily steps
daily_summary <- activity %>%
  group_by(date) %>%
  summarise(
    total_steps = sum(total_steps, na.rm = TRUE),
    total_active_minutes = sum(active_minutes, na.rm = TRUE),
    total_calories = sum(calories, na.rm = TRUE)
  )
ggplot(daily_summary, aes(x = date, y = total_steps)) +
  geom_line(color = "steelblue") +
  labs(title = "Daily Steps Over Time", x = "Date", y = "Total Steps") +
  theme_minimal()
  
## Steps vs. Calories
ggplot(data = activity, aes(x = total_steps, y = calories)) + geom_point() + geom_smooth() + labs(title = "Total Steps vs. Calories")

# Activity by Weekday vs Weekend
activity_by_daytype <- activity %>%
  group_by(weekday) %>%
  summarise(
    avg_steps = mean(total_steps, na.rm = TRUE),
    avg_active_minutes = mean(active_minutes, na.rm = TRUE),
    avg_calories = mean(calories, na.rm = TRUE)
  )
ggplot(activity_by_daytype, aes(x = weekday, y = avg_steps, fill = weekday)) +
  geom_col() +
  labs(title = "Average Steps: Weekday vs Weekend", y = "Average Steps") +
  theme_minimal()

  # Sleep summary
sleep_summary <- sleepday %>%
  group_by(date) %>%
  summarise(
    avg_sleep_hours = mean(sleep_hours, na.rm = TRUE),
    avg_time_in_bed = mean(time_in_bed_hours, na.rm = TRUE)
  )
sleep_activity <- activity %>%
  left_join(sleepday %>% select(id, date, sleep_hours), by = c("id", "date"))

cor(sleep_activity$total_steps, sleep_activity$sleep_hours, use = "complete.obs")
## [1] -0.1903439
# Activity vs Sleep Correlation
ggplot(sleep_activity, aes(x = total_steps, y = sleep_hours)) +
  geom_point(alpha = 0.5) +
  geom_smooth(method = "lm", color = "red") +
  labs(title = "Daily Steps vs Sleep Hours", x = "Total Steps", y = "Sleep Hours") +
  theme_minimal()
## Steps vs. Hours
  hourlysteps %>%
  group_by(hour) %>%
  summarise(avg_steps = mean(step_total, na.rm=TRUE)) %>%
  ggplot(aes(x=hour, y=avg_steps)) +
  geom_line(color="blue") +
  labs(title="Average Steps by Hour of Day", x="Hour", y="Average Steps")
