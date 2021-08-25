### Stored Procedures
- By default, all users have the necessary permissions to define stored procedures (because of the schema `public`)
- When you create a stored procedure, you have two types of security definition:
	- **DEFINER**:
		- The stored procedure will use the security permissions of the user that has defined the stored procedure to identify if the user has access to the underlying data used by the stored procedure.
	- **INVOKER**:
		- The stored procedure will use the security permissions of the user that has invoked the stored procedure, so, if the user doesn't have access to some data that is used, a permission denied will be thrown.
- It's a good practice to isolate procedures in a different schema to avoid the invocation by untrusted users.
- To allow another user besides the owner and the superuser the possibility to invoke a procedure, you should `GRANT EXECUTE` on the procedure.
- The owner of the procedure will have by default the permission to `CREATE`,`DROP` and `EXECUTE` the procedure.
### Compression Encodings
- Compressions that accept text data types can be one of bytedict, lzo, runlength, text and zstd.
### Vacuuming Tables
- To be able to VACUUM a table, the user should be the `owner` or a Redshift `superuser`.
- A user may be able to `VACUUM` the entire database without being a `superuser`, but, the vacuum will only take effect on tables that this user is a `owner`.
### Data Warehouse System Architecture
#### Leader Node and Compute Nodes:
- The `Leader node` manages the communcation with client programs and the compute notes.
- The `Leader Node` Compiles the execution plan and, when data in the compute nodes are reference by this execution plan, the leader node distribute the execution among the compute notes.
	- All queries that reference tables that starts with only with `pg_` will run on the `Leader Node`.
	- There are some functions that must run only on the `leader_node`. Example: `current_schema()
	- Tables created by the user or system tables that starts with the prefix `stl` or `stv` will run on the `Compute Nodes`.
- The `Compute nodes` executes the parsed partial execution plans and returns the intermediate results to the `leader node`.
- Each computed node is divided in `slices` that have a portion of the node's memory and disk space.


#### Result Caching
- Results will be cached if the following conditions are met:
	1. The user submitting the query has access privilege to the objects used in the query.
	2. The table or views in the query haven't been modified.
	3. The query doesn't use a function that must be evaluated each time it's run, such as `GETDATE`.
	4. The query doesn't reference Amazon Redshift Spectrum external tables.
	5. Configuration parameters that might affect query results are unchanged.
	6. The query syntactically matches the cached query.


#### Securely storing credentials for Redshift
1. You can use both AWS System Manager Parameter Store or AWS Secrets Manager
2. If there is a cost requirement, choose parameter store to not incur in additional charges.


#### Federating single sign-on access to your Cluster
- Use third party tools like PingIdentity, ADFS, Okta, Azure AD or other SAML browser base identity providers.
- You have to setup groups in one of those providers
- You have to create a identity provider inside the iam


1. *Workflow:*
- User send a request to the Identity Provider
- The identity provider validates the user and if the user is a valid user, it will receive a SAML Assertion.
- This SAML assertion is used to call STS with the function AssumeRoleWithSAML.
- STS deliver temporary user credentials to the user.


#### Queries hanging when you connect from outside an Amazon EC2

Most of the text in this section were extracted as is from this [webpage](https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-firewall-guidance.html).

##### Example issue

Your client connection to the database appears to hang or timeout when running long queries, such as a COPY command. In this case, you might observe that the Amazon Redshift console displays that the query has completed, but the client tool itself still appears to be running the query. The results of the query might be missing or incomplete depending on when the connection stopped.

##### Potential cause
TCP/IP timeout

##### AWS Recommendations:
-   Increase client system values that deal with TCP/IP timeouts. Make these changes on the computer you are using to connect to your cluster. The timeout period should be adjusted for your client and network. For more information, see [Change TCP/IP timeout settings](https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-firewall-guidance.html#connecting-firewall-guidance.change-tcpip-settings).
    
-   Optionally, set keepalive behavior at the DSN level. For more information, see [Change DSN timeout settings](https://docs.aws.amazon.com/redshift/latest/mgmt/connecting-firewall-guidance.html#connecting-firewall-guidance.change-dsn-settings).


##### Parameters at DNS Level:
**KeepAlivesCount**

The number of TCP keepalive packets that can be lost before the connection is considered broken.

**KeepAlivesIdle**

The number of seconds of inactivity before the driver sends a TCP keepalive packet.

**KeepAlivesInterval**

The number of seconds between each TCP keepalive retransmission.



#### Table Design


> **Tutoriais Dojo**
**DISTSTYLE** defines the data distribution style for the whole table. Amazon Redshift distributes the rows of a table to the compute nodes according the distribution style specified for the table. The distribution style that you select for tables affects the overall performance of your database.
>
**DISTSTYLE EVEN** - The leader node distributes the rows across the slices in a round-robin fashion, regardless of the values in any particular column. EVEN distribution is appropriate when a table does not participate in joins or when there is not a clear choice between KEY distribution and ALL distribution.
>
**DISTSTYLE KEY -** The rows are distributed according to the values in one column. The leader node places matching values on the same node slice. If you distribute a pair of tables on the joining keys, the leader node collocates the rows on the slices according to the values in the joining columns so that matching values from the common columns are physically stored together.
>
**DISTSTYLE ALL -** A copy of the entire table is distributed to every node. Where EVEN distribution or KEY distribution place only a portion of a table's rows on each node, ALL distribution ensures that every row is collocated for every join that the table participates in. ALL distribution is appropriate only for relatively slow-moving tables; that is, tables that are not updated frequently or extensively. Because the cost of redistributing small tables during a query is low, there isn't a significant benefit to define small dimension tables as DISTSTYLE ALL.


#### Sort Key Drawbacks
- Compound Sort Key: Queries get slower if you use the secondary sort key, but does not use the primary.
- Interleaved Sort Key: Performance improves when your query depends on the sortkey