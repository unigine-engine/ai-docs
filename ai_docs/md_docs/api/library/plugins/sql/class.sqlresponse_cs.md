# Unigine::Plugins::Sql::SqlResponse Class (CS)


This class manages the response from the SQL database.


## SqlResponse Class

### Properties

## 🔒︎ string ExecutedQuery

The query that was actually executed. This may differ from the query that was passed, for example if bound values were used with a prepared query and the underlying database doesn't support prepared queries.
## 🔒︎ bool IsReady

The value indicating that the data has been requested (the [*ExecAsync()*](../../../../api/library/plugins/sql/class.sqldatabase_cs.md#execAsync_SqlRequest_SqlResponse) method has been performed).
## 🔒︎ bool IsDataReady

The value indicating that the requested data has been uploaded in the response.
## 🔒︎ bool IsSuccess

The value indicating that there were no errors while receiving the response. If false is returned, use [*Error*](#getError_String) to find the error.
## 🔒︎ string Error

The string containing an error.
## 🔒︎ int NumRows

The number of rows in the obrained SQL response.
## 🔒︎ int NumColumns

The number of columns in the obtained SQL response.
### Members

---

## void Next ( uint maxRows = 20 )

Requests the specified number of next lines. This method can be called only after the [*ExecAsync()*](../../../../api/library/plugins/sql/class.sqldatabase_cs.md#execAsync_SqlRequest_SqlResponse) method, otherwise it will cause a crash.
### Arguments

- *uint* **maxRows** - Maximum number of database lines in request to be obtained.

## string GetColumnName ( int column )

Returns the name of the database column by its index.
### Arguments

- *int* **column** - Database column.

### Return value

Column name.
## Variable GetData ( int row , int column )

Returns the data in the specified cell of the database.
### Arguments

- *int* **row** - Database row index.
- *int* **column** - Database column index.

### Return value

Database variable.
