# SocialMedia-Twitter-NullClass

# NullClass-Data-Analytics (PowerBI) (1 Month Internship)

# Introduction

Social media platforms play a significant role in shaping modern communication, marketing strategies, and audience engagement. Analyzing data from these platforms provides organizations with critical insights into user behavior, preferences, and engagement trends.

Twitter, one of the most influential social media platforms, serves as a goldmine for real-time data analysis. With millions of tweets shared daily, it provides a wide array of metrics such as impressions, clicks, likes, retweets, and engagement rates. These metrics help measure the effectiveness of social media strategies and understand user interaction patterns.

## Task 1: Create a visual that shows the average engagement rate and total impressions for tweets posted between '01- 01-2020' and '30-06-2020'. Filter out tweets that received fewer than 100 impressions and like should be 0 and this graph should work only between 3Pm to 5 PM IST apart from that we should not show the graph.

#### Objective :

The primary objective of Task 1 is to analyze tweet engagement by focusing on specific criteria to identify patterns and trends in user interactions. This involves:

1. Calculating the average engagement rate and total impressions for tweets posted within the specified date range (01-01-2020 to 30-06-2020).

2. Filtering tweets to include only those with:
* At least 100 impressions.
* Zero likes to focus on underperforming tweets.

3. Ensuring the graph is displayed only between 3 PM to 5 PM IST, aligning with a targeted analysis window.

4. Visualizing the results to derive actionable insights that can help optimize engagement strategies during specific timeframes.


## Task 2: Create a clustered bar chart that breaks down the sum of URL clicks, user profile clicks, and hashtag clicks by tweet category (e.g., tweets with media, tweets with links, tweets with hashtags). Only include tweets that have at least one of these interaction types and this graph should work between 3 PM to 6 PM and the tweet date should be even number as well as tweet word count be below 40.

#### Objective : 

The goal of Task 2 is to analyze interaction patterns across different tweet categories to understand how various content types drive user engagement. Specifically, this task involves:

1. Breaking down interactions into three categories:
* URL clicks
* User profile clicks
* Hashtag clicks

2. Categorizing tweets based on their content type:
* Tweets with media.
* Tweets with links.
* Tweets with hashtags.

3. Filtering tweets to include only those with at least one of the specified interaction types.

4. Ensuring the visual (clustered bar chart) adheres to these constraints:
* Tweets posted on even-numbered dates.
* Tweets with a word count below 40.
* The graph should only function between 3 PM and 6 PM IST.

## Task 3: Analyse tweets to show a comparison of the engagement rate for tweets with app opens versus tweets without app opens. Include only tweets posted between 9 AM and 5 PM on weekdays and this graph should work between 12 PM to 6 PM and the tweet impression should be even number and tweet date should be odd number as well as tweet word count be below 40.

#### Objective : 

The objective of Task 3 is to compare the engagement rates of tweets based on whether users opened the app to engage with the content or interacted without opening the app. This analysis aims to uncover behavioral patterns and optimize strategies for improving engagement. The task involves:

1. Comparing Engagement Rates:

* Group tweets into two categories:
* Tweets with app opens.
* Tweets without app opens.

2. Filtering Criteria:

* Include only tweets posted between 9 AM and 5 PM on weekdays.

 Filter tweets where:

* Impressions are even numbers.
* Tweet dates are odd numbers.
* Tweet word count is below 40 words.

3. Time-Restricted Visual:

* Ensure the graph is displayed only between 12 PM and 6 PM IST, aligning with the analysis period for targeted insights.

#### Data Cleaning:

Clean the data by:

* removing rows that have values which are missing,
* changing the data type within a column, and
* removing columns which are not relevant to this task.
* splite column.
* rename column

#### Tools : PowerBI

## DAX (Calculated Column)

* Even date = IF(MOD(DAY(SocialMedia[Date]), 2) = 0,"Even","Odd")
* Has Interaction = IF(SocialMedia[url clicks] > 0 || SocialMedia[userprofileclicks] > 0 || SocialMedia[hashtag clicks] > 0,1, 0)
* IsEvenImpressions = IF(MOD(SocialMedia[impressions], 2) = 0, TRUE(), FALSE()) 
* IsOddDate = IF(MOD(DAY(SocialMedia[Date]),2) = 1, true (), FALSE ())
* IsTweetValid = IF(SocialMedia[IsOddDate] && SocialMedia[IsEvenImpressions]  && SocialMedia[IsWithInWorkHour] && SocialMedia[IsWordCountValid] && SocialMedia[IsWithInGraphTime], TRUE(), FALSE())
* IsWeekday = IF(WEEKDAY(SocialMedia[Date], 2) <= 5,TRUE(),FALSE())
* IsWithInGraphTime = IF(HOUR(SocialMedia[Time]) >= 12 && HOUR(SocialMedia[Time]) <= 18,TRUE(),FALSE())
* IsWithInWorkHour = IF(SocialMedia[Time] >= TIME(9,0,0) && SocialMedia[Time] <= TIME(17,0,0),TRUE(),FALSE())
* IsWordCountValid = IF(SocialMedia[Word count] < 40, TRUE(), FALSE())
* Task_1 Time Range = IF(HOUR(SocialMedia[Time]) >= 15 && HOUR(SocialMedia[Time]) < 17, "03 PM - 05 PM","Outside Range")
* Task_2 Time Range = IF(HOUR(SocialMedia[Time]) >= 15 && HOUR(SocialMedia[Time]) < 18,"3 PM - 6 PM","Outside range")
* Tweet Category = SWITCH(TRUE(),SocialMedia[media views] > 0, "Tweets with Media",SocialMedia[url clicks] > 0, "Tweets with Links",SocialMedia[hashtag clicks]  > 0, "Tweets with Hashtag","Other")
* TweetCate = IF(SocialMedia[Has Interaction] = 1, "with app opens", "without app opens")
* Weekday = SWITCH(WEEKDAY(SocialMedia[Date], 2), 1, "Monday", 2, "Tuesday", 3, "Wednesday", 4, "Thursday", 5, "Friday", 6, "Saturday",7, "Sunday")
* Word count = LEN(TRIM(SocialMedia[Tweet])) - LEN(SUBSTITUTE(TRIM(SocialMedia[Tweet]), " ", "")) + 1

## Charts Involved :

* Line and Clustered Column Chart
* Clustered Bar Chart
* Clustered Column Chart
* Use Filter Pane to Filter Data
