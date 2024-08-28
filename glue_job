from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.job import Job
import sys  # Ensure the sys module is imported

## @params: [JOB_NAME]
args = getResolvedOptions(sys.argv, ['JOB_NAME'])

# Initialize Spark and Glue Contexts
sc = SparkContext()
glueContext = GlueContext(sc)
spark = glueContext.spark_session
job = Job(glueContext)
job.init(args['JOB_NAME'], args)

# Load data from the Glue Data Catalog for each table
albums = glueContext.create_dynamic_frame.from_catalog(database="your_database_name", table_name="albums")
artists = glueContext.create_dynamic_frame.from_catalog(database="your_database_name", table_name="artists")
tracks = glueContext.create_dynamic_frame.from_catalog(database="your_database_name", table_name="tracks")

# Example transformations: Select specific fields
albums_transformed = albums.select_fields(['album_id', 'album_name', 'release_date', 'artist_id'])
artists_transformed = artists.select_fields(['artist_id', 'artist_name', 'genre'])
tracks_transformed = tracks.select_fields(['track_id', 'album_id', 'track_name', 'popularity'])

# Join albums and artists on artist_id
albums_artists_joined = Join.apply(albums_transformed, artists_transformed, 'artist_id', 'artist_id')

# Join the result with tracks on album_id
final_transformed = Join.apply(albums_artists_joined, tracks_transformed, 'album_id', 'album_id')

# Write the final transformed data to S3 in Parquet format
glueContext.write_dynamic_frame.from_options(
    frame=final_transformed,
    connection_type="s3",
    connection_options={"path": "s3://your-s3-bucket-name/data-warehouse/final_data/"},
    format="parquet"
)

# Commit the job
job.commit()
