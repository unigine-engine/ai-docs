# Database Operations (Qt SQL)

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Nodes Streaming (SQLite v3)

This sample demonstrates spatial streaming of scene data from an SQLite database using UNIGINE's *ObjectMeshCluster* and the **[UnigineSql](../../../code/plugins/sql/index.md)** plugin.


Features:


- On-demand loading of node data from a local SQLite database
- World chunking system based on player position, with configurable chunk size and visibility range
- Async SQL queries via *[SqlRequest](../../../api/library/plugins/sql/class.sqlrequest_cpp.md)* and *[SqlResponse](../../../api/library/plugins/sql/class.sqlresponse_cpp.md)*, mapped to a 2D grid of streamed chunks
- Runtime BLOB deserialization into nodes and placement via **spawn_nodes()** logic
- Automatic cleanup of completed queries and unused chunks.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/database_operations_qt_sql/nodes_streaming_sqlite_v3*
## Table View UI (SQLite v3)

This sample demonstrates the use of a local *SQLite* database as a structured data backend inside UNIGINE via the **[UnigineSql](../../../code/plugins/sql/index.md)** plugin.


It includes:


- Table creation using core SQLite types (**INTEGER, REAL, TEXT, BLOB**)
- **Insert / Update / Select / Delete (CRUD)** operations on the **variable_samples** table
- Safe prepared statements with positional and named parameter binding
- Sorting and dynamic column selection via **SELECT** queries.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/database_operations_qt_sql/table_view_ui_sqlite_v3*
