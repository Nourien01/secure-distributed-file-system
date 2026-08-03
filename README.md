# Secure Distributed File System

A secure distributed file system built with **Java RMI** as part of the **Distributed Systems Security** course

This project demonstrates how distributed systems can maintain consistency across replicated storage nodes while applying secure software engineering practices to defend against common Java RMI vulnerabilities.

---

## Project Overview

The system consists of three replicated storage nodes that allow authenticated clients to perform distributed file operations including:

- Upload
- Download
- Delete
- Rename
- Search
- List Files

To ensure consistency across replicas, all write operations are synchronized using **Totally Ordered Multicast (TO-Multicast)** with logical clocks. Read operations are served by a leader replica.

In addition to the distributed system implementation, the project includes a complete security hardening process to mitigate multiple attack vectors commonly affecting Java RMI applications.

---

## My Contribution

I contributed to the implementation of the distributed file system, with my primary responsibility focused on the **security engineering** aspects of the project. My work included:

- Implementing all required security fixes
- Securing Java RMI communication using Mutual TLS
- Preventing insecure object deserialization attacks
- Preventing remote codebase injection
- Implementing secure authentication and session management
- Developing replay attack protection using timestamps and nonces
- Testing the secured implementation against attack scenarios
- and actually finding all these vulnerabilities before fixing

---

## Features

- Three replicated storage nodes
- Java RMI-based communication
- User registration and authentication
- File upload, download, delete, rename, search, and listing
- Leader-based read operations
- Replicated write operations
- Totally Ordered Multicast (TO-Multicast)
- Logical clock synchronization
- Secure client-server and server-server communication

---

## Security Improvements

### 1. Insecure Object Deserialization (Remote Code Execution)

**Risk**

An attacker could send a malicious serialized object to execute arbitrary code on the server.

**Solution**

- Implemented whitelist-based object validation
- Allowed only trusted request classes during deserialization

---

### 2. Dynamic Class Loading (Remote Codebase Injection)

**Risk**

Java RMI could download malicious classes from external codebases.

**Solution**

- Disabled remote codebase loading
- Restricted class loading to local trusted classes only

---

### 3. Plaintext Communication

**Risk**

Network traffic could be intercepted or modified through Man-in-the-Middle attacks.

**Solution**

- Implemented Mutual TLS (mTLS)
- Secured both client-server and server-server communication
- Configured Java KeyStores (JKS)

---

### 4. Missing Authentication

**Risk**

Unauthorized users could access distributed file operations.

**Solution**

- User registration and login
- Salted SHA-256 password hashing
- Session token generation
- Session expiration

---

## Bonus Feature – Replay Attack Protection

To prevent replay attacks on write operations (Upload, Delete, Rename), each request includes:

- A unique nonce
- A timestamp

The server rejects requests when:

- The nonce has already been used
- The timestamp falls outside the allowed time window

This prevents attackers from replaying previously captured requests.

---

## Technologies Used

- Java
- Java RMI
- SSL/TLS
- Java KeyStore (JKS)
- SHA-256
- Distributed Systems
- Totally Ordered Multicast (TO-Multicast)
- Logical Clocks

---

## Project Structure

```
SecureDistributedFileSystem/
│
├── Vulnerable/
│   ├── Vulnerable Java RMI implementation
│   └── Demonstration of security vulnerabilities
│
├── Secured/
│   ├── Secure implementation
│   ├── Authentication
│   ├── TLS Configuration
│   ├── Replay Protection
│   └── Input Validation
│
├── Report/
│   └── Technical Report
│
└── README.md
```

---

## Learning Outcomes

Through this project, I gained practical experience in:

- Secure Java RMI development
- Distributed system design
- Secure serialization
- Mutual TLS configuration
- Authentication and session management
- Replay attack mitigation
- Distributed consistency using Totally Ordered Multicast
- Secure software engineering principles

---

\

## Team

- **Nourien Mohammed**
- **Saifeldin Sherif**

---

## Academic Context

This project was developed for the **Distributed Systems Security** course.
