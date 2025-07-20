# SOC Real-Time Lab Setup using Free Software

This project demonstrates the real-time setup of a Security Operations Center (SOC) using only free and open-source software. It simulates core SOC functions including log collection, analysis, incident response, and threat intelligence, integrating TheHive, Cortex, MISP, and the ELK Stack.

---

##  Architecture

<p align="center">
  <img src="architecture/architecture_diagram.png" alt="SOC Architecture Diagram" width="600"/>
</p>
<p align="center"><em>Figure 1: SOC Real-Time Lab Architecture Overview</em></p>

---

##  Tools Used

| Tool     | Purpose |
|----------|---------|
| **TheHive** | Incident response platform |
| **Cortex**  | Automated analysis and response engine |
| **MISP**    | Threat intelligence platform |
| **ELK Stack** (Elasticsearch, Logstash, Kibana) | Log aggregation and visualization |

---

##  How to Run This Lab

To replicate this SOC Real-Time Lab setup on your own infrastructure:

1. **Deploy TheHive v4**
   - Use OpenJDK 8 and Cassandra as backend.

2. **Integrate Cortex and MISP**
   - Use Cortex for automated response.
   - Feed MISP threat intel into TheHive.

3. **Connect to ELK Stack**
   - Forward logs to Logstash.
   - Visualize alerts and incidents via Kibana.

4. **Verify Alerts and Automation**
   - Test ingestion of fake IOCs (Indicators of Compromise).
   - Trigger Cortex analyzers and observe incident handling.

 See `notes/troubleshooting.md` for resolving common issues.

---

##  Folder Structure

```
SOC-Real-Time-Lab/
├── 01_architecture/       # SOC design diagram
├── 02_config/             # Config files (TheHive, Cortex, MISP)
├── 03_screenshots/        # UI screenshots of the tools
├── 04_notes/              # Troubleshooting notes
├── LICENSE                # MIT License
├── .gitignore             # Ignore system files
└── README.md              # Project summary and instructions
```

---

##  License

This project is licensed under the [MIT License](LICENSE).

---

##  Author

**Adesh R**  
Cybersecurity Enthusiast | Hands-on SOC & Threat Intelligence Projects  
GitHub: [adeshrr](https://github.com/adeshrr)
