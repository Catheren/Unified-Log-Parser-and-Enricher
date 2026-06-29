# Unified Log Parser and Enricher

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![MaxMind](https://img.shields.io/badge/MaxMind-GeoLite2-00A650)](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)

A Python log parsing and enrichment pipeline built in Jupyter — ingesting raw SSH auth logs, Nginx access logs, and firewall logs, normalizing them into a unified schema, and enriching each event with GeoIP country data. Output is structured JSON ready for ingestion into a SIEM or security analytics pipeline.

---

## What this demonstrates

| Skill | Implementation |
|---|---|
| Log parsing | Regex-based extraction from 3 different log formats |
| Log normalization | Unified schema across SSH, Nginx, and firewall log sources |
| GeoIP enrichment | MaxMind GeoLite2 database integration for country-level context |
| Security data engineering | Raw logs → structured JSON → enriched events pipeline |
| SOC/SIEM readiness | Output format designed for downstream analytics and ingestion |

---

## Pipeline

```
inputs/
  authlog.txt       SSH authentication logs
  nginx.txt         Nginx access logs
  firewall.txt      Firewall logs
        │
        ▼
Parse each source with format-specific regex
        │
        ▼
Normalize fields into unified schema
(timestamp, source_ip, event_type, user, status)
        │
        ▼
Enrich with GeoIP country data (MaxMind GeoLite2)
        │
        ▼
outputs/
  parsed_authlog.json
  parsed_nginx.json
  parsed_firewall.json
  combined_logs.json
  enriched_logs.json
```

---

## Sample enriched output

```json
{
  "timestamp": "2024-01-15T03:22:11",
  "source": "ssh",
  "event_type": "failed_login",
  "source_ip": "185.220.101.45",
  "user": "root",
  "status": "FAILED",
  "country": "Germany"
}
```

---

## Log sources supported

| Source | File | Fields extracted |
|---|---|---|
| SSH auth | `authlog.txt` | timestamp, user, source IP, status (accepted/failed) |
| Nginx access | `nginx.txt` | timestamp, source IP, method, path, status code, bytes |
| Firewall | `firewall.txt` | timestamp, source IP, destination IP, port, action |

---

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/Catheren/Unified-Log-Parser-and-Enricher.git
cd Unified-Log-Parser-and-Enricher
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Download MaxMind GeoLite2 database

Download the free GeoLite2 Country database from [MaxMind](https://dev.maxmind.com/geoip/geolite2-free-geolocation-data) (free account required) and place the `.mmdb` file in:

```
inputs/GeoLite2-Country/GeoLite2-Country.mmdb
```

### 4. Add your log files

Place your log files in `inputs/`:
```
inputs/authlog.txt
inputs/nginx.txt
inputs/firewall.txt
```

### 5. Run the notebook

```bash
jupyter notebook log_parser.ipynb
```

Run all cells — enriched output will be saved to `outputs/`.

---

## Repository structure

```
Unified-Log-Parser-and-Enricher/
  log_parser.ipynb          Parsing, normalization, and enrichment notebook
  inputs/
    authlog.txt             Sample SSH auth log
    nginx.txt               Sample Nginx access log
    firewall.txt            Sample firewall log
    GeoLite2-Country/       MaxMind GeoIP database (not committed)
  outputs/
    parsed_authlog.json
    parsed_nginx.json
    parsed_firewall.json
    combined_logs.json
    enriched_logs.json
  requirements.txt
```

---

## Dependencies

| Library | Purpose |
|---|---|
| `geoip2` | MaxMind GeoLite2 GeoIP lookups |
| `re` | Log format parsing via regex |
| `json` | Output formatting |

Install: `pip install geoip2`
