# Lab Activity Log
- **2025-08-09** — Added Local Speedtest Server VM under `projects/01-local-speedtest-server`
- **2025-08-07** — Updated Proxmox to 8.2, enabled 2FA for admin
- **2025-08-05** — Integrated Suricata IDS with Wazuh SIEM (initial alert testing)
- **2025-08-03** — Expanded VLAN segmentation to isolate legacy systems
- **2025-08-01** — Documented Samsung S25 Ultra thin-client setup in README

---

## Current Infrastructure

### 📱 WORKSTATION: DEDICATED Samsung Galaxy S25 Ultra  
(Hardened thin-client setup for remote workloads)

| Component | Details |
|---:|---|
| SoC | Snapdragon 8 Gen 4 |
| RAM | 12 GB LPDDR5X |
| Storage | 256 GB UFS 4.0 (OS + apps only) |
| Display | 6.8" 3120×1440 AMOLED 120 Hz |
| Secondary Display | 7" portable HDMI/USB-C field monitor (fits in small tablet bag) |
| Input | Wired keyboard + wired mouse |
| OS | Android 15 with Samsung Knox Work Profile |
| VPN | Always-on, AES-256 tunnel to private VLAN |
| Security Controls | Full-disk encryption, biometric + passphrase, MDM-compatible, remote wipe enabled |
| Role | SOC/IT thin client to headless server, dual screen in portable form factor |

**Security notes:**
- Knox profile separates work and personal apps  
- VPN required before server access  
- SSH keys only (no passwords)  
- Casting over wired HDMI or WPA3-only private networks  
- No sideloaded apps, OS always up to date

---

### 🖥️ HEADLESS SERVER  
(Primary compute environment for AI/LLM workloads)

| Component | Details |
|---:|---|
| CPU | Xeon Gold 5120 *(dual planned)* |
| RAM | 32 GB DDR4 *(64 planned)* |
| Storage A | 3×500 GB SSD in RAIDZ-1 (~1 TB usable, ZFS encryption enabled) |
| Storage B | NVMe 256 GB *(OS boot, encrypted)* |
| GPU 1 | Radeon HD 5770 1 GB *(RTX 4060 Ti 16 GB)* |
| GPU 2 | Nvidia GTX 1080 8 GB *(RTX 3090 24 GB)* |
| Motherboard | Dell OEM |
| OS 1 | Type-1 Hypervisor (Proxmox VE, 2FA for admin) |
| OS 2 | Windows 11 *(VM - isolated network segment)* |
| Case | Dell OEM |
| PSU | Dell OEM 950 W

**Security notes:**
- Type-1 hypervisor with VLAN network separation  
- Full disk encryption on all pools  
- SSH access restricted by IP allowlist  
- 2FA for hypervisor admin, hardware key for critical ops  
- Encrypted full backups taken monthly (1TB USB C SSD), additional ad-hoc before major changes
- GPU passthrough to isolated VMs

---

### 🕹️ Legacy Builds

#### 2012/14 “GB1 Gaming Build”
| Component | Details |
|---:|---|
| CPU | (USED) i5-2500 |
| CPU 2.0 | i5-2500 OC — Corsair H20 620 `//2013` |
| RAM | (HB1 + USED) 8 GB DDR3 |
| HDD A | (HB1) 500 GB 2.5" 5200 rpm |
| HDD B | (HB1) WD Green 2 TB |
| ~~GPU~~ | ~~(HB1) Radeon HD 6770 1 GB~~ |
| GPU 2.0 | Radeon HD 7950 3 GB `//2013` |
| Motherboard | mATX ASUS P8Z77-M PRO (LGA1155) |
| OS | Windows 7 Pro *(offline only for retro testing)* |
| Case | NZXT Vulcan Micro-ATX |
| PSU | (HB1) 550 W Antec VP550P |

#### 2011/12 “HB1 Homework Build” *(first malware sandbox 😅)*
| Component | Details |
|---:|---|
| CPU | AMD Athlon II X2 260 (stock) |
| RAM | 4 GB DDR3 — CMV4GX3M2A1333C9 |
| HDD A | (USED) 500 GB 2.5" 5200 rpm |
| HDD B | WD Green 2 TB — WD20EARX `//2012` |
| GPU | (USED) Radeon HD 6770 1 GB |
| Motherboard | mATX ASRock 880GMH-LE (AM3) |
| OS | Windows 7 Pro *que MIDI theme* |
| Case | E-waste `~~380w PSU flipped RCD~~` |
| PSU | 550 W Antec VP550P `//2012`

---

📌 **Note**: Legacy systems are physically isolated from main network, used for testing or sandbox work only.

![Screenshot 2025-08-02 at 2 37 32 AM](https://github.com/user-attachments/assets/013ede3d-d133-4e64-bc91-ccaaf8d5a913)  
![Screenshot 2025-08-02 at 2 59 06 AM](https://github.com/user-attachments/assets/c57979a1-cd7e-4a13-9219-6167c8b51c52)

## 📂 Folder Structure

```
home-soc-lab-flump-wazuh/
├── infrastructure/
│   ├── network-topology.md
│   ├── hardware-specs.md
│   └── proxmox-configs/
│       └── README.md
├── projects/
│   ├── 01-local-speedtest-server/
│   │   └── README.md
│   ├── 02-wazuh-siem/
│   │   └── README.md
│   ├── 03-suricata-ids/
│   │   └── README.md
│   ├── 04-dns-filter-pihole/
│   │   └── README.md
│   └── 05-internal-malware-lab/
│       └── README.md
└── docs/
    ├── lab-roadmap.md
    ├── security-policies.md
    └── learning-notes.md
```
