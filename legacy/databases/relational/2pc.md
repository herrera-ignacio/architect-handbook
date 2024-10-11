# 2PC: Two-phase commit protocol / XA Transactions

In transaction processing, databases, and computer networking, 2PC is a type of _Atomic Commitment Protocol (ACP)_. It __ensures atomicity of a distributed transaction__.

It is a __distributed algorithm that coordinates all the processes that participate in a distributed atomic transaction on whether to commit or abort (rollback) the transaction__.

The protocol achieves its goal even in many cases of temporary system failuire, however, it is not resilient to all possible failure configurations. To accommodate recovery from failure (automatic in most cases) the protocol's participant use _logging_ of the protocol's states. So __it does not guarantee that a distributed transaction can't fail, but it does guarantee that it can't fail silently__.

Many protocol variants exist that primarily differ in logging strategies and recovery mechanisms.

## When is used?

* When distributed transaction modofies more than one server including the coordinator node.
* When the client executes postgres' `PREPARE TRANSACTION` or other rdbms command, 2PC is used unconditionally.

### Examples

* https://xenovation.com/blog/development/java/java-professional-developer/what-is-a-two-phase-commit-2pc-xa-transaction

## Disadvantage

The greatest disadvantage of 2PC is that is a __blocking protocol__. If coordinator fails permanently, some participants will never resolve their transactions. And, after a participant has sent an _agreement_ message to the coordinator, it will block until a _commit_ or _rollback_ message is received.

## Phases

In a "normal execution" of any single distributed transaction, the protocol consists of two phases:

1. Commit-Request/Voting phase
2. Commit phase

### 1. Commit-Request/Voting phase

A _coordinator_ process attempts to prepare all the transaction's participating processes (workers) to take necessary steps for either committing or aborting the transaction, and to vote, either `yes` or `no`.

* `yes`: commit, if the worker's local portion execution has ended properly.
* `no`: abort, if a problem has been detected with the local portion.

#### Algorithm overview

1. Coordinator sends a __query to commit__ message to all participants and waits until it has received a reploy from all participants.
2. Participants execute transaction up to the point where they will be asked to commit. They each write an entry to their _undo log_ and an entry to their _redo log_.
3. Each participant replies with an __agreement__ message or an __abort__ message.

### 2. Commit phase

Based on _voting_ of the participants, the coordinator decides whether to commit (all have voted `yes`) or abort the transaction, and notifies the result to all participants.

The participants then follow with the needed actions (commit or abort) with their local transactional resources (also called _recoverable resources_) and their respective portions in the transaction's other output if applicable.

#### Success algorithm overview

If coordinator received an __agreement__ message from _all_ participants during the commit-request phase:

1. Coordinator sends a __commit__ message to all participants.
2. Each participant completes the operation, and releasess all the locks and resources held during the transaction.
3. Each participant sends an __acknowledgement__ to the coordinator.
4. Coordinator completes the transaction when all acknowledgements have been received.

#### Failure algorithm overview

If _any_ participant votes __abort__ (or coordinator's timeout __expires__):

1. Coordinator sends a __rollback__ message to all the participants.
2. Each participant undoes the transaction using the _undo log_, and releases the resources and locks held during the transaction.
3. Each participant sends an __acknowledgement__ to the coordinator.
4. Coordinator undoes the transaction when all acknowledgements have been received.


