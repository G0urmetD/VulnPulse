![](vulnpulse.png)
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
    - Host: 0.0.0.0 (127.0.0.1 would only listen on local)
    - Port: 8088
    - Pipeline: cisa_vulns_pipeline
3. copy the python script to your linux server & create the cronjob

## Cronjob
```bash
0 */3 * * * /usr/bin/python3 /pfad/zu/fetch_cisa_vulns.py >> /var/log/cisa_vulns.log 2>&1
```
