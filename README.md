
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

## Getting Started
### Prerequisites
- Python 3.7 or higher
- Apache Airflow
- Twitter Developer Account (for API keys)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/twitter-data-pipeline.git
   ```
2. Navigate to the project directory:
   ```bash
   cd twitter-data-pipeline
   ```
3. Install the required libraries:
   ```bash
   pip install -r requirements.txt
   ```

### Setup
1. Set up your Twitter API keys in the `twitter_etl.py` file:
   ```python
   access_key = "your_access_key" 
   access_secret = "your_access_secret" 
   consumer_key = "your_consumer_key"
   consumer_secret = "your_consumer_secret"
   ```
2. Initialize the Airflow database:
   ```bash
   airflow db init
   ```
3. Start the Airflow web server and scheduler:
   ```bash
   airflow webserver --port 8080
   airflow scheduler
   ```

### Usage
1. Access the Airflow web UI at `http://localhost:8080`.
2. Trigger the `twitter_dag` to start the ETL process.

## Business Value
This pipeline provides real-time insights into consumer sentiment and trends by analyzing Twitter data. It enables data-driven marketing strategies, increases customer engagement, and allows rapid responses to public comments, leading to better decision-making and improved overall business performance.


