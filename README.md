
# 🔐 Wazuh Threat Detection Lab – Sigma to Wazuh Rules, Suricata Integration & Multi-Agent Deployment

This project demonstrates the creation and deployment of custom threat detection rules using **Sigma**, their conversion to **Wazuh rules**, the integration of **Suricata IDS**, and the setup of Wazuh agents on various virtual machines for centralized threat monitoring.

---

## 📌 Objectives

- Convert custom **Sigma rules** to **Wazuh** rules.
- Integrate **Suricata IDS** with a Wazuh `.ova` installation.
- Create and configure Wazuh agents on:
  - 🐧 Ubuntu VM
  - 🪟 Windows VM
  - 🐦 Raven Linux VM
- Monitor agent activity and test detection of specific patterns/events.
- Validate rule triggers and visibility via the **Wazuh dashboard**.

---

## 🛠️ Technologies Used

| Tool          | Role                                 |
|---------------|--------------------------------------|
| **Wazuh**     | SIEM platform (central monitoring)   |
| **Sigma**     | Generic rule format for detections   |
| **Suricata**  | Network IDS/IPS for threat detection |
| **Linux**     | VMs and Agent platforms              |
| **Windows**   | Target VM for agent and log testing  |
| **Raven OS**  | Custom Linux-based VM                |

---

## ⚙️ Setup Instructions

### 1. 🧠 Sigma Rule Development

- Created custom detection rules in [Sigma YAML format](https://github.com/SigmaHQ/sigma).
- Rules target suspicious Windows event logs and Linux system events.

### 2. 🔄 Sigma to Wazuh Rule Conversion

Used [sigmac](https://github.com/SigmaHQ/sigmac) to convert `.yml` rules to Wazuh-compatible format:

```bash
sigmac -t wazuh -c path/to/config.yml myrule.yml > myrule_wazuh.xml
```

### 3️⃣ Wazuh Installation (OVA)

Deployed the official **Wazuh All-in-One OVA** to quickly set up the SIEM environment.

Steps:
- ✅ Imported `.ova` file into VirtualBox or VMware.
- ✅ Set network mode to **Bridged Adapter**.
- ✅ Accessed the Wazuh dashboard at:  
  `https://<your_wazuh_ip>:5601`
- ✅ Verified Wazuh manager and Elastic stack services are running.

---

### 4️⃣ Suricata Integration with Wazuh

Enabled **Suricata IDS** on the Wazuh server for real-time network threat detection.

Steps:
- ✅ Installed Suricata:

```bash
sudo apt install suricata
```

- ✅ Edited `suricata.yaml` to log JSON output.
- ✅ Configured Wazuh to monitor Suricata logs:

```xml
<localfile>
  <log_format>json</log_format>
  <location>/var/log/suricata/eve.json</location>
</localfile>
```

- ✅ Restarted Suricata and Wazuh services.
- ✅ Confirmed Suricata alerts in Wazuh dashboard.

---

### 5️⃣ Agent Deployment (Ubuntu / Windows / Raven)

Created and connected Wazuh agents on three platforms:

| VM Name | OS            | Status    |
|---------|---------------|-----------|
| Ubuntu  | Linux 22.04   | 🟢 Connected |
| Windows | Windows 10    | 🟢 Connected |
| Raven   | Lightweight OS| 🟢 Connected |

Agent Setup:
- Downloaded and installed Wazuh agents.
- Registered each agent with manager via:

```bash
manage_agents
```

- Copied agent keys into config files.
- Verified agent connectivity on dashboard.

---

### 6️⃣ Dashboard Monitoring & Rule Testing

Used the Wazuh Dashboard (Kibana) to:

- View real-time logs/events from all agents.
- Monitor Suricata alerts.
- Validate custom Sigma-based rule triggers.

Tested detections:
- Windows event log anomalies.
- Linux file integrity changes.

---

## 📷 Screenshots

# Wazuh Dashboard

![image](https://github.com/user-attachments/assets/9c65dcd1-34d9-4268-abde-d011329e8019)

![image](https://github.com/user-attachments/assets/ee648796-f837-4d2b-a8a8-38fbba2487c6)

# Create Sigma rule with Jupyter Notebook

![image](https://github.com/user-attachments/assets/beb6bd53-ae47-4963-aec3-1164ea46d3ee)

# Convert rule  with library sigwah 

![image](https://github.com/user-attachments/assets/075c63ce-c08b-43cf-9e59-c35938f3b1c9)

# Sigma Rule on Wazuh xml form

![image](https://github.com/user-attachments/assets/e3a2736e-bbd5-4a31-844e-c8d1eda42107)

# Enable rules

## nmap -Pn -p- 192.168.2.47

Custom Rules: 100003, 100004 και 100005

![image](https://github.com/user-attachments/assets/96a686b5-aa09-4d5e-8af2-367594a91b89)



## curl -XGET "http://192.168.2.47/users/?id=SELECT+*+FROM+users";

Next, in order to activate rule 100001, the command ssh -l steven 192.168.2.47
was executed with a failed attempt, triggering rule 100002 with a successful connection attempt

![image](https://github.com/user-attachments/assets/ceacfa96-a27e-40d7-89e9-274be561d283)


