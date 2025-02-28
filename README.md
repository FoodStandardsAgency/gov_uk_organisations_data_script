# GOV.UK Organisations Data Script

## Overview
This script pulls data from the GOV.UK API to retrieve information about government departments, agencies, public bodies, and teams listed on GOV.UK. The data is then processed and saved locally to avoid redundant API calls.

## Dataset Description
- **Source**: https://www.gov.uk/api/organisations
- **Dcoumentation**: https://docs.publishing.service.gov.uk/repos/collections/api.html
- **Total**: 1218 (as of 28th February, 2025)
- **Government departments, agencies, and public bodies**
- **Collector last ran on**: 2025-02-27 (as of 28th February, 2025)
- **Origin**: Contains some data created by MHCLG. Efforts are ongoing to replace it with data from authoritative sources.
- **Licence**: Licensed under the Open Government Licence v.3.0.
- **Attribution**: © Crown copyright and database right 2025
- **Summary**: A selection of departments, agencies, public bodies, and teams listed on GOV.UK. This data originally came from the government organisation register and is maintained to help identify the organisations which provide planning and housing data.

## Script Details

### Dependencies
- `os`
- `json`
- `time`
- `random`
- `http.client`
- `pandas` (for saving data to CSV)

### How It Works
1. **Check for Existing Data**: The script first checks if a local JSON file (`organisations_data.json`) exists. If it does, it reads the data from the file.
2. **Validate Data**: The script ensures that the data is not just keys with empty values. If this happens, delete the json file and start the script again.
3. **API Call**: If the local file does not exist or contains invalid data, the script makes API calls to retrieve the data.
4. **Process Data**: The script processes the data, extracting relevant information and relationships.
5. **Save Raw Data**: The processed data is saved to a local JSON file to avoid redundant API calls in the future.
6. **Create DataFrames**: Pandas DataFrames are created
7. **CSVs are Created**: Each DataFrame is written out
8. **Data into SQL**: Data is processed into 5 tables
 - organisations (with id as PRIMARY KEY)
 - parent_organisations (with organisation_id as FOREIGN KEY) 
 - child_organisations (with organisation_id as FOREIGN KEY) 
 - superseded_organisations (with organisation_id as FOREIGN KEY) 
 - superseding_organisations (with organisation_id as FOREIGN KEY) 
7. **Export to CSV**: The data is also exported to a CSV file (`superseded_organisations.csv`).

### Usage
To run the script, simply execute it in your Python environment. Ensure that all dependencies are installed.

### License
- **Data**: Licensed under the Open Government Licence v.3.0. (not stored on this repo, but pulled by the script) 
- **Code**: Licensed under the MIT License.

