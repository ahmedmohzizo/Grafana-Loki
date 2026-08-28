# Grafana Loki Log-Monitoring Lab

## Overview

This project documents a Linux log-monitoring lab using Grafana Loki for log storage and querying and Grafana for visualization. Loki indexes metadata labels while storing compressed log content, which makes it well suited to centralized operational and security logging.

## Learning Objectives

- Understand label-based log indexing
- Collect Linux logs in a central location
- Connect Loki as a Grafana data source
- Query logs with LogQL
- Use dashboards and logs to support troubleshooting and security analysis

## Components

- **Grafana Loki:** Stores and queries logs
- **Grafana:** Visualizes log data and supports investigation workflows
- **Grafana Alloy:** Current Grafana-recommended collector for sending logs to Loki
- **LogQL:** Loki's query language

## Recommended Setup

Grafana's installation methods and collector recommendations change over time. Use the current official documentation instead of copying version-specific download commands:

- [Install Grafana Loki](https://grafana.com/docs/loki/latest/setup/install/)
- [Run the official local quickstart](https://grafana.com/docs/loki/latest/get-started/quick-start/quick-start/)
- [Configure the Loki data source in Grafana](https://grafana.com/docs/grafana/latest/datasources/loki/configure/)

For a local demonstration, the official Docker Compose quickstart is the most reproducible starting point.

## Example LogQL Query

```logql
{job="varlogs"}
```

Use labels with low and predictable cardinality. Avoid placing highly variable values, such as request IDs or timestamps, in labels.

## Security Notes

- Loki does not include an authentication layer by default. Protect non-local deployments with authentication, TLS, network controls, and an appropriate reverse proxy.
- Do not expose port `3100` directly to the public internet.
- Avoid collecting secrets, credentials, or unnecessary personal data in logs.
- Treat this repository as a lab guide; production deployments require durable storage, retention policies, backups, and access controls.

