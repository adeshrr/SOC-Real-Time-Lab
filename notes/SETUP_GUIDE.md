
# SOC Real-Time Lab: Step-by-Step Setup Guide (Simplified for GitHub)

This guide provides a simplified set of essential steps extracted from the Cyber Talents "Build SOC With Open Source Tools" material to help replicate the lab.

---

## 1. ELK Stack Setup (Elastic, Logstash, Kibana)

### A. Install Docker & Docker Compose
```bash
sudo apt update && sudo apt upgrade
sudo apt install docker.io docker-compose -y
```

### B. Set Up ELK Stack using Docker
```bash
mkdir elastic && cd elastic
vi docker-compose.yml  # Paste ELK config here
sudo docker-compose up -d
```

### C. Verify and Access
- Check with: `netstat -ltpnd`
- Access Kibana: `http://<EC2_Public_IP>:5601`

---

## 2. Filebeat Setup

### A. Install Filebeat
```bash
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-amd64.deb
sudo dpkg -i filebeat-7.15.0-amd64.deb
```

### B. Configure
Edit `/etc/filebeat/filebeat.yml`:
```yaml
output.elasticsearch:
  hosts: ["http://<ELASTIC_IP>:9200"]
  username: "<elastic user>"
  password: "<elastic pass>"

setup.kibana:
  host: "http://<KIBANA_IP>:5601"
```

Enable and start system module:
```bash
cd /etc/filebeat/modules.d/
sudo filebeat modules enable system
sudo service filebeat start
```

---

## 3. MISP Installation
```bash
wget --no-cache -O /tmp/INSTALL.sh https://raw.githubusercontent.com/MISP/MISP/2.4/INSTALL/INSTALL.sh
bash /tmp/INSTALL.sh -c
```
- Login: `http://<MISP_IP>/`
- Default: `admin@admin.test / admin`

---

## 4. Cortex Installation

### A. Install Java & Elasticsearch
```bash
sudo apt install openjdk-8-jre-headless -y
sudo apt install elasticsearch
sudo vi /etc/elasticsearch/elasticsearch.yml  # Set host, port, cluster name
sudo systemctl start elasticsearch
```

### B. Install Cortex
```bash
echo 'deb https://deb.thehive-project.org release main' | sudo tee -a /etc/apt/sources.list.d/thehive-project.list
sudo apt update && sudo apt install cortex
```

### C. Configure & Access Cortex
Edit `/etc/cortex/application.conf` with your secret key and Elastic URL:
```hocon
play.http.secret.key = "<generated_key>"
search.uri = "http://<CORTEX_VM_IP>:9200"
```
Access: `http://<CORTEX_VM_IP>:9001`

---

## 5. TheHive Installation

### A. Install Cassandra & Java
```bash
sudo apt install openjdk-8-jdk
echo JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64" >> /etc/environment
sudo apt install cassandra
```

### B. Install TheHive
```bash
curl https://raw.githubusercontent.com/TheHive-Project/TheHive/master/PGP-PUBLIC-KEY | sudo apt-key add -
sudo apt update && sudo apt install thehive4
```

### C. Configure
Edit `/etc/thehive/application.conf`:
- Cassandra connection
- Cortex & MISP integration

Start: `service thehive start`

---

## 6. Integrations

### A. TheHive + Cortex
- Create API key in Cortex
- Add it to TheHive config under `cortex { servers: [...] }`

### B. TheHive + MISP
- Generate MISP API key
- Add it to TheHive config under `misp { servers: [...] }`

### C. ELK + TheHive
- In Kibana: Create webhook connector
- POST URL: `http://<TheHiveIP>:9000/api/case`
- Add auth header with Bearer token

---

##  Done!
You now have a working SOC lab using TheHive, Cortex, MISP, and ELK with real-time alerting and threat intel.
