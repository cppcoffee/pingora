## 2024-05-22 - Global Lock Contention in TransportConnector
**Learning:** `TransportConnector` uses a global `RwLock<HashMap>` for `PreferredHttpVersion` which is accessed on every new stream creation. This creates contention under high concurrency.
**Action:** Shard such structures (e.g., using `[RwLock<HashMap>; N]`) to reduce contention, as done in `pingora-pool`.
