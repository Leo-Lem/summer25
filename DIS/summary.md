[exercises](exercises.pdf)
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
## Anomalies
**lost update**: T2 update overwrites T1 update $\to$ locking, update validation.
**dirty read**: T2 reads uncommitted value after T1 update $\to$ read data only after commit.
**non-repeatable read**: values change while T2 is processed $\to$ lock read access, multiversion concurency control (multiple versions with timestamps or transaction numbers).
**phantom problem**: computation yields differen values, like non-repeatable read but for multiple records or whole relation.
## Isolation Levels
**Uncommitted read** (UR) / **Read Uncommited** (ANSI Level 0): for read only, no record locking. automatic upgrade to CS for modifications. 1 IN table lock.
**Cursor Stability** (CS)/ **Read Commited** (ANSI Level 1): default. locks and unlocks each row, 1 at a time. only returns committed data. 1 IS table lock, 1 NS row lock.
**Read Stability** (RS) / **Repeatable Read** (ANSI Level 2): all querying rows locked until transaction completed. release locks on non-predicated queries. stable result sets. 1 IS table lock, 3000 NS row locks.
**Repeatable Read** (RR) / **Serializable** (ANSI Level 3): lock all rows visited. keep locks until transaction complete. consistent results. 1 S table lock.
## Schedules
**serializability**: can be serially executed (deterministic).
**correctness**: equivalent to one of the serial scehdules.
**equivalence**: have the same effect.
## Concurrency control
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
## Locking
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
## Distributed DBMS
**Online Transaction Processing**: distributed consistency.
**Consensus**: proposal is decided by quorum (min number of nodes that have committed).
**Atomic commit**: must commit when all nodes vote to commit, must abort if any votes abort.
**Failures**: site (node is unavailable), communication.
**Transaction Coordinator and Manager**: coordinate overall execution, manage local operations.
**Distributed serializability**: differentiating global and local dependency. Solutions include functional limitations (restrict update capabilities globally), non-functional limitations (relax ACID), reduce local autonomy, reduce hetrogeneity (compatible sync and commit protocols).
**Quasi-serializability**: only local schedule are fully serializable, global transactions are executed sequentially.
**Scale-up v. scale-out**: bigger node v. more nodes.
- Shared disk: equal access to shared memory, network linked, don't share private memory.
- Shared nothing: each cluster has exclusive memory.
- Shared everything: disk and main-memory is shared (*N*on-*U*niform *M*emory *A*ccess).
- Federated Database: multiple databases connected to logical view. no direct sharing. not truly distributed.
- Heterogenous federation: use diferent DBS.
### Commit Protocols
*robustness (non-blocking, abort late) v. efficiency (few messages, log entries).*
**2-Phase-Commit**: prepare (coordinator sends prepare message, nodes vote), commit (coordinator sends commit or abort and nodes execute). robust-efficient compromise.
**Tree 2PC**: no central coordinator, but a tree of nodes. forward/receive to/from child nodes.
**Linear 2PC**: daisychain comms between participants. forward (ready/failed), then backward (commit/abort).
**3PC**: additional precommit phase (prepare to commit or abort, nodes acknowledge). Makes using new coordinator better. But has more messages and problems with network partitioning (network delays cause timeouts). very robust.
**1PC**: direct commit decision. rarely used for distributed systems. very efficient.
## Optimizations
**Storage Layouts**: row (tuple-wise) or collumn (attribute-wise).
**Query execution plan optimizations**: relational algebra for internal representation, reduce data as early and cheap as possible, chosen sequence is final Query Execution Plan QEP.
**Data processing models**
- tuple-at-a-time: intermediate tuples not stored but passed directly to next operator $\to$ operators can be fused but other optimization are limited.
- vector/block-at-a-time: vector/block of the column processed at once $\to$ operator fusion for small blocks, trade-off between operator fusion and memory access performance.
- operator-at-a-time: whole operator processed at once $\to$ no operator fusion, high potential for optimizing memory reads.
**User optimizations**
- views: virtual tables to simplify complex queries.
- indexes: trees or hashtables to quickly locate rows.
## NoSQL
***N*ot-*o*nly-*SQL***
**Big Data**: volume, variety, velocity, value, veracity (quality, bias).
**BASE**: Basically Available, Soft state, Eventually consistent.
**CAP**: only 2/3 of Consistency, Availability and Partition
**Key-Value**: simple CRUD implementation, stores arbitrary keyed data. Log-structured Merge (LSM) Trees power many KV stores: buffer writes in--memory, flushes data as sorted runs, merge runs into larger runs (compaction).
**Document**: KV with value being documents.
**Wide Table**: database is collection of KV pairs with 3-part keys (row key, column key, timestamp). flexible schema may differ from row-to-row.
**Graphs**: nodes (entities in ER) existing on their own with object identity. edges (relationships in ER) existing only between nodes and identiy depending on connected nodes.
**Others**: timeseries, spatial, arrays, …
# Data Warehouses and OLAP
# Data Mining
# Big Data Analytics