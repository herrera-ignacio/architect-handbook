# Read Phenomena

- [Read Phenomena](#read-phenomena)
  - [ISO SQL Standard](#iso-sql-standard)
    - [Dirty Read](#dirty-read)
    - [Non-repeatable (fuzzy) reads](#non-repeatable-fuzzy-reads)
    - [Phantom read](#phantom-read)

## ISO SQL Standard

The The *ANSI/ISO standard SQL 92* defines three read phenomena; issues that can occur when many people read and write to the same rows. These are:

* Dirty read
* Non-repeatable (fuzzy) read
* Phantom read

### Dirty Read

A dirty read is when you see *uncommitted rows in another transaction*.

There is no guarantee the other transaction will commit. Therefore, you could return data that was never saved to the database.

| Transaction 1                                                        	| Transaction 2                                                            	|
|----------------------------------------------------------------------	|--------------------------------------------------------------------------	|
| ```SELECT age FROM users WHERE id = 1; /* will read 20 */ ```    	|                                                                          	|
|                                                                      	| ```UPDATE users SET age = 21 WHERE id = 1; /* No commit here */  ``` 	|
| ```  SELECT age FROM users WHERE id = 1;  /* will read 21 */  ``` 	|                                                                          	|
|                                                                      	| ```ROLLBACK; /* lock-based DIRTY READ */ ```                         	|

### Non-repeatable (fuzzy) reads

A non-repeatable read is when *selecting the same row twice returns different results*.

This happens when someone else updates the row between queries.

> For example, after the first query in transaction 1, transaction 2 changes the shape of the row. So the second query sees the new value.

| Transaction 1 | Transaction 2 |
| - | - |
| ```insert into bricks (colour, shape) values ('red', 'cube'); commit;``` | |
| ```select shape from bricks where colour='red'; /* shape: cube */``` | |
| | ```update bricks set shape='pyramid'; commit;``` |
| ```select shape from bricks where colour='red'; /* shape: pyramid */``` | |

### Phantom read

A phantom read is a *special case of fuzzy read*. This happens when another session inserts or deletes rows that match the where clause of your query. So *repeated queries can return different rows*.

| Transaction 1 | Transaction 2 |
| - | - |
| ```insert into bricks (colour, shape) values ('red', 'cube'); commit;``` | |
| ```select shape from bricks where colour='red'; /* shape: cube */``` | |
| | ```insert into bricks (colour, shape) values ('red', 'pyramid'); commit;``` |
| ```select shape from bricks where colour='red'; /* shape: cube, pyramid */``` | |
