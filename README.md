# Network Security Monitoring and Event Analysis Pipeline

## Overview
This project implements a network security monitoring pipeline that captures,
ingests, indexes, and analyzes network security telemetry. The system uses
Suricata to inspect live network traffic and generate structured protocol-level
events, which are centrally collected using Filebeat, indexed in Elasticsearch,
and analyzed through Kibana.

The project focuses on understanding how intrusion detection and security
monitoring pipelines operate in practice rather than on custom signature
development.

## Architecture
Network Traffic  
→ Suricata (Network Traffic Inspection)  
→ eve.json (Structured Security Events)  
→ Filebeat (Log Ingestion)  
→ Elasticsearch (Indexing & Search)  
→ Kibana (Analysis & Visualization)

A detailed architecture diagram is provided in the `architecture/` directory.

## What This Project Demonstrates
- Deployment of a network traffic inspection engine
- Centralized ingestion of security telemetry
- Indexing and querying of time-series security events
- Visualization and exploration of network activity

## Scope
This implementation focuses on protocol-level telemetry (DNS, flows, TLS) and
default detection capabilities. Custom rule authoring and advanced alert tuning
are considered future work.
