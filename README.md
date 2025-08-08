## 🔧 Current Infrastructure — Security-Optimized Overview

---

### 📱 WORKSTATION — Samsung Galaxy S25 Ultra  
*(Hardened thin-client environment for secure remote workloads)*

| Component | Details |
|---:|---|
| SoC | Snapdragon 8 Gen 4 |
| RAM | 12 GB LPDDR5X |
| Storage | 270 GB UFS 4.0 *(OS + apps only, no sensitive data stored locally)* |
| Display | 6.8" 3120×1440 AMOLED @ 120 Hz |
| Secondary Display | Private-network TV or wired USB-C → HDMI output |
| Input | Encrypted dongle-based keyboard/mouse *(wired in sensitive locations)* |
| OS | Android 15 with Samsung Knox Work Profile |
| VPN | Always-on, AES-256 tunnel to private VLAN |
| Security Controls | Full-disk encryption, biometric + passphrase, MDM-compatible, remote wipe enabled |
| Role | Thin-client SSH interface to headless server (no local processing of sensitive data) |

**Security Posture Highlights:**
- **Samsung Knox isolation** separates work and personal profiles, preventing cross-app data leaks.
- **Company-approved VPN** enforced before any remote server access.
- **SSH key-based authentication only** — no password logins allowed.
- **Casting limited to wired HDMI** or WPA3 private network; no public Miracast/Chromecast.
- No sideloaded apps; OS updates applied immediately.

---

### 🖥️ HEADLESS SERVER  
*(Primary compute environment — secured for AI/LLM workloads)*

| Component | Details |
|---:|---|
| CPU | Xeon Gold 5120 *(dual planned)* |
| RAM | 32 GB DDR4 *(64 GB planned)* |
| Storage A | 3×500 GB SSD in **RAIDZ-1** (~1.0 TB usable, ZFS encryption enabled) |
| Storage B | NVMe 256 GB *(OS boot, encrypted)* |
| GPU 1 | Radeon HD 5770 1 GB *(legacy workload compatibility)* |
| GPU 2 | Nvidia GTX 1080 8 GB *(upgrade path to dual modern GPUs planned)* |
| Motherboard | Dell OEM |
| OS 1 | Type-1 Hypervisor (Proxmox VE with 2FA admin access) |
| OS 2 | Windows 11 *(VM — isolated network segment)* |
| Case | Dell OEM |
| PSU | Dell OEM 950 W (monitored for power draw) |

**Security Posture Highlights:**
- **Type-1 hypervisor** — workloads isolated in separate VMs with strict VLAN segmentation.
- **Full-disk encryption** on all storage pools (LUKS/ZFS native).
- **SSH access restricted by IP allowlist** — non-routable management interface.
- **2FA for hypervisor admin** + hardware key for critical operations.
- **Regular snapshot + offsite encrypted backup** to prevent ransomware impact.
- **GPU passthrough to dedicated VMs** for compartmentalized AI model execution.

---

### 🕹️ LEGACY BUILDS *(Archived/Low-Sensitivity Use)*

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
| OS | Windows 7 Pro *(offline-only for retro/game testing)* |
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
| OS | Windows 7 Pro *(air-gapped)* |
| Case | E-waste `~~380w PSU flipped RCD~~` |
| PSU | 550 W Antec VP550P `//2012` |

---

📌 **Note:** All legacy systems are **physically isolated** from the main network, used for testing or sandboxing only. No sensitive workloads are executed on these machines.

![Screenshot 2025-08-02 at 2 37 32 AM](https://github.com/user-attachments/assets/013ede3d-d133-4e64-bc91-ccaaf8d5a913)  
![Screenshot 2025-08-02 at 2 59 06 AM](https://github.com/user-attachments/assets/c57979a1-cd7e-4a13-9219-6167c8b51c52)
