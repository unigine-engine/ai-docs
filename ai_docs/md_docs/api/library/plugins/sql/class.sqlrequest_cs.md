# Unigine::Plugins::Sql::SqlRequest Class (CS)


This class manages the requests to the SQL database.


## SqlRequest Class

### Properties

## string Query

The query string using the syntax appropriate for the SQL database being queried.
## Sql.NUMERICAL_PRECISION_POLICY NumericalPrecisionPolicy

The numerical precision policy.
## Sql.BATCH_EXECUTION_MODE BatchExecutionMode

The batch execution mode.
### Members

---

## void BindValue ( int i , Variable value )

Binds a value to a positional parameter in a prepared SQL statement. After calling *bindValue*, when *[*Exec*()](../../../../api/library/plugins/sql/class.sqldatabase_cs.md#exec_SqlRequest_SqlResponse)* is executed, the engine substitutes the provided value for the ? placeholder in the SQL expression.
### Arguments

- *int* **i** - Index of the placeholder in the query, starting from 0.
- *[Variable](../../../../api/library/common/class.variable_cs.md)* **value** - Value to be bound.

## void BindValue ( string placeholder , Variable value )

Set the placeholder to be bound to the value in the prepared statement.
### Arguments

- *string* **placeholder** - Placeholder.
- *[Variable](../../../../api/library/common/class.variable_cs.md)* **value** - Value to be bound.

## void AddBindValue ( Variable [] value )

Binds the value to the next available position in the current record (row).
### Arguments

- *[Variable](../../../../api/library/common/class.variable_cs.md)[]* **value** - Value to be bound.

## void ClearBindings ( )

Clears all bindings.
## void Clear ( )

Clears the request.
