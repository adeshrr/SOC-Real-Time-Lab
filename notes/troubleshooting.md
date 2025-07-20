# Troubleshooting: SOC Real-Time Lab Setup

This document provides solutions to common issues encountered during the setup and configuration of the SOC Real-Time Lab using TheHive, Cortex, MISP, and the ELK Stack.

---

## 1. TheHive Service Not Starting

**Symptoms:**
- `thehive.service` fails to start
- Logs show Java or Cassandra connection issues

**Solutions:**
- Ensure Cassandra is running before starting TheHive
- Use OpenJDK 8 (not higher versions)
- Check `/etc/thehive/application.conf` for syntax errors

---

## 2. Cortex API Key Not Working

**Symptoms:**
- Error: "Unauthorized" when TheHive connects to Cortex

**Solutions:**
- Make sure the API key is active and correctly copied into TheHive’s config
- Ensure Cortex is reachable at the expected IP and port
- Restart both Cortex and TheHive after any configuration changes

---

## 3. MISP Feeds Not Updating

**Symptoms:**
- MISP feed updates fail or show 0 events

**Solutions:**
- Ensure MISP has internet access
- Update feed metadata
- Check permissions for API key and feed settings

---

## 4. Kibana Shows No Data

**Symptoms:**
- Dashboard is empty or blank
- Logs not appearing in Kibana

**Solutions:**
- Check if Logstash is running and parsing logs correctly
- Verify correct index pattern is set in Kibana
- Confirm Elasticsearch is receiving logs

---

## 5. Integration Fails Between Tools

**Symptoms:**
- Cortex not responding to TheHive
- MISP not sharing IOCs

**Solutions:**
- Test connections manually using `curl` or browser
- Check application logs for error messages
- Validate IP whitelists, ports, and API endpoints

---

## 6. General Tips

- Restart services after config changes:
  ```bash
  sudo systemctl restart thehive
  sudo systemctl restart cortex
  sudo systemctl restart misp
  ```

- Use logs:
  - `/var/log/thehive/application.log`
  - `/var/log/cortex/application.log`
  - `/var/log/misp/misp.log`
  - Elasticsearch logs in `/var/log/elasticsearch/`

- Keep backup copies of config files before modifying them

---

This document will be updated as more issues are encountered and resolved.
