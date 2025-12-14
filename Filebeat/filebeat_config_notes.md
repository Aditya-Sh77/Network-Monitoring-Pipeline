
# Filebeat Configuration Notes

Filebeat is used as a lightweight log ingestion service. It continuously reads
Suricata's `eve.json` output and forwards structured events to Elasticsearch.

## Why Filebeat
- Handles large, continuously growing log files efficiently
- Provides reliability and backpressure handling
- Decouples traffic inspection from storage and analysis

## Role in the Pipeline
Filebeat acts as the transport layer between Suricata and Elasticsearch,
ensuring that decoded security events are centrally available for querying and
visualization.
