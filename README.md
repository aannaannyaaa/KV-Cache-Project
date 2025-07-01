# Key-Value Cache Project

A fast, lightweight, in-memory key-value store with a straightforward HTTP API, developed using Rust for high efficiency.

## Setup

### Requirements
- Rust version 1.70 or above
- Cargo package manager

### Building from Source
```bash
# Download the repository
git clone https://github.com/aannaannyaaa/KV-Cache-Project
cd KV-Cache-Project

# Compile the project
cargo build --release

# Run the server
./target/release/key_value_cache
```

### Install via Cargo
```bash
# Install directly using cargo
cargo install --git https://github.com/Rushhaabhhh/Key-Value-Cache.git

# Run the server
key_value_cache
```

### Running with Docker
```bash
# Build the Docker image
docker build -t key-value-cache .

# Run the Docker container
docker run -p 7171:7171 key-value-cache
```

## Configuration Settings

Default parameters can be adjusted by adding a `.env` file in the root directory:

```
PORT=7171
MAX_KEY_SIZE=256
MAX_VALUE_SIZE=256
```

## API Endpoints

### Store a Value
```
POST /put
```
Request body example:
```json
{
  "key": "user:1234",
  "value": "John Doe"
}
```
Success response:
```json
{
  "status": "OK",
  "message": "Key successfully inserted or updated."
}
```

### Retrieve Entry
```
GET /get?key=user:1234
```
If found, response example:
```json
{
  "status": "OK",
  "key": "user:1234",
  "value": "John Doe",
  "message": "Key retrieved successfully."
}
```
If not found:
```json
{
  "status": "ERROR",
  "message": "Key not found."
}
```

## Architecture and Optimizations

### Efficient Memory Handling
- Employs an LRU cache using Rust's `LinkedHashMap` to track usage and evict the least recently used entries.
- Monitors system memory continuously, triggering eviction when usage hits 70% capacity.
- Uses a progressive eviction approach that increases eviction batch sizes gradually, preserving responsiveness.

### Enhancing Performance
- Built on Tokio's async runtime to handle multiple simultaneous requests efficiently.
- Thread-safe through Rust’s `Arc<RwLock<>>` for concurrent cache operations.
- Limits key and value sizes to maintain stable performance and prevent abuse.

### Increasing Reliability
- Supports graceful termination to avoid data loss on shutdown.
- Provides consistent and clear error responses through Rust’s error handling.
- Monitors resources actively to adapt to workload changes dynamically.

### Scalability
- Designed as a stateless application (outside of cache data) to easily scale horizontally behind a load balancer.
- Optimized for minimal memory usage, suited for deployment in environments with limited resources.

## Performance Highlights

This service delivers exceptional speed:
- Supports over 50,000 requests per second on typical hardware.
- 95th percentile response times below 5 milliseconds.
- Zero failing requests under heavy concurrent load (100+ users).

### Key Metrics:

- **Throughput:** 51,455 requests/second
- **Latency:** 95% of requests completed in under 3.14ms
- **Reliability:** No failures in nearly 17 million requests
- **Cache Efficiency:** Achieved 100% effective cache hits with over 8 million hits
- **Concurrency:** Maintained stability with 100 simultaneous virtual users

***

Would you like the text adjusted to be more formal or casual?