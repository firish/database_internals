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

### InnoDB
1. When Was It Made?
Year: 1999
Developer: Innobase Oy (later acquired by Oracle Corporation)

2. Which Real-World DBMS Use It?
DBMS: MySQL (default since version 5.5), MariaDB

3. What Is the Idea Behind It?
InnoDB was designed to provide a reliable and high-performance storage engine that supports ACID-compliant transactions and row-level locking. It supports features like foreign key constraints and crash recovery.
The idea is to facilitate applications that require robust transactional support and high concurrency.

Note: Row-Level Locking:
- Locks individual rows in a table during a transaction.
- Allows multiple transactions to access different rows simultaneously.
- Improves concurrency and reduces contention.
- The locking has some overhead reducing read performance.

5. Biggest Strengths and Biggest Weaknesses
Strengths:
ACID Compliance: Ensures data integrity through transactions.
Row-Level Locking: Allows multiple concurrent writes, enhancing performance in multi-user environments.
Foreign Key Support: Enforces referential integrity between tables.
Crash Recovery: Uses logs for automatic recovery after a crash.

Weaknesses:
Resource Intensive: Requires more memory and storage overhead due to transactional logs and indexing.
Complex Configuration: Optimal performance may require tuning numerous parameters.
Slower Read Performance: May be slower for read-heavy applications compared to engines like MyISAM.

5. When Is the Use Case for Using This?
Use Cases: Ideal for applications that require data integrity and transactional support, such as financial systems, e-commerce platforms, and any application where data consistency is critical.


### MyISAM
1. When Was It Made?
Year: 1999
Developer: MySQL AB

2. Which Real-World DBMS Use It?
DBMS: MySQL

3. What Is the Idea Behind It?
MyISAM was designed for simplicity and speed.
It is particularly optimized for read-heavy operations.
It uses table-level locking and does not support transactions or foreign keys, making it less complex but also less feature-rich than transactional engines.

Note: Table-Level Locking:
- Locks the entire table during a transaction.
- Simple to implement (less overhead) but reduces concurrency.
- Other transactions must wait until the lock is released.

4. Biggest Strengths and Biggest Weaknesses
Strengths:
Fast Read Operations: Optimized for quick data retrieval.
Low Resource Usage: Consumes less memory and storage without transactional overhead.
Simplicity: Easier to understand and manage.

Weaknesses:
No Transaction Support: Lacks ACID compliance.
Table-Level Locking: Reduces concurrency during write operations.
No Foreign Key Constraints: Does not enforce referential integrity.

5. When Is the Use Case for Using This?
Use Cases: Suitable for read-heavy applications where data does not change often and transactions are not critical, such as reporting systems, data warehousing, or simple web applications.

### RocksDB
1. When Was It Made?
Year: 2013
Developer: Facebook
2. Which Real-World DBMS Use It?
DBMS: MyRocks (MySQL variant), CockroachDB, Apache Kafka Streams
3. What Is the Idea Behind It?
RocksDB is an embeddable, high-performance key-value store designed for fast storage environments like SSDs. It builds upon LevelDB but adds improvements for performance and scalability. The idea is to handle workloads requiring high write throughput and low latency.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

High Write Performance: Optimized for write-heavy workloads.
Configurable: Highly tunable for various storage environments.
Space Efficiency: Supports compression and efficient storage.
Weaknesses:

Complex Tuning: Requires in-depth knowledge to optimize settings.
Limited Feature Set: Lacks some relational database features unless integrated into a DBMS.
Resource Usage: Can be CPU and memory-intensive.
5. When Is the Use Case for Using This?
Use Cases: Suitable for applications needing high write throughput and low latency, such as real-time analytics, logging systems, and large-scale data ingestion platforms.
WiredTiger
1. When Was It Made?
Year: 2010
Developer: WiredTiger Inc. (acquired by MongoDB Inc. in 2014)
2. Which Real-World DBMS Use It?
DBMS: MongoDB (default since version 3.2)
3. What Is the Idea Behind It?
WiredTiger was created to provide a modern storage engine with support for document-level concurrency and compression. It aims to improve performance and scalability in MongoDB by efficiently utilizing hardware resources and supporting larger data volumes.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

High Concurrency: Document-level locking increases parallelism.
Data Compression: Reduces disk space usage.
Scalability: Better performance with multi-core CPUs.
Weaknesses:

Complex Configuration: May require tuning for optimal performance.
Memory Consumption: Can be memory-intensive with large datasets.
Limited to MongoDB: Not used outside of MongoDB environments.
5. When Is the Use Case for Using This?
Use Cases: Ideal for MongoDB applications requiring high throughput, efficient storage, and scalability, such as content management systems, IoT platforms, and big data applications.
Memory (Heap) Engine
1. When Was It Made?
Year: Mid-1990s
Developer: MySQL AB
2. Which Real-World DBMS Use It?
DBMS: MySQL
3. What Is the Idea Behind It?
The Memory (Heap) engine is designed to store data in RAM, providing extremely fast data access. It's intended for temporary storage of data where speed is critical and persistence is not required.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

Ultra-Fast Access: RAM storage allows for rapid data retrieval and manipulation.
Low Latency: Ideal for applications requiring immediate response times.
Weaknesses:

Volatile Storage: Data is lost if the server restarts or crashes.
Size Limitations: Limited by the amount of available RAM.
No Transaction Support: Does not support ACID transactions.
5. When Is the Use Case for Using This?
Use Cases: Suitable for caching, session management, temporary tables, and lookup tables where data persistence is not essential.
Aria
1. When Was It Made?
Year: 2007
Developer: MariaDB Corporation
2. Which Real-World DBMS Use It?
DBMS: MariaDB
3. What Is the Idea Behind It?
Aria was developed as a crash-safe alternative to MyISAM, combining speed with reliability. It aims to serve as a general-purpose storage engine suitable for both transactional and non-transactional applications.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

Crash Recovery: Offers better data safety compared to MyISAM.
Fast Read Performance: Maintains high-speed data retrieval.
Versatility: Supports both transactional and non-transactional tables.
Weaknesses:

Incomplete Transaction Support: Lacks full ACID compliance.
Less Adoption: Not as widely used or tested as InnoDB.
Limited Community Support: Smaller user base may mean fewer resources.
5. When Is the Use Case for Using This?
Use Cases: Best for applications needing fast read performance with better reliability than MyISAM but not requiring full transactional support, such as content delivery systems and read-intensive applications.
NDB Cluster
1. When Was It Made?
Year: Early 2000s
Developer: MySQL AB (originally developed by Ericsson)
2. Which Real-World DBMS Use It?
DBMS: MySQL Cluster (separate product from standard MySQL)
3. What Is the Idea Behind It?
NDB Cluster is designed for distributed, high-availability environments, providing in-memory storage with data replication across multiple nodes. It aims to deliver real-time performance with no single point of failure.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

High Availability: Automatic failover and redundancy.
Scalability: Can scale horizontally by adding more data nodes.
Real-Time Performance: Low-latency access suitable for time-sensitive applications.
Weaknesses:

Complex Setup: Requires expertise to configure and maintain.
Resource Demanding: Needs significant memory and network resources.
Limited Feature Support: Not all MySQL features are available or fully supported.
5. When Is the Use Case for Using This?
Use Cases: Ideal for applications requiring 99.999% uptime, such as telecommunications, online gaming, and other mission-critical systems where data must always be available.
TokuDB
1. When Was It Made?
Year: 2009
Developer: Tokutek (acquired by Percona in 2015)
2. Which Real-World DBMS Use It?
DBMS: MariaDB, Percona Server for MySQL
3. What Is the Idea Behind It?
TokuDB utilizes Fractal Tree indexing to improve write performance and storage efficiency for large datasets. It's designed to handle high insertion rates and large volumes of data without significant performance degradation.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

High Insertion Rates: Optimized for fast data ingestion.
Compression: Significant storage savings through data compression.
Efficient Indexing: Maintains performance with large indexes.
Weaknesses:

Discontinued Development: As of 2020, TokuDB is no longer actively developed.
Compatibility Issues: May not support all features or latest versions of MySQL/MariaDB.
Complex Tuning: Requires specialized knowledge to optimize settings.
5. When Is the Use Case for Using This?
Use Cases: Suitable for applications handling big data and high write loads, like logging systems, data warehousing, and analytics platforms where storage efficiency and write performance are critical.
LevelDB
1. When Was It Made?
Year: 2011
Developer: Google
2. Which Real-World DBMS Use It?
DBMS: Used as an embedded database in applications like Bitcoin Core, Google Chrome, and Ethereum clients.
3. What Is the Idea Behind It?
LevelDB is a fast key-value storage library that provides an ordered mapping from keys to values. It's designed for high performance and low latency, using a log-structured merge-tree (LSM tree) data structure.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

High Performance: Efficient read/write operations.
Lightweight: Minimal overhead, suitable for embedding.
Simple API: Easy integration into various applications.
Weaknesses:

Limited Features: No support for SQL queries, transactions, or concurrent access by multiple processes.
Single-Process Access: Not designed for multi-process or networked environments.
No Built-In Replication: Lacks features for data replication or distribution.
5. When Is the Use Case for Using This?
Use Cases: Ideal for embedded systems, desktop applications, or components within larger systems where a simple, fast key-value store is needed without the complexity of a full-fledged database server.
Berkeley DB
1. When Was It Made?
Year: 1991
Developer: Sleepycat Software (acquired by Oracle Corporation in 2006)
2. Which Real-World DBMS Use It?
DBMS: Embedded within various applications and systems, including early versions of OpenLDAP and Subversion.
3. What Is the Idea Behind It?
Berkeley DB is an embedded database library that provides scalable, high-performance data management services to applications. It offers multiple data storage models, including key-value and relational-like tables, and supports transactions and concurrency.

4. Biggest Strengths and Biggest Weaknesses
Strengths:

High Performance: Efficient storage and retrieval.
ACID Transactions: Supports full transactional integrity.
Versatile APIs: Available for multiple programming languages.
Weaknesses:

No SQL Interface: Interactions are through APIs, requiring more complex application code.
Complex Configuration: Can be challenging to configure and optimize.
Licensing: Dual-license model may impose restrictions on proprietary use.
5. When Is the Use Case for Using This?
Use Cases: Suitable for applications needing an embedded, high-performance database with transactional support, such as mobile apps, embedded systems, or applications where a full database server is impractical.
