# Unigine::Plugins::Sql::SqlRequest Class (CPP)

**Header:** #include <plugins/Unigine/Sql/UnigineSql.h>


This class manages the requests to the SQL database.


## SqlRequest Class

### Members

## void setQuery ( const char * query )

Sets a new query string using the syntax appropriate for the SQL database being queried.
### Arguments

- *const char ** **query** - The query string using the syntax appropriate for the SQL database being queried.

## String getQuery () const

Returns the current query string using the syntax appropriate for the SQL database being queried.
### Return value

Current query string using the syntax appropriate for the SQL database being queried.
## void setNumericalPrecisionPolicy ( Sql::NUMERICAL_PRECISION_POLICY policy )

Sets a new numerical precision policy.
### Arguments

- *[Sql::NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_cpp.md#NUMERICAL_PRECISION_POLICY)* **policy** - The numerical precision policy, one of the [NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_cpp.md#NUMERICAL_PRECISION_POLICY) values.

## Sql::NUMERICAL_PRECISION_POLICY getNumericalPrecisionPolicy () const

Returns the current numerical precision policy.
### Return value

Current numerical precision policy, one of the [NUMERICAL_PRECISION_POLICY](../../../../api/library/plugins/sql/class.sql_cpp.md#NUMERICAL_PRECISION_POLICY) values.
## void setBatchExecutionMode ( Sql::BATCH_EXECUTION_MODE mode )

Sets a new batch execution mode.
### Arguments

- *[Sql::BATCH_EXECUTION_MODE](../../../../api/library/plugins/sql/class.sql_cpp.md#BATCH_EXECUTION_MODE)* **mode** - The batch execution mode, one of the [BATCH_EXECUTION_MODE](../../../../api/library/plugins/sql/class.sql_cpp.md#BATCH_EXECUTION_MODE) values.

## Sql::BATCH_EXECUTION_MODE getBatchExecutionMode () const

Returns the current batch execution mode.
### Return value

Current batch execution mode, one of the [BATCH_EXECUTION_MODE](../../../../api/library/plugins/sql/class.sql_cpp.md#BATCH_EXECUTION_MODE) values.
---

## void bindValue ( int i , const Variable & value )

Binds a value to a positional parameter in a prepared SQL statement. After calling *bindValue*, when *[*exec*()](../../../../api/library/plugins/sql/class.sqldatabase_cpp.md#exec_SqlRequest_SqlResponse)* is executed, the engine substitutes the provided value for the ? placeholder in the SQL expression.
### Arguments

- *int* **i** - Index of the placeholder in the query, starting from 0.
- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **value** - Value to be bound.

## void bindValue ( const char * placeholder , const Variable & value )

Set the placeholder to be bound to the value in the prepared statement.
### Arguments

- *const char ** **placeholder** - Placeholder.
- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **value** - Value to be bound.

## void addBindValue ( const Vector < Variable > & value )

Binds the value to the next available position in the current record (row).
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Variable](../../../../api/library/common/class.variable_cpp.md) > &* **value** - Value to be bound.

## void clearBindings ( )

Clears all bindings.
## void clear ( )

Clears the request.
