# databricks-taxi-medallion-pipeline
Small project to use and understand a medallion pipeline with a built-in dataset from Databricks Free Edition

# NYC Taxi Medallion Pipeline (Databricks Free Edition)

Bronze → Silver → Gold lakehouse pipeline using PySpark, SQL and Delta Lake,
orchestrated with a 3-task Databricks Job.

## Architecture
- **Bronze:** raw trips copied from samples.nyctaxi.trips + ingestion metadata
- **Silver:** validated, deduplicated (hash key), typed. Invalid rows go to a quarantine table (X% of rows rejected)
- **Gold:** daily revenue by pickup zip, hourly demand

## Data quality rules
fare > 0, distance > 0, dropoff after pickup, zips not null (null-safe)

## Delta Lake features explored
MERGE, DESCRIBE HISTORY, time travel, RESTORE, schema enforcement, OPTIMIZE

## What I learned
Its very interesting how you can ingest the raw data, even if its a built-in dataset, then clean it up on a Silver phase and then produce a Gold Notebook for further analysis of such data. Terms such as "quarantining a row" and NULL trap + usage of COALESCE are key to avoid losing data without noticing it, IMO. 

