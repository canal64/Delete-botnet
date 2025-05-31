Below is the pure Markdown source of the Windows botnet-removal tutorial, translated into English and kept beginner-friendly.
Copy-paste the entire block into any Markdown viewer (GitHub, Obsidian, VS Code…) to see the formatted version.

# Eradicating a Botnet on Windows – Simplified Guide (2025)

> 🎯 Goal: clean your PC without advanced technical knowledge.

---

## 🛠️ Hardware & software you’ll need
1. **A USB stick** (8 GB or larger) — handy for an “offline” scan.
2. **A clean Internet connection** (from another PC) to download the tools:
   - Windows **Malicious Software Removal Tool** (MSRT, KB890830)  
   - **eScan CERT-In Bot Removal Toolkit** (portable, free)

---

## Step 1 — Disconnect & back up essentials
- Unplug the Ethernet cable or disable Wi-Fi on the infected PC.  
- Copy your important documents to an external drive.

---

## Step 2 — Update Windows
1. **Settings › Windows Update › Check for updates**.  
2. Install *all* available patches, then restart.  
   *Why?* Many botnets reinfect through already-patched vulnerabilities.

---

## Step 3 — Boot into “Safe Mode with Networking”
1. **Win + I › System › Recovery › Advanced start-up › Restart now**.  
2. Troubleshoot › Advanced options › Start-up settings › Restart.  
3. Choose **[4] Safe Mode with Networking**.

---

## Step 4 — Quick scan with MSRT
1. Run **msert.exe** (no installation required).  
2. Select **Full Scan** and wait for completion.  
   > MSRT is updated monthly by Microsoft and removes the majority of known malware.

---

## Step 5 — Deep scan with Microsoft Defender
- Open **Windows Security › Virus & threat protection**.  
- Click **Scan options › Full scan › Scan now**.  
- Remove or quarantine everything it detects.

**Still infected?**  
Run **Microsoft Defender Offline** instead:  
Select **Offline scan**; the PC reboots, scans before Windows starts, and reboots again automatically.

---

## Step 6 — Second opinion (optional but recommended)
1. Download the **eScan CERT-In Bot Removal Toolkit** on a clean PC.  
2. Copy the executable to your USB stick → run it in Safe Mode.  
3. Select **Scan & Clean** and let it finish.

---

## Step 7 — Manually remove persistent start-ups (advanced)
- **Registry**: `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`  
- **Scheduled Tasks**: *Task Scheduler* › Library  
> Delete any unknown entry (random names, suspicious folders).  
  Search the Web first if you’re unsure.

---

## Step 8 — Final reboot & checks
1. Reboot into normal mode.  
2. Run a **Defender Quick Scan**: result should be *0 threats*.  
3. Watch Task Manager: CPU/Network usage should stay low when idle.

---

## Step 9 — Prevent a relapse
| Action | How to do it |
|--------|--------------|
| **Enable automatic updates** | Windows Update › Advanced options |
| **Keep Windows Firewall on** | Windows Security › Firewall & network protection |
| **Use MFA & strong passwords** | Microsoft account or local account + password manager |
| **Back up regularly** | File History, OneDrive, or a full-image backup |

---

## ⏱️ Quick-Check List (print me!)
- [ ] Internet disconnected, backups done  
- [ ] Windows updates applied  
- [ ] MSRT scan completed  
- [ ] Defender scan (or Offline scan) → no threats  
- [ ] eScan toolkit scan (optional) clean  
- [ ] Firewall & auto-updates enabled  

---

### Fast FAQ

**Q : Do I need a paid antivirus?**  
Not mandatory: Defender + MSRT cover 99 % of home scenarios.

**Q : My PC feels slow right after cleanup — normal?**  
Yes. Defender re-scans files in the background for about an hour. Let it finish.

**Q : Why Safe Mode?**  
It prevents most malware from injecting itself at start-up, making removal much easier.

---

*Guide written for absolute beginners; no complicated command lines, only official Microsoft tools plus one portable auxiliary scanner.*
