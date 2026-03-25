# Unigine::Plugins::Sql::SqlResponse Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class manages the response from the SQL database.


## SqlResponse Class

### Members

## String getExecutedQuery () const

Returns the current query that was actually executed. This may differ from the query that was passed, for example if bound values were used with a prepared query and the underlying database doesn't support prepared queries.
### Return value

Current query that was actually executed.
## int isReady () const

Returns the current value indicating that the data has been requested (the [*execAsync()*](../../../../api/library/plugins/sql/class.sqldatabase_usc.md#execAsync_SqlRequest_SqlResponse) method has been performed).
### Return value

Current the data has been requested
## int isDataReady () const

Returns the current value indicating that the requested data has been uploaded in the response.
### Return value

Current the response is obtained
## int isSuccess () const

Returns the current value indicating that there were no errors while receiving the response. If false is returned, use [*getError()*](#getError_String) to find the error.
### Return value

Current the response was received without errors
## String getError () const

Returns the current string containing an error.
### Return value

Current string containing an error.
## int getNumRows () const

Returns the current number of rows in the obrained SQL response.
### Return value

Current number of rows in the obrained SQL response.
## int getNumColumns () const

Returns the current number of columns in the obtained SQL response.
### Return value

Current number of columns in the obtained SQL response.
---

## void next ( unsigned int maxRows = 20 )

Requests the specified number of next lines. This method can be called only after the [*execAsync()*](../../../../api/library/plugins/sql/class.sqldatabase_usc.md#execAsync_SqlRequest_SqlResponse) method, otherwise it will cause a crash.
### Arguments

- *unsigned int* **maxRows** - Maximum number of database lines in request to be obtained.

## String getColumnName ( int column )

Returns the name of the database column by its index.
### Arguments

- *int* **column** - Database column.

### Return value

Column name.
## Variable getData ( int row , int column )

Returns the data in the specified cell of the database.
### Arguments

- *int* **row** - Database row index.
- *int* **column** - Database column index.

### Return value

Database variable.
