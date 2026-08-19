# Geospatial Analysis

A geospatial data collection and analysis system for gathering business information from the Google Maps and OneMap APIs for Singapore-based locations. It supports systematic collection of business data — including ratings, contact details, and postal codes — through automated API calls and data processing.

## Overview

This system collects and analyzes business data from multiple sources:

- **Google Maps API**: business details, ratings, and place information
- **OneMap API**: Singapore-specific postal code and address data
- **Custom Data Processing**: deduplication, filtering, and data enrichment

## Architecture

The project follows a modular architecture with distinct components.

### Core Components

- `Crobat.py`: main API handler for Google Maps and OneMap integration
- `search_classes/`: modular search implementations for area-based and point-based searches
- `LocationSplitter.py`: distributes data processing across multiple users/workers
- `key_parameters.py`: centralized configuration management

### Data Processing Pipeline

1. **Data Collection**: automated API calls to gather business information
2. **Data Deduplication**: removes duplicate entries based on `place_id`
3. **Data Enrichment**: adds postal codes and contact details
4. **Data Filtering**: filters based on ratings, review counts, and postal codes
5. **Data Merging**: combines results from multiple runs and users

## Key Features

- Multi-API integration combining Google Maps and OneMap
- Scalable processing across multiple users
- Configurable search radii, types, and parameters
- Built-in data quality filtering for business listings
- Automated deduplication across multiple runs
- Postal code enrichment for Singapore addresses
- Contact detail extraction (phone numbers and related information)

## Data Types Supported

The system can collect data for various business types, including:

- Restaurants and cafes
- Bars and nightlife venues
- Retail establishments
- Service businesses
- Any other category supported by the Google Places API

## Setup

1. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
2. Create a `.env` file from `env.template` and fill in your Google Maps and OneMap API credentials.
3. Configure `key_parameters.py`:
   - Parameter inputs for the respective API payloads. For required inputs by the Google Maps API, see the [project documentation](https://docs.google.com/document/d/1LMR_PapF468NU_nVOSQTbVeaDbuT1D0ERhoEOWYHWIM/edit).
   - Columns to return and column renaming. For the full list of columns returned by the Google API, see [this reference](https://docs.google.com/document/d/1LMR_PapF468NU_nVOSQTbVeaDbuT1D0ERhoEOWYHWIM/edit#bookmark=id.ayiz52nuepcx).
   - The `USER` setting in `key_parameters.py` — use `test` to verify your setup before running the full dataset in `combined_data.xlsx`. This runs all APIs against a single mall and a single bus stop.
4. Run the main collection script:
   ```
   python main.py
   ```

## Output Structure

The system generates multiple CSV files:

- `primary_data_[type].csv`: raw business data
- `stats_data_[type].csv`: search statistics
- `area_search_circles_[type].csv`: search area definitions
- Enhanced files with postal codes and contact details

## Configuration

Key configuration options in `key_parameters.py`:

- Search radii and types
- API call limits and buffers
- Data filtering criteria
- Output file paths
- User distribution settings

This project is suited for businesses, researchers, or analysts who need comprehensive geospatial business data for Singapore, with built-in scalability and data quality controls.
