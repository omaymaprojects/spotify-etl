# spotify-etl
Spotify Data Engineering Pipeline using AWS Glue, Athena, and QuickSight
Project Overview
This project aims to build a data engineering pipeline to process and analyze Spotify data using AWS services. The pipeline facilitates the transformation of raw Spotify data, performs necessary joins and aggregations, and visualizes the results to provide insightful analysis. The key AWS services used in this project are S3, Glue, Athena, and QuickSight.

Architecture Diagram
![image](https://github.com/user-attachments/assets/fc536bab-597e-41e1-821f-ee658ee3f09b)

View fullscreen

Project Steps
1. Data Collection
Data Source: CSV files containing Spotify data (albums.csv, artists.csv, tracks.csv).
Storage: The data is uploaded to an S3 bucket in the staging folder.
2. Data Processing with AWS Glue
AWS Glue Crawler: Automatically detects the schema from the raw data in S3 and creates corresponding tables in the Glue Data Catalog.
AWS Glue ETL Job: Performs data transformation tasks, including:
Reading data from the Glue Data Catalog tables.
Executing joins between albums, artists, and tracks based on keys such as artist_id and album_id.
Selecting relevant fields for analysis.
Writing the transformed data back to an S3 bucket in Parquet format, stored in the data-warehouse folder.
3. Data Querying with Amazon Athena
Purpose: Used to query the transformed data stored in S3.
Queries Executed: SQL queries to aggregate and analyze data, such as:
Identifying the most popular tracks.
Analyzing album popularity.
Aggregating artist follower counts.
Output: The results provide insights into Spotify data trends and patterns.
4. Data Visualization with Amazon QuickSight
Visualizations: The data queried in Athena is visualized using QuickSight to create insightful dashboards, including:
Popularity trends of tracks over time.
Genre distribution across artists.
Top albums with their popularity scores.
Interactive Dashboards: Created to explore the data interactively and gain insights.
5. Project Deployment
Documentation: The entire project, including data pipeline, transformations, SQL queries, and visualization dashboards, is documented and version-controlled on GitHub.
Outcome: Successfully processed and transformed Spotify data, providing valuable insights through interactive dashboards.
Technologies Used
Amazon S3: Storage for raw and transformed data.
AWS Glue: Schema detection, data transformation, and cataloging.
Amazon Athena: SQL querying of transformed data.
Amazon QuickSight: Data visualization and dashboard creation.
GitHub: Version control and collaboration.
Acknowledgments
Special thanks to the AWS community and the authors of the open-source libraries used in this project.




