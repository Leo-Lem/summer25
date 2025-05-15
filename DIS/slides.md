[slides](DIS/slides.pdf)
# Generalisation
**Horizontal Partitioning**: table per class.
**Vertical Partitioning**: joined subclasses with duplicated id.
**Full Redundancy**: each instance saved in every table.
**Single Table**: non-existing attributes nulled, discriminator column for type.
# Transactions
**Locking**: ensures data integrity.
**Table lock modes**: **I**ntent **N**one, **I**ntent **S**hare, **I**ntent e**X**clusive, **S**hare with **I**ntent e**X**clusive, **S**hare, **U**pdate, e**X**clusive, superexclusive (Z).
**Row lock modes**: **S**hare (min IS), **U**pdate (min IX), e**X**clusive (min IX), **W**eak exclusive (min IX), **N**ext key **S**hare (min IS), **N**ext key **W**eak exclusive (min IX).
## Isolation Levels
**Uncommitted read** (UR) / **Read Uncommited** (ANSI Level 0): for read only, no record locking. automatic upgrade to CS for modifications. 1 IN table lock.
**Cursor Stability** (CS)/ **Read Commited** (ANSI Level 1): default. locks and unlocks each row, 1 at a time. only returns committed data. 1 IS table lock, 1 NS row lock.
**Read Stability** (RS) / **Repeatable Read** (ANSI Level 2): all querying rows locked until transaction completed. release locks on non-predicated queries. stable result sets. 1 IS table lock, 3000 NS row locks.
**Repeatable Read** (RR) / **Serializable** (ANSI Level 3): lock all rows visited. keep locks until transaction complete. consistent results. 1 S table lock.
# Logging and Recovery
**buffer management**
- **non-atomic** (transactions are not immediately commited): logging and recovery required.
- **no-steal** (uncommited changes not written to disk): no undo needed.
- **no-force** (committed changes not written at commit): redo needed.
**recovery**: redo only, reissue lost modifications.
