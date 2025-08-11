
# OpenSearch Docker Compose

This project provides a Docker Compose setup for running an OpenSearch stack, including OpenSearch, OpenSearch Dashboards, and Logstash.

## Services

### 1. OpenSearch
- **Image:** `opensearchproject/opensearch:3.1.0`
- **Ports:** 9200 (REST API), 9600 (Performance Analyzer)
- **Environment:**
	- Runs as a single node
	- Security plugin disabled
	- Java heap size: 512MB
	- Initial admin password: `gKL-TVxTv3e`
- **Data Persistence:** Uses a Docker volume `opensearch-data` for data storage

### 2. Logstash
- **Image:** `opensearchproject/logstash-oss-with-opensearch-output-plugin:latest`
- **Ports:**
	- 5044: TCP input
	- 5045: HTTP input
	- 9601: Monitoring API
- **Pipeline Config:** Mounts `logstash.conf` from the project directory
- **Depends on:** OpenSearch

### 3. OpenSearch Dashboards
- **Image:** `opensearchproject/opensearch-dashboards:3.0.0`
- **Port:** 5601 (Web UI)
- **Environment:**
	- Connects to OpenSearch at `http://admin:admin@opensearch:9200`
- **Depends on:** OpenSearch

## Usage

1. **Clone this repository**
2. **Start the stack:**
	 ```sh
	 docker-compose up -d
	 ```
3. **Access the services:**
	 - OpenSearch API: [http://localhost:9200](http://localhost:9200)
	 - OpenSearch Dashboards: [http://localhost:5601](http://localhost:5601)
	 - Logstash TCP input: `localhost:5044`
	 - Logstash HTTP input: `localhost:5045`

4. **Stop the stack:**
	 ```sh
	 docker-compose down
	 ```

## Files

- `docker-compose.yml`: Main Docker Compose file
- `logstash.conf`: Logstash pipeline configuration

## Notes
- Default OpenSearch admin password is set to `gKL-TVxTv3e` (change for production!)
- Data is persisted in the `opensearch-data` Docker volume
- All services are connected via the `opensearch-net` Docker network

---
For more information, see the [OpenSearch documentation](https://opensearch.org/docs/).
