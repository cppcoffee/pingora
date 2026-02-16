## 2024-03-24 - [Avoid Redundant Hash Calculation in Connectors]
**Learning:** `TransportConnector::new_stream` and `reused_stream` call `peer.reuse_hash()` repeatedly. In high-throughput scenarios, especially with complex `Peer` implementations (e.g., `HttpPeer` hashing multiple strings), this adds measurable overhead.
**Action:** Pass the calculated hash down the call stack instead of recomputing it. Use `*_with_hash` internal helpers.
