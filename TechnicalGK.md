## **SQL Vs NoSQL Databases**

https://www.thorntech.com/sql-vs-nosql/

| SQL Database                                                 | NoSQL Database                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Great fit for transaction oriented systems/systems with structured data | Great fot for unstructured data                              |
| Used when you need **ACID** (Atomicity, Consistency, Isolation, Durability) compliance | Built with flexibility & Scalability in mind and follows **BASE** consistency model |
| **Atomicity** - Each transaction either succeeds completely or is fully rolled back. **Consistency**: data must be valid according to all defined rules. **Isolation**: Transactions are run concurrently, they do not contend with each other.   **Durability** - Once transaction has been committed, it is considered permanent, even in the event of system failure. | **Basic Availability**: While DB gaurantees availability of data, the DB may fail to obtain the requested data. **Soft state**: The state of DB can be chaning over time. Eventual **Consistency**: The DB will eventually become consistent |
| Can scale only vertically, meaning can add RAM, storage etc. | Can scale horizontally, meaning you can add more servers     |
| Data stored in a predefined schema                           | The data can be column stores, document-oriented, graph-based, or key-value pairs |


**NoSQL Databases**

***Mongo DB Vs Cassandra/DynamoDB***
- 1 master, multiple slave **Vs** Multiple master/slave configuration - because of this reason write performance of Cassandra is better
- Write requests goes only to master, hence less scalable for write operation **Vs** Multiple master node makes writing more scalable
- Possibility of downtime (20-30 secs) when the master goes down until the slave becomes master **Vs** because of multiple master it is highly available
- Availability of Secondary Index makes querying faster **Vs** Only cursory support for secondary index
- Suuports BSON, JSON data format **Vs** JSON only
- Supports unstructured/nested data **Vs** Data still stored in rows/cols (just not relational)
- Both support Sharding/Horizontal Partitioning


## XMPP Vs WSS
https://www.cometchat.com/blog/xmpp-vs-websockets-instant-messaging-protocol-comparison#:~:text=XMPP%20only%20allows%20you%20to,I%20should%20be%20using%20WebSocket.%22

Both creates persistent connection between client and server.

***XMPP*** Extensible Messaging and Presence Protocol
Each client has has unique Jabber ID user@domain.com/resource
***WSS*** Web Socket Secured protocol
