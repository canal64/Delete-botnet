# Delete-botnet
Guide to delete botnet (scan and delete)
Below is the raw Markdown source of the full playbook.
Copy-paste it into any Markdown viewer (GitHub, Obsidian, VS Code, etc.) to see the formatted version.

# Botnet Response Playbook (2025)

## 1 – Get the ground ready

| Goal | Why it matters | Recommended actions / tools |
|------|----------------|-----------------------------|
| **Back up and inventory first** | You may need to rebuild or analyse offline. | Air-gapped backup; list every device, OS version, role and IP address. |
| **Patch everything** | Shrinks the attack surface and stops re-infection during cleanup. | Windows Update; `apt upgrade` / `dnf upgrade`; IoT firmware. |
| **Plan for isolation** | Lets you quarantine a host instantly. | Create quarantine VLANs, firewall rules, ACLs. |

---

## 2 – Detect: scanners & indicators

| Scope | Key indicators | 2025-era tools that work |
|-------|----------------|--------------------------|
| **Single workstation / server** | Unknown processes or services, CPU/RAM spikes, unusual outbound connections (`netstat -an`, `Get-NetTCPConnection`). | **MSRT** (Malicious Software Removal Tool, standalone)<br>**eScan CERT-In Bot Removal Toolkit** (portable)<br>**SUPERAntiSpyware Portable** (second opinion) |
| **Network-wide** | Traffic to C2 hosts, DNS NXDOMAIN bursts, beaconing patterns. | **Zeek** or **Suricata** with Emerging-Threats rules; **Snort 3**; SIEM dashboards (ELK, Splunk). |
| **Cloud / web tier** | Automated requests, credential-stuffing, scraping spikes. | Bot-management platforms such as DataDome, HUMAN, Imperva, Netacea. |

> **Quick Windows trick:** Boot in *Safe Mode with Networking*, run **MSRT** first, then a portable second engine (eScan or Malwarebytes); malware has far less room to hide.

---

## 3 – Contain right now

1. **Unplug or VLAN-shift** the suspect host (pull Wi-Fi, yank the cable, or move it to “quarantine”).  
2. Disable remote-admin channels (RDP, SSH) except from investigation IPs.  
3. **Preserve evidence:** memory dump (FTK Imager, Magnet RAM Capture), log export, or disk image for severe cases.

Rapid isolation limits spread while keeping artefacts for forensics.

---

## 4 – Eradicate cleanly

| Step | What to do |
|------|------------|
| **Offline analysis** | Mount the drive in an isolated VM with no network; scan with multiple AV/EDR engines. |
| **Manual removal (advanced)** | • Delete rogue services, Run/RunOnce keys, scheduled tasks, rootkit drivers.<br>• Inspect `C:\Windows\System32\drivers\etc\hosts`, firewall rules, proxy settings. |
| **Automation option** | Academic tool **ECHO** (released Apr 2025) hijacks many botnets’ own update logic to uninstall them in minutes; currently SOC-only but promising. |
| **Re-image if in doubt** | If firmware might be tampered: format, deploy a known-good image, update UEFI/BIOS; for IoT, reflash or factory-reset. |

---

## 5 – Harden so it can’t return

1. **Continuous patching** (WSUS, Ansible, MDM).  
2. **MFA everywhere**, rotate passwords, protect SSH keys with passphrases.  
3. **Least privilege** (GPO, `sudoers`).  
4. **Real-time monitoring:** feed Zeek/Suricata into a SIEM with C2-beacon alerts.  
5. **WAF / bot-management** for public apps (DataDome, Imperva Sonar, etc.).  
6. **User awareness**: phishing drills, macro blocking, security briefings.

---

## 6 – When to bring in an expert

- Critical infrastructure or evidence of a persistent APT.  
- Firmware-level rootkits, suspicious encryption, tampered boot loaders.  
- Legal / regulatory pressure (GDPR, NIS 2, PCI-DSS) requiring certified forensic reports.

---

### One-page “express” checklist

- [ ] Offline backup completed  
- [ ] Hosts quarantined / VLAN isolation active  
- [ ] MSRT + second scanner finished  
- [ ] Logs and memory dumps secured  
- [ ] Patches applied, passwords rotated  
- [ ] Post-cleanup network monitoring live

---

**Bottom line:** use layered detection (EDR + IDS/IPS), isolate at the first sign of compromise, eradicate with proven cleaning tools—or, for stubborn cases, advanced methods such as the **ECHO** framework. Finish with systematic hardening and continuous monitoring; that’s the only way to ensure a wiped botnet stays gone.
