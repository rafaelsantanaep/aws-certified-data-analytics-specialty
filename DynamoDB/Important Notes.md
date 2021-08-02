#### Perform ad-hoc analysis on DynamoDB Data

##### Option 1
1. Create a consumer application to read from DynamoDB and write to Kinesis Firehose
2. Configure a Kinesis Firehose Delivery stream to S3
3. Crawn your S3 data using AWS Glue
4. Perform ad-hoc analysis on your data using AWS Athena
5. Use lifecycle policies to control the storage tiers of your S3 objects over time.

##### Option 2
