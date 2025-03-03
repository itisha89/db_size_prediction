# Predicting Mount Point Usage

## Problem Statement
ABC Group wants to predict the mount point size and has not subscribed to the paid services by Oracle. The goal of this project is to predict the mount point usage of the database on a month-by-month basis until exhaustion, helping the business plan for memory upgrades or reallocation. Accurate predictions of storage consumption can inform proactive decisions regarding infrastructure management, memory planning, and performance optimization. 

## Aim
The aim of this report is to forecast the usage of the mount point size, considering historical growth patterns and potential storage demands, while ensuring that storage resources are efficiently managed. The model predicts the mount point size until December 2025, allowing the business to prepare for potential memory upgrades if the usage exceeds available resources.

## Data
### Data Source
The data for this analysis has been sourced from the internal logs and historical storage usage records of the company's database system. The data is primarily collected from September 2022 to February 2025, and it includes various parameters related to database and file storage. The original data files used in this analysis are:
- **db_size_history.csv**
- **extract_archive_log_gen_count.csv**
- **tablespace_usage.csv**
- **transaction_trends.csv**


Additionally, **generated_data.csv** contains the generated data used for forecasting.

### About the Data
The dataset contains the following key variables:
- **db_size_history:** This variable tracks the growth of the user database size with active files. Data for this variable has been collected since the database's inception in September 2022. Records for db_size_history are only logged when there is an increase in size, resulting in missing records for months where no increase occurred.

- **archive_log_gb:** This variable represents the size of archived log files and has a fixed value of 316 GB. The fixed size is based on company policies for archival storage, which might be constant due to the volume of logs generated each month. The archive logs have a validity of 7 days, meaning after 7 days, the data gets deleted. Therefore, we consider a constant average value of 316 GB per month.

### Other Variables:
- **TOTAL_DATAFILES:** 128 data files used in the system.
- **LESS_THAN_31GB_AUTOEXT_NO:** 15 files are smaller than 31 GB and do not automatically extend.
- **LESS_THAN_31GB_AUTOEXT_YES:** 79 files are smaller than 31 GB and automatically extend.
- **TOTAL_MOUNT_POINT_SIZE:** 3 TB, which is the total capacity of the mount point for the database, including redo, undo, temp files, control files, archive logs, and database size. This is our target variable.

## Limitations
Since we had missing logs and the company had not subscribed to paid services, we considered the database growth rate as follows:
- Oracle database mount point total size: 3 TB
- Current used size: 2.7 TB
- Current free space: 354 GB
- Oracle database mount point occupied by database size: 2347 GB
- Additional median size of archive logs: 316 GB

### Database Growth Statistics
Here’s a well-formatted version of your data for a **README** file:  

---

# Database Growth Report  


| Date   | Database Size (MB) | Used Space (MB) | Used %  | Free Space (MB) | Free %  | Daily Growth (MB) | Daily Growth % | Weekly Growth (MB) | Weekly Growth % |
|--------|--------------------|----------------|--------|----------------|--------|------------------|----------------|------------------|----------------|
| SEP-22 | **2,402,985.74**   | **2,096,165.74** | **87.23%** | **306,820.34** | **12.77%** | **2,311.27** | **0.096%** | **16,178.9** | **0.673%** |


## Dataset Creation
Considering the database usage as of 25th Feb 2025:
- Oracle database mount point total size: 3 TB
- Current used size: 2.7 TB
- Current free space: 354 GB

We reconstructed the dataset by considering the historical growth trend. A fixed value of 316 GB for archive logs was added to obtain the mount point size.

## Model Used
LSTM (Long Short-Term Memory) was used for the prediction, as the data is time-series in nature.

## Model Performance
The performance of the LSTM model was evaluated using the following metrics:
- **Mean Absolute Error (MAE):** 24.74 GB
- **Mean Squared Error (MSE):** 839.66 GB

## Predictions (March 2025 - December 2025)
The predicted mount point size for the next 10 months is as follows:
| Month | Predicted Mount Point Size (GB) |
|--------|--------------------------------|
| March 2025 | 2412.91 |
| April 2025 | 2506.71 |
| May 2025 | 2593.87 |
| June 2025 | 2675.13 |
| July 2025 | 2750.27 |
| August 2025 | 2818.81 |
| September 2025 | 2880.23 |
| October 2025 | 2939.87 |
| November 2025 | 2992.89 |
| December 2025 | 3040.08 |

![image](https://github.com/user-attachments/assets/4ca00cd3-d195-4e35-933a-96ff54d8255c)



## Conclusion
This predictive analysis provides valuable insights into mount point storage usage trends, enabling ABC Group to proactively manage its storage capacity. By forecasting usage until December 2025, the business can strategically plan for memory upgrades and reallocation to avoid potential storage constraints. The LSTM model demonstrated reasonable accuracy, and its predictions offer a reliable foundation for decision-making in database infrastructure management.

