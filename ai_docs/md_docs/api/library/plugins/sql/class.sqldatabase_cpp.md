# Unigine::Plugins::Sql::SqlDatabase Class (CPP)

**Header:** #include <plugins/Unigine/Sql/UnigineSql.h>


This class manages operations with SQL databases.


## SqlDatabase Class

### Members

## bool isOpen () const

Returns the current value indicating if the database connection is currently open.
### Return value

**true** if the database connection is currently open is enabled ; otherwise **false**.
## bool isOpenError () const

Returns the current value indicating if there was an error opening the database connection. Error information can be retrieved using [*getLastError()*](#getLastError_String).
### Return value

**true** if there was an error opening the database connection is enabled ; otherwise **false**.
## String getLastError () const

Returns the current information about the last error that occurred on the database.
### Return value

Current information about the last error that occurred on the database.
## bool isValid () const

Returns the current value indicating if the database has a valid driver.
### Return value

**true** if the database has a valid driver is enabled ; otherwise **false**.
## void setDatabaseName ( const char * name )

Sets a new connection's database name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Arguments

- *const char ** **name** - The connection's database name.

## String getDatabaseName () const

Returns the current connection's database name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Return value

Current connection's database name.
## void setUserName ( const char * name )

Sets a new connection's user name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Arguments

- *const char ** **name** - The connection's user name.

## String getUserName () const

Returns the current connection's user name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Return value

Current connection's user name.
## void setPassword ( const char * password )

Sets a new connection's password. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Arguments

- *const char ** **password** - The connection's password.

## String getPassword () const

Returns the current connection's password. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Return value

Current connection's password.
## void setHostName ( const char * name )

Sets a new connection's host name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Arguments

- *const char ** **name** - The connection's host name.

## String getHostName () const

Returns the current connection's host name. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Return value

Current connection's host name.
## void setPort ( )

Sets a new connection's port number. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Arguments

- **port** - The connection's port number.

## getPort () const

Returns the current connection's port number. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Return value

Current connection's port number.
## void setConnectOptions ( const char * options )

Sets a new database-specific options. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Arguments

- *const char ** **options** - The database-specific options.

## String getConnectOptions () const

Returns the current database-specific options. To have effect, the value must be set before the connection is opened. Alternatively, you can [close](#close_void) the connection, set the value, and call [open](#open_int) again.
### Return value

Current database-specific options.
## String getDriverName () const

Returns the current connection's driver name.
### Return value

Current connection's driver name.
## String getConnectionName () const

Returns the current connection name.
### Return value

Current connection name.
## void setNumericalPrecisionPolicy ( Sql::NUMERICAL_PRECISION_POLICY policy )

Sets a new numerical precision policy.
### Arguments

- *[Sql::NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_cpp.md#NUMERICAL_PRECISION_POLICY)* **policy** - The numerical precision policy, one of the [NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_cpp.md#NUMERICAL_PRECISION_POLICY).

## Sql::NUMERICAL_PRECISION_POLICY getNumericalPrecisionPolicy () const

Returns the current numerical precision policy.
### Return value

Current numerical precision policy, one of the [NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_cpp.md#NUMERICAL_PRECISION_POLICY).
---

## void getTables ( Vector < String > & OUT_tables , Sql::TABLE_TYPE type ) const

Returns a list of the database's tables, system tables and views, as specified by the type.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **OUT_tables** - Output buffer for the list of tables. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Sql::TABLE_TYPE](../../../../api/library/plugins/sql/class.sql_cpp.md#TABLE_TYPE)* **type** - Type of the table.

## bool open ( )

Opens the database connection using the current connection values. In case of failure, error information can be retrieved using [*getLastError()*](#getLastError_String).
### Return value

true if the database connection is open, otherwise false.
## void close ( )

Closes the database connection, freeing any resources acquired, and invalidating any existing queries that are used with the database.
## bool transaction ( )

Begins a transaction on the database if the driver supports transactions.
### Return value

true if the operation succeeded, otherwise false.
## bool commit ( )

Commits a transaction to the database if the driver supports transactions and a [transaction has been started](#transaction_int).
### Return value

true if the operation succeeded, otherwise false.
## bool rollback ( )

Rolls back a transaction on the database, if the driver supports transactions and a [transaction has been started](#transaction_int).
### Return value

true if the operation succeeded, otherwise false.
## SqlRequest * createRequest ( )

Creates an SQL request.
### Return value

Created SQL request.
## SqlResponse * exec ( SqlRequest * request )

Executes the SQL request and returns the received data as an SQL response.
### Arguments

- *[SqlRequest](../../../../api/library/plugins/sql/class.sqlrequest_cpp.md) ** **request** - SQL request.

### Return value

Response to the SQL request.
## SqlResponse * exec ( const char * query )

Executes the SQL in query and returns the received data as an SQL response.
### Arguments

- *const char ** **query** - Query string. The syntax should be appropriate for the SQL database being queried.

### Return value

Response to the SQL request.
## SqlResponse * execAsync ( SqlRequest * request )

Executes the SQL request asynchronously and returns the received data as an SQL response.
> **Notice:** Calling this method implies adding a new task to the threadpool. Therefore, consider that calling this method too many times may cause delay in receiving the data.


### Arguments

- *[SqlRequest](../../../../api/library/plugins/sql/class.sqlrequest_cpp.md) ** **request** - SQL request.

### Return value

Response to the SQL request.
## SqlResponse * execAsync ( const char * query )

Executes the SQL in query asynchronously and returns the received data as an SQL response.
> **Notice:** Calling this method implies adding a new task to the threadpool. Therefore, consider that calling this method too many times may cause delay in receiving the data.


### Arguments

- *const char ** **query** - Query string using the syntax appropriate for the SQL database being queried.

### Return value

Response to the SQL request.
## void deleteRequest ( SqlRequest * request )

Deletes the SQL request.
### Arguments

- *[SqlRequest](../../../../api/library/plugins/sql/class.sqlrequest_cpp.md) ** **request** - SQL request.

## void deleteResponse ( SqlResponse * response )

Deletes the SQL response.
### Arguments

- *[SqlResponse](../../../../api/library/plugins/sql/class.sqlresponse_cpp.md) ** **response** - SQL response.
