### Monitoring Kinesis with CloudWatch
#### Stream Level Metrics
- Collected per minute with no additional cost

#### Shard Level Metrics (Enhanced Monitoring)
- Can be collected per minute, but this option is not enabled by defauilt. Additional charges are applied.

Available Metrics:

|Stream Level  |Shard Level |
|--------------|------------|
|GetRecords.Bytes |OutgoingBytes| 
|GetRecords.IteratorAge	(Deprecated) | |
|GetRecords.IteratorAgeMilliseconds	|IteratorAgeMilliseconds|
|GetRecords.Latency	||
|GetRecords.Records	|OutgoingRecords|
|GetRecords.Success	||
|IncomingBytes	| IncomingBytes|
|IncomingRecords	|IncomingRecords|
|PutRecord.Bytes	||
|PutRecord.Latency	||
|PutRecord.Success	||
|PutRecords.Bytes||
|PutRecords.Latency	||
|PutRecords.Records	||
|PutRecords.Success	||
|PutRecords.TotalRecords	||
|PutRecords.SuccessfulRecords	||
|PutRecords.FailedRecords	||
|PutRecords.ThrottledRecords	||
|ReadProvisionedThroughputExceeded	|ReadProvisionedThroughputExceeded|
|SubscribeToShard.RateExceeded	||
|SubscribeToShard.Success||
|SubscribeToShardEvent.Bytes|OutgoingBytes|
|SubscribeToShardEvent.MillisBehindLatest||
|SubscribeToShardEvent.Records	||
|SubscribeToShardEvent.Success||
|WriteProvisionedThroughputExceeded|WriteProvisionedThroughputExceeded|


### Kinesis Firehose

#### Tagging Delivery Streams Using the Amazon Kinesis Data Firehose API

##### Creating Stream with Tags
- It's possible to create a stream with tags.
##### Adding tags to existing Kinesis Firehose Stream
-   TagDeliveryStream -> Add tag in existing Kinesis Firehose Stream
-  ListTagsForDeliveryStream -> List Tags on existing Kinesis Stream
-   UntagDeliveryStream -> Remove Tag From Stream

