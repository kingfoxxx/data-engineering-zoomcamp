This project demonstrates the creation of a fully automated ETL (Extract, Transform, Load) pipeline using Apache NiFi, designed to process and load GeoJSON-based power line data into a PostgreSQL/PostGIS database. The pipeline is built to handle malformed data, manage spatial data (via PostGIS), and integrate geospatial geometry efficiently for analysis and storage.

Key Features:

Data Ingestion:
Extracts GeoJSON data from an external API using the InvokeHTTP processor in NiFi.

Data Transformation:
Splits the incoming GeoJSON into individual records using the SplitJson processor.
Extracts relevant attributes (e.g., osm_id, name, voltage, geometry) using EvaluateJsonPath.
Transforms and formats extracted fields using ReplaceText to match PostgreSQL's schema requirements.
Uses regular expressions to clean malformed voltage values inside other_tags.

Data Loading:
Inserts transformed data into the PostgreSQL/PostGIS database using the PutDatabaseRecord processor.
The geometry field is handled using PostGIS functions to store geographical coordinates in a spatial column (geometry).

Error Handling & Backpressure:
Implements proper error handling to route invalid records to a failure queue.
Configures backpressure thresholds to ensure the flow is efficient and scalable.

Geospatial Data:
Utilizes PostGIS functions to store and manipulate LineString geometries, making the data ready for spatial queries.

Project Process & Workflow:
Ingestion: Data is fetched via HTTP, and each GeoJSON feature is processed individually.
Parsing & Transformation: Each record is parsed, cleaned, and formatted with regex for easy insertion into PostgreSQL.
Database Insertion: Data is inserted into the power_lines table in PostgreSQL/PostGIS with spatial geometry (geometry column).
Automation: NiFi automates the entire process, making it scalable and efficient for future data uploads.

Challenges Overcome:
Handling Malformed Data: Some records had missing or malformed data, requiring custom regex logic to clean and extract valid values (e.g., voltage from other_tags).
Geometry Handling: Integrating PostGIS functions into NiFi to store complex geospatial data (LineString geometries).
Error Handling: Ensured proper error handling and backpressure configuration to avoid system overloads.

Technical Stack:
Apache NiFi 2.6.0: For building and managing the data pipeline.
PostgreSQL 15+: Database used for storing and querying transformed data.
PostGIS: PostGIS extension for geospatial data handling.
Java (OpenJDK 21): Required runtime environment for NiFi.
Regex in NiFi Expression Language: Used for cleaning and transforming data values.


# GeoJSON ETL Pipeline using Apache NiFi and PostgreSQL/PostGIS

## Overview

This project creates an **ETL pipeline** using **Apache NiFi** to automate the extraction, transformation, and loading of **GeoJSON** power line data into a **PostgreSQL/PostGIS** database. It handles geospatial data, cleans malformed records, and integrates **PostGIS functions** for spatial analysis.

## Key Features

- Extracts GeoJSON data from an external API.
- Transforms and cleans data, including parsing the `voltage` field.
- Loads data into a PostgreSQL/PostGIS database for geospatial analysis.
- Configurable error handling and backpressure management in NiFi.

## Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/geojson-etl-pipeline.git
