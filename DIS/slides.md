[exercise slides](exercise%20slides.pdf)
[slides](slides-11.pdf)
# Architectures of Database Systems
Relational model succeeded over network and hierarchical models.
**5-layer model**: (hardware) | file system (paged files), buffer (page replacement and materialization strategy, logging/backup/recovery), storage (record/free page management, physical access paths), access system (system catalog, record format, logical access paths), data system (parsing, plan generation, optimization and execution) | (application)
ACID properties of transactions: atomicity (all or nothing), consistency (success means integrity), isolation (logical single user mode), durability (modified data must survive failure).
## Generalisation
**Horizontal Partitioning**: table per class.
**Vertical Partitioning**: joined subclasses with duplicated id.
**Full Redundancy**: each instance saved in every table.
**Single Table**: non-existing attributes nulled, discriminator column for type.

# Transaction Management: Synchronization, Logging & Recoversy
### Anomalies
**lost update**: T2 update overwrites T1 update $\to$ locking, update validation.
**dirty read**: T2 reads uncommitted value after T1 update $\to$ read data only after commit.
**non-repeatable read**: values change while T2 is processed $\to$ lock read access, multiversion concurency control (multiple versions with timestamps or transaction numbers).
**phantom problem**: computation yields differen values, like non-repeatable read but for multiple records or whole relation.
### Isolation Levels
**Uncommitted read** (UR) / **Read Uncommited** (ANSI Level 0): for read only, no record locking. automatic upgrade to CS for modifications. 1 IN table lock.
**Cursor Stability** (CS)/ **Read Commited** (ANSI Level 1): default. locks and unlocks each row, 1 at a time. only returns committed data. 1 IS table lock, 1 NS row lock.
**Read Stability** (RS) / **Repeatable Read** (ANSI Level 2): all querying rows locked until transaction completed. release locks on non-predicated queries. stable result sets. 1 IS table lock, 3000 NS row locks.
**Repeatable Read** (RR) / **Serializable** (ANSI Level 3): lock all rows visited. keep locks until transaction complete. consistent results. 1 S table lock.
### Schedules
**serializability**: can be serially executed (deterministic).
**correctness**: equivalent to one of the serial scehdules.
**equivalence**: have the same effect.
### Concurrency control
***Pessimistic Scheduling**: operations are sequenced by schedular and can be set back. when more writes expected.
- **static v. dynamic locks**: claimed at start of transaction v. whenever needed.
- **2 *P*hase *L*ocking**: expanding and shrinking phase (one a lock is released no more can be claimed).
	- *S*trict 2PL: all write locks are released at operations end.
	- *S*trong *S*trict 2PL: all read and write locks released.
**Deadlocks**: detect (waits-for graph), avoid (wait/die, wound/wait, wait: for lock to be released, wound: try to rollback locking transaction, die: claiming transaction rolled back).
**Optimistic Concurrency Control**: operation executed ASAP. when more reads expected.. 3-phase processing.
- **read**: execute transaction, changes are stored in buffer.
- **validate**: check conflicts between parallel transactions, resolve by rollback, validation sequence defines serialization sequence.
	- **backward-oriented**: validate against all successfully validated transactions during read. problems include high number of comparisons, risk of rolling back long-running transactions, rollback at EOT means unnecessary work, keep WS of finished transactions.
	- **forward-oriented**: writing transactions validate against running transactions. advantages include earlier rollback, kill or die approach, no need for write sets. problems include high number of rollbacks, WS(T) must be locked so RS(T_j) does not change.
- **write**: propagate changes after successful validation, reading transactions do not need this.
***M*ulti-*V*ersion *C*oncurrency *C*ontrol**: each object gets version number, changes increase version number. risk of reading older versions but not of discarded work, needs additional storage/maintenance.
### Locking
**Table lock modes**: **I**ntent **N**one, **I**ntent **S**hare, **I**ntent e**X**clusive, **S**hare with **I**ntent e**X**clusive, **S**hare, **U**pdate, e**X**clusive, superexclusive (Z).
**Row lock modes**: **S**hare (min IS), **U**pdate (min IX), e**X**clusive (min IX), **W**eak exclusive (min IX), **N**ext key **S**hare (min IS), **N**ext key **W**eak exclusive (min IX).
## Logging and Recovery
**buffer management**
- **non-atomic** (transactions are not immediately commited): logging and recovery required.
- **no-steal** (uncommited changes not written to disk): no undo needed.
- **no-force** (committed changes not written at commit): redo needed.
**recovery**: redo only, reissue lost modifications.
**ACID**: Atomicity (all or nothing), Consistency (success means integrity), Isolation (logical single user), Durability (survive any failure).
**Failure types**: transaction (violation of system restrictions), system (crash with memory loss), device (destruction of storage), disaster (destruction of data center)
**Actions**: DO (state -> state and log), REDO (state, log -> state), UNDO (new state, log -> old state, compensation log).
**Recovery classes**: R1 (effect of transaction must be undone), R2+3 (uncommited transactions must be rolled back, commited transactions preserved), R4 (reovery via archive state and log in remote system).
**Durability modes**: guarenteed (wait for flush to disk), delayed (immediately return, might fail).
**Insertion strategies**: update-in-place (each page is written to same block on disc, non-redundant), twin-block (page is assigned to two pages in secondary storage, actual insertion happens later), shadow storage (like twin-block but only changed pages are duplicated).
Checkpoints: transaction-consistent (new transactions must wait), action-consistent (all write ops need to be done), fuzzy (only pageid is written).
# Modern Database Technology
TODO
# Data Warehouses and OLAP
TODO
# Data Mining
TODO
# Big Data Analytics
TODO