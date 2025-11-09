# Bellabeat-Case-study-using-R
## Bellabeat Case Study: Analyzing Smart Device Data for Growth
This project is a detailed case study conducted as a Junior Data Analyst for Bellabeat, a high-tech wellness company focused on products for women. The objective was to analyze public smart device data to uncover user activity, sleep, and lifestyle patterns. These insights are used to recommend actionable marketing strategies for Bellabeat's flagship product, the Time watch.

The analysis followed the six-step data analysis process: Ask, Prepare, Process, Analyze, Share, and Act.

## Business Task
Analyze public smart device data to identify user activity, sleep, and lifestyle patterns and leverage these insights to recommend marketing strategies for Bellabeat's Time watch.

## Tools and Technologies
R Programming Language
RStudio
Tidyverse (for data manipulation and visualization)
Lubridate (for date-time handling)
Janitor (for data cleaning)

# Data Source
The primary data source is FitBit Fitness Tracker Data, a public dataset available on Kaggle.

## Key Data Limitations:

Small Sample Size: Data is from only 33 distinct users.

Demographic Gap: The dataset lacks demographic information (e.g., gender and age), which is crucial given Bellabeat's target audience of women.

Outdated: The data was collected in 2016 and may not reflect current fitness trends.

## Key Findings and Insights 

High Sedentary Time: The average user recorded approximately 7,638 steps per day, but also spent about 16.5 hours in sedentary behavior. This indicates a significant opportunity to encourage movement throughout the day.

Steps Drive Calories: A strong positive correlation exists between total steps and calories burned, confirming that greater activity directly leads to higher calorie expenditure.
Weekend Activity Peak: Users are most active on Saturdays and least active on Sundays.

Activity vs. Sleep Trade-off: There is a slight negative correlation between daily steps and sleeping hours—as users sleep more, total steps tend to decrease.

Engagement Decline: Total step counts show a noticeable downward trend starting in early May, suggesting reduced user engagement over time.

Peak Activity Hours: The highest activity periods occur during the late afternoon and early evening (4 PM – 8 PM), likely reflecting post-work activities.
## Recommendations for Bellabeat's Marketing

Enhance Engagement with Gamification: To combat the decline in daily steps, integrate personalized reminders, goal adjustments, or gamified challenges to sustain user motivation over time.

Leverage Weekend Activity: Launch targeted campaigns, such as a "Weekend Wellness Challenge," and send timely app notifications on Friday afternoons or Saturday mornings to maximize high-activity periods.

Boost Weekday Movement: Share bite-sized wellness content (e.g., short workouts, mindfulness exercises) to increase activity and engagement during the work week.
