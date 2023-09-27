---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/system-design/system-design/","tags":["SDE/System-Design"],"noteIcon":"1"}
---


# System Design 系统设计
  
## Computer Architecture

- Serves as basic building blocks of a system
- CPU (and cache): fast, expensive, cannot be scaled too much
- RAM
- Disk (HDD/SSD)

## Application Architecture

- Dev -> build & deploy -> server -> storage
- Other services:
	- Logging
	- Metrics
	- Alerts
- Scaling:
	- **Vertical scaling**: scale one server to be more powerful (has limitations due to CPU)
	- **Horizontal scaling**:
		- Multiple servers to handle more requests at the same time
		- Load balancer: forward the request to one of the servers 

## Design Requirements

### Move Data

### Store Data

### Transform Data

### Measurement of a good design

- `Availability = uptime / (uptime + downtime)`
- SLO (service level objective)
- SLA (service level agreement)
- **Reliability**: Probability that the system won't fail
- **Fault Tolerance**
- **Redundancy** 
- **Throughput**: the amount of sth. Over some period of time
	- Requests/sec (for server)
	- Queries/sec (for DB)
	- Bytes/sec
- **Latency**: time for the individual operation to be completed

## Networking

### IP address

- Public / Private
- Static / Dynamic

### Packets

- IP packet: IP header + TCP header + Application data

### Ports

### TCP and UDP (Internet Protocol Suite)

- TCP/IP
	- Reliable: retransmission
	- 3-way handshake (establish connection)
- UDP: low overhead but not reliable (could be used for video streaming)

### DNS (Domain Name System)

- Domain Name -> IP address

## APIs

### HTTP

- Request & response
- Receive single response each time

### WebSockets

- filling the gap in HTTP Protocol, can be used to send and receive messages on both sides multiple times after establishing a connection, e.g. live chats

### API Paradigms

- REST (Representation State Transfer)
	- Stateless: server doesn't need to store the users' states
	- Stateless is important when we have more than 1 server
	- Format: JSON (JavaScript Object Notation)
- GraphQL
	- Resolve over fetching, multiple requests
	- GraphQL specifies each field of resource, groups requests into a single request
	- Single Endpoint: Query, Mutation
	- Based on HTTP POST, cannot be cached like REST
- GRPC
	- Cannot be used on a browser directly, usually used for server-server communication
	- Faster performance, sending protocol buffers instead of JSON

### API Design

- CRUD (create, update, delete)
- Backward compatible -> use versions: new API will not break old versions
- Pagination: not return all large number of data
	- Limit
	- Offset

## Caching Basics

### Caching

- Low latency, high throughput, low network cost
- Write-around cache: put in cache when resources being read
- Write-through cache: put in cache when resources being created
- Write-back cache
	- Faster but not reliable
	- Ignore disk when creating a resource, then periodically copy to disk
- E.g. use memory as cache for disk (e.g. Redis)

### Eviction Policy

- Which cache we need to replace when cache is full?
	- FIFO (first in first out)
	- LRU (least recently used)
	- LFU (least frequently used)

### CDN (Content Delivery Network)

- Can only put static content
- Users don't need to access the original server every time

## Proxies

### Proxies and Load Balancing

- Forward Proxy: hide the client
- Reverse Proxy: hide the server, e.g. CDN, load balancer
- Load Balancer strategies
	- Round Robin
	- Least number of connections
	- User Location
	- Hashing
- Load balancer layer
	- Layer 4 (TCP): based on IP, faster
	- Layer 7: based on application, flexible 

### Consistent Hashing

- The objective is to make users still go to their still-alive original assigned servers when some of the servers go down, so that we can still make use of the cache

## Storage

### SQL (Standard Query Language, relational)

- Data Structure: B+ Tree
- Index: the key attribute we want to search for
- Primary key: uniquely identify each record (row)
- Foreign key: a key value has constraints that all values exists in another table's key values
- Transaction: a query or a collection of queries (from `begin` to `commit`)
- ACID
	- Atomicity: in a transaction, either all queries committed or none
	- Consistency: follow constraints
	- Isolation: concurrent transactions appear to happen in order
	- Durability: e.g. data store on disk
- Hard to scale horizontally (distributed)

### NoSQL (Not Only SQL, non-relational)

- Main objective: scale up
- Types of NoSQL
	- `key-value`: like Redis, mainly used for cache
	- `document store`: collection document, like JSON. Flexible, not constraints
	- `wide column`: good for a lot of writes, Cassandra
	- `GraphDB`: complex relations
- Tradeoffs: eventual consistency, not ACID, but more read scalability

### Replication

- Scale up reads
- Leader-Follower
- Sync vs async

### Sharding

- Break individual databases into multiple pieces
- shard key: e.g. range based shard key
- Consistent sharding: hashing
- SQL will lose ACID, more suitable for NoSQL

### CAP Theorem

- Consistency: each read will read the up-to-date data
- Availability
- Partition Tolerance: network partition between the nodes will not prevent the system from functioning
- PACELC:
	- Given P, choose A or C, Else, favor Latency or Consistency

### Object Storage

- Former: BLOB (Binary Large Object)
- Storing Images and Videos in DB does not make sense, use object storage

## Big Data

### Message Queues

- E.g. RabbitMQ, Kafka, GCP, etc.

### MapReduce

## How to Approach

### Scoping with interviewer

- Functional or Non-Functional (scalability/Storage Capacity/Throughput/Latency)

## Examples

- [[1 P(Projects)/SDE Interview Prep/System Design/Chat APP System Design\|Chat APP System Design]]
- 