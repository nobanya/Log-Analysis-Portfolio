#  Intro To Log Analysis Using ELK Stack (Elasticsearch, Logstash, Kibana)

## Introduction
This project introduces hands on log analysis using the ELK Stack, a widely adopted open-source platform for collecting, storing, and visualizing log data. The stack is composed of Elasticsearch for data indexing and search, Logstash for data ingestion and processing, and Kibana for data exploration and visualization. By completing this project, learners will deploy the ELK Stack, ingest log files, and build visual dashboards to analyze log activity.

## Requirements
- Basic familiarity with log files and logging concepts
- Comfort working in the Linux command line
- A Linux system (Ubuntu 20.04 or newer recommended)
- Java installed on the system

## Lab Environment and Tools
- Ubuntu 20.04 or later
- [Elasticsearch](https://www.elastic.co/downloads/elasticsearch) installed
- [Logstash](https://www.elastic.co/downloads/logstash) installed
- [Kibana](https://www.elastic.co/downloads/kibana) installed
- Sample log files for ingestion

## Exercises

### Exercise 1: Installing Elasticsearch

**Steps**:

1. Download and install Elasticsearch:
    ```bash
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.12.1-amd64.deb
    sudo dpkg -i elasticsearch-7.12.1-amd64.deb
    ```
2. Start & enable the Elasticsearch service:
    ```bash
    sudo systemctl start elasticsearch
    sudo systemctl enable elasticsearch
    ```
3. Confirm Elasticsearch is operational by opening "http://localhost:9200" in a web browser.

**Expected Output**: Elasticsearch is successfully running and reachable at "http://localhost:9200".

___

### Exercise 2: Installing & Configuring Logstash

**Steps:**

1. Download and install Logstash:
    ```bash
    wget https://artifacts.elastic.co/downloads/logstash/logstash-7.12.1.deb
    sudo dpkg -i logstash-7.12.1.deb
    ```
2.  Create a logstash configuration file (`logstash-simple.conf`):
    ```bash
    sudo nano /etc/logstash/conf.d/logstash-simple.conf
    ```
    Add the following configuration:
    ```plaintext
    input {
      file {
        path => "/path/to/your/logfile.log"
        start_position => "beginning"
      }
    }
    output {
      elasticsearch {
        hosts => ["localhost:9200"]
      }
      stdout { codec => rubydebug }
    }
    ```
3. Start & enable the Logstash service:
    ```bash
    sudo systemctl start logstash
    sudo systemctl enable logstash
    ```

**Expected Output**: Logstash is configured to read log files and forward data to Elasticsearch.

---

### Exercise 3: Installing Kibana

**Steps:**

1. Download and install Kibana:
    ```bash
    wget https://artifacts.elastic.co/downloads/kibana/kibana-7.12.1-amd64.deb
    sudo dpkg -i kibana-7.12.1-amd64.deb
    ```
2. Start & enable the Kibana service:
    ```bash
    sudo systemctl start kibana
    sudo systemctl enable kibana
    ```
3. Verify Kibana is accesible at`http://localhost:5601` in a web browser.

**Expected Output**: Kibana is running, & accessible at `http://localhost:5601`.

---

### Exercise 4: Ingesting Logs with Logstash

**Steps:**

1. Confirm the log file referenced in 'logstash-simple.conf' exists and contains sample data.
2. Monitor Logstash logs to verify ingestion:
    ```bash
    sudo tail -f /var/log/logstash/logstash-plain.log
    ```
3. Validate that indices are being created in Elasticsearch by accessing the Elasticsearch API:
    ```bash
    curl -X GET "localhost:9200/_cat/indices?v"
    ```

**Expected Output**: Log data is successfully ingested and indexed in Elasticsearch.

---

### Exercise 5: Building Visualizations in Kibana

**Steps:**

1. Open Kibana in a web browser (`http://localhost:5601`).
2. Create an index pattern to match the log data indexed by Logstash:
    - Navigate to "Management" > "Kibana" > "Index Patterns".
    - Create a new index pattern matching the Logstash index (logstash-*`).
3. Use the Discover tab to explore fields and log entries for log data.
4. Build visualizations based on the log data:
    - Navigate to "Visualize" > "Create new visualization".
    - Choose a visualization type ( bar chart, line graph) and configure it using the log data fields.
5. Save the visualizations and then add them to a new dashboard.

**Expected Output**: A functional Kibana dashboard displaying visual insights derived from the ingested log data.

---
### Outcome
By completing these exercises, learners develop practical experience deploying and using the ELK Stack, including configuring Elasticsearch, Logstash, and Kibana, ingesting log data, and building visualizations to analyze and interpret results.
