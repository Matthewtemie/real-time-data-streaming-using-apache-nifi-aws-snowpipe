# Real-Time Data Streaming with Apache NiFi, AWS, Snowpipe, Stream & Task

## Overview
This project demonstrates a comprehensive pipeline for real-time data streaming and processing using **Apache NiFi**, **AWS**, **Snowpipe**, **Streams**, and **Tasks**. The pipeline ingests dynamically generated data, processes it through a cloud storage service (AWS S3), and streams it into a Snowflake database. The solution is designed to handle raw data, apply updates, and maintain historical records for audit and analysis.

## Key Features
- **Dynamic Data Generation:** Data is created using Python to simulate real-world events.
- **Data Ingestion:** Apache NiFi orchestrates the pulling and loading of data into an AWS S3 bucket.
- **Real-Time Streaming:** Snowpipe efficiently streams data from AWS S3 into Snowflake.
- **Data Management:** Snowflake manages data across three tables:
  - `customer_raw`: Stores raw ingested data.
  - `customer`: Reflects the latest updates from the streaming pipeline.
  - `customer_history`: Maintains a record of all updates for historical analysis.

---

## Project Steps

### 1. Data Generation
- **Tool Used:** Python
- A Python script dynamically generates mock customer data to simulate a real-time data source.

### 2. Data Ingestion with Apache NiFi
- **Flow Configuration:**
  - Pulls generated data.
  - Loads the data into an AWS S3 bucket for further processing.

### 3. Real-Time Streaming with Snowpipe
- **Process:**
  - Configured Snowpipe to monitor the AWS S3 bucket.
  - Automated data ingestion from S3 into Snowflake.

### 4. Data Transformation in Snowflake
- **Schema Design:**
  - `customer_raw`: Captures raw ingested data.
  - `customer`: Continuously updated to reflect the latest data.
  - `customer_history`: Tracks all historical updates for every change.
- **Tools Used:** Snowflake Streams and Tasks
  - Streams detect changes in `customer_raw`.
  - Tasks automate the updates to `customer` and log entries in `customer_history`.

---

## Process Explanation

### Data Generation
The data generation script written in Python creates a continuous flow of customer records. This simulates incoming real-time data from a production environment.

### Apache NiFi Workflow
NiFi acts as the data pipeline orchestrator. It:
1. Fetches the generated data from the local environment or another data source.
2. Processes the data (e.g., adding metadata or formatting).
3. Loads the processed data into an AWS S3 bucket.

### AWS S3 to Snowflake via Snowpipe
1. **Snowpipe Configuration:**
   - A Snowflake Stage is created to link Snowflake with the AWS S3 bucket.
   - Snowpipe monitors the bucket for new data.
   - Incoming data files are automatically ingested into the `customer_raw` table.
   
2. **Real-Time Streaming:**
   - Snowpipe ensures that data moves seamlessly and in near-real-time from S3 to Snowflake.

### Data Management in Snowflake
- **Streams:** Monitors changes in the `customer_raw` table.
- **Tasks:** Scheduled processes that:
  - Insert new or updated records into the `customer` table.
  - Log updates into the `customer_history` table to preserve an audit trail.

---

## Repository Structure
