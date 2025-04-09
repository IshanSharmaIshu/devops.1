# devops-assignment
This is for Assignment Task

## Instructions for Deploying the Setup using CI/CD Pipeline

1. Ensure you have Docker and Docker Compose installed on your machine.
2. Clone the repository to your local machine.
3. Navigate to the directory containing the `docker-compose.yml` file.
4. Run the following command to start the services:
   ```sh
   docker-compose up -d
   ```
5. Access Grafana by navigating to `http://localhost:3000` in your web browser.
6. Log in with the default credentials (username: `admin`, password: `admin`).
7. Configure your data sources and dashboards as needed.

## Information about the Filters for Log Visualization

The setup includes the following filters for log visualization:

- `observed_timestamp_rfc3339`: The timestamp when the log was observed, in RFC3339 format.
- `instrumentation_scope`: The scope of the instrumentation that generated the log.
- `severity_text`: The severity level of the log message.

These filters are configured in the following files:

- `promtail/config.yml`: Configures Promtail to send logs to Loki with the specified filters.
- `grafana/provisioning/datasources/datasource.yml`: Configures Grafana to use Loki as a data source with the specified filters.
