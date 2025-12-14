# Suricata Configuration Notes

Suricata is used as a network traffic inspection and decoding engine. It captures
live network traffic and generates structured protocol-level events rather than
raw packet dumps.

## Event Types Observed
- DNS events (queries and responses)
- Network flow records
- TLS handshake metadata
- Statistics and counters

These events are written in JSON format to `eve.json`, which allows downstream
systems to ingest and analyze them efficiently.

## Role in the Pipeline
Suricata provides the raw security telemetry that forms the foundation of the
monitoring pipeline. Detection and analysis are performed downstream using
indexed event data.
