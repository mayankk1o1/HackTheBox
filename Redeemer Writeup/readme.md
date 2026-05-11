# Overview

Redeemer is a beginner-friendly Linux machine on Hack The Box that focuses on Redis enumeration and interacting with exposed in-memory databases.

The machine started with a basic Nmap scan, which revealed that port `6379` was open and running a Redis service.

Since Redis was exposed, the next step was to interact with the service using `redis-cli`.

Install the Redis client tools using this command:

```bash
sudo apt install redis-tools
```

After installation, connect to the Redis server with:

```bash
redis-cli -h <IP>
```


Once connected successfully, Redis returned an interactive shell where enumeration could begin.

A useful command for gathering information about the Redis server is:

```bash
info
```

This revealed details about the Redis instance, including the available databases and keyspace information.

The database was selected using:

```bash
select 0
```

Next, all keys stored inside the database were enumerated using:

```bash
keys *
```


A key containing the flag was discovered. The value associated with the key was retrieved using:

```bash
get <key>
```


The flag was successfully extracted directly from the Redis database.

This machine demonstrates a common real-world security issue where Redis services are exposed without authentication, allowing attackers to enumerate databases and retrieve sensitive information remotely.

---

## Key Learnings

- Performing Redis enumeration with Nmap
- Understanding Redis databases and key-value storage
- Installing and using `redis-cli`
- Enumerating Redis databases and keys
- Retrieving values from Redis databases
- Identifying insecure Redis configurations
- Understanding risks of exposed Redis services

---

## Skills Practiced

- Redis Enumeration
- Linux Service Reconnaissance
- Database Enumeration
- Key-Value Database Interaction
- Information Disclosure Exploitation
- Basic Penetration Testing Methodology
