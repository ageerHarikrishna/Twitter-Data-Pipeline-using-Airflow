
# Twitter Data Pipeline Using Airflow

## Overview
This project demonstrates an end-to-end data engineering pipeline using Airflow and Python to extract, transform, and load (ETL) Twitter data. By analyzing Twitter data, businesses can gain valuable insights into customer sentiments and trends, enabling data-driven marketing strategies and improved customer engagement.

## Project Structure
- **twitter_dag.py**: Defines the Airflow DAG that schedules and runs the ETL pipeline.
- **twitter_etl.py**: Contains the ETL logic for extracting tweets, transforming the data, and saving it to a CSV file.
- **twitter_commands.sh**: Shell script for setting up and running the Airflow environment.
- **data/**: Directory to store the output CSV files.
- **README.md**: Documentation and project overview.

## Features
- **Data Extraction**: Extracts tweets using the Twitter API and Tweepy library.
- **Data Transformation**: Processes and refines tweet data, capturing key attributes like user, text, favorite count, retweet count, and creation time.
- **Data Loading**: Saves the transformed data into a CSV file for further analysis.
- **Airflow Orchestration**: Uses Airflow to schedule and manage the ETL workflow.

###Airflow DAG Setup:
The Directed Acyclic Graph (DAG) in Airflow is crucial for scheduling and managing the ETL tasks. The DAG defines the workflow and the dependencies between tasks. Below is a critical block of code from the twitter_dag.py file:
###Using Tweepy for Twitter API Requests:
Tweepy is a Python library used to interact with the Twitter API. It simplifies the process of making API requests, handling authentication, and parsing responses.
Rate Limits: The Twitter API has rate limits that restrict the number of requests you can make within a 15-minute window. For example, the user timeline endpoint (user_timeline) is limited to 900 requests per 15-minute window. It is essential to handle rate limits in your code to avoid exceeding these limits and receiving errors.
###ETL Process:This function authenticates with the Twitter API, retrieves tweets from a specified user, processes the tweet data, and saves it into a CSV file.
```python
api = tweepy.API(auth)
    tweets = api.user_timeline(screen_name='@elonmusk', 
                            # 200 is the maximum allowed count
                            count=200,
                            include_rts = False,
                            # Necessary to keep full_text 
                            # otherwise only the first 140 words are extracted
                            tweet_mode = 'extended'
                            )

    list = []
    for tweet in tweets:
        text = tweet._json["full_text"]

        refined_tweet = {"user": tweet.user.screen_name,
                        'text' : text,
                        'favorite_count' : tweet.favorite_count,
                        'retweet_count' : tweet.retweet_count,
                        'created_at' : tweet.created_at}
        
        list.append(refined_tweet)

    df = pd.DataFrame(list)
    df.to_csv('refined_tweets.csv')
```
![image](https://github.com/ageerHarikrishna/Twitter-Data-Pipeline-using-Airflow/blob/main/Screenshot%202024-06-16%20003450.png)

## Business Value
This pipeline provides real-time insights into consumer sentiment and trends by analyzing Twitter data. It enables data-driven marketing strategies, increases customer engagement, and allows rapid responses to public comments, leading to better decision-making and improved overall business performance.


