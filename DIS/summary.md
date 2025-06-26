[exercises](exercises.pdf) | [slides](slides-17.pdf)
# Database System Architectures
Relational model succeeded over network and hierarchical models.
**5-layer model**: (hardware) | file system (paged files), buffer (page replacement and materialization strategy, logging/backup/recovery), storage (record/free page management, physical access paths), access system (system catalog, record format, logical access paths), data system (parsing, plan generation, optimization and execution) | (application)
ACID properties of transactions: atomicity (all or nothing), consistency (success means integrity), isolation (logical single user mode), durability (modified data must survive failure).
## Generalisation
**Horizontal Partitioning**: table per class.
**Vertical Partitioning**: joined subclasses with duplicated id.
**Full Redundancy**: each instance saved in every table.
**Single Table**: non-existing attributes nulled, discriminator column for type.

# Transaction Management
## Anomalies
**lost update**: T2 update overwrites T1 update $\to$ locking, update validation.
**dirty read**: T2 reads uncommitted value after T1 update $\to$ read data only after commit.
**non-repeatable read**: values change while T2 is processed $\to$ lock read access, multi-version concurrency control (multiple versions with timestamps or transaction numbers).
**phantom problem**: computation yields different values, like non-repeatable read but for multiple records or whole relation.
## Isolation Levels
**Uncommitted read** (UR) / **Read Uncommitted** (ANSI Level 0): for read only, no record locking. automatic upgrade to CS for modifications. 1 IN table lock.
**Cursor Stability** (CS)/ **Read Committed** (ANSI Level 1): default. locks and unlocks each row, 1 at a time. only returns committed data. 1 IS table lock, 1 NS row lock.
**Read Stability** (RS) / **Repeatable Read** (ANSI Level 2): all querying rows locked until transaction completed. release locks on non-predicated queries. stable result sets. 1 IS table lock, 3000 NS row locks.
**Repeatable Read** (RR) / **Serialisable** (ANSI Level 3): lock all rows visited. keep locks until transaction complete. consistent results. 1 S table lock.
## Schedules
**serialisability**: can be serially executed (deterministic).
- full/strict serialisability/linearisability: includes real-time ordering (if tA completes before tB effects are visible). consistency across distributed systems.
- final state serialisability FSR: final database state matches serial execution, no preservation of real-time ordering.
- view serialisability VSR: same reads and writes as serialisable schedule (allows blind writes).
- conflict serialisable CSR: a schedule is CSR when it is conflict equivalent to some serial schedule. acyclic $\to$ CSR. build a conflict graph with nodes=transactions and edges=conflict.
- order-CSR: only committed ordering matter for conflicts.
- committed-order serialisability with commit-sequence constraints COSCSR: ensures commit order corresponds to some serial order, can allow intermediate anomalies.
- serial: weakest here.
**correctness**: equivalent to one of the serial schedules.
**equivalence**: have the same effect.
## Locking
**Table lock modes**: **I**ntent **N**one, **I**ntent **S**hare, **I**ntent e**X**clusive, **S**hare with **I**ntent e**X**clusive, **S**hare, **U**pdate, e**X**clusive, superexclusive (Z).
**Row lock modes**: **S**hare (min IS), **U**pdate (min IX), e**X**clusive (min IX), **W**eak exclusive (min IX), **N**ext key **S**hare (min IS), **N**ext key **W**eak exclusive (min IX).
## Concurrency control
***Pessimistic Scheduling**: operations are sequenced by schedular and can be set back. when more writes expected.
- **static v. dynamic locks**: claimed at start of transaction v. whenever needed.
- **2 *P*hase *L*ocking**: expanding and shrinking phase (after unlcok no more lock).
	- *S*trict 2PL: all (write) locks are released at transaction end.
	- *S*trong *S*trict 2PL: all read **and** write locks released at transaction end.
- **Preclaiming**: all locks are set before other operations.
**Deadlocks**: detect (waits-for graph), avoid (wait/die, wound/wait, wait: for lock to be released, wound: try to rollback locking transaction, die: claiming transaction rolled back).
**Optimistic Concurrency Control**: operation executed ASAP. when more reads expected.. 3-phase processing.
- **read**: execute transaction, changes are stored in buffer.
- **validate**: check conflicts between parallel transactions, resolve by rollback, validation sequence defines serialisation sequence.
	- **backward-oriented**: validate against all successfully validated transactions during read. problems include high number of comparisons, risk of rolling back long-running transactions, rollback at EOT means unnecessary work, keep WS of finished transactions.
		- BOCC+: add timestamp to to check if committed during read.
	- **forward-oriented**: writing transactions validate against running transactions. advantages include earlier rollback, kill or die approach, no need for write sets. problems include high number of rollbacks, WS(T) must be locked so RS(T_j) does not change.
- **write**: propagate changes after successful validation, reading transactions do not need this.
***M*ulti-*V*ersion *C*oncurrency *C*ontrol**: each object gets version number, changes increase version number. risk of reading older versions but not of discarded work, needs additional storage/maintenance.
## Logging and Recovery
**ACID**: Atomicity (all or nothing), Consistency (success means integrity), Isolation (logical single user), Durability (survive any failure).
**Failure types**
- transaction: violation of system restrictions.
- system: crash with memory loss.
- device: destruction of storage.
- disaster: destruction of data center.
**Actions**
- DO: state -> state and log.
- REDO: state, log -> state.
- UNDO: new state, log -> old state, compensation log.
**Recovery classes**
- R1: effect of transaction must be undone.
- R2+3: uncommitted transactions must be rolled back, committed transactions preserved.
- R4: recovery via archive state and log in remote system.
**Durability modes**
- guaranteed: wait for flush to disk.
- delayed: immediately return, might fail.
**Insertion strategies**
- update-in-place: each page is written to same block on disc, non-redundant.
- twin-block: page is assigned to two pages in secondary storage, actual insertion later.
- shadow storage: like twin-block but only changed pages are duplicated.
**Checkpoints**
- transaction-consistent: new transactions must wait.
- action-consistent: all write ops need to be done.
- fuzzy: only page ID is written.
**exemplary buffer management**
- **non-atomic** (transactions not all/nothing on hardware level): logging and recovery required.
- **no-steal** (uncommitted changes not written to disk): no undo needed.
- **no-force** (committed changes not directly written at commit): redo needed.
$\hookrightarrow$ **recovery**: redo only, reissue lost modifications.
# Modern Database Technology
## Distributed DBMS
**Online Transaction Processing**: distributed consistency.
**Consensus**: proposal is decided by quorum (min number of nodes that have committed).
**Atomic commit**: must commit when all nodes vote to commit, must abort if any votes abort.
**Failures**: site (node is unavailable), communication.
**Transaction Coordinator and Manager**: coordinate overall execution, manage local operations.
**Distributed serialisability**: differentiating global and local dependency. Solutions include functional limitations (restrict update capabilities globally), non-functional limitations (relax ACID), reduce local autonomy, reduce heterogeneity (compatible sync and commit protocols).
**serialisability**: only local schedule are fully serialisable, global transactions are executed sequentially.
**Scale-up v. scale-out**: bigger node v. more nodes.
- Shared disk: equal access to shared memory, network linked, don't share private memory.
- Shared nothing: each cluster has exclusive memory.
- Shared everything: disk and main-memory is shared (*N*on-*U*niform *M*emory *A*ccess).
- Federated Database: multiple databases connected to logical view. no direct sharing. not truly distributed.
- Heterogenous federation: use different DBS. TODO: taxonomies
### Commit Protocols
*robustness (non-blocking, abort late) v. efficiency (few messages, log entries).*
**2-Phase-Commit**: prepare (coordinator sends prepare message, nodes vote), commit (coordinator sends commit or abort and nodes execute). robust-efficient compromise.
**Tree 2PC**: no central coordinator, but a tree of nodes. forward/receive to/from child nodes.
**Linear 2PC**: daisy chain comms between participants. forward (ready/failed), then backward (commit/abort).
**3PC**: additional pre-commit phase (prepare to commit or abort, nodes acknowledge). Makes using new coordinator better. But has more messages and problems with network partitioning (network delays cause timeouts). very robust.
**1PC**: direct commit decision. rarely used for distributed systems. very efficient.
### Exercises
- How many messages are required to perform the 2-Phase-Commit Protocol (with a flattened process tree) for this transaction in case of a successful processing? 20.
- How would that change, if T5 fails before sending the Ready message? 17 for implicit failure, 18 for explicit failure (negative vote).
- How does it change if 1PC, Tree 2PC, or 3PC is used? 10, 20, 30
- How many messages are necessary with 2PC when ST1 and ST5 are read-only? 16
---
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
**Document**: KV with value being documents.
**Wide Table**: database is collection of KV pairs with 3-part keys (row key, column key, timestamp). flexible schema may differ from row-to-row.
**Graphs**: nodes (entities in ER) existing on their own with object identity. edges (relationships in ER) existing only between nodes and identiy depending on connected nodes.
**Others**: timeseries, spatial, arrays, …

| Type            | Requirements                            |
| --------------- | --------------------------------------- |
| RDBMS           | Transactions, structured data           |
| Document Store  | Flexible schema, nested data            |
| Key-Value Store | Caching, sessions, simple fast reads    |
| Column Store    | Analytical workloads, big data          |
| Graph DB        | Relationship-heavy, complex connections |
| Time-Series DB  | Monitoring, sensors, real-time inserts  |
| Search DB       | Full-text search, log analysis          |
### Key-Value stores
**simple CRUD implementation, stores arbitrary keyed data.**
**Log-structured Merge (LSM) Trees** power many KV stores: buffer writes in-memory, flushes data as sorted runs, merge runs into larger runs (compaction).
**Sorted String Table SST**: write data to separate string and use index for position as long as inserted data is increasing in index, otherwise new string and index.
### Graph database
**Types**: Property graph model, resource description framework, property graph query language (imitates sql).
**Neo4j PGM**: Entity with properties, schema implicitly given with instances.
**Representations**
- Adjacency matrix: Aij=1 if there is an edge. very fast lookup. memory inefficient (sparseness).
- Compress sparse row CSR: very compact O(V+E). efficient for parallelism.
- triple table: subject, predicate, object.
- vertex and edge table.
- clustered property table: all properties of single node are stored together. lower compression and harder to optimise.
- property-class table: separate table per node/edge type. better compression, stronger typing, but less flexible and harder to change.
**Concepts**: path, simple path (no cycles), cliques (fully edge-connected), cycle, subgraph, connected components (path between every pair of vertices).
- **Degree** (Valency): in/out edges of vertex.
- **Distance**: number of edges in shortest path.
**Patterns** in neo4j (match subgraphs)
- Vertex: ()
- Edge: --(>)
- Graph ()-->()<--()
**Queries**
- MATCH: specify subgraph to return.
- OPTIONAL MATCH: null-columns for non-matched, but return row.
- WHERE: filter results (because MATCH does not support everything like inequality).
- Projection: map the results.
# Data Warehouses
_Enable (analytic) access to consistent data in centralised database with extraction and multi-stage loading of integrated (and historicised) data for analytical tools._
**Steps of descriptive statistics**: data recording (raw data), preparation (processed raw data), and analysis (enriched data, aggregates, macrocosmos).
**Characteristics**: analysis-orientation, integration of different sources, no user updates, historic data.
**Non-volatile data**: no deletion, only flag to keep history.
**Basic architecture**
- **Data transformation**: Extract, Transform, Load (ETL)
- **Data consolidation:** integrated database, not specifically modelled so no optimisations for schemas or physical database.
- **Data provisioning**: dispositive database, optimised for analysis
- Data Marts: related subset derived from main DWH.
	- dependent (redundant)
	- independent.
**Lambda architecture**
- Batch layer: store all historical data and compute batch views.
- Speed layer: process real-time data for fast updates.
- Serving layer: expose combined results to end-users.
**Logical DWH**: combine DWH RDBMS with data lakes virtually.
## Data cubes
**Multidimensional(-Cube) tables**: for online analytical processing (OLAP), data mining, visualisation.
- Dimensions (descriptive information): cube edges.
- Facts (quantified information): cube cells.
- Characteristics of summability: disjointness, completeness.
- Summation types
	- flow (event at time T): can be aggregated freely, usually things per time.
	- stock (status at time T): can be aggregated freely, but not temporally.
	- value-per-unit VPU: can be summed (except for min/max/avg).
**Operations**
- slicing: selection via specification of one dimension.
- dicing: selecting a subcube (or multiple).
- drill-down: moving to smaller dimension hierarchy (state $\to$ city).
- roll-up: moving to larger dimension hierarchy (city $\to$ state).
- drill-across: change from one subcube to another.
## Multidimensional databases
**Relational** ROLAP: use relational database.
- **Star schema**: central fact table with denormalised dimension tables. better query performance, simplicity of structure.
- **Snowflake schema**: central fact table with normalised dimension tables (each datum stored only once).
- **Galaxy schema**: multiple fact tables, shared dimension tables.
- pros: scalability, proven database technology.
- cons: mapping overhead, extensive metadata management, slower.
- relational mapping of hierarchies
	1. vertical: explicit using separate relations. normalised. snowflake.
	2. horizontal: implicit through attributes. denormalised. star.
	3. recursive vertical: combination with horizontal possible. explicitly mapping arbitrary deep hierarchies.
**Multidimensional** MOLAP: use multidimensional database (direct storage as cubes).
- pros: no transfer of modelling concepts, fast and efficient.
- cons: proprietary, missing compression/scalability, limited dimensions.
**Hybrid** HOLAP: combine the two approaches.
# Data Mining
_Knowledge discovery in databases._
**Process**: raw data -select> data -prepare/transform> data (in DW) -mine> pattern -interpret> knowledge.
**CRISP-DM**: understand business -> understand data -> prepare data -> model -> evaluate -> deploy.
**Another process**: identify -> estimate -> apply -> evaluate -> adapt.
**Preprocessing**: decrease runtime and resource intensity. increase quality.
- data types: nominal (categories). ordinal (+ranking). interval (+distance). ratio (+zero point).
- metrics
	- numerics: distance (minkowski, manhattan, euclidian, tchebychev).
	- set/bags/vectors: cosine similarity, Jaccard coefficient.
	- signatures, histograms, probability distributions: Wasserstein metric
	- strings: soundex (phonetic), Levenshtein distance (number of insert/delete/exchange).
- missing data: ignore, manual complete, automatic complete.
- outliers: manual detection, statistical methods, domain knowledge, distance-based, deviation-based.
- dimensions: feature selection or composition, PCA.
- value count: splitting of bias.
# Big Data