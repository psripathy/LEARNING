## 				**<u>General Items to know</u>**

**SQL Vs NoSQL Databases**

https://www.thorntech.com/sql-vs-nosql/

| SQL Database                                                 | NoSQL Database                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Great fit for transaction oriented systems/systems with structured data | Great fot for unstructured data                              |
| Used when you need **ACID** (Atomicity, Consistency, Isolation, Durability) compliance | Built with flexibility & Scalability in mind and follows **BASE** consistency model |
| **Atomicity** - Each transaction either succeeds completely or is fully rolled back. **Consistency**: data must be valid according to all defined rules. **Isolation**: Transactions are run concurrently, they do not contend with each other.   **Durability** - Once transaction has been committed, it is considered permanent, even in the event of system failure. | **Basic Availability**: While DB gaurantees availability of data, the DB may fail to. obtainthe requested data. **Soft state**: The state of DB can be chaning over time. Eventual **Consistency**: The DB will eventually become consistent |
| Can scale only vertically, meaning can add RAM, storage etc. | Can scale horizontally, meaning you can add more servers     |
| Data stored in a predefined schema                           | The data can be column stores, document-oriented, graph-based, or key-value pairs |
