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