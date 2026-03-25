# Unigine::Plugins::Sql::SqlResponse Class (CPP)

**Header:** #include <plugins/Unigine/Sql/UnigineSql.h>


This class manages the response from the SQL database.


## SqlResponse Class

### Members

## String getExecutedQuery () const

Returns the current query that was actually executed. This may differ from the query that was passed, for example if bound values were used with a prepared query and the underlying database doesn't support prepared queries.
### Return value

Current query that was actually executed.
## bool isReady () const

Returns the current value indicating that the data has been requested (the [*execAsync()*](../../../../api/library/plugins/sql/class.sqldatabase_cpp.md#execAsync_SqlRequest_SqlResponse) method has been performed).
### Return value

**true** if the data has been requested; otherwise **false**.
## bool isDataReady () const

Returns the current value indicating that the requested data has been uploaded in the response.
### Return value

**true** if the response is obtained; otherwise **false**.
## bool isSuccess () const

Returns the current value indicating that there were no errors while receiving the response. If false is returned, use [*getError()*](#getError_String) to find the error.
### Return value

**true** if the response was received without errors; otherwise **false**.
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

Requests the specified number of next lines. This method can be called only after the [*execAsync()*](../../../../api/library/plugins/sql/class.sqldatabase_cpp.md#execAsync_SqlRequest_SqlResponse) method, otherwise it will cause a crash.
### Arguments

- *unsigned int* **maxRows** - Maximum number of database lines in request to be obtained.

## String getColumnName ( int column ) const

Returns the name of the database column by its index.
### Arguments

- *int* **column** - Database column.

### Return value

Column name.
## Variable getData ( int row , int column ) const

Returns the data in the specified cell of the database.
### Arguments

- *int* **row** - Database row index.
- *int* **column** - Database column index.

### Return value

Database variable.
