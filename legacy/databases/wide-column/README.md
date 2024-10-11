# Wide-column Store

A **wide-column-store** (or *extensible record stores*) is a type of *NoSQL database*. It uses tables, rows, and columns, but unlike a relational database, the **names and format of the column can vary from row to row** in the same table.

> A wide-column store can be interpreted as a two-dimensional *key-value store*.

## Wide-column versus columnar databases

Wide-column stores' two-level structures do not use a columnar data layout. In genuine column stores, **a columnar data layout is adopted such that each column is stored separately on disk**.

In Wide-column, all data is stored in a row-by-row fashion, such that the columns for a given row are stored together, rather than each column being stored separately.
