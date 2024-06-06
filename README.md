# Data Portfolio Project : Top USA YouTubers 2024
## Excel to SQL to Power BI



# Table of Contents


# Business Case

Sharon works for a social media agency and is the head of marketing. She wants to run successful marketing campaigns with successful YouTubers from the USA. She has a budget approved by the board so she wants to be certain where to channel the budget towards.

# Objective

The Head of Marketing wants to find out who the top YouTubers are in 2024 to decide on which YouTubers would be best to run marketing campaigns throughout the rest of the year.


- How will we help Sharon run successful and profitable marketing campaigns?


We will utilize 2024 YouTube data to create a dashboard and draw insights from the dashboard. This data will include : 

- Subscriber Count 
- Total Views
- Total Videos, and
- Engagement Metrics

We will analyze this information to provide informed recommendations on which YouTuber to collaborate with to Sharon and the marketing team.

### Challenges

Trying to find successful youtubers she can work with, but : 

- Struggled to find the right information on the internet, there are inconsistencies with whom she should work with
- 3rd party providers are out of budget, and
- BI reporting team does not have the bandwidth to assist Sharon with the assignment

Solution : 

Create a simple dashboard that displays the top USA Youtubers by : 

- Subscribers
- Video uploads
- Views 

With the information above, she can make a more insightful decision on who to collaborate with.

### Target Audience 

Who are we aiming to support?

- Primary : Sharon (Head of Marketing)
- Secondary - Marketing Team Members (who are involved with this campaign)

## User Story 

As the head of marketing, I want to identify the top YouTubers in the USA based on subscriber count, videos uploaded and views accumulated, so that I can decide on which channels would be best to run marketing campaigns with to generate a good ROI.
Also, I want to analyze the potential for successful campaigns with the top Youtubers so that I can maximize the ROI.



## Acceptance Criteria

The dashboard should : 

- List the top Youtube Channels by subscribers, videos, and views
- Display key metrics (channel name, subscribers, videos, views, engagement ratio)
- Be user-friendly and easy to filter/ sort
- Use the most recent data possible

The solution should : 

- Recommend Youtube channels best suited for different campaign types (e.g. product placement, sponsored video series, influencer marketing)
- Consider reach, engagement and potential revenue based on estimated conversion rates
- Clearly explain the recommendations with data-driven justifications 

## Success Criteria 

Sharon can : 

- Easily identify the top performing Youtube channels based on the key metrics mentioned above
- Assess the potential for successful campaigns with top Youtubers based on reach, engagement and potential revenue
- Make informed decisions based on the ideal collaborations to advance with based on recommendations

This allows Sharon to achieve a good ROI and build relationships with Youtubers for future collaborations, which leads to recognition within the company.


# Data Source 

- What data is needed to achieve our objective?

We need top USA YouTuber 2024 data which include : 

- Channel name 
- Total subscribers 
- Total videos uploaded 
- Total views 
- Average views per video
- Subscriber engagement ratio
- Views per subscriber

## Data Quality Checks

We need to add measures in place to confirm the dataset contains the data required without any issues - here are some of the data quality checks we need to conduct : 

- Row count check
- Column count check
- Data type check
- Duplicate check


# Stages

- Design
- Development
- Testing
- Analysis
- Recommendations

  
# Design

## Dashboard Components

What questions are we trying to answer with this dashboard? 

1. Who are the top 10 YouTubers with most subscribers?
2. Who are the top 10 YouTubers with the most viewership?
3. Which 3 channels uploaded the most videos?
4. Which 3 channels have the highest average views per video?
5. Which 3 channels have the highest views per subscriber ratio?
6. Which 3 channels have the highest subscriber engagement rate per video uploaded?

## Dashboard Mockup

What will this dashboard look like? What visuals will we be including? 

1. Data Table
2. Treemap
3. Scorecards
4. Horizontal Bar Chart

## Tools 

| Tool | Purpose |
| --- | --- |
| Excel | Exploring the data |
| SQL Server | Cleaning, testing, and analyzing the data |
| Power BI | Visualizing the data via interactive dashboards |
| GitHub | Hosting the project documentation and version control |
| Mokkup AI | Designing the wireframe/mockup of the dashboard | 



# Development 

Stages of development : 

1. Collect top YouTuber data
2. Explore data on Excel
3. Import data into SQL Server Management Studio
4. Clean the data w/ SQL
5. Test the data w/ SQL
6. Create a view w/ SQL
7. Import view into Power BI for visualiztion
8. Create DAX measures and Power BI Dashboard
9. Create an analysis workbook
10. Generate findings based on insights
11. Provide recommendations to stakeholder
12. Publish the data to GitHub Pages


## Initial Data Exploration

Initial Observations : 

1. There are 4 columns we will need : channel_name, total_subscribers, total_views, and total_videos. We will filter for these 4 columns during the SQL cleaning phase.
2. The channel_name column includes the channel name followed by an @ and the channel id, so we will need to extract the channel name from this string.
3. We will need to check for any null values during the data cleaning process. 


## Data Cleaning

What should the clean data look like? 

We are aiming to refine our dataset to include only relevant infomration for accurate analysis. 

The clean data should be the following constraints : 

- channel_name, total_subscribers, total_views, and total_videos columns
- Ensure all data types are appropriate
- No null values, complete dataset
- No unknown character values
- Provide appropriate alias, or rename

  
Below is a table outlining the constraints on our cleaned dataset:

| Property | Description |
| --- | --- |
| Number of Rows | 100 |
| Number of Columns | 4 |

And here is a tabular representation of the expected schema for the clean data:

| Column Name | Data Type | Nullable |
| --- | --- | --- |
| channel_name | VARCHAR | NO |
| total_subscribers | INTEGER | NO |
| total_views | INTEGER | NO |
| total_videos | INTEGER | NO |


### Data Cleaning Steps

1. Remove the unnecessary columns by only selecting the ones we need
2. Extract the YouTube channel name from channel_name column
3. Rename columns using aliases


### Transform the data 


```sql

/*
Goal :
  1. select all columns that are necessary and leave out ones that are not
  2. extract channel names from name column
  3. rename name column to show channel_name
*/

select
    cast(substring(u.name, 1, charindex('@', u.name) - 1) as varchar(100)) as channel_name
  , u.total_subscribers
  , u.total_views
  , u.total_videos
from
	us_top_youtubers_2024 u

```

### Create the SQL view


```sql

/*
Goal : 
	1. create view to store cleaned and transformed data
*/


create view view_us_top_youtubers_2024 as (

		select
			  cast(substring(u.name, 1, charindex('@', u.name) - 1) as varchar(100)) as channel_name
		  , u.total_subscribers
		  , u.total_views
		  , u.total_videos
		from
			us_top_youtubers_2024 u
)

```











