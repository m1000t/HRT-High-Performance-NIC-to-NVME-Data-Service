

# High-Performance Key-Value Append Service

A networked key–value storage service optimized for high-throughput data ingestion and append-heavy workloads.

This project is inspired by low-latency infrastructure systems used in high-frequency trading environments, where large volumes of data must be transferred from the network to disk with minimal overhead.

---

## 🚀 Overview

This system allows clients to create keys and append data to them over the network. Data is stored in an append-only log format and can be read back efficiently using offset-based reads.

The architecture is designed to be modular, allowing the networking and storage layers to be optimized independently.

---

## ✨ Features

* Create, read, append, and delete keys
* Append-only log storage model
* Offset-based reads
* Concurrent client support
* Crash-safe write headers (basic recovery)
* Benchmarking + load testing tools
* Modular networking + storage layers

---

## 🧠 Use Cases

* Market data ingestion
* Logging pipelines
* Telemetry storage
* Time-series data backends
* Event sourcing systems

---

## 🏗️ Architecture

```
Clients
   │
   ▼
Networking Layer (TCP / RPC)
   │
   ▼
Request Parser & Dispatcher
   │
   ▼
Key-Value Service Logic
   │
   ▼
Append-Only Storage Engine
   │
   ▼
Disk I/O Layer
   │
   ▼
Persistent Storage (NVMe / SSD)
```

---

## 📦 Storage Design

Data is stored using a log-structured layout.

Each append is written as:

```
[Header | Payload]
```

Header fields include:

* Key ID / Name
* Payload length
* Timestamp (optional)
* Checksum (optional)

This enables:

* Sequential disk writes
* Efficient appends
* Crash recovery via log scanning

---

## 🔌 API

### Create Key

```
CREATE <key>
```

### Append Data

```
APPEND <key> <data_length>
<data>
```

### Read Data

```
READ <key> <offset> <length>
```

### Delete Key

```
DELETE <key>
```

---

## ⚙️ Tech Stack

**Learner Version**

* Language: (Go / Rust / C++)
* Networking: TCP sockets
* Storage: POSIX file I/O
* Concurrency: Threads / async runtime

**Future Optimizations**

* DPDK for kernel-bypass networking
* SPDK for user-space NVMe I/O
* Zero-copy packet → disk pipelines

---

## 🧪 Benchmarking

Benchmark tool included to measure:

* Throughput (MB/s)
* Requests/sec
* p95 / p99 latency
* Performance vs payload size

Example:

```
Clients: 16
Payload: 4KB
Append Throughput: 820 MB/s
p95 Latency: 3.2 ms
```

---

## 📂 Project Structure

```
server/
  networking/
  protocol/
  storage/
  kv/
client/
bench/
docs/
```

---

## 🛠️ Getting Started

### 1. Clone repo

```
git clone https://github.com/<your-username>/kv-append-service.git
cd kv-append-service
```

### 2. Run server

```
make run-server
```

### 3. Run client

```
make run-client
```

---

## 🧭 Roadmap

* [ ] Basic KV append API
* [ ] Persistent log storage
* [ ] Recovery on restart
* [ ] Concurrent client handling
* [ ] Benchmark suite
* [ ] Write batching
* [ ] Zero-copy networking (future)
* [ ] NVMe direct I/O (future)

---

## 📚 Learning Goals

This project explores:

* Storage engine design
* Log-structured data layouts
* Networking protocols
* Concurrency control
* Crash recovery
* Systems performance optimization

---

## 📄 License

MIT License
