
# Network Security Monitoring Pipeline – Detailed Diagram

Below is a **detailed, end-to-end pipeline diagram** describing how data flows through the system. This diagram is written in Markdown so it can live directly in the repository and be rendered by GitHub.

---

## High-Level Flow

```
┌──────────────────────────┐
│      Network Traffic     │
│ (User activity, DNS,     │
│  TCP/UDP flows, TLS)     │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│        Suricata          │
│  Network Traffic Engine  │
│                          │
│ • Packet capture         │
│ • Protocol decoding      │
│ • Flow tracking          │
│ • Telemetry generation   │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│   eve.json (JSON Events) │
│                          │
│ • DNS events             │
│ • Flow records           │
│ • TLS metadata           │
│ • Statistics             │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│        Filebeat          │
│   Log Ingestion Agent    │
│                          │
│ • Tails eve.json         │
│ • Parses JSON events     │
│ • Normalizes fields      │
│ • Forwards events        │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│      Elasticsearch       │
│  Search & Index Engine   │
│                          │
│ • Stores events as docs  │
│ • Indexes by time/type   │
│ • Enables fast queries   │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│          Kibana          │
│  Analysis & Visualization│
│                          │
│ • Discover views         │
│ • Filters & queries      │
│ • Dashboards             │
└──────────────────────────┘
```

---

## Layer-by-Layer Explanation

### 1. Network Traffic (Input Layer)

This represents all live network activity on the monitored interface:

* DNS queries and responses
* TCP/UDP connections
* TLS handshakes
* General packet flows

This is **raw input** and contains no structure or interpretation.

---

### 2. Suricata – Network Traffic Inspection

Suricata operates at the network layer and performs:

* Packet capture from the network interface
* Protocol decoding (DNS, HTTP, TLS, etc.)
* Flow and session tracking
* Generation of structured telemetry

Suricata **does not store data long-term**. It converts packets into structured events.

---

### 3. eve.json – Structured Event Output

Suricata writes decoded events into a single JSON log file:

```
/var/log/suricata/eve.json
```

Each line is a JSON document describing one event, such as:

* A DNS query
* A network flow
* A TLS handshake

This file acts as the **handoff point** between detection and analysis.

---

### 4. Filebeat – Log Ingestion Layer

Filebeat continuously monitors `eve.json` and:

* Reads new events as they are written
* Parses JSON fields
* Adds metadata (timestamps, host info)
* Reliably ships events downstream

This layer **decouples traffic inspection from storage**, making the pipeline robust.

---

### 5. Elasticsearch – Storage & Search Layer

Elasticsearch receives events from Filebeat and:

* Stores each event as a document
* Indexes fields such as time, protocol, source IP
* Enables fast time-based and field-based queries

This layer is optimized for **high-volume, time-series security data**.

---

### 6. Kibana – Analysis & Visualization Layer

Kibana provides the human-facing interface:

* Explore events in Discover
* Filter by protocol, time range, fields
* Build dashboards for trends and visibility

Kibana **does not collect or store data**. It only queries Elasticsearch.

---

## Summary


## Data Flow Description
- Suricata decodes live traffic and emits structured protocol events
- Filebeat continuously reads Suricata event logs
- Elasticsearch indexes events for fast querying
- Kibana provides an interface for analysis and visualization


This pipeline demonstrates how raw network traffic is transformed into structured, searchable, and analyzable security telemetry using a modular, industry-relevant architecture.

Each component has a single responsibility, and together they form a complete network security monitoring system.
