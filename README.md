# sb8200_exporter
A prometheus exporter for the Arris SB8200. The grabs the connection status page at http://192.168.100.1/ and pulls values from the table it provides in html.

# Run with docker
Make sure http://192.168.100.1/ is accessible.
```
docker run --restart unless-stopped --name arris-exporter -d -p9195:9195 jcwimer/arris-exporter:latest
```

# Scrape with prometheus
Add the following to your prometheus config
```
- job_name: 'arris'
  scrape_timeout: 60s
  static_configs:
    - targets: ['10.0.0.104:9195']
```
The scrape_timeout is needed because the SB8200 page loads very slowly (at least it does for me).

# Grafana
A grafana page is provided [here](grafana/sb8200-dashboard.json). Copy the json and import it in grafana.
