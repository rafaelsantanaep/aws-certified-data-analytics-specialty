
**What is AWS Config?**

AWS Config is a fully managed service that provides you with an AWS resource inventory, configuration history, and configuration change notifications to enable security and governance. With AWS Config you can discover existing AWS resources, export a complete inventory of your AWS resources with all configuration details, and determine how a resource was configured at any point in time. These capabilities enable compliance auditing, security analysis, resource change tracking, and troubleshooting.


##### Config Rules
- A desired configuration determined by the user to a set of resources. These rules are evaluated against a resource configuration that is being changed.
- Managed Rules are supported for most of the main services of AWS.
- Custom Rules can also be created.

##### Configuration Items
Configuration items are used by other features and components of AWS Config, such as:
-   Configuration History - Configuration items are used to look up all changes that have been made to a resource
-   Configuration Streams - Configuration items are sent to an SNS Topic to enable analysis of the data
-   Configuration Snapshots - Configuration items are used to create a point in time snapshot of all supported resources