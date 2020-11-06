# View

In a database, a __view__ is the __result set of a stored query__ on the data, which users can query just as they would in a persistent database collection object.

Unlike ordinary _base tables_ in a relational database, a view __does not form part of the physical schema__, it is a __virtual table__ computed or collated dynamically from data in the database when access to that view is requested. Changes applied to the data in a relevant _underlying table_ are reflected in the data shown in the subsequent invocations of the view.

## Advantages

* Represent a subset of data contained in a table. Consequently, limit the degree of exposure of the underlying tables: a given user may have permission to query the view, while denied access to the rest of the base table.
* Join and simplify multiple tables into a single virtual table.
* Act as aggregated tables, where the database engine aggregates data (`SUM`, `AVERAGE`, etc.) and presents calculated results as part of the data.
* Hide complexity of data.

## Examples

* [Views in PostgreSQL](https://www.postgresql.org/docs/current/tutorial-views.html)
