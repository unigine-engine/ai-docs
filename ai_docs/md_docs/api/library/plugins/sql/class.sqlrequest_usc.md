# Unigine::Plugins::Sql::SqlRequest Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class manages the requests to the SQL database.


## SqlRequest Class

### Members

## void setQuery ( String query )

Sets a new query string using the syntax appropriate for the SQL database being queried.
### Arguments

- *String* **query** - The query string using the syntax appropriate for the SQL database being queried.

## String getQuery () const

Returns the current query string using the syntax appropriate for the SQL database being queried.
### Return value

Current query string using the syntax appropriate for the SQL database being queried.
## void setNumericalPrecisionPolicy ( int policy )

Sets a new numerical precision policy.
### Arguments

- *int* **policy** - The numerical precision policy, one of the [NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_usc.md#NUMERICAL_PRECISION_POLICY) values.

## int getNumericalPrecisionPolicy () const

Returns the current numerical precision policy.
### Return value

Current numerical precision policy, one of the [NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_usc.md#NUMERICAL_PRECISION_POLICY) values.
## void setBatchExecutionMode ( int mode )

Sets a new batch execution mode.
### Arguments

- *int* **mode** - The batch execution mode, one of the [BATCH_EXECUTION_MODE](../../../../api/library/plugins/sql/class.sql_usc.md#BATCH_EXECUTION_MODE) values.

## int getBatchExecutionMode () const

Returns the current batch execution mode.
### Return value

Current batch execution mode, one of the [BATCH_EXECUTION_MODE](../../../../api/library/plugins/sql/class.sql_usc.md#BATCH_EXECUTION_MODE) values.
---

## void bindValue ( int i , Variable value )

Binds a value to a positional parameter in a prepared SQL statement. After calling *bindValue*, when *[*exec*()](../../../../api/library/plugins/sql/class.sqldatabase_usc.md#exec_SqlRequest_SqlResponse)* is executed, the engine substitutes the provided value for the ? placeholder in the SQL expression.
### Arguments

- *int* **i** - Index of the placeholder in the query, starting from 0.
- *Variable* **value** - Value to be bound.

## void bindValue ( String placeholder , Variable value )

Set the placeholder to be bound to the value in the prepared statement.
### Arguments

- *String* **placeholder** - Placeholder.
- *Variable* **value** - Value to be bound.

## void addBindValue ( Vector<Variable> value )

Binds the value to the next available position in the current record (row).
### Arguments

- *Vector<Variable>* **value** - Value to be bound.

## void clearBindings ( )

Clears all bindings.
## void clear ( )

Clears the request.
