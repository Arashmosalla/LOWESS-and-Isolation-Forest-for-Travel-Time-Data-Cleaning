# README: LOWESS and Isolation Forest for Travel Time Data Cleaning

## Overview
This script processes travel time data to remove outliers and refine the dataset using a combination of **Locally Weighted Scatterplot Smoothing (LOWESS)** and **Isolation Forest**. The methodology eliminates records from days with fewer than 100 recorded instances or when cameras operated for less than two hours. By applying statistical smoothing and anomaly detection techniques, the script ensures a high-integrity dataset for further analysis.

## Methodology
### 1. **Data Cleaning Criteria**
- Excludes days with **fewer than 100 data points**.
- Excludes days where cameras operated for **less than two hours**.
- Removes extreme residuals detected using **LOWESS** regression and **three standard deviation (3STD) threshold**.
- Identifies and eliminates outliers using **Isolation Forest**, a machine learning-based anomaly detection technique.

### 2. **LOWESS Smoothing**
- Used to fit the model to travel time data, capturing trends while reducing noise.
- The `frac` parameter (fraction of data used for local regression) is set to **0.15**, ensuring sensitivity to local variations.
- The residual between actual and predicted travel time values is calculated.
- Outliers are identified where the residual exceeds **three standard deviations**.

### 3. **Gap Detection**
- Identifies large time gaps between recorded data points.
- Marks pre-gap, post-gap, and near-gap regions to assist in filtering out unreliable records.

### 4. **Isolation Forest Outlier Detection**
- The **Isolation Forest** algorithm is applied with a **contamination rate of 0.01** (assuming 1% of the data is anomalous).
- Outliers identified by the model are removed from the dataset.

## Code Execution
1. Load the dataset into a Pandas DataFrame (`df`).
2. Run the script to process travel time data for each unique date in the dataset.
3. The cleaned data is saved to `cleaned_data.csv`.

## Usage Instructions
1. **Prepare Input Data**:
   - Ensure the dataset contains the following required columns:
     - `date.1`: The date of each record.
     - `time_of_day`: Time in minutes from 00:00 (midnight).
     - `travel_time_minute`: Travel time recorded at that timestamp.

2. **Run the Script**:
   - Load the dataset and execute the script.
   - The script will process data for each day, applying LOWESS smoothing and Isolation Forest.
   - Outliers and unreliable records will be filtered out automatically.

3. **Output**:
   - The cleaned dataset will be saved as `cleaned_data.csv`.
   - This dataset is ready for further analysis or modeling.

## Dependencies
- Python 3.7+
- Pandas
- NumPy
- Matplotlib
- Statsmodels
- Scikit-learn

## Notes
- This script ensures the data integrity necessary for travel time analysis by removing anomalous data points effectively.
- Parameters for LOWESS and Isolation Forest can be adjusted to optimize results based on different datasets.

## Author
Developed for travel time analysis, integrating **LOWESS smoothing** and **machine learning-based anomaly detection** to enhance dataset reliability.
