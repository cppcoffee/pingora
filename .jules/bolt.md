## 2025-02-19 - Redundant Reuse Hash Calculation
**Learning:** `Peer::reuse_hash()` was being called multiple times (2-3x) during connection establishment (in `new_stream`, `get_stream`, and `new_http_session`). This involves hashing multiple fields including strings.
**Action:** When implementing or modifying connector logic, calculate the hash once and pass it down using `*_with_hash` helper methods. This reduces CPU usage during high connection churn.
