### Supported Machine Learning Models
- ML Powered Anomaly Detection (Random Cut Forest)
- ML Powered Forecasting: Detecting seasonality, trends over time, excluding outliers and imputing missing values.
- Autonarratives


##### Dataset requirements for ML in quicksight:
- At least one metric
- At least one dimension that is entirely not null
- Minimum of 15 data points for training
- If you want to analyze anomalies, you also need one date dimension


### Using Row Level Security to Restrict a Dataset
- Enterprise only feature.
- It's possible to do it before or after the dataset was created.


#### Rules Dataset
1. Create a file or query that has a column UserName, GroupName or both.  Alternatively, you can create a query or file that has one column named `UserARN`, `GroupARN`, or both.
2. You add one column to the query or file for each field that you want to restrict. A NULL values means that the user has access to all the rows.
3. If you don't add a rule for a user or group, that user can't see any data.
4. Rules Quotas: 999 rules per User.
#### Apply row Level security using a file or query
1. Confirm that you have added a dataset.
2. On the dataset page, choose the dataset, then choose permissions.
3. From the list of dataset, choose your permission dataset.
4. Choose the permissions policy.
5. Apply dataset.


**Important Note**: If a permissions dataset is removed before you remove it from the permissions of a target dataset, the target dataset will bem marked as *RESTRICTED*. To bypass this behavior, you should create a new permissions dataset to replace the one that was deleted.


#### Encryption
- Quicksight offers encryption in transit.
- Encryption for each source that you use for data is controlled by that data source or file system. Amazon QuickSight doesn't store any actual data except metadata and data that you upload into SPICE. In Enterprise edition, data at rest in SPICE is encrypted using block-level encryption with AWS-managed keys. In Standard edition, data at rest in SPICE is securely stored, but not encrypted.


#### JOIN Limitations
The following limitations apply to joins:

-   For joins of multiple data sources, the result set is a SPICE dataset.
-   For joins of multiple data sources, there's no size restriction on the data that you use to create the dataset. You should always begin the join with your largest table. Often, this is a fact table. The rest of the tables combined must total less than 1 GB in size.
-   You can't join on calculated fields that you created in Amazon QuickSight.
-   You can't join on fields that use the geospatial data type.
-   You can't use a custom SQL query in a join between multiple data sources. To use custom SQL to join tables from different data sources, create the join before importing to Amazon QuickSight.

