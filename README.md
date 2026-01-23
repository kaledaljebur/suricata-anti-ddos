# suricata-lab

This repository provides a **step-by-step basic guide** for using the **suricata-lab VMWare VM**,  
a lightweight Linux lab for experimenting with **Suricata IDS** and **EveBox**,
using **DVWA** as a traffic target.

---

## 📦 VM Download

- Download the VMware image [here](https://github.com/)

---

## 🧩 What’s Inside the VM

- Debian (XFCE)
- Suricata (IDS mode)
- EveBox (SQLite backend)
- DVWA (Apache + MariaDB)
- SSH (Open SSH)

This VM is designed for **detection and alert analysis**, not prevention.

---

## 🚀 Getting Started
- Uncompress the `.7z` image file
- Open the VM folder from VMware


## 🖥 Desktop Launchers (Inside the VM)

The VM desktop includes several shortcuts to simplify common tasks:

### 📁 Root folder
Opens the filesystem root (`/`) with administrative privileges.  
Useful for inspecting system directories and logs.

### ▶ Suricata start
Starts **Suricata manually** in IDS mode on the primary network interface.  
Suricata is intentionally **not run as a service** in this lab.
```bash
sudo suricata -c /etc/suricata/suricata.yaml -i ens33
```
### ⚙ Suricata config
Opens the main Suricata configuration file (`suricata.yaml`) with admin rights.  
Used to enable/disable logging options and adjust detection behaviour.
```bash
sudo mousepad /etc/suricata/suricata.yaml
```
### 📜 Suricata Local Rules
Opens the local rules file (`local.rules`) where custom detection rules
(e.g. SYN flood detection) are defined and modified.
```bash
sudo mousepad /var/lib/suricata/rules/local.rules
```
### 📊 EveBox
Starts **EveBox**, the web-based alert viewer for Suricata.  
EveBox reads alerts from `eve.json` and provides a simple UI for analysis.
```bash
sudo /evebox/evebox-0.23.0-linux-x64/evebox server --datastore sqlite --input /var/log/suricata/eve.json --host 0.0.0.0
```

**All launchers are provided for convenience; commands can also be run manually from a terminal.**

## 🚨 Included Detection Rule

The VM includes a **custom Suricata rule for detecting SYN-based DoS/DDoS attacks**.

- The rule detects **abnormally high rates of TCP SYN packets**
- Detection is based on **destination-based tracking** (`by_dst`)
- Alerts are **rate-limited** to avoid log flooding
- Alerts are visible in **EveBox**

This rule is intended for **learning and experimentation** and can be modified
by students to observe how threshold values affect detection and false positives.

The rule can be found at:
```bash
/var/lib/suricata/rules/local.rules
```

## 📬 Contact, Support, and Suggestions

This lab VM is provided for **educational use**.

If you encounter issues, have questions, or would like to suggest improvements
(e.g. additional detection scenarios, rules, or lab tasks), please use one of the following:

- **GitHub Issues:**  
  Open an issue in this repository for bugs, errors, or suggestions.

- **Pull Requests:**  
  Improvements to documentation are welcome via pull requests.

This project is maintained on a **best-effort basis** and primarily intended for
teaching and learning purposes.

