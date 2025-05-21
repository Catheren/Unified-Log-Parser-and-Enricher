# Unified-Log-Parser-and-Enricher
A Python tool to parse, normalize, and enrich logs from multiple sources — SSH authentication logs, Nginx access logs, and firewall logs — outputting structured JSON enriched with GeoIP country data.

---

## 🚀 Features

- 🔍 Parses different log formats with regex:
  - SSH auth logs (`- .txt`)
  - Nginx access logs (`nginx.txt`)
  - Firewall logs (`firewall.txt`)
- 🔄 Normalizes fields across log types for consistent analysis
- 🌍 Enriches logs with GeoIP country information using MaxMind GeoLite2 database
- 📦 Outputs parsed and enriched logs as JSON files for downstream use
- 🧩 Modular functions for easy extension to other log types or enrichments

---

## 📁 Project Structure

- `inputs/` - Place your raw log files here
- `outputs/` - Parsed, normalized, and enriched JSON files will be saved here
- `main.py` - Main parsing and enrichment script
- `requirements.txt` - Python dependencies (e.g. `geoip2`)

---

## ⚙️ Setup and Usage

### 1. Clone the repo

```bash
git clone https://github.com/yourusername/unified-log-parser.git
cd unified-log-parser
```

### 2. Install dependencies
```
pip install -r requirements.txt
```
### 3. Prepare inputs
Place your log files in the inputs/ folder:

- authlog.txt — SSH authentication logs

- nginx.txt — Nginx access logs

- firewall.txt — Firewall logs

Also download the MaxMind GeoLite2 Country database and place the .mmdb file in inputs/GeoLite2-Country/.
### 4. Run the script
```
python main.py
```
### 5. View outputs
Parsed and enriched logs will be saved as JSON files in the outputs/ folder:

- parsed_authlog.json

- parsed_nginx.json

- parsed_firewall.json

- combined_logs.json

- enriched_logs.json

### This Project Demonstrates:
- Python scripting for security log parsing

- Regular expressions to extract structured data

- Log normalization across disparate sources

- Integration with GeoIP databases for threat context enrichment

- JSON output for security analytics pipelines
