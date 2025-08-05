A comprehensive geospatial data collection and analysis system designed to gather business information from Google Maps and OneMap APIs for Singapore-based locations. This project enables systematic collection of business data including ratings, contact details, and postal codes through automated API calls and data processing.

## �� Project Overview

This system is built for collecting and analyzing business data from multiple sources:
- **Google Maps API**: For business details, ratings, and place information
- **OneMap API**: For Singapore-specific postal code and address data
- **Custom Data Processing**: For deduplication, filtering, and data enrichment

## ��️ Architecture

The project follows a modular architecture with distinct components:

### Core Components
- **`Crobat.py`**: Main API handler for Google Maps and OneMap integration
- **`search_classes/`**: Modular search implementations for area-based and point-based searches
- **`LocationSplitter.py`**: Distributes data processing across multiple users/workers
- **`key_parameters.py`**: Centralized configuration management

### Data Processing Pipeline
1. **Data Collection**: Automated API calls to gather business information
2. **Data Deduplication**: Removes duplicate entries based on place_id
3. **Data Enrichment**: Adds postal codes and contact details
4. **Data Filtering**: Filters based on ratings, review counts, and postal codes
5. **Data Merging**: Combines results from multiple runs and users

## �� Key Features

- **Multi-API Integration**: Seamlessly combines Google Maps and OneMap APIs
- **Scalable Processing**: Supports distributed processing across multiple users
- **Configurable Search**: Customizable search radii, types, and parameters
- **Data Quality Control**: Built-in filtering for high-quality business listings
- **Automated Deduplication**: Ensures data integrity across multiple runs
- **Postal Code Enrichment**: Adds Singapore postal codes to business listings
- **Contact Detail Extraction**: Retrieves phone numbers and contact information

## 📊 Data Types Supported

The system can collect data for various business types including:
- Restaurants and cafes
- Bars and nightlife venues
- Retail establishments
- Service businesses
- And any other Google Places API supported categories

## �� Getting Started

1. Install dependencies: `pip install -r requirements.txt`
2. Configure API credentials in `api_secrets.py`
3. Adjust parameters in `key_parameters.py`
4. Run the main collection script: `python main.py`

## �� Output Structure

The system generates multiple CSV files:
- `primary_data_[type].csv`: Raw business data
- `stats_data_[type].csv`: Search statistics
- `area_search_circles_[type].csv`: Search area definitions
- Enhanced files with postal codes and contact details

## �� Configuration

Key configuration options in `key_parameters.py`:
- Search radii and types
- API call limits and buffers
- Data filtering criteria
- Output file paths
- User distribution settings

This project is ideal for businesses, researchers, or analysts needing comprehensive geospatial business data for Singapore, with built-in scalability and data quality controls.

# Setup
1.) Run `pip install -r requirements.txt` to get all the required python packages\
2.) Create your own `api_secrets.py` file to access Google and OneMap API using `api_secrets_template.py`\
3.) Check `key_parameters.py` for:\
    &ensp; a.) Parameter inputs for the respective API payloads. For required inputs by Google Maps API view [Project documentation](https://docs.google.com/document/d/1LMR_PapF468NU_nVOSQTbVeaDbuT1D0ERhoEOWYHWIM/edit)\
    &ensp; b.) Columns you want to return and column renaming. For list of columns that Google API will return: https://docs.google.com/document/d/1LMR_PapF468NU_nVOSQTbVeaDbuT1D0ERhoEOWYHWIM/edit#bookmark=id.ayiz52nuepcx\
    &ensp; c.) USER in key_parameters (use 'test' to test if you've set everything up properly before querying the entire dataset in `combined_data.xlsx`, this will run all the APIs for 1 Mall and 1 Busstop) 