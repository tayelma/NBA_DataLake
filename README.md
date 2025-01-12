# NBA_DataLake


# NBA Data Lake with AWS Glue and QuickSight

This project sets up a serverless data lake for NBA sports analytics using AWS services such as S3, Glue, and Athena. Additionally, it integrates AWS QuickSight for creating visualizations on the data. The pipeline retrieves NBA player data from the [sportsdata.io](https://sportsdata.io) API and stores it in a structured format for further analysis.

## Features

- **Data Ingestion**:
  - Fetches NBA player data from the sportsdata.io API.
  - Converts data into line-delimited JSON format.

- **AWS Integration**:
  - Creates an Amazon S3 bucket to store raw data.
  - Utilizes AWS Glue to create a database and define metadata for structured data analysis.
  - Configures AWS Athena for querying the structured data.

- **Data Visualization**:
  - Integrates with AWS QuickSight to generate interactive visualizations on the ingested data.

- **Fully Automated Workflow**:
  - The script orchestrates the end-to-end workflow for setting up the data lake, from data ingestion to querying setup.

## Requirements

- Python 3.8 or later
- AWS credentials configured with necessary permissions to access the following:
  - S3
  - Glue
  - Athena
  - QuickSight
- A sportsdata.io API key (sign up [here](https://sportsdata.io))
- A `.env` file to securely store your API keys.

## Project Structure

## Setup

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/nba-data-lake.git
cd nba_data_lake
```

### 2. Configure Environment Variables
Create a `.env` file in the root of the project and set the following variables:

>SPORTS_DATA_API_KEY=your_sportsdata_api_key 
NBA_ENDPOINT=your_nba_endpoint 
AWS_ACCESS_KEY_ID=your_aws_access_key_id 
AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key

### 4. Run the Script
Run the script to set up the data lake:

```bash
python nba_data_lake.py
```

### 5. Set Up QuickSight Visualizations
Once the data is ingested and available in AWS Glue, you can connect AWS QuickSight to the Glue database and create interactive reports and dashboards. Follow the [AWS QuickSight Documentation](https://docs.aws.amazon.com/quicksight/latest/user/welcome.html) to perform the setup and explore the different charts and graphs[PS: Quicksight is a pretty expensive AWS service hence, do not forget to delete resources unless you don't mind losing a couple of dollars].

## AWS Services Used

- **Amazon S3**: Stores raw and processed data.
- **AWS Glue**: Catalogs the data and enables schema definition.
- **Amazon Athena**: Executes SQL queries on data stored in the S3 bucket.
- **AWS QuickSight**: Provides data visualization capabilities.

## Example Queries in Athena

Below are example SQL queries you can try in the Athena query editor after the data has been ingested:

- Fetch all players and their teams:
  ```sql
  SELECT FirstName, LastName, Team FROM nba_analytics.nba_players;
  ```

- Calculate the average points by team:
  ```sql
  SELECT Team, AVG(Points) as AveragePoints
  FROM nba_analytics.nba_players
  GROUP BY Team;
  ```
###

## Challenges Faced

I faced permisions issues when creating visualisations with Quicksight. The problem was I had not given Quicksight the GetObject permission to s3.
Compare your policies with the policies in the policies folder.


## Future Improvements

- Automate QuickSight dashboard creation using APIs.
- Add streaming data pipelines for live updates to the data lake.
- Integrate enhanced data sources, such as player stats from additional seasons.

## Contributing

Feel free to open issues or submit pull requests to improve the project. Contributions are welcome!


