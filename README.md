<img src="vulnpulse.png" alt="VulnPulse Logo" width="200" />

# ELK-CVE-Fetcher
Fetches CVE's &amp; parse it into Elasticsearch with the `HTTP Endpoint Logs (custom)` integration & Elastic Agent.

## How To
1. create a new ingest pipeline `cisa_vulns_pipeline` (Dev-Tools -> paste -> fire)
2. Install the Elastic agent & add the integration `HTTP Endpoint Logs (custom)`
  - Kibana -> Fleet -> Policies
  - Add integration
  - HTTP Endpoint Logs (custom)
  - Settings:
    - Name: cisa-vulns-ingest
    - Host: localhost
    - Port: 8088
    - Pipeline: cisa_vulns_pipeline
3. copy the python script to your linux server & create the cronjob
  - set the environment variable `AGENT_ENDPOINT`, if not, second parameter is used `http://localhost:8088`

## Cronjob
```bash
0 */3 * * * /usr/bin/python3 /pfad/zu/fetch_cisa_vulns.py >> /var/log/cisa_vulns.log 2>&1
```
