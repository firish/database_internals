## What Are Storage Engines?

A storage engine is a software component of a database management system (DBMS).
This component handles the creation, retrieval, updating, and deletion of data in a database. 
It determines how data is stored on the physical disk.

Different storage engines offer various features and optimizations, such as support for transactions, foreign keys, indexing strategies, and data compression.

Note: Database systems (DMBS) as we know it, use storage engines behind the scenes. 
DBMS, or database engines use a storage engine and build additional logic like GUI based schemas, transactions, replication on top of these engines.

### Why Are Storage Engines Important?
Choosing the right storage engine is crucial because it affects:
- Performance: Read/write speeds, indexing efficiency, and query execution times.
- Data Integrity: Support for transactions and data consistency models.
- Scalability: How well the database handles increasing amounts of data.
- Functionality: Features like full-text search, geospatial indexing, and replication.


### Key Considerations When Choosing a Storage Engine
- Transaction Support: Do you need ACID-compliant transactions?
- Concurrency Control: How does the engine handle multiple simultaneous operations?
- Distributed features: For distributed systems, whats the most important? Consistency, Availability, or Partial Tolerance (CAP)? 
- Data Volume: Can it efficiently handle your expected data size? (account for scalability requirements as well)
- Read/Write Patterns: Is your application read-heavy, write-heavy, or balanced?
- Data Durability: Is data persistence critical, or can you afford data loss in certain scenarios?
- Feature Set: Do you need full-text search, geospatial indexing, or other specialized features?

### Most Important Storage engines

