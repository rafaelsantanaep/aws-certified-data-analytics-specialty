### Ensuring encryption in transit and at rest
#### HDFS
- Transparent Data Encryption
#### S3
**At Rest**: Server-side encryption or client-side encryption.
**In Transit**: SSL/TLS.

#### Security configurations
- Are useful when you want to setup encryption access patterns for multiple clusters and for multiple s3 buckets.
- You can specify ARNs that will be used for encryption at rest, or a zip file in s3 containing the certificates for encryption in transit.


#### Block public access
- Is a new feature from EMR that allow to block all public access in EMR clusters by default in all clusters created in a specific region.
- The ports that can be opened to the internet are configurable.


#### EMR Managed Scaling
- Feature only available in instance groups for now.
- Usually utilizes two metrics to see if it needs to scale or not: **CONTAINERS PENDING** OR **YARNMemoryAvailablePercentage**.
- You can establish the maximum number of core nodes
- You can establish the maximum number of nodes
- You can establish the maximum number of on demand instances.
- You can establish the minimum amount of core nodes.
