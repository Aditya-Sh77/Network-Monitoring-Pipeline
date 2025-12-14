# Setup Steps

## Environment
- Linux system (Ubuntu recommended)
- Docker and Docker Compose installed
- Suricata installed on host system
- Filebeat installed on host system

## High-Level Setup
1. Start Elasticsearch and Kibana using Docker Compose
2. Configure Suricata to monitor the primary network interface
3. Enable eve.json output for protocol-level events
4. Configure Filebeat to ingest Suricata logs
5. Verify data ingestion in Elasticsearch
6. Explore events using Kibana

## Verification
- Suricata generates events in `/var/log/suricata/eve.json`
- Filebeat indexes events into Elasticsearch
- Kibana displays events using the `filebeat-*` index pattern
