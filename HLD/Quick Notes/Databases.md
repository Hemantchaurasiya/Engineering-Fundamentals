## Introduction to Databases

Databases are organized collections of data that can be easily accessed, managed, and updated. They are essential for storing and retrieving structured or unstructured information in various domains, including web applications, enterprise software, and mobile applications. Databases ensure data consistency, integrity, and security while supporting multiple concurrent users.

---

## SQL Databases

SQL (Structured Query Language) databases are relational databases that use tables to store data. Each table has rows and columns, with a fixed schema that defines the structure of the data. Popular SQL databases include:

- MySQL
- PostgreSQL
- Microsoft SQL Server
- Oracle Database

Key Features:

- Strong schema and data validation
- Support for complex queries and transactions
- ACID (Atomicity, Consistency, Isolation, Durability) compliance

---

## NoSQL Databases

NoSQL databases are non-relational and are designed for unstructured, semi-structured, or schema-less data. They are scalable and flexible, making them suitable for modern applications like real-time analytics and big data processing. Types of NoSQL databases include:

- Document stores (e.g., MongoDB, Couchbase)
- Key-value stores (e.g., Redis, DynamoDB)
- Column-family stores (e.g., Apache Cassandra, HBase)
- Graph databases (e.g., Neo4j, ArangoDB)

Key Features:

- Schema-less design
- High scalability and performance
- BASE (Basically Available, Soft state, Eventual consistency) model

---

## SQL vs. NoSQL

| Feature        | SQL Databases         | NoSQL Databases          |
| -------------- | --------------------- | ------------------------ |
| Data Model     | Relational (tables)   | Non-relational (varied)  |
| Schema         | Fixed                 | Dynamic or schema-less   |
| Query Language | SQL                   | APIs or custom languages |
| Scalability    | Vertical scaling      | Horizontal scaling       |
| Use Cases      | Transactional systems | Big data, real-time apps |

---

## ACID vs BASE Properties

### ACID Properties (SQL):

- Atomicity: Transactions are all-or-nothing.
- Consistency: Data remains in a valid state.
- Isolation: Concurrent transactions don’t interfere.
- Durability: Completed transactions persist.

### BASE Properties (NoSQL):

- Basically Available: Guarantees availability.
- Soft State: Data may change over time.
- Eventual Consistency: Data becomes consistent eventually.

---

## Real-World Examples and Case Studies

### SQL Use Cases:

- Banking systems (e.g., transactions)
- Inventory management systems

### NoSQL Use Cases:

- Social media platforms (e.g., Facebook, Instagram)
- Real-time analytics and IoT applications

Case Study:

- Netflix: Uses Cassandra (NoSQL) for scalability and high availability.
- Banking Systems: Use Oracle Database (SQL) for transactional integrity.

---

## SQL Normalization and Denormalization

### Normalization:

- Process of organizing data to minimize redundancy and improve integrity.
- Normal forms (1NF, 2NF, 3NF, etc.) define the levels of normalization.

### Denormalization:

- Combines tables to reduce join operations, improving read performance at the cost of redundancy.

---

## In-Memory Database vs. On-Disk Database

### In-Memory Database:

- Stores data in RAM for ultra-fast access.
- Examples: Redis, Memcached

### On-Disk Database:

- Stores data on physical disk with slower access speeds but larger storage capacity.
- Examples: MySQL, PostgreSQL

| Aspect      | In-Memory          | On-Disk           |
| ----------- | ------------------ | ----------------- |
| Speed       | Very fast          | Moderate to slow  |
| Persistence | Volatile           | Persistent        |
| Use Cases   | Caching, real-time | Long-term storage |

---

## Data Replication vs. Data Mirroring

### Data Replication:

- Copies data across multiple databases or nodes.
- Ensures high availability and fault tolerance.

### Data Mirroring:

- Maintains identical copies of a database in real-time.
- Used for disaster recovery and high availability.

| Feature     | Replication          | Mirroring      |
| ----------- | -------------------- | -------------- |
| Flexibility | Multiple copies      | Identical copy |
| Latency     | Eventual consistency | Near-instant   |

---

## Database Federation

Database federation integrates multiple autonomous databases into a single system. Users can query and access data from multiple sources as if they were a single database.

Benefits:

- Unified access to distributed data
- Scalability and flexibility
- Avoids data duplication

Examples:

- Federated queries in AWS Redshift
- Google’s BigQuery federation support

