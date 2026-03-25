# Unigine::Plugins::Sql::Sql Class (CPP)

**Header:** #include <plugins/Unigine/Sql/UnigineSql.h>

> **Notice:** This class is a singleton.


This class is intended for creating and deleting SQL databases and checking the available drivers.


## Sql Class

### Enums

## TABLE_TYPE

| Name | Description |
|---|---|
| **TABLES** = 0x01 | All the tables visible to the user. |
| **SYSTEM_TABLES** = 0x02 | Internal tables used by the database. |
| **VIEWS** = 0x04 | All the views visible to the user. |
| **ALL_TABLES** = 0xff | All of the above. |

## NUMERICAL_PRECISION_POLICY

| Name | Description |
|---|---|
| **LOW_PRECISION_INT32** = 0x01 | Force 32bit integer values. In case of floating point numbers, the fractional part is silently discarded. |
| **LOW_PRECISION_INT64** = 0x02 | Force 64bit integer values. In case of floating point numbers, the fractional part is silently discarded. |
| **LOW_PRECISION_DOUBLE** = 0x04 | Force double values. This is the default policy. |
| **HIGH_PECISION** = 0 | Strings will be used to preserve precision. |

## BATCH_EXECUTION_MODE

| Name | Description |
|---|---|
| **VALUES_AS_ROWS** = 0 | Batch execution mode. Treats every entry in a query as a value for updating the next row. Updates multiple rows. |
| **VALUES_AS_COLUMNS** = 1 | Batch execution mode. Treats every entry in a query as a single value of an array type. Updates a single row. |

---

## void getDrivers ( Vector < String > & OUT_drivers ) const

Returns a list of all the available database drivers.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../../api/library/common/class.string_cpp.md)> &* **OUT_drivers** - Output buffer for the list of database drivers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## SqlDatabase * createDatabase ( const char * type , const char * connectionName )

Adds a database to the list of database connections using the driver type and the connection name. Before using the connection, it must be initialized. e.g., call some or all of setDatabaseName(), setUserName(), setPassword(), setHostName(), setPort(), and setConnectOptions(), and, finally, open().
### Arguments

- *const char ** **type** - Driver type.
- *const char ** **connectionName** - Database connection name. If you add a connection with the same name as an existing connection, the new connection replaces the old one. If connectionName is not specified, the new connection becomes the default connection for the application, and subsequent calls to database() without the connection name argument will return the default connection.

### Return value

The newly added database connection.
## void deleteDatabase ( SqlDatabase * database )

Deletes the specified database connection.
### Arguments

- *[SqlDatabase](../../../../api/library/plugins/sql/class.sqldatabase_cpp.md) ** **database** - The database connection to be removed.
