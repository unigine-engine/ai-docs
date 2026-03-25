# Unigine::Plugins::Sql::Sql Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class is intended for creating and deleting SQL databases and checking the available drivers.


## Sql Class

---

## void getDrivers ( Vector<String>& OUT_drivers )

Returns a list of all the available database drivers.
### Arguments

- *Vector<String>&* **OUT_drivers** - Output buffer for the list of database drivers. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## SqlDatabase createDatabase ( string type , string connectionName )

Adds a database to the list of database connections using the driver type and the connection name. Before using the connection, it must be initialized. e.g., call some or all of setDatabaseName(), setUserName(), setPassword(), setHostName(), setPort(), and setConnectOptions(), and, finally, open().
### Arguments

- *string* **type** - Driver type.
- *string* **connectionName** - Database connection name. If you add a connection with the same name as an existing connection, the new connection replaces the old one. If connectionName is not specified, the new connection becomes the default connection for the application, and subsequent calls to database() without the connection name argument will return the default connection.

### Return value

The newly added database connection.
## void deleteDatabase ( SqlDatabase * database )

Deletes the specified database connection.
### Arguments

- *[SqlDatabase](../../../../api/library/plugins/sql/class.sqldatabase_usc.md) ** **database** - The database connection to be removed.
