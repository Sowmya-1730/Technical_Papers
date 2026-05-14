# CAP Theorem in Distributed Databases

# Introduction

CAP Theorem is one of the most important concepts in distributed database systems.

It explains the trade-offs between:

* Consistency
* Availability
* Partition Tolerance

The theorem states:

"A distributed system can guarantee only two out of the following three properties at the same time:"

1. Consistency (C)
2. Availability (A)
3. Partition Tolerance (P)


# What is a Distributed System?

A distributed system is a collection of multiple computers (nodes) working together as a single system.

Examples:

* Cloud databases
* Banking systems
* Social media platforms
* Distributed storage systems

Popular distributed databases:

* Cassandra
* MongoDB
* DynamoDB
* HBase
* CockroachDB


# The Three Properties of CAP Theorem

# 1. Consistency (C)

# Definition

Consistency means all nodes in the distributed system return the same latest data at the same time.

Every read operation receives:

* Most recent write
  OR
* An error

# Example

Suppose:

* User updates account balance to ₹5000 on Node A.

If another user reads from Node B immediately:

* Node B must also show ₹5000.

All nodes remain synchronized.

# Real-World Example

## Banking System

When money is transferred:

* Every ATM and banking server must show the same updated balance.

Strong consistency is extremely important.

# Advantages of Consistency

1. Accurate data
2. Reliable transactions
3. Prevents stale data
4. Important for financial systems

# Disadvantages of Consistency

1. Slower responses
2. Reduced availability during failures
3. More synchronization overhead

# 2. Availability (A)

# Definition

Availability means every request receives a response, even if some nodes fail.

The system should remain operational.

# Example

Suppose:

* One server crashes.

Users should still:

* Access the application
* Read data
* Write data

The system continues functioning.

# Real-World Example

## Social Media Platforms

Applications like:

* Facebook
* Instagram
* Twitter

Prioritize availability.

Even during server failures:

* Users can still access services.

# Advantages of Availability

1. High uptime
2. Better user experience
3. Continuous service access
4. Important for large-scale systems

# Disadvantages of Availability

1. Temporary inconsistent data possible
2. Stale reads may occur

# 3. Partition Tolerance (P)

# Definition

Partition tolerance means the system continues operating even when communication between nodes is interrupted.

A network partition occurs when nodes cannot communicate due to network failures.

# Example

Suppose:

* Data center in one region loses network connection with another region.

The system should still:

* Continue operating
* Serve requests
* Avoid complete shutdown

# Why Partition Tolerance is Important

In distributed systems:

* Network failures are unavoidable
* Hardware failures happen
* Internet disruptions occur

Partition tolerance is essential for distributed databases.

# Real-World Example

## Cloud Systems

Cloud providers like:

* AWS
* Azure
* Google Cloud

Operate across multiple regions.

If one region disconnects:

* Other regions should continue working.
