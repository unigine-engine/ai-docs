# Unigine::Plugins::Sql::SqlDatabase Class (CS)


This class manages operations with SQL databases.


## SqlDatabase Class

### Properties

## 🔒︎ bool IsOpen

The value indicating if the database connection is currently open.
## 🔒︎ bool IsOpenError

The value indicating if there was an error opening the database connection. Error information can be retrieved using [*LastError*](#getLastError_String).
## 🔒︎ string LastError

The information about the last error that occurred on the database.
## 🔒︎ bool IsValid

The value indicating if the database has a valid driver.
## string DatabaseName

The connection's database name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
## string UserName

The connection's user name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
## string Password

The connection's password. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
## string HostName

The connection's host name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
## int Port

The connection's port number. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
## string ConnectOptions

The database-specific options. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
## 🔒︎ string DriverName

The connection's driver name.
## 🔒︎ string ConnectionName

The connection name.
## Sql.NUMERICAL_PRECISION_POLICY NumericalPrecisionPolicy

The numerical precision policy.
### Members

---

## void GetTables ( string[] OUT_tables , Sql.TABLE_TYPE type )

Returns a list of the database's tables, system tables and views, as specified by the type.
### Arguments

- *string[]* **OUT_tables** - Output buffer for the list of tables. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Sql.TABLE_TYPE](../../../../api/library/plugins/sql/class.sql_cs.md#TABLE_TYPE)* **type** - Type of the table.

## bool Open ( )

Opens the database connection using the current connection values. In case of failure, error information can be retrieved using [*LastError*](#getLastError_String).
### Return value

true if the database connection is open, otherwise false.
## void Close ( )

Closes the database connection, freeing any resources acquired, and invalidating any existing queries that are used with the database.
## bool Transaction ( )

Begins a transaction on the database if the driver supports transactions.
### Return value

true if the operation succeeded, otherwise false.
## bool Commit ( )

Commits a transaction to the database if the driver supports transactions and a [transaction has been started](#transaction_int).
### Return value

true if the operation succeeded, otherwise false.
## bool Rollback ( )

Rolls back a transaction on the database, if the driver supports transactions and a [transaction has been started](#transaction_int).
### Return value

true if the operation succeeded, otherwise false.
## SqlRequest CreateRequest ( )

Creates an SQL request.
### Return value

Created SQL request.
## SqlResponse Exec ( SqlRequest request )

Executes the SQL request and returns the received data as an SQL response.
### Arguments

- *[SqlRequest](../../../../api/library/plugins/sql/class.sqlrequest_cs.md)* **request** - SQL request.

### Return value

Response to the SQL request.
## SqlResponse Exec ( string query )

Executes the SQL in query and returns the received data as an SQL response.
### Arguments

- *string* **query** - Query string. The syntax should be appropriate for the SQL database being queried.

### Return value

Response to the SQL request.
## SqlResponse ExecAsync ( SqlRequest request )

Executes the SQL request asynchronously and returns the received data as an SQL response.
> **Notice:** Calling this method implies adding a new task to the threadpool. Therefore, consider that calling this method too many times may cause delay in receiving the data.


### Arguments

- *[SqlRequest](../../../../api/library/plugins/sql/class.sqlrequest_cs.md)* **request** - SQL request.

### Return value

Response to the SQL request.
## SqlResponse ExecAsync ( string query )

Executes the SQL in query asynchronously and returns the received data as an SQL response.
> **Notice:** Calling this method implies adding a new task to the threadpool. Therefore, consider that calling this method too many times may cause delay in receiving the data.


### Arguments

- *string* **query** - Query string using the syntax appropriate for the SQL database being queried.

### Return value

Response to the SQL request.
## void DeleteRequest ( SqlRequest request )

Deletes the SQL request.
### Arguments

- *[SqlRequest](../../../../api/library/plugins/sql/class.sqlrequest_cs.md)* **request** - SQL request.

## void DeleteResponse ( SqlResponse response )

Deletes the SQL response.
### Arguments

- *[SqlResponse](../../../../api/library/plugins/sql/class.sqlresponse_cs.md)* **response** - SQL response.
